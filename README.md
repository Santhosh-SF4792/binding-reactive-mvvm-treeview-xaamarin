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

STEP 3: ContentPage should inherit from ReactiveContentPage<TViewModel> and we are going to use ReactiveUI Binding to bind our ViewModel to our View.
### XAML
```xaml
<syncfusion:SfTreeView x:Name="treeView"
    ItemHeight="40"
    Indentation="15"
    ExpanderWidth="40"
    ChildPropertyName="SubFiles"
    ItemsSource="{Binding ImageNodeInfo}">
    <syncfusion:SfTreeView.ItemTemplate>
        <DataTemplate>
            <Grid>
                <Grid.ColumnDefinitions>
                    <ColumnDefinition Width="40" />
                    <ColumnDefinition Width="*" />
                </Grid.ColumnDefinitions>
                <Image Grid.Column="0"
                    Source="{Binding Content.ImageIcon}"
                    HeightRequest="35"
                    WidthRequest="35"/>
                <Label Grid.Column="1"
                    Text="{Binding Content.ItemName}" 
                    VerticalOptions="Center"/>
            </Grid>
        </DataTemplate>
    </syncfusion:SfTreeView.ItemTemplate>
</syncfusion:SfTreeView>
```

## Requirements to run the demo

To run the demo, refer to [System Requirements for Xamarin](https://help.syncfusion.com/xamarin/system-requirements)

## Troubleshooting
### Path too long exception
If you are facing path too long exception when building this example project, close Visual Studio and rename the repository to short and build the project.
