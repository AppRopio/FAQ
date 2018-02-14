# Работа с темой всего проекта и создание темы модуля

## Тема проекта

### iOS

Все тематические настройки проекта содержатся в JSON файлах, которые находятся по пути `Settings/ThemeConfigs/`

Главным конфигурационным файлом среди всех является `App.json`. Именно в нем определены стили основных контролов, задана цветовая схема и прописаны шрифты. Помимо него, в этой же папке лежат кофигурации тем под каждый модуль, использующийся в проекте (для понимания того, что можно настраивать в теме каждого модуля, рекомендуется посмотреть в `Assembly Browser` структуру класса `ThemeConfig`, который есть в каждом UI проекте каждого модуля).

**Главный принцип темы** – все модули обязаны использовать значения, определенные в `App.json`, но при этом должна быть возможность изменить тему каждого элемента в отдельности.

Разберем подробнее `App.json`. Он содержит в себе настройки трех видов компонентов, на которые ссылаются основные модули (это сделано для обеспечения консистентного вида UI в приложении и упрощения его изменений):
* `controlPalette` – палитра контролов (наследники UIView) – здесь определены темы основных контролов, использующихся для построения UI. В большинстве ситуаций, если тебе потребовалось задать своему контролу тему – тебе уже есть на что сослаться в палитре контролов, для того чтобы задать значение по умолчанию
* `colorPalette` – палитра цветов – здесь определены все цвета, использующиеся в приложении. В большинстве ситуаций, при разработке модуля, цвет берется именно из этой палитры
* `fontsPalette` –  палитра шрифтов – здесь определены все шрифты, использующиеся в приложении. Всегда необходимо использовать один из шрифтов этой палитры


**НЕОБХОДИМО ПОМНИТЬ**
- если нужно внести изменение, касающееся всего приложения, то **обязательно** это нужно делать изменяя `App.json`
- если нужно внести изменение, касающееся конкретного котрола, то необходимо это делать изменяя соответствующий конфигурационный файл темы этого модуля

## Тема модуля

### iOS



Каждый модуль обязан содержать в себе модель соответствующего конфигурационного файла темы, использующегося для задания стиля контролам, из которых состоит UI данного модуля.

Название модели должно удовлетворять маске `{название_модуля}ThemeConfig`

Важно дать возможность кастомизации как можно большего числа элементов и стараться, чтобы все 100% контролов модуля были покрыты темой.

При реализации модели темы необходимо задавать для каждого контрола значения по умолчанию, которые можно взять из различных палитр общей темы (`App.json`). 

**Пример темы на модуле "Меню"**
```
public class MenuThemeConfig
{
    [JsonProperty("navBarMenuImage")]
    public Image NavBarMenuImage { get; private set; }

    [JsonProperty("flyoutController")]
    public FlyoutController FlyoutController { get; private set; }

    [JsonProperty("leftViewController")]
    public LeftViewController LeftViewController { get; private set; }

    public MenuThemeConfig()
    {
        NavBarMenuImage = new Image();
        FlyoutController = new FlyoutController();
        LeftViewController = new LeftViewController();
    }
}

public class FlyoutController
{
    [JsonProperty("menuSlidesWithTopView")]
    public bool MenuSlidesWithTopView { get; private set; }
}

public class LeftViewController
{
    [JsonProperty("size")]
    public Size Size { get; private set; }

    [JsonProperty("backgroundColor")]
    public Color BackgroundColor { get; private set; }

    [JsonProperty("menuTable")]
    public MenuTable MenuTable { get; private set; }

    [JsonProperty("logotypeHeaderImage")]
    public Image LogotypeHeaderImage { get; private set; }

    public LeftViewController()
    {
        Size = new Size { Width = 270 };
        BackgroundColor = (Color)Theme.ColorPalette.BackgroundMenu.Clone();
        MenuTable = new MenuTable();
    }
}

public class MenuTable
{
    [JsonProperty("margins")]
    public Margins Margins { get; private set; }

    [JsonProperty("contentInsets")]
    public ContentInsets ContentInsets { get; private set; }

    [JsonProperty("background")]
    public Color Background { get; private set; }

    [JsonProperty("menuCell")]
    public MenuCell MenuCell { get; private set; }

    public List<OverlayCellTheme> OverlayCellThemes { get; private set; }

    [JsonProperty("sectionHeaderHeight")]
    public float SectionHeaderHeight { get; private set; }

    public MenuTable()
    {
        Margins = new Margins { Top = 20 };
        ContentInsets = new ContentInsets { Top = 44 };
        Background = (Color)Theme.ColorPalette.BackgroundMenu.Clone();
        MenuCell = new MenuCell();
        SectionHeaderHeight = 0;
        OverlayCellThemes = new List<OverlayCellTheme>();
    }
}

public class OverlayCellTheme
{
    public IndexPath IndexPath { get; set; }

    public string ViewModelType { get; set; }

    [JsonProperty("menuCell")]
    public MenuCell MenuCell { get; private set; }

    public OverlayCellTheme()
    {
        MenuCell = new MenuCell();
    }
}

public class MenuCell : View
{
    [JsonProperty("size")]
    public Size Size { get; private set; }

    [JsonProperty("name")]
    public Label Name { get; private set; }

    [JsonProperty("badge")]
    public Label Badge { get; private set; }

    public MenuCell()
    {
        Size = new Size { Height = 50 };
        Name = new Label { TextColor = (Color)Theme.ColorPalette.TextMenu.Clone(), Font = Theme.FontsPalette.SemiboldOfSize(16) };
        Badge = new Label { TextColor = (Color)Theme.ColorPalette.TextAccent.Clone(), Font = Theme.FontsPalette.SemiboldOfSize(14), Background = (Color)Theme.ColorPalette.Accent.Clone(), TextAlignment = TextAlignment.Center };
    }
}
```


