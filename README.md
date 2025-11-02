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



## Task - New & Convert

Designed to streamline the creation and modification of tasks. It provides an interactive, prompt-based workflow to quickly set task types, add multiple tags, and assign dates, all without manually typing complex syntax.

The script is intelligent: it remembers your last-used tagon your device, pre-selects existing values when editing a task, and places your cursor exactly where you need it next. Use the keyboard to navigate and select as necessary. 

### ✨ Features

*   **Interactive Workflow**: Uses pop-up menus to guide you through creating or editing a task.
*   **Comprehensive Task Types**: Comes with 23 pre-configured task statuses, including to-do, in-progress, cancelled, important, idea, and more.
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


