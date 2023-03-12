---
title: "C# Scripting"
date: 2023-03-11T18:30:10-06:00
tags: ["2023","Coding", "CSharp", "TIL"]
description: "A quick introduction to Scripting using C Sharp."
draft: false
---

## Intro
I came across C# scripting a few months ago as my team was trying to decide on a standard for how we wanted to share little scripts we had written to do
small tasks. Traditionally I'd use a tool like [LinqPad](https://www.linqpad.net/) to accomplish this, but since we didn't want to buy a 
Enterprise License we decided to try out C# Scripts.  I've been surprised by how nice it is to have a small scratch pad to test out new ideas
or to rapidly prototype a solution. The following article is a quick getting-started guide and some notes for myself on common things I find myself
searching for.

## Getting Started

Assuming you have [.Net 6.0 or .Net 7.0](https://dotnet.microsoft.com/en-us/download) all you need to do to get started with scripting in C# is to open a terminal and type:

```
dotnet tool install -g dotnet-script
```

Once you have it installed, create a folder and within that folder run the command

```
dotnet script init
```

This will do a few important things. 

1. Create a `main.csx` file, which will be where we start our journey.
2. Create a `.vscode` folder and a `launch.json` file so that we can debug using VS Code
3. Create a `.omnisharp.json` file, for configuring omnisharp.

You can pass in a file name if you don't want to call your main file `main.csx`. 

To run the file it's as simple as:

```
dotnet script main.csx
```

Or you can click on the debugging icon in VS Code and run it that way.


## Importing other files and Nuget packages.

To reference Nuget packages you just need to add a reference at the top of the file like so:

```csharp
#r "nuget: CsvHelper 30.0.1"
```

To get the correct spelling I go to [https://www.nuget.org](https://www.nuget.org) and get the name and latest version. 

> **Note:** Omnisharp needs to be restarted after adding a new package reference. To do so use Ctrl+Shift+P and search for "Omnisharp: Restart Omnisharp"

To add a reference to a local file we use the `#load` command. I found this particularly useful if I had a set of common classes that I'd used over and over again.

```csharp
#load "./StudentModel.csx"
```
You can also load .cs files.  

As with `#r` I found I benefited from restarting Omnisharp after adding other classes. 

The file paths can be either relative or absolute, and according to the [documentation](https://github.com/dotnet-script/dotnet-script) on GitHub
you can use URLs to run remote scripts. 

## Other Useful Things

- Just like the new Console App Template there is no top-level using statements or namespaces. I find that this makes things cleaner and easier to get started. Often times I'm just wanting to 
test a simple function or LINQ statement so it's nice to just be able to pull in the things I need and get straight to work.

- Debugging in VS Code isn't as nice as Visual Studio or Rider, but for the most part, it's been sufficient for what I've needed. 

- Reading through the documentation there is also a REPL which would be fun and potentially useful. I'll be sure to update this once I've played with it some.

- You can pass in arguments that are stored in a global `Args` variable. 

- On Windows, you can use `dotnet script register` to execute the script from the shell!

## References

- [Dotnet Scripts on Github](https://github.com/dotnet-script/dotnet-script)