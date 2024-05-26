# Thens

Perform actions if the When criteria for the Rule are met.

<!-- TOC depthto:2 depthfrom:1 -->

- [Thens](#thens)
	- [Break](#break)
	- [Build HTTP Message](#build-http-message)
	- [Comment](#comment)
	- [Delay](#delay)
	- [Delete Value](#delete-value)
	- [Delete Variable](#delete-variable)
	- [Drop](#drop)
	- [Evaluate](#evaluate)
	- [Extract](#extract)
	- [Generate](#generate)
	- [Highlight](#highlight)
	- [Intercept](#intercept)
	- [Log](#log)
	- [Parse HTTP Message](#parse-http-message)
	- [Prompt](#prompt)
	- [Read File](#read-file)
	- [Repeat](#repeat)
	- [Run Process](#run-process)
	- [Run Rules](#run-rules)
	- [Run Script](#run-script)
	- [Save File](#save-file)
	- [Send Message](#send-message)
	- [Send Request](#send-request)
	- [Send To](#send-to)
	- [Set Encoding](#set-encoding)
	- [Set Event Direction](#set-event-direction)
	- [Set Value](#set-value)
	- [Set Variable](#set-variable)
	- [Transform](#transform)
	- [Common Fields](#common-fields)
	- [Additional Notes](#additional-notes)

<!-- /TOC -->

## Break

Stop Rules or then action processing

Availability: HTTP, WebSocket

### Fields

Break Type - If Skip Next Thens, skip running any further Thens of the Rule. If Skip Next Rules, skip running any further Thens and Rules for this event.

## Build HTTP Message

Build an HTTP request or response message and store the full text in a variable. The actual request or response message of the event is not changed.

Availability: HTTP, WebSocket

### Fields

Starter HTTP Message - Text to use as the starting template for the HTTP message. Supports variable tags.

Message Value Setters - Set parts of the HTTP message.

Source Text - The text to set in the message. Supports variable tags.

Destination Message Value - The HTTP message entity to set the value of.

Destination Identifier - The property of the HTTP message to set the value of. Only available for certain [Message Values](MessageValues.html) (e.g. request header). Supports variable tags.

Destination Identifier Placement - Placement of the value to set if there are multiple (i.e. First, Last, All, Only - Keep One, New - Add additional). Only available for certain [Message Values](MessageValues.html) (e.g. request header).

Destination Variable Source - Single item or list variants of the Global, Event, or Session scope. See [Set List Variable](#set-list-variable) for fields that are available if a list variant is chosen.

Destination Variable Name - The name of the variable to hold the built HTTP message. Supports variable tags.

## Comment

Add a comment to the line item in the HTTP/WebSocket history

Availability: HTTP, WebSocket

### Fields

Text - The text of the comment. Supports variable tags.

## Delay

Delay further processing/sending of the HTTP/WebSocket event

Availability: HTTP, WebSocket

### Fields

Delay (milliseconds) - The amount of time to delay further processing. Supports variable tags.

## Delete Value

Remove an HTTP message entity

Availability: HTTP

### Fields

Message Value - The HTTP event entity to delete.

Identifier - The property of the HTTP entity to delete. Only available for certain [Message Values](MessageValues.html) (e.g. request header). Supports variable tags.

Identifier Placement - Placement of the value to delete if there are multiple. (i.e. First, Last, All)

## Delete Variable

Delete a variable

Availability: HTTP, WebSocket

### Fields

Variable Source - Single item or list variants of the Global, Event, or Session scope.

Variable Name - The name of the variable to delete. Supports variable tags.

Item Placement - `First`: Delete the first item in the list; `Last`: Delete the last item in the list; `Index`: Delete zero-based Nth item of the list; `All`: Delete the entire list variable. Only available if `Variable Source` is a list variant.

Index - The zero-based index of the item to delete from the list. The index must already exist in the list. Only available if `Variable Source` is a list variant and `Item Placement` is `Index`. Supports variable tags.

## Drop

Have Burp drop the connection

Availability: HTTP, WebSocket

### Fields

Drop Message - If selected, Burp will be told to drop the connection.

## Evaluate

Perform operations on values

Availability: HTTP, WebSocket

### Fields

X - First value. Supports variable tags.

Operation - `Add`, `Subtract`, `Multiply`, `Divide By`, `Increment`, `Decrement`, `Mod`, `Abs`, `Round`, `Not`, `Equals`, `Not Equals`, `Contains`, `Greater Than`, `Greater Than Or Equals`, `Less Than`, or `Less Than Or Equals`

Y - Second value. Only available for certain operations. Supports variable tags.

## Extract

Extract values into lists

Availability: HTTP, WebSocket

### Fields

Text - The text to extract from. Supports variable tags.

Extractor Type - `Regex`, `JSONPath`, `CSS Selector`, `XPath`, or `Chunk`.

Pattern - The regex pattern to match against. Each matched value is added to the list. Only available if `Extractor Type` is `Regex`. Supports variable tags.

Path - The JSONPath (See https://goessner.net/articles/JsonPath/) or XPath expression. Each node/value located by the expression is added to the list. Only available if `Extractor Type` is `JSONPath` or `XPath`. Supports variable tags.

Selector - The CSS selector expression (See https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors). Each node/value located by the expression is added to the list. Only available if `Extractor Type` is `CSS Selector`. Supports variable tags.

Size - The size of each chunk to split the text by. Each chunk is added to the list. Only available if `Extractor Type` is `Chunk`. Supports variable tags.

List Variable Source - List variants of the Global, Event, or Session scope.

List Variable Name - The name list variable. Supports variable tags.

Delimiter - The delimiter used when the values of the list variable are joined into single text. Note, use special variable tags to specify characters like new lines. Supports variable tags.

Items Placement - `Add First`: Insert all items at the beginning of the list; `Add Last`: Insert all items at the end of the list; `Overwrite`: Remove all current items in the list and add the new items.

## Generate

Generate a value

Availability: HTTP, WebSocket

### Fields

Generate Option - `UUID`, `Words`, `Password`, `Bytes`, `Integer`, `IP Address`, `Timestamp`, or `UNIX Timestamp`.

Destination Variable Source - Single item or list variants of the Global, Event, or Session scope. See [Set List Variable](#set-list-variable) for fields that are available if a list variant is chosen.

Destination Variable Name - The name of the variable to hold the generated value. Supports variable tags.

#### UUID

Version - `V3`, `V4`, or `V5`.

Namespace (UUID) - UUID value to represent the UUID namespace parameter. Only available if `Version` is `V3` or `V5`. Supports variable tags.

Name - Value for the name UUID parameter. Only available if `Version` is `V3` or `V5`. Supports variable tags.

#### Words

Generator Type - `Word`, `Sentence`, or `Paragraph`

Count - The number of made-up words, sentences, or paragraphs to generate. Supports variable tags.

Separator - Text to separate each generated entity with. Only available if `Count` is not equal to `1`. Supports variable tags.

#### Password

Min Length - The lower bounds (inclusive) of the password length. Supports variable tags.

Max Length (Exclusive) - The upper bounds (exclusive) of the password length. Supports variable tags.

Character Groups -The type of characters to include in the password. Options are `Lowercase Letters`, `Uppercase Letters`, `Numbers`, and/or `Symbols`. If selected, the password will include at least one of each group.

#### Bytes

Length - The number of bytes to generate.

Encoding - The charset/encoding to use when converting the bytes to text (e.g. ISO-8859-1). ISO-8859-1 is recommended if the text is expected to be converted back to bytes. Supports variable tags.

#### Integer

Min Value - The lower bounds (inclusive) of the integer. Supports variable tags.

Max Value (Exclusive) - The upper bounds (exclusive) of the integer. Supports variable tags.

Base - Number system base/radix. The default is `10`. Supports variable tags.

#### IP Address

Version - `V4` or `V6`.

#### Timestamp

Format - The format of the date/timestamp to generate. The default is `yyyy-MM-dd`. Supports variable tags.

Min Timestamp - The lower bounds (inclusive) of the date/timestamp. The value must match the given format. The default is the current date/time. Supports variable tags.

Max Timestamp (Exclusive) - The upper bounds (exclusive) of the date/timestamp. The value must match the given format. The default is the current date/time. Supports variable tags.

#### UNIX Timestamp

Min/Max Timestamp Format - The format of the provided Min Timestamp and Max Timestamp. The default is `yyyy-MM-dd`. Supports variable tags.

Min Timestamp - The lower bounds (inclusive) of the UNIX milliseconds timestamp. The value must match the given format. The default is the current date/time. Supports variable tags.

Max Timestamp (Exclusive) - The upper bounds (exclusive) of the UNIX milliseconds timestamp. The value must match the given format. The default is the current date/time. Supports variable tags.

## Highlight

Highlight the line item in the HTTP/WebSocket history

Availability: HTTP, WebSocket

### Fields

Color - The color used to highlight the line item.

## Intercept

Intercept the message in the Proxy interceptor

Only relevant for Proxy tool-captured events.

Availability: HTTP, WebSocket

### Fields

Action - User Defined, Intercept, or Disable.

## Log

Log message to the Burp extension console

Availability: HTTP, WebSocket

### Fields

Text - The text to log. Supports variable tags.

## Parse HTTP Message

Extract values from an HTTP request or response message and store the values in a variable.

Availability: HTTP, WebSocket

### Fields

HTTP Message - Text to use as the HTTP message. Supports variable tags.

Message Value Getters - Get parts of the HTTP message.

Source Text - The text to set in the message. Supports variable tags.

Source Message Value - The HTTP message entity from which to extract a value.

Source Identifier - The property of the HTTP entity to extract a value from. Only available for certain [Message Values](MessageValues.html) (e.g. request header). Supports variable tags.

Source Identifier Placement - Placement of the value to get if there are multiple (i.e. First, Last). Only available for certain [Message Values](MessageValues.html) (e.g. request header).

Destination Variable Source - Single item or list variants of the Global, Event, or Session scope. See [Set List Variable](#set-list-variable) for fields that are available if a list variant is chosen.

Destination Variable Name - The name of the variable to hold the built HTTP message value. Supports variable tags.

## Prompt

Get text via a prompt dialog

Availability: HTTP, WebSocket

### Fields

Description - Description text to display in the prompt above the text entry field. Supports variable tags.

Starter Text - Initial text in the text entry field. Supports variable tags.

Fail After (milliseconds) - Flag the request as failed after waiting the specified amount of time for the response. Only available if `Wait for Completion` is selected. Supports variable tags.

Break After Failure - Do not run any other Thens or Rules for this event if the request was flagged as failed. Only available if `Wait for Completion` is selected.

Capture Variable Source - Single item or list variants of the Global, Event, or Session scope. See [Set List Variable](#set-list-variable) for fields that are available if a list variant is chosen.

Capture Variable Name - The name of the variable to store the response message. Supports variable tags.

## Read File

Read a file

Availability: HTTP, WebSocket

### Fields

File Path - File path of the file including the file name. Supports variable tags.

Encoding - The charset/encoding of the file (e.g. UTF-8). Supports variable tags.

Capture Variable Source - Single item or list variants of the Global, Event, or Session scope. See [Set List Variable](#set-list-variable) for fields that are available if a list variant is chosen.

Capture Variable Name - The name of the variable to store the captured output. Supports variable tags.

## Repeat

Repeat a group of Then actions by count, boolean value, or for each item in a list

Availability: HTTP, WebSocket

### Fields

Number of Following Thens Included - The number of Then items immediately following this one that are a part of the repeat group. They will not run independently of the repeat group.

Repeat Condition - `Count`: Repeat a specified number of times; `Has Next Item`: Repeat for each item in a list variable; `While True`: Repeat while a value is true, y, 1, yes, or on.

Count - Number of times to repeat. Only available if `Repeat Condition` is `Count`. Supports variable tags.

List Variable Source - List variants of the Global, Event, or Session scope. Only available if `Repeat Condition` is `Has Next Item`.

List Variable Name - The name of the variable to repeat for each item of it. Only available if `Repeat Condition` is `Has Next Item`. Supports variable tags.

Item Event Variable Name - The name of the single item Event variable to store the current item of the list for each repeat iteration. Only available if `Repeat Condition` is `Has Next Item`. Supports variable tags.

Boolean Value - Repeat while this value is `true`, `y`, `1`, `yes`, or `on`. Boolean Value should contain a variable tag whose value would change between the repeat iterations in order to avoid unexpected repeating. Only available if `Repeat Condition` is `While True`. Supports variable tags.

Max Count - The max number of times to repeat in situations where `Boolean Value` never evaluates to a false equivalent value. Only available if `Repeat Condition` is `While True`.

## Run Process

Execute a command in a separate process

Availability: HTTP, WebSocket

### Fields

Command - Command to execute in a separate process. Supports variable tags. Example: `cmd.exe /c dir`

Stdin - Value to send to standard input. Supports variable tags.

Wait for Completion - Wait for the process to exit before continuing.

Fail After (milliseconds) - Flag the process as failed after waiting the specified amount of time for the process to exit. Only available if `Wait for Completion` is selected. Supports variable tags.

Fail on Non-Zero Exit Code - Flag the process as failed if the process returned a non-zero exit code. Only available if `Wait for Completion` is selected.

Kill After Failure - Kill the process after a wait timeout. Only available if `Wait for Completion` is selected.

Break After Failure - Do not run any other Thens or Rules for this event if the process was flagged as failed. Only available if `Wait for Completion` is selected.

Capture Output - Capture standard out of the process. Only available if `Wait for Completion` is selected.

Capture After Failure - Capture standard out even if the process is flagged as failed. Only available if `Wait for Completion` and `Capture Output` is selected.

Capture Variable Source - Single item or list variants of the Global, Event, or Session scope. See [Set List Variable](#set-list-variable) for fields that are available if a list variant is chosen.

Capture Variable Name - The name of the variable to store the captured output. Supports variable tags.

## Run Rules

Run a specific Rule or all auto-run Rules

Availability: HTTP, WebSocket

### Fields

Run Single - Run a specific Rule is selected. Otherwise, run all auto-run Rules.

Run Name - The name of the Rule to run. Only available if `Run Single` is selected.

## Run Script

Execute a JavaScript script

Availability: HTTP, WebSocket

The engine supports up to partial ES6/ES2015. Scripts have access to certain Reshaper-specific functions. See [Scripting Library](ScriptingLibrary.html)

### Fields

Script - The text of the JavaScript script to run.

Max Execution (secs) - Terminate long-running scripts after this time.

## Save File

Save text to a file

Availability: HTTP, WebSocket

### Fields

File Path - File path of the file including the file name. Supports variable tags.

Text - The text to save. Supports variable tags.

Encoding - The charset/encoding of the file (e.g. UTF-8). Supports variable tags.

File Exists Action - Action to do if the file already exists: None (Don't write), Overwrite, Append

## Send Message

Send a separate WebSocket message

Availability: WebSocket

### Fields

Event Direction - Send to Client or Server. Sending to the client is only allowed for WebSockets captured by the Proxy tool.

Message - The message to send. Supports variable tags.

## Send Request

Send a separate HTTP request

Availability: HTTP, WebSocket

### Fields

Request - The HTTP request message to send. Uses the value from the current event if left blank. Supports variable tags.

URL - The URL of the request. If this is set, it overrides the Host request header, the request message URI, protocol, address, and port. Supports variable tags.

Protocol - `http` or `https`. If this is set, it overrides the values from the URL (if set) or the current event. Supports variable tags.

Address - Hostname without port. If this is set, it overrides the values from the URL (if set) or the current event. Example: `www.example.com`. Supports variable tags.

Port - Example: `80`. If this is set, it overrides the values from the URL (if set) or the current event. Supports variable tags.

Wait for Completion - Wait for a response before continuing.

Fail After (milliseconds) - Flag the request as failed after waiting the specified amount of time for the response. Only available if `Wait for Completion` is selected. Supports variable tags.

Fail on Error Status Code - Flag the request as failed if the response returned a 4xx or 5xx HTTP status code. Only available if `Wait for Completion` is selected.

Break After Failure - Do not run any other Thens or Rules for this event if the request was flagged as failed. Only available if `Wait for Completion` is selected.

Capture Output - Capture the HTTP response message. Only available if `Wait for Completion` is selected.

Capture After Failure - Capture the HTTP response message even if the request is flagged as failed. Only available if `Wait for Completion` and `Capture Output` is selected.

Capture Variable Source - Single item or list variants of the Global, Event, or Session scope. See [Set List Variable](#set-list-variable) for fields that are available if a list variant is chosen.

Capture Variable Name - The name of the variable to store the response message. Supports variable tags.

## Send To

Send data to other Burp tools or the system's default browser

Availability: HTTP, WebSocket

### Fields

Send To - Comparer, Intruder, Repeater, Browser, Organizer, Decoder, or Site Map

Override Defaults - Select to be able to override values to send to the given Burp tool

Host - Leave empty to use the default value. Only available for Intruder, Repeater, Organizer, and Site Map, and if `Override Defaults` is selected. Supports variable tags.

Port - Leave empty to use the default value. Only available for Intruder, Repeater, Organizer, and Site Map, and if `Override Defaults` is selected. Supports variable tags.

Protocol - HTTP or HTTPS. Leave empty to use the default value. Only available for Intruder, Repeater, Organizer, and Site Map, and if `Override Defaults` is selected. Supports variable tags.

Request - Full HTTP request text. Leave empty to use the default value. Only available for Intruder, Repeater, Organizer, and Site Map, and if `Override Defaults` is selected. Supports variable tags.

Response - Full HTTP response text. Leave empty to use the default value. Only available for Organizer and Site Map, and Site Map, and if `Override Defaults` is selected. Supports variable tags.

Comment - Comment to add to the line item for this event. Only available for Site Map, and if `Override Defaults` is selected.

Highlight Color - Highlight color of the line item for this event. Only available for Site Map, and if `Override Defaults` is selected.

Value - Value to compare. Leave empty to use the default value. Only available for Comparer and Decoder, and if `Override Defaults` is selected. Supports variable tags.

URL - Leave empty to use the default value. Only available for Browser, and `Override Defaults` is selected. Supports variable tags.

## Set Encoding

Set the encoding used to read and write bytes of the HTTP request or response body, or WebSocket binary message

Availability: HTTP, WebSocket

### Fields

Encoding - The charset/encoding of the file (e.g. UTF-8). Supports variable tags.

## Set Event Direction

Change whether to send a request or to send a response at the end of processing

Availability: HTTP

If the event direction is switched from request to response, no request is sent. Instead, whatever is set in the HTTP response message is sent. Switching from response to request is not functional.

### Fields

Set Event Direction - Request or Response.

## Set Value

Set the value of an HTTP/WebSocket event using another value (text, variable, or HTTP/WebSocket event entity)

Availability: HTTP, WebSocket

### Fields

Use Message Value - Use [Message Value](MessageValues.html) (HTTP/WebSocket event entity) as the source value. Otherwise, use the specified text.

Source Message Value - The HTTP/WebSocket event entity from which to get the source value. Only available if `Use Message Value` is selected.

Source Identifier - The property of the HTTP/WebSocket entity to get the source value from. Only available for certain [Message Values](MessageValues.html) (e.g. request header). Supports variable tags.

Source Identifier Placement - Placement of the value to get if there are multiple (i.e. First, Last). Only available for certain [Message Values](MessageValues.html) (e.g. request header).

Source Text - The text to use as the source value. Only available if `Use Message Value` is not selected. Supports variable tags.

Source Value Type - Declare that the value is Text, JSON (node), HTML (element), or Params (value). See [Value Types and Paths](#value-types-and-paths) for more details.

Source Value Path - Specify a JSONPath for JSON, a CSS selector for HTML, or a param name for Params to get a value from within the original value and then use this value instead. See [Value Types and Paths](#value-types-and-paths) for more details. Only available if `Source Value Type` is JSON, HTML, or Params. Supports variable tags.

Use Regex Replace - Use regex on the source value.

Regex Pattern - The Regex pattern to run on the source value. If there is a successful match, a Regex replacement is performed on the value using `Regex Replacement Text`. Only available if `Use Regex Replace` is selected. Supports variable tags.

Regex Pattern - The replacement value to use in the Regex replacement. Only available if `Use Regex Replace` is selected. Supports variable tags.

Destination Message Value - The HTTP/WebSocket event entity to set the value of.

Destination Identifier - The property of the HTTP/WebSocket entity to set the value of. Only available for certain [Message Values](MessageValues.html) (e.g. request header). Supports variable tags.

Destination Identifier Placement - Placement of the value to set if there are multiple (i.e. First, Last, All, Only - Keep One, New - Add additional). Only available for certain [Message Values](MessageValues.html) (e.g. request header).

Destination Value Type - Declare that the value to set is Text, JSON (node), HTML (element), or Params (value). See [Value Types and Paths](#value-types-and-paths) for more details.

Destination Value Path - Specify a JSONPath for JSON, a CSS selector for HTML, or a param name for Params to set a value at the specified path inside the current value at the destination. See [Value Types and Paths](#value-types-and-paths) for more details. Only available if `Destination Value Type` is JSON, HTML, or Params. Supports variable tags.

## Set Variable

Set a variable using another value (text, variable, or HTTP/WebSocket event entity)

Availability: HTTP, WebSocket

### Fields

Use Message Value - Use [Message Value](MessageValues.html) (HTTP/WebSocket event entity) as the source value. Otherwise, use the specified text.

Source Message Value - The HTTP/WebSocket event entity from which to get the source value. Only available if `Use Message Value` is selected.

Source Identifier - The property of the HTTP/WebSocket entity to get the source value from. Only available for certain [Message Values](MessageValues.html) (e.g. request header). Supports variable tags.

Source Identifier Placement - Placement of the value to get if there are multiple (i.e. First, Last). Only available for certain [Message Values](MessageValues.html) (e.g. request header).

Source Text - The text to use as the source value. Only available if `Use Message Value` is not selected. Supports variable tags.

Source Value Type - Declare that the value is Text, JSON (node), HTML (element), or Params (value). See [Value Types and Paths](#value-types-and-paths) for more details.

Source Value Path - Specify a JSONPath for JSON, a CSS selector for HTML, or a param name for Params to get a value from within the original value and then use this value instead. Only available if `Source Value Type` is JSON, HTML, or Params. Supports variable tags. See [Value Types and Paths](#value-types-and-paths) for more details.

Use Regex Replace - Use regex on the source value.

Regex Pattern - The Regex pattern to run on the source value. If there is a successful match, a Regex replacement is performed on the value using `Regex Replacement Text`. Only available if `Use Regex Replace` is selected. Supports variable tags.

Regex Pattern - The replacement value to use in the Regex replacement. Only available if `Use Regex Replace` is selected. Supports variable tags.

Destination Variable Source - Single item or list variants of the Global, Event, or Session scope. See [Set List Variable](#set-list-variable) for fields that are available if a list variant is chosen.

Destination Variable Name - The name of the variable to set. Supports variable tags.

Destination Value Type - Declare that the value to set is Text, JSON (node), HTML (element), or Params (value). See [Value Types and Paths](#value-types-and-paths) for more details.

Destination Value Path - Specify a JSONPath for JSON, a CSS selector for HTML, or a param name for Params to set a value at the specified path inside the current value at the destination. See [Value Types and Paths](#value-types-and-paths) for more details. Only available if `Destination Value Type` is JSON, HTML, or Params. Supports variable tags.

## Transform

Transform/convert a value

### Fields

Transform Option - `Base64`, `Escape`, `JWT Decode`, `Case`, `Hash`, `Hex`, or `Integer`, `Trim`.

Input - The value to transform. Supports variable tags.

#### Base64

Variant - `Standard` or `URL`.

Action - `Encode` or `Decode`

Encoding - The charset/encoding to use when converting text to/from Base64 (e.g. ISO-8859-1). ISO-8859-1 is recommended. Supports variable tags.

#### Escape

Entity Type - `HTML`, `XML`, `JSON`, or `URL`.

Action - `Escape` or `Unescape`

#### JWT Decode

Segment - `Header`, `Payload`, or `Signature`.

#### Case

Phrase Case - `lower case`, `UPPER CASE`, `flatcase`, `camelCase`, `PascalCase`, `snake_case`, `CONSTANT_CASE`, `dash-case`, `COBOL-CASE`, `Title Case`, or `Sentence case`.

#### Hash

Hash Type - `SHA-1`, `SHA-256`, `SHA-512`, `SHA3-256`, `SHA3-512`, or `MD5`.

#### Hex

Action - `From Text` or `To Text`

Encoding - The charset/encoding to use when converting text to/from a hexidecimal string (e.g. ISO-8859-1). ISO-8859-1 is recommended. Supports variable tags.

#### Integer

Source Base - The base/radix of the input integer. The default is `10` Supports variable tags.

Target Base - The base/radix to convert the input integer to. The default is `16`. Supports variable tags.

#### Trim

Trim Option - `Start`, `End`, or `Start And End`.

Trim Characters - Characters to remove from the front/end of the input. For example, to remove all parentheses and braces, this value would be `[]{}()`.  The default is to remove whitespace.


## Common Fields

### Set List Variable

The following fields are only available if the variable source is a list variant.

Item Placement - `First`: Set/overwrite the first item in the list; `Last`: Set/overwrite the last item in the list; `Index`: Set/overwrite zero-based Nth item of the list; `Add First`: Insert as the first item in the list; `Add Last`: Insert as the last item in the list; `All`: Reset the list with a new delimited value;

Index - The zero-based index to place the value in the list. The index must already exist in the list or be +1 beyond the last item in the list. Only available if `Item Placement` is `Index`. Supports variable tags.

Delimiter - The delimiter used to split the value to create individual items in the list. Note, use special variable tags to specify characters like new lines. Only available if `Item Placement` is `All`. Supports variable tags.

## Additional Notes

### Value Types and Paths

Some Thens offer the ability to retrieve/insert text from/into a container text. The supported container text value types are JSON, HTML, and query/form params. If one of these value types are selected for the source text, the value retrieved will be the value at the given selector/path of the container text. If one of these value types are selected for the destination text, the current value of the destination is considered the container text, and the value in transit will be placed inside the container text at the location specified by the selector/path.

#### JSON

The pathing/selector syntax for JSON is based on JSONPath (See https://goessner.net/articles/JsonPath/). 


##### Source Example

Given the following source text:

```
{ "category": "reference",
	"author": "Nigel Rees",
	"title": "Sayings of the Century",
	"price": 8.95
}
```
And the following path: `$.title` 

The value retrieved with be: `Sayings of the Century`

##### Destination Example

Given the following value to set: `Hello World`

And the destination currently holding the following value:

```
{
	"firstName": "John", 
	"lastName": "Doe", 
	"age": 30,
	"favoritePhrase": "Greetings World"
}
```

And the following path: `$.favoritePhrase`

The final value held by the destination will be:

```
{
	"firstName": "John", 
	"lastName": "Doe", 
	"age": 30,
	"favoritePhrase": "Hello World"
}
```

#### HTML

The pathing/selector syntax for HTML is based on CSS selectors (See https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors). Additionally, the custom pseudo-element selector `::innerHTML` can be used at the end of a selector to get or set the inner HTML of an element.


##### Source Example

Given the following source text:

```
<html>
	<head></head>
	<body>
		<div class="greeting">
			Greetings World
		</div>
	</body>
</html>
```
And the following path: `.greeting::innerHTML` 

The value retrieved with be: `Greetings World`

##### Destination Example

Given the following value to set: `Hello World`

And the destination currently holding the following value:

```
<html>
	<head></head>
	<body>
		<div class="greeting">
			Greetings World
		</div>
	</body>
</html>
```

And the following path: `.greeting::innerHTML` 

The final value held by the destination will be:

```
<html>
	<head></head>
	<body>
		<div class="greeting">
			Hello World
		</div>
	</body>
</html>
```

#### Params

The path for a param is the name of the param.


##### Source Example

Given the following source text: `name=ferret&color=purple`

And the following path: `color`

The value retrieved with be: `purple`

##### Destination Example

Given the following value to set: `red`

And the destination currently holding the following value: `name=ferret&color=purple`

And the following path: `color` 

The final value held by the destination will be: `name=ferret&color=red`
