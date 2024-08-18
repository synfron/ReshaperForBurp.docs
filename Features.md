# Features

* auto-gen TOC:
{:toc}

## Rules & Variables

Rules and Variables are core features of Reshaper. See our dedicated pages for how create and use them.

[Rules](https://synfron.github.io/ReshaperForBurp/Rules.html)

[Variables](https://synfron.github.io/ReshaperForBurp/Variables.html)

## Workspaces

Create, manage, and switch between multiple workspaces. Each workspace can be customized with specific rules, variables, and settings tailored to different testing scenarios, projects, or organizational preferences.

### Enable the Workspaces Feature

Workspaces are disabled by default. To enable them go to the Settings tab in Reshaper and click `Enable Workspaces`.

### Manage Workspaces

Once the Workspaces feature is enabled, a new tab bar will appear above the traditional Reshaper tabs for Rules, Global Variables etc. You can right-click on any tab in this bar to open a context menu that contains options to perform these various actions.

**Rename** - Change the name displayed in the Workspace tab.

**Delete** - Delete the Workspace and all of its data.

**Set As Default** - Focus on this Workspace when Reshaper first opens, and use this Workspace as the target of Burp context menu actions. Only available if the Workspace is not already default.

**Add New Workspace** - Add a new Workspace tab.

**Disable Workspace** - Removes the Workspaces tab bar. Only available if there is just one Workspace.


### Disable the Workspaces Feature

Workspaces can only be disabled if you have just one Workspace remaining. An option to `Disable Workspaces` will be available in both the Settings tab or the lone tab's right-click menu.

## Settings

Note, all settings are Workspace specific.

**Enable Event Diagnostics** - If enabled, each Rule that is run prints diagnostics details about its handling of the request or request to the Logs tab. For each When, the printout will show the value of inputs and whether the constraint passed. If the When constraints passed, for each Then, the printout will show the value of inputs, outputs, and execution errors.

**Diagnostic Value Max Length** - Truncate the printout for values in Event Diagnostic logs to the specified length.

**Enable Sanity Check Warnings** - If enabled, print out warning messages to the Logs tabs if Rules are constructed with contradictory or seemingly unintended operations.

**Replicate Logs to Extension Output** - If enabled, messages in Reshaper's Logs tab are also printed to Burp's Extensions tab's Output for Reshaper.

**Logs Tab Character Limit** - Trim the oldest messages in the Logs tab if the total text length exceeds the specified value.

**Hide Features** - Provides options to hide features you don't use in order to reduce interface clutter. Hide specified tabs and When/Then type dropdown options. This hides the display of these features, but does not disable their functionality if they're already in use.

**Reset Data** - Deletes all Rules and Global Variables. This action is unrecoverable. Be sure to create exports if needed before usage.

**Default Encoding** - Sets the encoding to use when processing event messages. For most usages, this should be left as is.

**Capture Traffic From** - Select which Burp tools Reshaper should receive messages from. If unselected, Rules will not run against any messages from that tool.

**Enable Workspaces/Disable Workspaces** - Adds or removes the Workspace tab bar. See [Workspaces](#workspaces) for more details.

**Items to Export** - Select Rules and Global Variables to export as a JSON/YAML file. Note, the only Global Variables that are selectable will be those marked as `Persistent` in the Global Variables tab.

**Export Data** - Export the selected `Items to Export` as JSON or YAML. Click the arrow on the right side of the button to choose between JSON or YAML.

**Overwrite Duplicates** - If enabled, any Rules or Global Variables that match the name of an existing item of that type will be replaced by the imported item. Otherwise, the item to import will be skipped.

**Import Data** - Import a previously exported JSON/YAML file that contains Rules or Global Variables from a file or URL. Click the arrow on the right side of the button to choose between File or URL based import.