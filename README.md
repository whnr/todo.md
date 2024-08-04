# todo.md formmd
A complete primer on the whys and hows of todo.md.

The first and most important rule of todo.md:

> A single line in your todo.md text file represents a single task.


## Why plain text?

Plain text is software and operating system agnostic.
It's searchable, portable, lightweight, and easily manipulated.
It works when someone else's web server is down or your Outlook `.PST` file is corrupt.
There's no exporting and importing, no databases or tags or flags or stars or prioritizing or _insert company name here_-induced rules on what you can and can't do with it.

## How this compares to todo.txt

This is a fork of [todo.txt](http://todotxt.org/).
It is keeping all features and general syntax.

The main change is the introduction of hierarchy through indentation.

This fact is breaking the ability to easily sort the file in a text editor.
Also most standard `todo.txt` apps and clients will struggle with the indentation.

### Another philosophy

FIXME don't really need project tags anymore!
But you can fold now


## The 3 axes of an effective todo list

Using special notation in todo.md, you can create a list that's sliceable by 3 key axes.


### Priority
Your todo list should be able to tell you what's the next most important thing for you to get done;
either by project or by context or overall.
You can optionally assign tasks a priority that'll bubble them up to the top of the list.


### Project
The only way to move a big project forward is to tackle a small subtask associated with it.
Your `todo.md` should be able to list out all the tasks specific to a project.

In order to move along a project like "Cleaning out the garage," my task list should give me the next logical action to take in order to move that project along.
"Clean out the garage" isn't a good todo item;
but "Call Goodwill to schedule pickup" in the "Clean out garage" project is.


### Context
[Getting Things Done](https://en.wikipedia.org/wiki/Getting_Things_Done) author David Allen suggests splitting up your task lists by context —
ie, the place and situation where you'll work on the job.
Messages that you need to send go in the `@email` context; calls to be made `@phone`, household projects `@home`.

That way, when you've got a few minutes in the car with your cell phone, you can easily check your `@phone` tasks and make a call or two while you have the opportunity.

## `todo.md` format rules

<img src="./description.svg" width="100%" height="500">

Your `todo.md` is a plain text file.
To take advantage of structured task metadata like priority, projects, context, creation, and completion date, there are a few simple but flexible file format rules.

Philosophically, the `todo.md` file format has two goals:

- The file contents should be human-readable without requiring any tools other than a plain text viewer or editor.
- A user can manipulate the file contents in a plain text editor in sensible, expected ways.

Here are the rest.

## Hierarchy indentation starts a line

If hirearchy indentation exists, it is the first character(s) on the line

Only simple whitespace ` ` is allowed.
Any number of whitespace is allowed to determine the indentation level;
the quantity can vary in the file as long as the local indentation is consistent.

```
Bake bread
  Feed starter
  Mix dough
      50g starter
      400g flour
      350g water
  Proof
  Bake dough
```



## Incomplete Tasks: 3 Format Rules

The beauty of todo.md is that it's mostly unstructured;
the fields you can attach to each task are only limited by your imagination.
To get started, use special notation to indicate task context (e.g. `@phone` ), project (e.g. `+GarageSale` ) and priority (e.g. `(A) `).

A todo.md file might look like the following:

```
(A) Thank Mom for the meatballs @phone
Organize the GarageSale
  (B) Schedule Goodwill pickup +GarageSale @phone
  Post signs around the neighborhood +GarageSale
@GroceryStore Eskimo pies
```

A search and filter for the `@phone` contextual items would output:

```
(A) Thank Mom for the meatballs @phone
  (B) Schedule Goodwill pickup +GarageSale @phone
```

To just see the `+GarageSale` project items would output:

```
  (B) Schedule Goodwill pickup +GarageSale @phone
  Post signs around the neighborhood +GarageSale
```

There are three formatting rules for incomplete todos.

### Rule 1: If priority exists, it appears after any indentation

The priority is an uppercase character from A-Z enclosed in parentheses and followed by a space.

Two of these tasks have a priority:

```
(A) Call Mom
Write book
  (B) Write 25m
```

These tasks do not have any priorities:

```
Really gotta call Mom (A) @phone @someday
(b) Get back to the boss
(B)->Submit TPS report
```


### Rule 2: A task's creation date may optionally appear directly after priority and a space.

If the creation date exists, it shall be in the format `YYYY-MM-DD`.

These tasks have creation dates:

```
2011-03-02 Document +TodoMd task format
(A) 2011-03-02 Call Mom
```

This task doesn't have a creation date:

```
(A) Call Mom 2011-03-02
```


### Rule 3: Contexts and Projects may appear anywhere in the line _after_ indentation/priority/prepended date.

- A *context* is preceded by a single space and an at-sign (`@`).
- A *project* is preceded by a single space and a plus-sign (`+`).
- A *project* or *context* contains any non-whitespace character.
- A *task* may have zero, one, or more than one *projects* and *contexts* included in it.

For example, this task is part of the `+Family` and `+PeaceLoveAndHappiness` projects as well as the `@iphone` and `@phone` contexts:

```
(A) Call Mom +Family +PeaceLoveAndHappiness @iphone @phone
```

This task has no contexts in it:

```
Email SoAndSo at soandso@example.com
```

This task has no projects in it:

```
Learn how to add 2+2
```



## Complete Tasks: 2 Format Rules

Two things indicate that a task has been completed.


### Rule 1: A completed task starts with an lowercase x character followed by a space (`x `) after any indentation

If a task starts with an `x` (case-sensitive and lowercase) followed directly by a space, it is marked as complete.

These are completed tasks:

```
x 2011-03-03 Call Mom
Write book
  (B) Write 25m

```

These are not complete tasks.

```
xylophone lesson
X 2012-01-01 Make resolutions
(A) x Find ticket prices
```

We use a lowercase x so that completed tasks sort to the bottom of the task list using standard sort tools.


### Rule 2: The date of completion appears directly after the x, separated by a space.

For example:

```
x 2011-03-02 2011-03-01 Review Tim's pull request +TodoTxtTouch @github
```

If you’ve prepended the creation date to your task, on completion it will appear directly after the completion date.
This is so your completed tasks sort by date using standard sort tools. Many todo.txt clients discard priority on task completion.
To preserve it, use the `key:value` format described below (e.g. `pri:A`)

With the completed date (required), if you've used the prepended date (optional), you can calculate how many days it took to complete a task.



## Additional File Format Definitions

Tool developers may define additional formatting rules for extra metadata.

Developers should use the format `key:value` to define additional metadata (e.g. `due:2010-01-02` as a due date).

Both `key` and `value` must consist of non-whitespace characters, which are not colons. Only one colon separates the `key` and `value`.

