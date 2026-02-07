type:: Permanent
tags:: #C#, #[[Avalonia UI]], #GUI

- MainWindow.cs
  collapsed:: true
	- ```c#
	  using Avalonia;
	  using Avalonia.Controls;
	  using Avalonia.Layout;
	  using Avalonia.Interactivity;
	  
	  namespace AvaloniaUI
	  {
	      public class MainWindow : Window
	      {
	          public MainWindow()
	          {
	              // 1. Setup the Window
	              this.Title = "C# Only Interface";
	              this.Width = 300;
	              this.Height = 150;
	  
	              // 2. Create the Controls (DOM Elements)
	              var textBox = new TextBox
	              {
	                  Watermark = "Type here...",
	                  Margin = new Thickness(0, 0, 0, 10) // CSS equivalent: margin-bottom
	              };
	  
	              var button = new Button
	              {
	                  Content = "Submit",
	                  HorizontalAlignment = HorizontalAlignment.Stretch // Make button full width
	              };
	  
	              // 3. Create the Layout Container (Like a <div>)
	              // StackPanel stacks items vertically by default, like standard HTML flow
	              var panel = new StackPanel
	              {
	                  Margin = new Thickness(20),
	                  Children = { textBox, button }
	              };
	  
	              // 4. Assign the container to the Window
	              this.Content = panel;
	  
	              // 5. Add Interactivity (Event Listener)
	              button.Click += (sender, args) =>
	              {
	                  // In Avalonia, we access the .Text property instead of .value
	                  var inputVal = textBox.Text;
	  
	                  // Since Avalonia doesn't have a built-in 'alert()', 
	                  // we will update the button text to show the result.
	                  button.Content = "You typed: " + inputVal;
	              };
	          }
	      }
	  }
	  ```
- Program.cs
  collapsed:: true
	- ```C#
	  using Avalonia;
	  using System;
	  
	  namespace AvaloniaUI;
	  
	  class Program
	  {
	      // Initialization code. Don't use any Avalonia, third-party APIs or any
	      // SynchronizationContext-reliant code before AppMain is called: things aren't initialized
	      // yet and stuff might break.
	      [STAThread]
	      public static void Main(string[] args) => BuildAvaloniaApp()
	          .StartWithClassicDesktopLifetime(args);
	  
	      // Avalonia configuration, don't remove; also used by visual designer.
	      public static AppBuilder BuildAvaloniaApp()
	          => AppBuilder.Configure<App>()
	              .UsePlatformDetect()
	              .WithInterFont()
	              .LogToTrace();
	  }
	  
	  ```
- app.cs
  collapsed:: true
	- ```c#
	  using Avalonia;
	  using Avalonia.Controls.ApplicationLifetimes;
	  using Avalonia.Styling;
	  using Avalonia.Themes.Fluent; // Required for FluentTheme
	  
	  namespace AvaloniaUI;
	  
	  public class App : Application
	  {
	      public override void Initialize()
	      {
	          // 1. Replaces RequestedThemeVariant="Default" in XAML
	          RequestedThemeVariant = ThemeVariant.Default;
	  
	          // 2. Replaces <FluentTheme /> in XAML
	          Styles.Add(new FluentTheme());
	      }
	  
	      public override void OnFrameworkInitializationCompleted()
	      {
	          if (ApplicationLifetime is IClassicDesktopStyleApplicationLifetime desktop)
	          {
	              // Ensure this matches your C#-only MainWindow class name
	              desktop.MainWindow = new MainWindow();
	          }
	  
	          base.OnFrameworkInitializationCompleted();
	      }
	  }
	  ```
- AvaloniaUI.csproj
  collapsed:: true
	- ```c#
	  <Project Sdk="Microsoft.NET.Sdk">
	    <PropertyGroup>
	      <OutputType>WinExe</OutputType>
	      <TargetFramework>net9.0</TargetFramework>
	      <Nullable>enable</Nullable>
	      <ApplicationManifest>app.manifest</ApplicationManifest>
	      <AvaloniaUseCompiledBindingsByDefault>true</AvaloniaUseCompiledBindingsByDefault>
	    </PropertyGroup>
	  
	    <ItemGroup>
	      <PackageReference Include="Avalonia" Version="11.3.11" />
	      <PackageReference Include="Avalonia.Desktop" Version="11.3.11" />
	      <PackageReference Include="Avalonia.Themes.Fluent" Version="11.3.11" />
	      <PackageReference Include="Avalonia.Fonts.Inter" Version="11.3.11" />
	      <!--Condition below is needed to remove Avalonia.Diagnostics package from build output in Release configuration.-->
	      <PackageReference Include="Avalonia.Diagnostics" Version="11.3.11">
	        <IncludeAssets Condition="'$(Configuration)' != 'Debug'">None</IncludeAssets>
	        <PrivateAssets Condition="'$(Configuration)' != 'Debug'">All</PrivateAssets>
	      </PackageReference>
	    </ItemGroup>
	  </Project>
	  
	  ```
- AvaloniaUI.sln
  collapsed:: true
	- ```c#
	  Microsoft Visual Studio Solution File, Format Version 12.00
	  # Visual Studio Version 17
	  VisualStudioVersion = 17.5.2.0
	  MinimumVisualStudioVersion = 10.0.40219.1
	  Project("{FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}") = "AvaloniaUI", "AvaloniaUI.csproj", "{87903766-34B5-4865-8AF7-3DBC19878114}"
	  EndProject
	  Global
	  	GlobalSection(SolutionConfigurationPlatforms) = preSolution
	  		Debug|Any CPU = Debug|Any CPU
	  		Release|Any CPU = Release|Any CPU
	  	EndGlobalSection
	  	GlobalSection(ProjectConfigurationPlatforms) = postSolution
	  		{87903766-34B5-4865-8AF7-3DBC19878114}.Debug|Any CPU.ActiveCfg = Debug|Any CPU
	  		{87903766-34B5-4865-8AF7-3DBC19878114}.Debug|Any CPU.Build.0 = Debug|Any CPU
	  		{87903766-34B5-4865-8AF7-3DBC19878114}.Release|Any CPU.ActiveCfg = Release|Any CPU
	  		{87903766-34B5-4865-8AF7-3DBC19878114}.Release|Any CPU.Build.0 = Release|Any CPU
	  	EndGlobalSection
	  	GlobalSection(SolutionProperties) = preSolution
	  		HideSolutionNode = FALSE
	  	EndGlobalSection
	  	GlobalSection(ExtensibilityGlobals) = postSolution
	  		SolutionGuid = {8C26BE11-34A3-43B0-A1C2-59A9452B6ABB}
	  	EndGlobalSection
	  EndGlobal
	  
	  ```
- app.manifest
  collapsed:: true
	- ```xml
	  <?xml version="1.0" encoding="utf-8"?>
	  <assembly manifestVersion="1.0" xmlns="urn:schemas-microsoft-com:asm.v1">
	    <!-- This manifest is used on Windows only.
	         Don't remove it as it might cause problems with window transparency and embedded controls.
	         For more details visit https://learn.microsoft.com/en-us/windows/win32/sbscs/application-manifests -->
	    <assemblyIdentity version="1.0.0.0" name="AvaloniaUI.Desktop"/>
	  
	    <compatibility xmlns="urn:schemas-microsoft-com:compatibility.v1">
	      <application>
	        <!-- A list of the Windows versions that this application has been tested on
	             and is designed to work with. Uncomment the appropriate elements
	             and Windows will automatically select the most compatible environment. -->
	  
	        <!-- Windows 10 -->
	        <supportedOS Id="{8e0f7a12-bfb3-4fe8-b9a5-48fd50a15a9a}" />
	      </application>
	    </compatibility>
	  </assembly>
	  ```