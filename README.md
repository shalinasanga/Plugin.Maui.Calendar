+
# Calendar Plugin for .NET MAUI

This is a .NET MAUI port of the [lilcodelab](https://github.com/lilcodelab/) Xamarin.Forms  [Calendar Plugin](https://github.com/lilcodelab/Xamarin.Plugin.Calendar)

 Available on NuGet: <https://www.nuget.org/packages/Plugin.Maui.Calendar> [![NuGet](https://img.shields.io/nuget/v/Plugin.Maui.Calendar.svg?label=NuGet)](https://www.nuget.org/packages/Plugin.Maui.Calendar/)


Simple cross-platform plugin for Calendar control featuring:
- Displaying events by binding EventCollection
- Localization support with System.Globalization.CultureInfo
- Customizable colors, day view sizes/label styles, custom Header/Footer template support
- UI reactive to EventCollection, Culture, and other changes 

### What's new
V2.0.0
* Updated to .NET 9
* Optimized startup time: iOS 20 % / Android 40 % 
* Fixed memory leaks* 
* Revamped calendar structure
* Added **Styles** (check [Available Styles](#available-styles) section) that replace some **properties**
* Added **WeekendTitleStyle**
* Added sample page (Default calendar) to test memory leaks with [MemoryToolkit.Maui](https://github.com/AdamEssenmacher/MemoryToolkit.Maui) )
* Updated samples
* Added native digits support (added **UseNativeDigits** Property)
* Added **OtherMonthWeekIsVisible** and **DayViewBorderMargin** properties

### Breaking  Changes

Properties that Styles have replaced
```xml
DayViewFontSize --> DaysLabelStyle
MonthLabelColor --> MonthLabelStyle
YearLabelColor --> YearLabelStyle

ArrowsBackgroundColor, ArrowsBorderColor, ArrowsBorderWidth, ArrowsFontAttribute, ArrowsFontSize, ArrowsFontFamily, ArrowsColor --> 
ArrowsSymbolPrev --> PreviousMonthArrowButtonStyle
ArrowsSymbolNext --> NextMonthArrowButtonStyle
ArrowsSymbolPrev --> PreviousYearArrowButtonStyle
ArrowsSymbolNext --> NextYearArrowButtonStyle

ArrowsFontFamily, ArrowsColor --> FooterArrowLabelStyle
SelectedDateColor --> SelectedDateLabelStyle

DaysTitleHeight, DaysTitleColor --> DaysTitleLabelStyle
DaysTitleHeight, DaysTitleWeekendColor --> WeekendTitleStyle
```
> ⚠️ **Breaking Change**:  
> The `SelectedDates` property is now an `ObservableCollection<DateTime>`.  
> To ensure the calendar updates when dates are added/removed, use:
>
> ```csharp
> SelectedDates = new ObservableCollection<DateTime> { ... };
> ```
>
> Do not use `List<DateTime>` for `SelectedDates` binding.

V1.0.x
* Removed all the platform-specific code, hence it supports all available .NET MAUI backends: iOS, Android, Windows, Mac, Tizen (not tested yet)
* Added Multiselection support (Latest PR that was not merged previously)
* Refactored and revamped code
* Updated to .NET 8
* Added OnShownDateChangedCommand so we can take action when a date is changed.
* Added new property **OtherMonthSelectedDayColor**
* Fixed bug with **OtherMonthDayIsVisible** property
* Added a weekend calendar sample
* Added a Windows 11 calendar sample
* Added theme support
* Added new property **FirstDayOfWeek**
* Added support for multiple event dots (multidots) in calendar 
* Added **MonthChanged** Event and **MonthChangedCommand**
* Added **AllowDeselecting** property
* Added **SelectedDatesRangeBackgroundColor** property
* Updated samples

## YouTube
[![Free and Complete Calendar Control for .NET MAUI: Plugin.Maui.Calendar](https://img.youtube.com/vi/bmkizbS4jb4/0.jpg)](https://www.youtube.com/watch?v=bmkizbS4jb4)


## Screenshots
| Android | iOS |
| ------- | ------ |
| ![Android Calendar Screenshot](https://github.com/yurkinh/Plugin.Maui.Calendar/blob/main/res/android.png) | ![iPhone Calendar Screenshot](https://github.com/yurkinh/Plugin.Maui.Calendar/blob/main/res/ios.png) |

| Win     | Mac    |
| ------- | ------ |
| ![Windiws Calendar Screenshot](https://github.com/yurkinh/Plugin.Maui.Calendar/blob/main/res/win.png) | ![Mac Calendar Screenshot](https://github.com/yurkinh/Plugin.Maui.Calendar/blob/main/res/mac.png) |

Theme support
| Ligth | Dark | Settings |
| ------- | ------ | ------ |
| ![Light theme Screenshot](https://github.com/yurkinh/Plugin.Maui.Calendar/blob/main/res/LightTheme.png) | ![Dark theme Screenshot](https://github.com/yurkinh/Plugin.Maui.Calendar/blob/main/res/DarkTheme.png) | ![Settings Page Screenshot](https://github.com/yurkinh/Plugin.Maui.Calendar/blob/main/res/ThemeSettingPage.png) |

Culture support
| Android | iOS |
| ------- | ------ |
| ![Android Culture Screenshot](https://github.com/yurkinh/Plugin.Maui.Calendar/blob/main/res/Culture_support_android.png) | ![iPhone Culture Screenshot](https://github.com/yurkinh/Plugin.Maui.Calendar/blob/main/res/Culture_support_iOS.png) |


# New Samples

Windows 11 calendar
| Win     | Mac    |
| ------- | ------ |
| ![Windiws 11 android Calendar Screenshot](https://github.com/yurkinh/Plugin.Maui.Calendar/blob/main/res/W11_android.png) | ![Windiws 11 Calendar IOS Screenshot](https://github.com/yurkinh/Plugin.Maui.Calendar/blob/main/res/W11_ios.png) |

Weekend calendar
| Android     | IOS    |
| ------- | ------ |
| ![Weekend calendar Android Screenshot](https://github.com/yurkinh/Plugin.Maui.Calendar/blob/main/res/WeekendCalendar_android.png) | ![Weekend calendar IOS Screenshot](https://github.com/yurkinh/Plugin.Maui.Calendar/blob/main/res/WeekendCalendar_ios.png) |

### Usage
To get started just install the package via Nuget.
You can take a look on the sample app to get started or continue reading.

Reference the following xmlns to your page:
```xml
xmlns:controls="clr-namespace:Plugin.Maui.Calendar.Controls;assembly=Plugin.Maui.Calendar" 
```

Basic control usage:
```xml
<controls:Calendar
        Day="14"
        Month="5"
        Year="2019"
        VerticalOptions="Fill"
        HorizontalOptions="Fill"/>
```

Bindable properties:
* `Culture` _CultureInfo_ calender culture/language
* `Day` _int_ currently viewing day
* `Month` _int_ currently viewing month
* `Year` _int_ currently viewing year
* `Events` _EventCollection_ (from package) your events for calender
* Custom colors, fonts, sizes ...


__Remark: You can use `ShownDate` as an alternative to `Year`, `Month` and `Day`__
```xml
<controls:Calendar
        ShownDate="2019-05-14"
        VerticalOptions="Fill"
        HorizontalOptions="Fill"/>
```

#### Binding events:
In your XAML, add the data template for events, and bind the events collection, example:
```xml
<controls:Calendar
    Events="{Binding Events}">
    <controls:Calendar.EventTemplate>
        <DataTemplate>
            <StackLayout
                Padding="15,0,0,0">
                <Label
                    Text="{Binding Name}"
                    FontAttributes="Bold"
                    FontSize="Medium" />
                <Label
                    Text="{Binding Description}"
                    FontSize="Small"
                    LineBreakMode="WordWrap" />
            </StackLayout>
        </DataTemplate>
    </controls:Calendar.EventTemplate>
</controls:Calendar>
```

In your ViewModel reference the following namespace:
```csharp
using Plugin.Maui.Calendar.Models;
```

Add property for Events:
```csharp
public EventCollection Events { get; set; }
```

Initialize Events with your data:
```csharp
 Events = new EventCollection
 {
    [DateTime.Now] = new List<EventModel>
    {
        new() { Name = "Cool event1", Description = "This is Cool event1's description!" },
        new() { Name = "Cool event2", Description = "This is Cool event2's description!" }
    },
    // 5 days from today
    [DateTime.Now.AddDays(5)] = new List<EventModel>
    {
        new() { Name = "Cool event3", Description = "This is Cool event3's description!" },
        new() { Name = "Cool event4", Description = "This is Cool event4's description!" }
    },
    // 3 days ago
    [DateTime.Now.AddDays(-3)] = new List<EventModel>
    {
        new() { Name = "Cool event5", Description = "This is Cool event5's description!" }
    },
    // custom date
    [new DateTime(2024, 3, 16)] = new List<EventModel>
    {
        new() { Name = "Cool event6", Description = "This is Cool event6's description!" }
    }
 };
```

Initialize Events with your data and a different dot color per day:
```csharp
Events = new EventCollection
{
    //2 days ago
    [DateTime.Now.AddDays(-2)] = new DayEventCollection<EventModel>(Colors.Purple, Colors.Purple)
    {
        new() { Name = "Cool event1", Description = "This is Cool event1's description!" },
        new() { Name = "Cool event2", Description = "This is Cool event2's description!" }
    },
    // 5 days ago
    [DateTime.Now.AddDays(-5)] = new DayEventCollection<EventModel>(Colors.Blue, Colors.Blue)
    {
        new() { Name = "Cool event3", Description = "This is Cool event3's description!" },
        new() { Name = "Cool event4", Description = "This is Cool event4's description!" }
    },
};
//4 days ago
Events.Add(DateTime.Now.AddDays(-4), new DayEventCollection<EventModel>(GenerateEvents(10, "Cool")) { EventIndicatorColor = Colors.Green, EventIndicatorSelectedColor = Colors.Green });
```

Where `EventModel` is just an example, it can be replaced by any data model you desire.

`EventsCollection` is just a wrapper over `Dictionary<DateTime, ICollection>` exposing custom `Add` method and `this[DateTime]` indexer which internally extracts the `.Date` component of `DateTime` values and uses it as a key in this dictionary.

`DayEventCollection` is just a wrapper over `List<T>` exposing custom properties `EventIndicatorColor` and `EventIndicatorSelectedColor` for assigning a custom color to the dot.


#### DayTappedCommand
The **DayTappedCommand** is triggered when a user taps on a specific day in the calendar.

XAML Usage:
```xml
DayTappedCommand="{Binding DayTappedCommand}"
```


#### Set up culture

In your ViewModel add property for Culture:
```csharp
public CultureInfo Culture => new CultureInfo("hr-HR")
```

In XAML add Culture binding
```xml
<controls:Calendar
    Culture="{Binding Culture}"/>
</controls:Calendar>
```

#### Available color customization
Sample properties:
```xml
EventIndicatorColor="Red"
EventIndicatorSelectedColor="White"
DeselectedDayTextColor="Blue"
OtherMonthDayColor="Gray"
SelectedDayTextColor="Cyan"
SelectedDayBackgroundColor="DarkCyan"
SelectedTodayTextColor="Green"
TodayOutlineColor="Blue"
TodayFillColor="Silver"
TodayTextColor="Yellow"
OtherMonthSelectedDayColor="HotPink"
```

#### Available Styles
| Style Key                       | Based On (`DefaultStyles`)                           |
| ------------------------------- | ---------------------------------------------------- |
| `DaysLabelStyle`                | `DefaultStyles.DefaultLabelStyle`                    |
| `MonthLabelStyle`               | `DefaultStyles.DefaultMonthLabelStyle`               |
| `YearLabelStyle`                | `DefaultStyles.DefaultYearLabelStyle`                |
| `PreviousMonthArrowButtonStyle` | `DefaultStyles.DefaultPreviousMonthArrowButtonStyle` |
| `NextMonthArrowButtonStyle`     | `DefaultStyles.DefaultNextMonthArrowButtonStyle`     |
| `PreviousYearArrowButtonStyle`  | `DefaultStyles.DefaultPreviousYearArrowButtonStyle`  |
| `NextYearArrowButtonStyle`      | `DefaultStyles.DefaultNextYearArrowButtonStyle`      |
| `FooterArrowLabelStyle`         | `DefaultStyles.DefaultFooterArrowLabelStyle`         |
| `SelectedDateLabelStyle`        | `DefaultStyles.DefaultSelectedDateLabelStyle`        |
| `WeekdayTitleStyle`             | `DefaultStyles.DefaultDaysTitleLabelStyle`           |
| `WeekendTitleStyle`             | `DefaultStyles.DefaultWeekendTitleStyle`             |


#### Available customization properties
```xml
FirstDayOfWeek="Monday"
UseNativeDigits="True"
OtherMonthWeekIsVisible="False"
DayViewBorderMargin
```

#### Calendar Layout customizations
You can set the layout of the calendar with the property `CalendarLayout`

- Available layouts are: 

    `OneWeek` - only one week is shown

    `TwoWeeks` - two weeks are shown

    `Month` - the whole month is shown (default value)

```xml
CalendarLayout="Month"
```

You can also choose to display the shown week number instead of the month name

```xml
CalendarLayout="Week"
WeekViewUnit="WeekNumber"
```

##### Event indicator customizations
You can customize how the event indication will look with the property `EventIndicatorType`

- Available indicators are: 
`BottomDot` - event indicator as dot bellow of date in the calendar (default value)
`TopDot` - event indicator as the dot on top of the date in the calendar
`Background` - event indicator as colored background in calendar
`BackgroundFull` // event indicator as larger size colored background in the calendar

```xml
EventIndicatorType="Background"
```
##### Calendar swipe customizations
You can write your own customizations commands for swipe. 
```xml
SwipeLeftCommand="{Binding SwipeLeftCommand}"
SwipeRightCommand="{Binding SwipeRightCommand}"
SwipeUpCommand="{Binding SwipeUpCommand}"
```

You can also disable default swipe actions.
```xml
SwipeToChangeMonthEnabled="False"
SwipeUpToHideEnabled="False"
```

##### Selection type of calendar

You can either use the `Calender` class implementation for a single selection mode, multiselection mode or `RangeSelectionCalendar` for a range selection mode.

```xml
    <plugin:Calendar
        SelectedDate="{Binding SelectedDate}"/>
```
On the `RangeSelectionCalendar` you can use binding for start date `SelectedStartDate` and end date `SelectedEndDate` or get list of selected dates with `SelectedDates`.
```xml
    <plugin:RangeSelectionCalendar
        x:Name="rangedCalendar"
        SelectedDates="{Binding SelectedDates}"
        SelectedEndDate="{Binding SelectedEndDate}"
        SelectedStartDate="{Binding SelectedStartDate}">
```
On the `MultiselectionCalendar` you can select multiple separate dates

```xml
    plugin:MultiSelectionCalendar
        Events="{Binding Events}"
        MaximumDate="{Binding MaximumDate}"
        MinimumDate="{Binding MinimumDate}"
        Month="{Binding Month}" >
```

__Remark: Don't use both `SelectedDates` and `SelectedStartDate`/`SelectedEndDate`__

##### Other customizations

Enable/Disable the visibility of the Events scrollview panel at the bottom
Sample properties:
```xml
EventsScrollViewVisible="True"
```

#### Section templates
There are several templates that can be used to customize the calendar. You can find an example for each one in the AdvancedPage.xaml.
You can create your own custom control file or you can also write customization directly inside of Templates.

##### Calendar control sections
These sections provide customization over appearance of the controls of the calendar, like showing the selected month and year, month selection controls etc.

###### HeaderSectionTemplate
Customize the header section (top of the calendar control). Example from AdvancedPage.xaml
```xml
<plugin:Calendar.HeaderSectionTemplate>
    <controls:CalendarHeader />
</plugin:Calendar.HeaderSectionTemplate>
```

###### FooterSectionTemplate
Customize the footer section (under the calendar part, above the events list). Example from AdvancedPage.xaml
```xml
<plugin:Calendar.FooterSectionTemplate>
    <DataTemplate>
        <controls:CalendarFooter />
    </DataTemplate>
</plugin:Calendar.FooterSectionTemplate>
```

###### BottomSectionTemplate
Customize the bottom section (at the bottom of the calendar control, below the events list). Example from AdvancedPage.xaml
```xml
<plugin:Calendar.BottomSectionTemplate>
    <controls:CalendarBottom />
</plugin:Calendar.BottomSectionTemplate>
```

##### Event templates
These templates provide customization for the events list.

###### EventTemplate
Customize the appearance of the events section. Example from AdvancedPage.xaml
```xml
<plugin:Calendar.EventTemplate>
    <DataTemplate>
        <controls:CalenderEvent CalenderEventCommand="{Binding BindingContext.EventSelectedCommand, Source={x:Reference advancedCalendarPage}}" />
    </DataTemplate>
</plugin:Calendar.EventTemplate>
```

###### EmptyTemplate
Customize what to show in case the selected date has no events. Example from AdvancedPage.xaml
```xml
<plugin:Calendar.EmptyTemplate>
    <DataTemplate>
        <StackLayout>
            <Label Text="NO EVENTS FOR THE SELECTED DATE" HorizontalTextAlignment="Center" Margin="0,5,0,5" />
        </StackLayout>
    </DataTemplate>
</plugin:Calendar.EmptyTemplate>
```
