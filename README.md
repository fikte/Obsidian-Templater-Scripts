# Obsidian Templater Scripts


## ⚙️ Setup Instructions

To use this script, you first need the [Templater](https://silentvoid.github.io/templater/) community plugin installed and enabled in Obsidian.

1.  **Ensure Templater is Enabled**
    *   Go to `Settings` > `Community Plugins` and make sure the toggle for `Templater` is on.
    *   The script uses core Templater functions that are enabled by default, so **no other specific settings need to be changed** for it to work.

2.  **Save the Script File**
    *   Create a new file in your designated Templater templates folder (you can find this location in `Settings` > `Templater` > `Template folder location`).
    *   Name the file something memorable, like `Task Helper.md`.
    *   Copy and paste the entire script code into this new file.

3.  **Assign a Hotkey (Recommended)**
    *   For fast and convenient use, assign a keyboard shortcut to this template.
    *   Go to `Settings` > `Hotkeys`.
    *   Search for the name of your template (e.g., "Task Helper").
    *   Click the `+` icon to set a custom hotkey, such as `Ctrl+T` or `⌘+T`. This will allow you to run the script from anywhere in Obsidian.


---

## List of Templater scripts in this repo: 

Scripts/

├─ [Task - New & Convert](https://github.com/fikte/Obsidian-Templater-Scripts/tree/main?tab=readme-ov-file#task---new--convert)

├─ [Update Npte Creation Date (macOS Only)](https://github.com/fikte/Obsidian-Templater-Scripts/tree/main?#update-note-creation-date-macos-only)


# Task - New & Convert

Designed to streamline the creation and modification of tasks. It provides an interactive, prompt-based workflow to quickly set task types, add multiple tags, and assign dates, all without manually typing complex syntax.

The script is intelligent: it remembers your last-used tagon your device, pre-selects existing values when editing a task, and places your cursor exactly where you need it next. Use the keyboard to navigate and select as necessary. 

### ✨ Features

*   **Works with the Emoji or Dataview formats from the Tasks plugin**
*   **Interactive Workflow**: Uses pop-up menus to guide you through creating or editing a task. 
*   **Comprehensive Task Types**: Comes with 23 pre-configured task statuses, including to-do, in-progress, cancelled, important, idea, and more.
*   **Set alerts times (works with my Calendar Period Week Notes plugin)**:
    * Select and alert date time from a list of up to two weeks before the due date, or enter the alert date / time manually
*   **Choose and easily set the tag priority**:
    *   Chosoe the priotiy to set your task.      
*   **Advanced Tag Management**:
    *   Interactively add or remove multiple tags.
    *   Remembers the last tag you used and automatically applies it to new tasks.
    *   Supports a pre-defined list of common tags and allows for custom one-off tags.
*   **Smart Date Picker**:
    *   Offers dynamic suggestions for "Today," "Tomorrow," and upcoming weekdays.
    *   Allows for manual date entry or selecting no date at all.
*   **Context-Aware Editing**: When you run the script on an existing task line, it automatically reads its current type, tags, and date, placing them at the top of the suggestion list for quick changes.
*   **Intelligent Cursor Placement**:
    *   For **new tasks**, the cursor is placed after the tags, ready for you to type the description.
    *   For **modified tasks**, the cursor is moved to the end of the line.

### 🚀 How to Use

Once set up, you can run the script from any line in a note using your assigned hotkey.

### Creating a New Task

1.  Place your cursor on a new, empty line or one that has text you will to convert to a task.
2.  Press your assigned hotkey to launch the script.
3.  A series of prompts will appear:
    *   **Choose a Task Type**: Select the status, such as `- [ ] to-do`. TIP: use the numbers assinged and keyboard to select the task type quickly.
    *   **Manage Tags**: A menu will show the currently assigned tags (your last-used tag is added automatically). You can add more from your list, add a custom one, remove tags, or continue.
    *   **Select a Date**: Choose one of the quick suggestions or enter a date manually.
4.  The script will insert the formatted task components, and the cursor will be positioned perfectly for you to start typing your task description.

### Modifying an Existing Task

1.  Place your cursor anywhere on the line containing the task you wish to edit.
2.  Press your assigned hotkey.
3.  The script reads the existing task details. The same series of prompts will appear, but this time they will be pre-populated:
    *   The task's **current type** will be at the top of the list.
    *   The tag manager will show the task's **existing tags**. Selecting Other allows you to type a tag not currently listed. 
    *   The task's **current date** will be the first option in the date picker.
4.  Make any changes you need through the prompts. The script will rewrite the line with the updated information and place the cursor at the end.

## 🔧 Customization

You can easily customize the available task types and the predefined tag list by editing the script file.

### Customizing Task Types

Open the template file and locate the `taskTypes` constant. You can add, remove, or edit any object in this array. Each object requires a `display` value (for the menu) and a `value` (the text inserted into the note).

```
const taskTypes = [
{ display: "1. - [ ] to-do", value: "- [ ]" },
{ display: "2. - [/] In Progress", value: "- [/]" },
// Add your own custom type here
{ display: "24. - [h] home", value: "- [h]" }
];
```

### Customizing Predefined Tags

Locate the `tags` constant in the script. You can edit this list to include the tags you use most frequently. The "Other" option will always be available for adding tags not on this list so do not remove this.

```
const tags = ["#Project-A", "#Work", "#Personal", "#Errands"];

```

# Update Note Creation Date (macOS only)

This guide provides step-by-step instructions to configure a powerful Templater workflow on your Mac. The setup involves three key components: a Templater script, a shell script, and a Templater user function. Together, they allow you to modify a file's "creation date" directly from Obsidian using an interactive prompt.

This is particularly useful for aligning the file system's creation date with a date inside your note's metadata, ensuring consistency for sorting and querying files.

## Overview of the Workflow

1.  **Templater Script (`.md` file)**: This is what you trigger with a hotkey. It gets the active file path and prompts you to enter a new date and time.
2.  **Shell Script (`.sh` file)**: This is the engine. It takes the date and file path provided by Templater and uses a macOS command (`SetFile`) to change the file's creation date in the file system.
3.  **Templater User Function**: This is the bridge. It connects the Templater script to the shell script, allowing them to communicate and pass data.

## ⚙️ Setup Instructions

Follow these three parts carefully.

### Part 1: Install Xcode Command Line Tools

The shell script relies on a command called `SetFile`, which is part of the Xcode Command Line Tools.

1.  Open the **Terminal** app on your Mac (you can find it in `Applications/Utilities/` or search for it with Spotlight).
2.  Copy and paste the following command into the Terminal and press **Enter**:
    ```
    xcode-select --install
    ```
3.  A dialog box will appear asking you to install the tools. Click **"Install"** and agree to the terms. The download and installation will take a few minutes. If it says the tools are already installed, you can proceed to the next step.

### Part 2: Create the Shell Script

This script will execute the command to change the file date.

1.  **Choose a Location**: Create a dedicated folder on your Mac to store your Obsidian-related scripts. A good, reliable location is inside your home directory. For example, `~/Documents/obsidian-scripts/`.
2.  **Create the Script File**:
    *   Open a plain text editor (like TextEdit, but make sure it's in "Plain Text" mode, or use a code editor like VS Code).
    *   Copy and paste the code below into the new file:
        ```
        #!/bin/bash
        
        # This script sets the creation date of a file.
        # It expects two arguments:
        # $1: The date string in "MM/DD/YYYY HH:mm:ss" format.
        # $2: The full path to the file.
        
        SetFile -d "$1" "$2"
        ```
    *   Save the file inside your scripts folder (e.g., `~/Documents/obsidian-scripts/`) with the name `set-date.sh`.

3.  **Make the Script Executable**:
    *   Open the **Terminal** app again.
    *   Navigate to the folder where you saved the script. For example:
        ```
        cd ~/Documents/obsidian-scripts/
        ```
    *   Run the following command to give the script permission to execute:
        ```
        chmod +x set-date.sh
        ```
    This step is crucial; without it, Templater will not be able to run the script.

### Part 3: Configure Obsidian and Templater

Now, let's set up the Templater side.

1.  **Create the Templater Script**:
    *   In your Obsidian vault, go to your Templater templates folder.
    *   Create a new note and name it something like `Set File Date.md`.
    *   Copy and paste the Templater script code you provided into this note.

2.  **Define the User Function in Templater Settings**:
    *   Go to Obsidian `Settings` > `Templater`.
    *   Scroll down to the **"User Functions"** section.
    *   Define a new function that points to your shell script. The function should be entered in the format `FunctionName: Command`.
        *   **Function Name**: `setfile` (this must match `tp.user.setfile` in the script).
        *   **Command**: The full, absolute path to your shell script.
    *   Your entry should look like this (adjust the path to match where you saved your script):
        ```
        setfile: /Users/YOUR_USERNAME/Documents/obsidian-scripts/set-date.sh
        ```
        > **Tip**: You can get the full path by right-clicking the `set-date.sh` file in Finder, holding the **Option** key, and selecting **"Copy 'set-date.sh' as Pathname"**.

3.  **Assign a Hotkey**:
    *   Go to `Settings` > `Hotkeys`.
    *   Search for your template name ("Set File Date").
    *   Assign a convenient hotkey (e.g., `Ctrl+Shift+D`) to trigger the template.

## 🚀 How to Use

1.  Open the note in Obsidian whose creation date you want to change.
2.  Press the hotkey you assigned in the final setup step.
3.  A prompt will appear, pre-filled with the file's current creation date.
4.  You can either accept the date by hitting **Enter** or edit it to your desired date and time. The format must be `DD/MM/YYYY HH:mm`.
5.  After you submit, the script will run, and you'll see a confirmation notice: "✅ File date updated successfully".

The file's creation date in the macOS Finder will now be updated to match what you entered.




