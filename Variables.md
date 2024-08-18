# Variables

## Custom Variables

Custom variables allow the sharing of values between Rules and are scoped at the Global, Session, or Event level. They can be set by Thens or in the UI (Global variables only). Custom variables are only accessible within Reshaper and are readable by Whens and Thens.

### List Variables

List variables are a collection of multiple values. The values can be accessed and modified by first item, last item, index, or as a single concatenated value with each item joined by a delimiter.

### Types

Event scoped variables are shared among Rules processing a single HTTP event (either request or response).

Global scoped variables are shared among Rules across all events for as long as the extension is loaded or until the variables are deleted. 

The Global Variables tab provides a way to manage Global and Global List variables. You can toggle between adding a single or list variable using the Add button's dropdown. When a list variable is selected for edit, a delimiter field is provided which is used to determine how to divide the entered text into multiple items in the list. The variables can also be set to be Persistent which enables them to be saved and reloaded between Reshaper sessions.

Session scoped variables are shared among Rules processing the same HTTP request and response, or all WebSocket events within the same WebSocket connection.

## Accessor Variables

Accessor variables provide access to utility functionality and data that is not strictly created by Reshaper.

Message variables provide access to event message values (e.g. Request URI).

Annotation variables process access to HTTP or WebSocket message annotation values (i.e. comments and highlight colors).

File variables provide access to the contents of a text file.

Special character variables provide access to special characters which typically require escape character sequences to use. (e.g. new lines, tabs, unicode characters)

## Variable Tags

Variables can be read by Whens and Thens when a variable tag is specified in supporting text fields. Variable tags can be typed in manually or inserted via the `Insert Variable Tags` option in the right-click menu for those text fields.
{% raw %}

Note, use of `<someText>` in the syntax definitions below signify a description of the value that it needs to be replaced with. `<` and `>` should not remain in the final tag. Values not surrounded by `<` and `>` are literal values. Surround the value in quotes (`"`) if the value contains special characters or any of the following characters: `{}:`.

### Event Variable Tag (event, e)
Syntax - `{{event:<MyVariableName>}}`

### Event List Variable Tag (eventlist, el)
Syntax - `{{eventlist:<MyVariableName>}}` or `{{eventlist:<MyVariableName>:all}}`: Full text (All items concatenated), `{{eventlist:<MyVariableName>:first}}`: First item, `{{eventlist:<MyVariableName>:last}}`: Last item, `{{eventlist:<MyVariableName>:<index>}}`: Item at index, `{{eventlist:<MyVariableName>:<size>}}`: Count of items

### Global Variable Tag (global, g)
Syntax - `{{global:<MyVariableName>}}`

### Global List Variable Tag (globallist, el)
Syntax - `{{globallist:<MyVariableName>}}` or `{{globallist:<MyVariableName>:all}}`: Full text (All items concatenated), `{{globallist:<MyVariableName>:first}}`: First item, `{{globallist:<MyVariableName>:last}}`: Last item, `{{globallist:<MyVariableName>:<index>}}`: Item at index, `{{globallist:<MyVariableName>:size}}`: Count of items

### Session Variable Tag (session, sn)
Syntax - `{{session:<MyVariableName>}}`

### Session List Variable Tag (sessionlist, el)
Syntax - `{{sessionlist:<MyVariableName>}}` or `{{sessionlist:<MyVariableName>:all}}`: Full text (All items concatenated), `{{sessionlist:<MyVariableName>:first}}`: First item, `{{sessionlist:<MyVariableName>:last}}`: Last item, `{{sessionlist:<MyVariableName>:<index>}}`: Item at index, `{{sessionlist:<MyVariableName>:size}}`: Count of items

If Global variable named `firstName` has the value `John` and variable named `lastName` has the value `Smith`. A field with the value `{{global:firstName}}'s full name is {{global:firstName}} {{global:lastName}}` will be read as `John's full name is John Smith`.

### Message Variable Tag (message, m)
Syntax - `{{message:messageValueKey}}` or `{{message:messageValueKey:identifier}}` (e.g. `{{message:httprequesturi}}`, `{{message:httprequestheader:Host}}`). 

See [Message Values](MessageValues.html) to determine the appropriate values for `messageValueKey` and `identifier`.

### Cookie Jar Tag (cookiejar, cj)
Syntax - `{{cookiejar:domain:name}}` or `{{cookiejar:domain:name:path}}`. Example: `{{cookiejar:example.com:tracker:/}}`

### Macro (macro, mc)
Syntax - `{{macro:macroItemNumber:messageValueKey}}` or `{{macro:macroItemNumber:messageValueKey:identifier}}`. 

This tag is only applicable when Reshaper is invoked by a session handling rule marco post-run action. See [Message Values](MessageValues.html#) to determine the appropriate values for `messageValueKey` and `identifier`.

### Annotation Variable Tag (annotation, a)
Syntax - `{{annotation:comment}}` to get the current comment or `{{annotation:highlightcolor}}` to get the current highlight color of the line item in HTTP or WebSocket history for this event.

### File Variable Tag (file, f)
Syntax - `{{file:encoding:filePath}}`. Example: `{{file:utf-8:~/Documents/file.txt}}`

### Generator Variable Tag (generator, gr)
UUID Syntax - `{{generator:uuid:v3:<namespace>:<name>}}` or `{{generator:uuid:v4}}` or `{{generator:uuid:v5:<namespace>:<name>}}`<br>
Words Syntax - `{{generator:words:<generatorType>:<count>:<separator>}}`<br>
Password Syntax - `{{generator:password:<minLength>:<maxLength>:<commaSeparatedCharacterGroups>}}`<br>
Bytes Syntax - `{{generator:bytes:<length>:<encoding>}}`<br>
Integer Syntax - `{{generator:integer:<minValue>:<maxValue>:<base>}}`<br>
IP Address Syntax - `{{generator:ipaddress:<V4|V6>}}`<br>
Timestamp Syntax - `{{generator:timestamp:<format>}}` or `{{generator:timestamp:<format>:<minDateTime>:<maxDateTime>}}`<br>
UNIX Timestamp Syntax - `{{generator:unixtimestamp}}` or `{{generator:unixtimestamp:<format>:<minDateTime>:<maxDateTime>}}`

Provides the same generate options as [Then Generate](Thens.html#generate). See that documentation for more details.

### Special Character Tag (special, s)
Syntax - `{{s:specialCharacterSequences}}`

For example, `{{s:n}}` returns a new line, `{{s:rn}}` returns carriage return + new line, and `{{s:u00A9}}` return the Copyright symbol.


{% endraw %}
