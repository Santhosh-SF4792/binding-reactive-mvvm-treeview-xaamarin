# binding-reactive-mvvm-treeview-xaamarin

The SfTreeView allows you to bind ItemTemplate to the reactive UI ViewModel which is a composable and cross-platform model-view-viewmodel framework for all .NET platforms.

## Sample

To achieve this, follow the below steps:

STEP 1: Install the ReactiveUI and ReactiveUI.XamForms in your project.

STEP 2: Create ViewModel which should implement ReactiveObject.
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
STEP 4: View can be connected in one-way dependent manner to the ViewModel through bindings. You can set the BindingContext for the SfTreeView in MainPage.cs itself in code behind like below.
### C#
```csharp
public partial class MainPage : ReactiveContentPage<ViewModel>
{
    public MainPage(ViewModel viewModel)
    {
        ViewModel = viewModel;
        InitializeComponent();
    }
}
```

## Requirements to run the demo
Visual Studio 2017 or Visual Studio for Mac.
Xamarin add-ons for Visual Studio (available via the Visual Studio installer).

## Troubleshooting
### Path too long exception
If you are facing path too long exception when building this example project, close Visual Studio and rename the repository to short and build the project.

## License

Syncfusion® has no liability for any damage or consequence that may arise from using or viewing the samples. The samples are for demonstrative purposes. If you choose to use or access the samples, you agree to not hold Syncfusion® liable, in any form, for any damage related to use, for accessing, or viewing the samples. By accessing, viewing, or seeing the samples, you acknowledge and agree Syncfusion®'s samples will not allow you seek injunctive relief in any form for any claim related to the sample. If you do not agree to this, do not view, access, utilize, or otherwise do anything with Syncfusion®'s samples.

## Conclusion

I hope you enjoyed learning about how to do binding reactive mvvm in Xamarin.Forms TreeView (SfTreeView).

You can refer to our Xamarin.Forms TreeViewfeature tour page to know about its other groundbreaking feature representations and documentation, and how to quickly get started for configuration specifications.

For current customers, you can check out our components from the License and Downloads page. If you are new to Syncfusion, you can try our 30-day free trial to check out our other controls.

If you have any queries or require clarifications, please let us know in the comments section below. You can also contact us through our support forums, Direct-Trac, or feedback portal. We are always happy to assist you!