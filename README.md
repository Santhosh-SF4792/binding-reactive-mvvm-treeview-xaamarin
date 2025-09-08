# binding-reactive-mvvm-treeview-xaamarin

The SfTreeView allows you to bind ItemTemplate to the reactive UI ViewModel which is a composable and cross-platform model-view-viewmodel framework for all .NET platforms.

## Sample

```csharp
public class ViewModel : ReactiveObject
{
    private ObservableCollection<FileManager> imageNodeInfo;
    public ObservableCollection<FileManager> ImageNodeInfo
    {
        get => imageNodeInfo;
        set => this.RaiseAndSetIfChanged(ref imageNodeInfo, value);
    }

    public ViewModel()
    {
        GenerateSource();
    }

    private void GenerateSource()
    {
        // Populate imageNodeInfo with FileManager items,
        // each having ItemName, ImageIcon (ImageSource), and SubFiles
    }
}
```

## Requirements to run the demo

To run the demo, refer to [System Requirements for Xamarin](https://help.syncfusion.com/xamarin/system-requirements)

## Troubleshooting
### Path too long exception
If you are facing path too long exception when building this example project, close Visual Studio and rename the repository to short and build the project.
