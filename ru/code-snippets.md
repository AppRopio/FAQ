# code-snippets

## Commands

### IMvxCommand

**Name** `cmvx`

**Template**

```text
private IMvxCommand _$privateName$;
public IMvxCommand $PublicName$ => _$privateName$ ?? (_$privateName$ = new MvxCommand(() => { }));
```

### IMvxAsyncCommand

**Name** `camvx`

**Template**

```text
private IMvxCommand _$privateName$;
public IMvxCommand $PublicName$ => _$privateName$ ?? (_$privateName$ = new MvxCommand(() => { }));
```

## Properties

**Name** `lmvx`

**Template**

```text
private $type$ _$name$;
public $type$ $Name$ 
{
    get => _$name$;
    set => SetProperty(ref _$name$, value, nameof($Name$));
}
```

## BindingSet

**Name** `set`

**Template**

```text
set.Bind($View$).To(vm => vm.$Property$);
```

**Name** `vset`

**Template**

```text
set.Bind($View$).For("Visibility").To(vm => vm.$Property$).WithConversion("Visibility");
```

## ViewModel

**Name** `vm`

**Template**

```text
#region Fields

#endregion

#region Commands

#endregion

#region Properties

#endregion

#region Services

#endregion

#region Constructor

public $ViewModel$()
{

}

#endregion

#region Private

#endregion

#region Protected

#region Init

protected virtual void Prepare($VmBundle$ parameters)
{
    //TODO: init properties
}

#endregion

protected async Task LoadContent()
{
    //TODO: load content
}

#endregion

#region Public

public override Task Initialize()
{
    return LoadContent();
}

public override void Prepare(MvvmCross.Core.ViewModels.IMvxBundle parameters)
{
    var bundle = parameters.ReadAs<$VmBundle$>();
    this.Prepare(bundle);
}

#endregion
```

