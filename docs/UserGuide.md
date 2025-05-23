---
layout: page
title: User Guide
---

TuitionBook is a streamlined, fast, and efficient way to access key student and parent information. Designed with simplicity and speed in mind, this solution is perfect for private tuition teachers who prefer a no-frills, text-based approach to managing student data.

* Table of Contents
{:toc}

--------------------------------------------------------------------------------------------------------------------

## Quick start

1. Ensure you have Java `17` or above installed in your Computer.<br>
   **Mac users:** Ensure you have the precise JDK version prescribed [here](https://se-education.org/guides/tutorials/javaInstallationMac.html).

1. Download the latest `.jar` file from [here](https://github.com/AY2425S2-CS2103-F10-3/tp/releases).

1. Copy the file to the folder you want to use as the _home folder_ for your TuitionBook.

1. Open a command terminal, `cd` into the folder you put the jar file in, and use the `java -jar tuitionbook.jar` command to run the application.<br>
   A GUI similar to the below should appear in a few seconds. Note how the app contains some sample data.<br>
   ![Ui](images/Ui.png)

1. Type the command in the command box and press Enter to execute it. e.g. typing **`help`** and pressing Enter will open the help window.<br>
   Some example commands you can try:

    * `list` : Lists all contacts.

    * `add n/John Doe p/98765432 e/johnd@example.com a/John street, block 123, #01-01 l/Elementary Mathematics;2025-10-03T12:00:00` : Adds a contact named `John Doe` to TuitionBook.

    * `delete 3` : Deletes the 3rd contact shown in the current list.

    * `clear` : Deletes all contacts.

    * `exit` : Exits the app.

1. Refer to the [Features](#features) below for details of each command.

--------------------------------------------------------------------------------------------------------------------

## Features

<div markdown="block" class="alert alert-info">

**:information_source: Notes about the command format:**<br>

* Words in `UPPER_CASE` are the parameters to be supplied by the user.<br>
  e.g. in `add n/NAME`, `NAME` is a parameter which can be used as `add n/John Doe`.

* Items in square brackets are optional.<br>
  e.g `n/NAME [t/TAG]` can be used as `n/John Doe t/friend` or as `n/John Doe`.

* Items with `…`​ after them can be used multiple times including zero times.<br>
  e.g. `[t/TAG]…​` can be used as ` ` (i.e. 0 times), `t/friend`, `t/friend t/family` etc.

* Parameters can be in any order.<br>
  e.g. if the command specifies `n/NAME p/PHONE_NUMBER`, `p/PHONE_NUMBER n/NAME` is also acceptable.

* Extraneous parameters for commands that do not take in parameters (such as `help`, `list`, `exit` and `clear`) will be ignored.<br>
  e.g. if the command specifies `help 123`, it will be interpreted as `help`.

* If you are using a PDF version of this document, be careful when copying and pasting commands that span multiple lines as space characters surrounding line-breaks may be omitted when copied over to the application.
</div>

### Viewing help : `help`

Shows a message explaning how to access the help page.

![help message](images/helpMessage.png)

Format: `help`


### Adding a person: `add`

Adds a person to TuitionBook.

Format: `add n/NAME p/PHONE_NUMBER e/EMAIL a/ADDRESS [l/LESSON_NAME;LESSON_DATETIME]…​ [t/TAG]…​`

<div markdown="span" class="alert alert-primary">:bulb: **Tip:**
A person can have any number of tags and lessons (including 0)
</div><br>

<div markdown="block" class="alert alert-info">

:information_source: **Notes about Add command:**<br>

* A person's name should only contain alphanumeric characters and spaces.
  Only English characters are accepted, special characters and characters of other languages are not supported.

* Capitalization of a person's name differs from the same name without capitalization.<br>
  e.g. `John Doe` and `john doe` are considered different names.

* Additional spaces in a person's name will be replaced with a single space.

* LESSON_NAME provided must not contain any special characters, and LESSON_DATETIME must follow the format `yyyy-mm-ddTHH:mm:ss`.

* Duplicate emails and phone numbers with other existing contacts are allowed intentionally. This accounts for students who may not have their own phone numbers or emails and would have to another person's email or phone number such as their parents or friends.
</div>

Examples:
* `add n/John Doe p/98765432 e/johnd@example.com a/John street, block 123, #01-01`
* `add n/John Doe p/98765432 e/johnd@example.com a/John street, block 123, #01-01 l/Elementary Math;2025-03-12T18:00:00 t/Sec4`
* `add n/John Doe p/98765432 e/johnd@example.com a/John street, block 123, #01-01 l/Elementary Math;2025-03-12T18:00:00 l/Biology;2025-03-13T15:00:00 t/Sec4`


### Listing all persons : `list`

Shows a list of all persons in TuitionBook.

<div markdown="span" class="alert alert-info">:information_source: **Note:**
    TuitionBook will only show up to 2 upcoming lessons (if any), and will display a default message if there is no lessons to display.
</div>

Format: `list`

### Editing a person : `edit`

Edits an existing person in TuitionBook.

<div markdown="span" class="alert alert-info">:information_source: **Note:**
    This command does not support updating of lessons. For these features, see lesson-* commands below.
</div>

Format: `edit INDEX [n/NAME] [p/PHONE] [e/EMAIL] [a/ADDRESS] [t/TAG]…​`

* Edits the person at the specified `INDEX`. The index refers to the index number shown in the displayed person list. The index **must be a positive integer** 1, 2, 3, …​
* At least one of the optional fields must be provided.
* Existing values will be updated to the input values.
* When editing tags, the existing tags of the person will be removed i.e adding of tags is not cumulative.
* You can remove all the person’s tags by typing `t/` without
  specifying any tags after it.

Examples:
*  `edit 1 p/91234567 e/johndoe@example.com` Edits the phone number and email address of the 1st person to be `91234567` and `johndoe@example.com` respectively.
*  `edit 2 n/Betsy Crower t/` Edits the name of the 2nd person to be `Betsy Crower` and clears all existing tags.

### Locating persons by name: `find`

Finds persons whose names contain any of the given keywords.

Format: `find KEYWORD [MORE_KEYWORDS]`

* The search is case-insensitive. e.g `hans` will match `Hans`
* The order of the keywords does not matter. e.g. `Hans Bo` will match `Bo Hans`
* Only the name is searched.
* Only full words will be matched e.g. `Han` will not match `Hans`
* Persons matching at least one keyword will be returned (i.e. `OR` search).
  e.g. `Hans Bo` will return `Hans Gruber`, `Bo Yang`

Examples:
* `find John` returns `john` and `John Doe`
* `find alex david` returns `Alex Yeoh`, `David Li`<br>
  ![result for 'find alex david'](images/findAlexDavidResult.png)

### Deleting a person : `delete`

Deletes the specified person from TuitionBook.

Format: `delete INDEX`

* Deletes the person at the specified `INDEX`.
* The index refers to the index number shown in the displayed person list.
* The index **must be a positive integer** 1, 2, 3, …​

Examples:
* `list` followed by `delete 2` deletes the 2nd person in TuitionBook.
* `find Betsy` followed by `delete 1` deletes the 1st person in the results of the `find` command.

### Adding lesson(s) to a person : `lesson-add`

Adds the specified lesson(s) to a person in TuitionBook.

Format: `lesson-add INDEX [l/LESSON_NAME;LESSON_DATETIME]…​`

* Adds lesson(s) to a person identified by the specified index.
* The index refers to the index number shown in the displayed person list.
* The index **must be a positive integer** 1, 2, 3, …​
* The lesson(s) provided must not have the same date & time slot as existing lesson(s) across TuitionBook.
* The lesson(s) added may be older than the current date & time.

Examples:
* `lesson-add 1 l/Elementary Mathematics;2025-12-12T12:00:00`
* `lesson-add 3 l/Chemistry;2025-12-12T13:00:00 l/Biology;2025-12-12T15:00:00 l/Biology;2025-12-22T17:00:00`

### Deleting a person's lesson(s) : `lesson-delete`

Deletes the specified lesson(s) from a person in TuitionBook.

<div markdown="span" class="alert alert-info">:information_source: **Note:** 
    If the same two lessons are provided (same module name and datetime) in the user's command, TuitionBook will remove one of the duplicates and perform the deletion of lessons as per normal.
</div>

Format: `lesson-delete INDEX [l/LESSON_NAME;LESSON_DATETIME]…​`

* Deletes a person's lesson(s) at specified index
* The index refers to the index number shown in the displayed person list.
* The index **must be a positive integer** 1, 2, 3, …​
* The lesson(s) provided must be valid (person selected must have the lessons specified in argument provided)

Examples:
* `lesson-delete 1 l/Elementary Mathematics;2025-12-12T12:00:00`
* `lesson-delete 3 l/Chemistry;2025-12-12T13:00:00 l/Biology;2025-12-12T15:00:00 l/Biology;2025-12-22T17:00:00`

### Viewing a person's lessons: `lesson-list`

Shows the specified person's lesson(s) in a separate window.

<div markdown="span" class="alert alert-danger">:exclamation: **Warning:**
    This command will not auto-reload on updates to TuitionBook. The user is required to re-run the command to refresh the contents.
</div>

Format: `lesson-list INDEX`

* Shows a person's lesson(s) at specified index
* The index refers to the index number shown in the displayed person list.
* The index **must be a positive integer** 1, 2, 3, …​
* A person with no lessons will be returned with `No lessons found`.
* Opens a new window to show the lessons.

Examples:
* `lesson-list 2`
  ![lesson window](images/lessonWindow.png)

### Clearing all entries : `clear`

Clears all entries from TuitionBook.

Format: `clear`

### Exiting the program : `exit`

Exits the program.

Format: `exit`

### Saving the data

TuitionBook data are saved in the hard disk automatically after any command that changes the data. There is no need to save manually.

### Editing the data file

TuitionBook data are saved automatically as a JSON file `[JAR file location]/data/tuitionbook.json`. Advanced users are welcome to update data directly by editing that data file.

<div markdown="span" class="alert alert-warning">:exclamation: **Caution:**
If your changes to the data file makes its format invalid, TuitionBook will ignore the data file and start empty in the next run. Any new changes in the next run will overwrite the corrupted data file. Hence, it is recommended to take a backup of the file before editing it.<br>
Furthermore, certain edits can cause the TuitionBook to behave in unexpected ways (e.g., if a value entered is outside of the acceptable range). Therefore, edit the data file only if you are confident that you can update it correctly.
</div>

--------------------------------------------------------------------------------------------------------------------

## FAQ

**Q**: How do I transfer my data to another Computer?<br>
**A**: Install the app in the other computer and overwrite the empty data file it creates with the file that contains the data of your previous TuitionBook home folder.

--------------------------------------------------------------------------------------------------------------------

## Known issues

1. **When using multiple screens**, if you move the application to a secondary screen, and later switch to using only the primary screen, the GUI will open off-screen. The remedy is to delete the `preferences.json` file created by the application before running the application again.
2. **If you minimize the Help Window** and then run the `help` command (or use the `Help` menu, or the keyboard shortcut `F1`) again, the original Help Window will remain minimized, and no new Help Window will appear. The remedy is to manually restore the minimized Help Window.

--------------------------------------------------------------------------------------------------------------------

<div style="page-break-after: always;"></div>

## Command summary

Action | Format, Examples
--------|------------------
**Add** | `add n/NAME p/PHONE_NUMBER e/EMAIL a/ADDRESS [l/LESSON_NAME;LESSON_DATETIME]…​ [t/TAG]…​` <br> e.g., `add n/James Ho p/22224444 e/jamesho@example.com a/123, Clementi Rd, 1234665 l/Elementary Math;2025-03-12T18:00:00 t/Sec4`
**Clear** | `clear`
**Delete** | `delete INDEX`<br> e.g., `delete 3`
**Edit** | `edit INDEX [n/NAME] [p/PHONE_NUMBER] [e/EMAIL] [a/ADDRESS] [t/TAG]…​`<br> e.g.,`edit 2 n/James Lee e/jameslee@example.com`
**Find** | `find KEYWORD [MORE_KEYWORDS]`<br> e.g., `find James Jake`
**List** | `list`
**Add Lesson** | `lesson-add INDEX [l/LESSON_NAME;LESSON_DATETIME]…​` <br> e.g., `lesson-add 1 l/Elementary Mathematics;2025-12-12T12:00:00`
**Delete Lesson** | `lesson-delete INDEX [l/LESSON_NAME;LESSON_DATETIME]…​` <br> e.g., `lesson-delete 1 l/Elementary Mathematics;2025-12-12T12:00:00`
**List Lesson** | `lesson-list INDEX` <br> e.g., `lesson-list 1`
**Help** | `help`
