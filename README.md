# About

This is an Omni Automation single-file plugin library for OmniFocus that provides a variety of useful functions that can be used by other plugins or scripts.

_Please note that all scripts on my GitHub account (or shared elsewhere) are works in progress. If you encounter any issues or have any suggestions please let me know--and do please make sure you backup your database before running scripts from a random amateur on the internet!)_

## Known issues 

None yet! 🤞

# Installation & Set-Up

(For instructions on getting started with Omni Automation, see [here](https://kaitlinsalzke.com/how-to/how-to-add-a-omnijs-plug-in-to-omnifocus-and-assign-a-keyboard-shortcut/).)

1. Click on the green `Clone or download` button above to download a `.zip` file of the file in this GitHub repository.
2. Unzip the downloaded file.
3. Move the `.omnifocusjs` file to your OmniFocus plug-in library folder.

# Usage

To use a function from this library, you will need to do something like the following (taking the `getAllRemainingTasks` function as an example):

```
functionLibrary = PlugIn.find("com.KaitlinSalzke.functionLibrary").library("functionLibrary");
remainingTasks = functionLibrary.getAllRemainingTasks();
```

# Functions

## adjustDateByDays(date, days)

This function takes a date object and an integer representing the number of days to adjust that date by (this can be negative) and returns the adjusted date.

For example, passing this function the date 1 Jan 2020 and -1 would return 31 Dec 2019.

## findTag (nameToFind)

Given a tag name, this will return the first tag object with a matching name.

## getAllRemainingTasks

This function returns all the 'remaining' tasks in the database as an array.

## getContainingFolder (task)

This function takes a task or project object as input and returns the top-level folder object that the task is contained in. If the task or project is not contained within a top-level folder (for example if it is in the inbox or in a project that is not nested inside a folder) the string "No Result" is returned.

## getParent (task)

This function takes a task object as input and returns the task's "parent" task (i.e. the task that directly contains it). If it has no parent (because it is, for example, the top-level task in a project) then `null` is returned.

## getRootTask (childTask)

This function takes a task object as input and returns the top-level task that contains the task (whether or not it is a direct child of the task). 

For example: in a project that looks like...

- Project
  - Task number one
    - Nested task
      -  Really nested task

...passing the "Really nested task" task object would return the "Task number one" task object.

## getTaskWithId (taskId, [tagToSearch])

Given a string `taskId` this function returns the task object with that string, or `null` if a matching task is not found.

Optionally, a second `tagToSearch` parameter can also be passed containing a tag object. This restricts the search scope to just that tag.

## isStalled (project)

Given a project object, this fuction returns a boolean value.

'False' is returned if:
 - The project is a single-action list, or
 - The project has a next task, or
 - The project has children that are not treated as 'next tasks' because they have a 'Blocked' status (i.e. they have a future defer date or on-hold tag, or are blocked by a preceding task in a sequential project)

'True' is returned if:
 - The project has no children, or
 - None of the `False` items are applicable

## removeProjectTagsFromTasks (taskArray, projectTagArray)

Given an array of task objects and an array of tag objects, this function checks each of the tasks in the array. For each task, it removes the tag if it is applied.

This function is designed to be used to clean-up where tags are only intended to be applied to the project but are automatically inherited by tasks created within that project.

## removeTrailingSpaceFromName (task)

Given a task object, this function removes trailing spaces from the end of that task's name.

## replaceTag (tasksArray, oldTag, newTag)

Given an array of tasks and two tag objects, this function removes the first tag from the task and adds the second.

# Contributing

If you have corrections, suggestions for functions to be added, or encounter any issues, please let me know. Issues and/or pull requests welcome.