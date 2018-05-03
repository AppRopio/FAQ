# rabota-s-navigatsiei

Платформа AppRopio использует последние версии пакетов MvvmCross, поэтому принципы работы с навигацией всегда совпадают с принципами, указанными в актуальной документации MvvmCross. Здесь мы рассмотрим некоторые особенности работы с `NavigationVmService`.

## ViewModel

В текущей версии MvvmCross \(5.5+\) рекомендуется использовать `MvxNavigationService` для осуществления навигации между VM. Этот сервис изменяет последовательность и сами методы, вызывающиеся при создании ViewModel, зато позволяет передать в ViewModel параметр напрямую, не используя сериализацию/десериализацию. Для реализации универсального параметра навигации, в AppRopio используется `IMvxBundle` в качестве параметра для навигации между `ViewModel`. Это значит, что тебе не нужно использовать наследование от `MvxViewModel<TParameter>`, достаточно создать объект, реализующий интерфейс `IMvxBundle` и использовать его в качестве необходимого параметра в соответствующем `NavigationVmService`. Принимать параметр, переданный при навигации необходимо в методе `Prepare(IMvxBundle parameter)`, например, как показано в коде ниже:

```text
public override void Prepare(IMvxBundle parameters)
{
    base.Prepare(parameters);

    var navigationBundle = parameters.ReadAs<NavigationBundle>();
    this.InitFromBundle(navigationBundle);
}

protected virtual void InitFromBundle(NavigationBundle parameters)
{
    VmNavigationType = parameters.NavigationType == NavigationType.None ?
                                                    NavigationType.ClearAndPush :
                                                    parameters.NavigationType;

    _id = parameters.Id;
}
```

В этих методах необходимо лишь проинициализировать основные свойства своей ViewModel. Тяжелую работу обязательно нужно выполнять внутри `Task Initialize()`

## NavigationVmService

Этот сервис используется для навигации внутри всего модуля \(и иногда даже для навигации в его зависимости\), поэтому в модуле не может быть больше одного `NavigationVmService` Сам по себе сервис является фасадом, закрывающим конкретную реализацию навигации \(в теории можно отвязать навигацию от механизмов MvvmCross\). Кроме того, сервис будет использован другими модулями, если будет такая потребность. Поэтому интерфейс сервиса должен явно использовать все навигационные параметры, использующимися ViewModel в модуле. Для удобства можно использовать `BaseVmNavigationService` в качестве "родителя" сервиса, использующегося в твоем модуле \(он уже реализует всю логику навигации, тебе остается лишь правильно вызвать эти реализации и передать соответствующие параметры навигации\)

Например, рассмотрим сервис, использующийся в модуле "Каталог".

**IProductsNavigationVmService**

```text
public interface IProductsNavigationVmService : IBaseVmNavigationService
{
    void NavigateToContentSearch(BaseBundle bundle);

    void NavigateToMain(BaseBundle bundle);

    void NavigateToSSCategory(CategoryBundle bundle);

    void NavigateToCategory(CategoryBundle bundle);

    void NavigateToProducts(ProductsBundle bundle);

    void NavigateToFilters(FiltersBundle bundle);

    void NavigateToSelection(Base.Filters.Core.Models.Bundle.SelectionBundle bundle);

    void NavigateToSelection(Models.Bundle.SelectionBundle bundle);

    void NavigateToSort(SortBundle bundle);

    void NavigateToProduct(ProductCardBundle bundle);

    void NavigateToTextContent(BaseTextContentBundle bundle);

    void NavigateToWebContent(BaseWebContentBundle bundle);

    void NavigateToCustomType(Type customVmType, BaseBundle bundle);
}
```

**ProductsNavigationVmService**

```text
public class ProductsNavigationVmService : BaseVmNavigationService, IProductsNavigationVmService
{
    protected IFiltersNavigationVmService FiltersNavigationVmService { get { return Mvx.Resolve<IFiltersNavigationVmService>(); } }

    public void NavigateToContentSearch(BaseBundle bundle)
    {
        NavigateTo<IContentSearchViewModel>(bundle);
    }

    public void NavigateToMain(BaseBundle bundle)
    {
        NavigateTo<IProductsViewModel>(bundle);
    }

    public void NavigateToSSCategory(CategoryBundle bundle)
    {
        NavigateTo<ISSCategoriesViewModel>(bundle);
    }

    public void NavigateToCategory(CategoryBundle bundle)
    {
        NavigateTo<ICategoriesViewModel>(bundle);
    }

    public void NavigateToProducts(ProductsBundle bundle)
    {
        NavigateTo<ICatalogViewModel>(bundle);
    }

    public void NavigateToProduct(ProductCardBundle bundle)
    {
        NavigateTo<IProductCardViewModel>(bundle);
    }

    public void NavigateToFilters(FiltersBundle bundle)
    {
        FiltersNavigationVmService.NavigateToFilters(bundle);
    }

    public void NavigateToSelection(Base.Filters.Core.Models.Bundle.SelectionBundle bundle)
    {
        FiltersNavigationVmService.NavigateToSelection(bundle);
    }

    public void NavigateToSort(SortBundle bundle)
    {
        FiltersNavigationVmService.NavigateToSort(bundle);
    }

    public void NavigateToSelection(Models.Bundle.SelectionBundle bundle)
    {
        NavigateTo<IProductDetailsSelectionViewModel>(bundle);
    }

    public void NavigateToTextContent(BaseTextContentBundle bundle)
    {
        NavigateTo<IProductTextContentViewModel>(bundle);
    }

    public void NavigateToWebContent(BaseWebContentBundle bundle)
    {
        NavigateTo<IProductWebContentViewModel>(bundle);
    }

    public void NavigateToCustomType(Type customVmType, BaseBundle bundle)
    {
        NavigateTo(customVmType, bundle);
    }
}
```

