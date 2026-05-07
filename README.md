[Notes for Android Dev With Java.md](https://github.com/user-attachments/files/27499157/Notes.for.Android.Dev.With.Java.md)
>First and foremost, you can right click on the elements that are on the Palette and select "Android Documentation" to learn more about them. Might help while designing layouts.

**Constraint Layout** is the base of a screen basically. The background or whatever you want to call that. Relative Layouts were used before **Constraint Layouts**. There are also **Linear Layouts**.

Widgets are called **Views**. A button, text box , slider etc. on a Constraint Layout is called a View.

Events: when you want a widget to do something, you have to write code that responds to it.

Button -> Event: tap, for example. 

Activities and the Activity Lifecycle *(more about these later in the notes)*

sp -> scale independent pixel (for text)

dp -> device independent pixel

Baseline constraint -> Vertical restriction. Used for aligning widgets horizontally. If a widget has a vertical constraint, you can't create a baseline constraint from it.

Margin -> Allows you to reduce the area that a widget can travel across. It is used for positioning. It is like an offset in a way.

Wrap content for view layout_width or layout_height doesn't respect constraints. Match constraint (0 dp) does.

Start and end properties were introduced in API 17, depending on the scrollbar's position, its indicators change, and for example, if you want to use a right indicator for a right leaning view, you can use right and end to allow compatibility with right to left languages like Persian or Arabic. Or likewise, left and start. **(This doesn't really make sense anymore though, just use end instead of right and end as any device before API 17 doesn't really exist right now.)**

Start = Left
End = Right

While developing, test:

- All rotations (android recreates the current activity when the device orientation changes)

- Dark mode compatibility

- How the experience differs with gesture, 3 buttons and on screen keyboard (all of these change the available screen space)

Widgets are subclasses of View. For example, android.widget.EditText extends android.view.View
Yes, widgets are indeed views.

R class -> resources

Anything in the resources folder **can't have** capital letters. Only underscore, 0 - 9 and lowercase.

Activities (derived class, subclass, child class...) extending AppCompatActivity (backwards compatibility enabling base class, super class, parent class, whatever...) can use bundles to automatically restore **editable** widgets inside an app during runtime. So, in that case, if you change device orientation during runtime then the state of editable widgets will be restored.
Hence why, super.onCreate(savedInstanceState) is used in onCreate definitions of activities. (overriding) note: savedInstanceState is of Bundle type.

write logt then auto-complete to initialize tag variables (per class, activity) and logd to generate logging methods in an activity. (for activity lifecycle check etc.)

alt + insert (on windows) to view available overrides and more... (it is normally accessed through code > generate.. not AI generated)

You can check adb (android debug bridge) commands that were run before starting the app from the run tab.
Use the logcat tab to check anything else.
### 5 main states induced by users using apps

> **First open**: onCreate -> onStart -> onResume 

> **Leave** *(back button or home button on 3 buttons, a full swipe up on gesture navigation or even tapping on anywhere from recents):* onPause -> onStop -> onSaveInstanceState 

>**Open again from recents** *(app still in memory)*: onRestart -> onStart -> onResume

>**Close from recents** *(app is freed from memory, tapping clear all from recents does the same thing):* onPause -> onStop -> onSaveInstanceState -> onDestroy

>**Orientation change** *(rotation of the screen):* onPause -> onStop -> onSaveInstanceState -> onDestroy (a close till here) -> onCreate -> onStart -> onRestoreInstanceState -> onResume (first open + a restore right before resuming)

---

It is important to use **restores and saves** to make sure apps behave normally between rotations.

**Bundles** are objects to pass data around within android (not the only object/way, surely)

A Bundle contains a list of **key-val pairs**. In the onSaveInstanceState and onRestoreInstance methods, android automatically passes a bundle as parameter.

onRestoreInstanceState and onSaveInstanceState methods' order of handling data is different and there is a simple reason.
The super methods handle the saving and restoration of states. So, you modify the bundle first then save with super if in onSaveInstanceState, and if you are in onRestoreInstanceState, you restore the state with super *then* retrieve the data manually using the bundle.

onResume and onPause are where data is *usually* permanently saved.

Keep in mind that activities **aren't destroyed** when you leave apps.

USB OTG (connecting a keyboard and/or mouse to a device) disables touch mode

When a device is in touch mode, widgets are **not focusable** (focusable enables on screen keyboard) except for widgets like editText (disable focusable for editText etc. if you don't want users to interact with them using keyboards)

Some attributes have tri-state checkboxes: - (dash) means default, tick means true *(obviously)* and blank means false.

Some attributes have a wrench next to their name. Those attributes are called **tool attributes**. They only apply to the layout designer which means anything you change with them doesn't *actually* change the app, only the app in the designer.

Select **Create Landscape Qualifier**, it is on top left of the designer, to create a landscape layout variant.

If you get a black screen while trying to run your app in an emulator, try to change the hardware accelaration setting of your emulator from automatic to software.

Android Studio has its own diff tool to compare file/folder(s), you can select a file then go to view > compare with... Make sure your codes are properly formatted/in order before diffs to make the comparison easier.

Guidelines are one of the helper objects used on ConstraintLayout.
Helper objects are not displayed on a device.
Vertical guidelines have a width of zero and the height of their ConstraintLayout parent.
Horizontal guidelines have a height of zero and the width of their ConstraintLayout parent.






