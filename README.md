# Windows 11 Desktop ListView Enforcer 
##### Tested on Microsoft Windows 11 Professional (x64) Build 26300.9974 (26H2)
##### A lightweight, unobtrusive and rock-solid utility that keeps the Windows 11 desktop icon view set to **ListView mode**.
#

**Windows 11 Desktop ListView Enforcer** runs in the background and monitors the desktop ListView control. 

When accessing icon views from desktop context menu it will always conform the sizing in the listview mode.

The utility is designed to remain active during normal Windows use and recover when Windows Explorer restarts.

You will not see a change or revert of the desktop icon view size, particularly after Explorer restarts or crashes. This will not ever happen.

## Features

- **Automatic enforcement / Continuous background monitoring**  
  Monitors the Windows desktop ListView control and ensures that it is enforced.

- **Ctrl + Mouse Wheel correction**  
  The desktop icon sizes may be changed by holding Ctrl and scrolling the mouse wheel, which can make the listview icons larger if needed and also revert back the other way to restore the listview/small icons mode.

- **Explorer restart detection**  
  Monitors the Windows Explorer process ID to detect when Explorer has restarted, rather than relying solely on whether the desktop window exists.
  When Explorer restarts, the utility invalidates its previous desktop window reference and searches for the newly created desktop ListView control.

- **Window handle validation**  
  Checks whether its cached ListView window handle is still valid. If the handle is no longer valid, it attempts to locate the current desktop ListView again.

- **Automatic recovery after an Explorer crash**  
  If Explorer crashes or is forcibly terminated and subsequently restarted, the utility continues monitoring, waits for the desktop interface to become available, rediscovers the ListView control and resumes enforcing Small icons mode.

- **Controlled redraw**  
  Temporarily suppresses redraw while applying a required style change, then refreshes the desktop ListView.

- **Single-instance protection**  
  Uses a global Windows mutex to prevent multiple instances of the utility from running simultaneously.

## Installation

1. Download `DesktopListView_Enforcer.exe` from the GitHub Releases section.
2. Place the executable in a permanent folder of your choice.
3. Do not delete or move the executable after configuring Task Scheduler.

## Configure Windows Task Scheduler

For automatic operation whenever you sign in to Windows, configure the utility to run at user logon.

1. Open the Windows Start menu.
2. Search for **Task Scheduler** and open it.
3. Select **Create Task** (not Create Basic Task).
4. Under the **General** tab:
   - Name: `Windows 11 Desktop ListView Enforcer`
   - Select **Run only when user is logged on**.
   - Leave **Run with highest privileges** unchecked.
5. Open the **Triggers** tab.
   - Select **New**.
   - Begin the task: **At log on**.
   - Select your user account.
   - Click OK.
6. Open the **Actions** tab.
   - Select **New**.
   - Action: **Start a program**.
   - Browse to the location of `DesktopListView_Enforcer.exe`.
   - Click OK.
7. Under the **Conditions** tab, review the settings and disable any conditions that could prevent the task from starting when you sign in.
8. Under the **Settings** tab:
   - Allow the task to be run on demand.
   - If the task is already running, select **Do not start a new instance**.
9. Click OK to save the task.

The utility should now start automatically each time you sign in to Windows.

## Operation

Once running, the utility operates in the background.

It monitors the desktop ListView control and intervenes only when the view needs correcting.

If you change the desktop icon size using Ctrl + Mouse Wheel, the utility detects the changed view and restores Small icons mode automatically.

If Windows Explorer restarts, the utility detects the changed Explorer process, discards stale window references and searches for the recreated desktop ListView control. It retries discovery while the desktop interface is being rebuilt.

Once the new ListView control is available, normal monitoring and enforcement resume.

The utility does not need to be manually restarted after an Explorer restart.

## Important Notes

- This utility has only been tested as working on Windows 11 64-bit OS.
- It must run within your logged-in Windows desktop session to interact with the desktop ListView.
- Task Scheduler is recommended for automatic startup. Although it can be run manually for testing.
- Single-instance protection prevents accidental duplicate instances.

## Project

**Repository:** Windows-11-Desktop-ListView-Enforcer

**Executable:** `DesktopListView_Enforcer.exe`

**Platform:** Windows 11, 64-bit

**Distribution:** Compiled executable

## Disclaimer

This is an independent Windows utility. It is provided as-is, without any guarantee of compatibility with every future Windows update or Explorer implementation.

Use at your own discretion.
