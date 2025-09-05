# binding-reactive-mvvm-treeview-xaamarin

The SfTreeView allows you to bind ItemTemplate to the reactive UI ViewModel which is a composable and cross-platform model-view-viewmodel framework for all .NET platforms.

**[View document in Syncfusion Xamarin Knowledge base](https://www.syncfusion.com/kb/12181/how-to-bind-data-using-reactive-mvvm-in-xamarin-forms-treeview-sftreeview)**

## Sample

To achieve this, follow the below steps:

STEP 1: Install the ReactiveUI and ReactiveUI.XamForms in your project.

STEP 2: Create ViewModel which should implement ReactiveObject.
```csharp
public class ViewModel : ReactiveObject
{
    #region Fields
 
    private ObservableCollection<FileManager> imageNodeInfo;
 
    #endregion
 
    #region Constructor
 
    public ViewModel()
    {
        GenerateSource();
    }
 
    #endregion
 
    #region Properties
 
    public ObservableCollection<FileManager> ImageNodeInfo
    {
        get { return imageNodeInfo; }
        set { this.RaiseAndSetIfChanged(ref imageNodeInfo, value); }
    }
 
    #endregion
    #region Generate Source
    private void GenerateSource()
    {
        var nodeImageInfo = new ObservableCollection<FileManager>();
        Assembly assembly = typeof(MainPage).GetTypeInfo().Assembly;
        var doc = new FileManager() { ItemName = "Documents", ImageIcon = ImageSource.FromResource("TreeViewXamarin.Icons.treeview_folder.png", assembly) };
        var download = new FileManager() { ItemName = "Downloads", ImageIcon = ImageSource.FromResource("TreeViewXamarin.Icons.treeview_folder.png", assembly) };
        var mp3 = new FileManager() { ItemName = "Music", ImageIcon = ImageSource.FromResource("TreeViewXamarin.Icons.treeview_folder.png", assembly) };
        var pictures = new FileManager() { ItemName = "Pictures", ImageIcon = ImageSource.FromResource("TreeViewXamarin.Icons.treeview_folder.png", assembly) };
        var video = new FileManager() { ItemName = "Videos", ImageIcon = ImageSource.FromResource("TreeViewXamarin.Icons.treeview_folder.png", assembly) };
 
        var pollution = new FileManager() { ItemName = "Environmental Pollution.docx", ImageIcon = ImageSource.FromResource("TreeViewXamarin.Icons.treeview_word.png", assembly) };
        var globalWarming = new FileManager() { ItemName = "Global Warming.ppt", ImageIcon = ImageSource.FromResource("TreeViewXamarin.Icons.treeview_ppt.png", assembly) };
        var sanitation = new FileManager() { ItemName = "Sanitation.docx", ImageIcon = ImageSource.FromResource("TreeViewXamarin.Icons.treeview_word.png", assembly) };
        var socialNetwork = new FileManager() { ItemName = "Social Network.pdf", ImageIcon = ImageSource.FromResource("TreeViewXamarin.Icons.treeview_pdf.png", assembly) };
        var youthEmpower = new FileManager() { ItemName = "Youth Empowerment.pdf", ImageIcon = ImageSource.FromResource("TreeViewXamarin.Icons.treeview_pdf.png", assembly) };
 
        var games = new FileManager() { ItemName = "Game.exe", ImageIcon = ImageSource.FromResource("TreeViewXamarin.Icons.treeview_exe.png", assembly) };
        var tutorials = new FileManager() { ItemName = "Tutorials.zip", ImageIcon = ImageSource.FromResource("TreeViewXamarin.Icons.treeview_zip.png", assembly) };
        var typeScript = new FileManager() { ItemName = "TypeScript.7z", ImageIcon = ImageSource.FromResource("TreeViewXamarin.Icons.treeview_zip.png", assembly) };
        var uiGuide = new FileManager() { ItemName = "UI-Guide.pdf", ImageIcon = ImageSource.FromResource("TreeViewXamarin.Icons.treeview_pdf.png", assembly) };
 
        var song = new FileManager() { ItemName = "Gouttes", ImageIcon = ImageSource.FromResource("TreeViewXamarin.Icons.treeview_mp3.png", assembly) };
 
        var camera = new FileManager() { ItemName = "Camera Roll", ImageIcon = ImageSource.FromResource("TreeViewXamarin.Icons.treeview_folder.png", assembly) };
        var stone = new FileManager() { ItemName = "Stone.jpg", ImageIcon = ImageSource.FromResource("TreeViewXamarin.Icons.treeview_png.png", assembly) };
        var wind = new FileManager() { ItemName = "Wind.jpg", ImageIcon = ImageSource.FromResource("TreeViewXamarin.Icons.treeview_png.png", assembly) };
 
        var img0 = new FileManager() { ItemName = "WIN_20160726_094117.JPG", ImageIcon = ImageSource.FromResource("TreeViewXamarin.Icons.treeview_img0.png", assembly) };
        var img1 = new FileManager() { ItemName = "WIN_20160726_094118.JPG", ImageIcon = ImageSource.FromResource("TreeViewXamarin.Icons.treeview_img1.png", assembly) };
 
        var video1 = new FileManager() { ItemName = "Naturals.mp4", ImageIcon = ImageSource.FromResource("TreeViewXamarin.Icons.treeview_video.png", assembly) };
        var video2 = new FileManager() { ItemName = "Wild.mpeg", ImageIcon = ImageSource.FromResource("TreeViewXamarin.Icons.treeview_video.png", assembly) };
 
        doc.SubFiles = new ObservableCollection<FileManager>
        {
            pollution,
            globalWarming,
            sanitation,
            socialNetwork,
            youthEmpower
        };
 
        download.SubFiles = new ObservableCollection<FileManager>
        {
            games,
            tutorials,
            typeScript,
            uiGuide
        };
 
        mp3.SubFiles = new ObservableCollection<FileManager>
        {
            song
        };
 
        pictures.SubFiles = new ObservableCollection<FileManager>
        {
            camera,
            stone,
            wind
        };
        camera.SubFiles = new ObservableCollection<FileManager>
        {
            img0,
            img1
        };
 
        video.SubFiles = new ObservableCollection<FileManager>
        {
            video1,
            video2
        };
 
        nodeImageInfo.Add(doc);
        nodeImageInfo.Add(download);
        nodeImageInfo.Add(mp3);
        nodeImageInfo.Add(pictures);
        nodeImageInfo.Add(video);
        imageNodeInfo = nodeImageInfo;
    }
    #endregion
}
```

STEP 3: ContentPage should inherit from ReactiveContentPage<TViewModel> and we are going to use ReactiveUI Binding to bind our ViewModel to our View.
### XAML
```xaml
<ContentPage.Content>
    <syncfusion:SfTreeView x:Name="treeView"
                       ItemHeight="40"
                       Indentation="15"
                       ExpanderWidth="40"
                       ChildPropertyName="SubFiles"
                       ItemTemplateContextType="Node"
                       ItemsSource="{Binding ImageNodeInfo}"
                        >
        <syncfusion:SfTreeView.ItemTemplate>
            <DataTemplate>
                <Grid x:Name="grid" RowSpacing="0" >
                    <Grid.RowDefinitions>
                        <RowDefinition Height="*" />
                        <RowDefinition Height="1" />
                    </Grid.RowDefinitions>
                    <Grid RowSpacing="0" Grid.Row="0">
                        <Grid.ColumnDefinitions>
                            <ColumnDefinition Width="40" />
                            <ColumnDefinition Width="*" />
                        </Grid.ColumnDefinitions>
                        <Grid Padding="5,5,5,5">
                            <Image Source="{Binding Content.ImageIcon}"
                               VerticalOptions="Center"
                               HorizontalOptions="Center"
                               HeightRequest="35" 
                               WidthRequest="35"/>
                        </Grid>
                        <Grid Grid.Column="1"              
                          RowSpacing="1"
                          Padding="1,0,0,0"
                          VerticalOptions="Center">
                            <Label LineBreakMode="NoWrap"
                               Text="{Binding Content.ItemName}"
                               VerticalTextAlignment="Center">
                            </Label>
                        </Grid>
                    </Grid>
                    <StackLayout Grid.Row="1"/>
                </Grid>
            </DataTemplate>
        </syncfusion:SfTreeView.ItemTemplate>
    </syncfusion:SfTreeView>
</ContentPage.Content>
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