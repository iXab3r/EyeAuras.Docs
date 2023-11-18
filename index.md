<div class="article">

**EyeAuras**  is an automation tool that allows you to model desired behaviour via system of Triggers and Actions. Color search, image search, OCR (text recognition),  global and conditional hotkeys in conjunction with a wide variety of ways to emulate user input bring up an extremely powerful tool to your toolset. And, as a cherry on top, you can always fallback to C# for triggers and actions. 

[Getting Started](/articles/guides/getting-started.html)

![](https://wiki.eyeauras.net/eyeauras_tw5l8cdz4c.png)

## Main concept

-   **Aura** \- combination of Triggers, Actions, Overlays and Enabling conditions. This is what you'll share with others, and this does the actual work.
-   [Enabling conditions](/en/enabling-conditions)
-   **Triggers** \- any kind of state which could be described in Active/NotActive terms. This could be Hotkey (pressed/unpressed or toggle),  foreground Window check (active/not active), Image/Text/Color search result(matched/not matched).  Aura Active/NotActive state is a combination of states of her child Triggers. Trigger has three states:
    -   Active - this means that condition is met, e.g. for WindowIsActive trigger this means that Window with matching title is Active
    -   Not Active - this means that conditions is not met
    -   Unknown - this means that for some reason it is not possible to calculate trigger state. For example, if Window specified in ImageSearch is not found that means that corresponding Trigger will have Unknown state as it is not possible to do comparison without any actual image.
-   **Actions** \- showing notifications, key/mouse presses, sending Telegram messages  or e-mails - these all is considered an Action and could be used inside Aura. Actions could be assigned to one of 3 groups:
    -   On Enter -  these are executed when Aura becomes Active
    -   While Active - these will be executed repeatedly while Auras is Active
    -   On Exit - these are executed when Aura becomes Not Active
-   **Overlays** \- always-on-top overlays which could show text, image, custom UI or anything else. Overlays are a part of Aura and are shown only while Aura is Active

### Triggers

-   [**Fixed Value**](/api/EyeAuras.DefaultAuras.Triggers.Default.html) - the most primitive trigger, you can control it's state by selecting it either manually or by using C# scripts
-   [**Color Search**](/api/EyeAuras.OpenCVAuras.Triggers.ColorSearch.html) - active when Average color of a selected region matches with Target color. Similarity threshold could be specified.
-   [**Image Search**](/api/EyeAuras.OpenCVAuras.Triggers.ImageSearch.html) - active when some Image is found with a specified similarity
-   [**AI/ML Search**](/api/EyeAuras.OpenCVAuras.Triggers.MLSearch.html) \- machine-learning powered [object detection](https://docs.ultralytics.com/tasks/detect/)/[segmentation](https://docs.ultralytics.com/tasks/segment/) or [classification](https://docs.ultralytics.com/tasks/classify/), currently supports only [**Yolo8**](https://docs.ultralytics.com/) **in ONNX format**, may be extended later
-   [**Text Search**](/api/EyeAuras.OpenCVAuras.Triggers.TextSearch.html) - active when recognized text matches with specified expression. It could be comparison by Contains, regexp or C# Lambda
-   [**Aura Is Active**](/api/EyeAuras.DefaultAuras.Triggers.AuraIsActive.html) - active when linked Auras have specified state (Active/NotActive)
-   [**Hotkey Is Active**](/api/EyeAuras.DefaultAuras.Triggers.HotkeyIsActive.html) - active when specified combination of keys is either held down or toggled
-   [**Window Is Active**](/api/EyeAuras.DefaultAuras.Triggers.WinActive.html) \- active when window matching specified expression is active (in foreground)
-   [**Window Exists**](/api/EyeAuras.DefaultAuras.Triggers.WinExists.html) - active when window matching specified expression exists in the system
-   [**Timer**](/api/EyeAuras.DefaultAuras.Triggers.Timer.html) \- periodically activates itself for specified duration
-   [**Message Subscription**](/api/EyeAuras.NetworkAuras.Triggers.MessageSubscription.html) - activates/deactivates when specified message is received from EyeAuras webserver. Messages are separated by Channels and could be sent using SendMessage action
-   [**File Contains**](/api/EyeAuras.DefaultAuras.Triggers.FileContains.html) - activates when specified text is found in specified file
-   [**Telegram Subscription**](/api/EyeAuras.AdvancedAuras.Triggers.TelegramMessage.html) - activates/deactivates when specified message is received in Telegram channel
-   [**Volume Control**](/api/EyeAuras.AdvancedAuras.Triggers.VolumeLevel.html) - activates/deactivates when volume level of specified audio device or process reaches specified threshold
-   **C# Script** \- custom scripts that use the latest version of C# language with full access to internal EyeAuras API. As soon as API will be stabilized there will be examples/docs.

### Actions

-   [**Send**](/en/actions/sendinput/options) \- emulates user input - mouse movement, clicks, keyboard presses, etc. Supports multiple input methods starting from most basic ones that are used WinAPI and all the way to hardware-level emulation that uses Usb2Kbd physical device.
    -   [Input](/en/actions/sendinput/send-input) \- generates single keyboard/mouse event
    -   [Text](/en/actions/sendinput/send-text) - inputs specified text either via clipboard or by typing each character individually
    -   [Sequence](/en/actions/sendinput/send-sequence) - replayed the specified sequence of keyboard presses, mouse clicks and mouse movements
-   [**Play Sound**](/api/EyeAuras.DefaultAuras.Actions.PlaySound.html) - plays specified sound
-   [**Win Activate**](/api/EyeAuras.DefaultAuras.Actions.WinActivate.html) - activates specified window
-   [**Delay**](/api/EyeAuras.DefaultAuras.Actions.Delay.html) \- waits for some time before proceeding to the next action
-   [**Send To Telegram**](/api/EyeAuras.AdvancedAuras.Actions.SendToTelegram.html) - sends message to Telegram channel
-   [**Send Message**](/api/EyeAuras.NetworkAuras.Actions.SendMessage.html) - sends network message through EyeAuras infrastructure to a specified Channel. All other instances of EyeAuras on other computers can subscribe and process these messages via Message Subscription trigger
-   **C# Script** \- custom scripts that use the latest version of C# language with full access to internal EyeAuras API. As soon as API will be stabilized there will be examples/docs.

### Overlays

-   [**Text**](/en/overlays/text) \- shows text, content could be modified either manually or using C# scripts
-   [**Image**](/en/overlays/image) \- shows an image, animated/transparent GIFs are supported
-   [**Replica**](/en/overlays/replica) \- created a real-time visual clone of any specified window or its subregion. This allows you to clone parts of UI (e.g. bring cooldowns closer to the middle of you screen) or show downsized version of YouTube player while farming
-   [**Dependencies Viewer**](/en/overlays/dependencies-viewer) \- debugging tool which could be used to check what states linked Auras have. Very useful for debugging complex models.
-   [**Custom UI**](/en/overlays/custom-ui) \- allows you to develop a full-blown custom user interface using combination of [Microsoft Razor Pages](https://learn.microsoft.com/en-us/aspnet/core/razor-pages/?view=aspnetcore-7.0&tabs=visual-studio) (html+css+js) and **C#** to wire it all together inside EyeAuras

</div>