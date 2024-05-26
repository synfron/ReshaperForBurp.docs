# Whens

Check if an event message meets certain criteria. Multiple Whens are checked in order and treated as AND conditions logically by default. If the relevant value does not match the constraints of the When (opposite if `Negate Result` is selected), unless the following When has specified to `Use OR Condition`, no further Whens are processed for the current Rule and all Thens are skipped.



<!-- TOC depthto:2 depthfrom:1 -->

- [Whens](#whens)
	- [Content Types](#content-types)
	- [Event Direction](#event-direction)
	- [From Tool](#from-tool)
	- [Has Entity](#has-entity)
	- [In Scope](#in-scope)
	- [Matches Text](#matches-text)
	- [Message Type](#message-type)
	- [MIME Type](#mime-type)
	- [Proxy Name](#proxy-name)
	- [Repeat](#repeat)

<!-- /TOC -->

## Content Type

If the HTTP request body is reported to match specified content types

Availability: HTTP, WebSocket

### Fields

Request Content Type - None, JSON, XML, URL Encoded, Multi-Part, AMF, and/or Unknown

## Event Direction

If the HTTP message is a Request or Response, or if the WebSocket message is directed toward the client or server

Availability: HTTP, WebSocket

### Fields

Event Direction - Request or Response for HTTP, Client or Server for WebSockets

## From Tool

If the HTTP/WebSocket message is from a specific Burp tool

Availability: HTTP, WebSocket

### Fields

Tool - Proxy, Repeater, Intruder, Target, Scanner, Extender, or Session

## Has Entity

If the HTTP/WebSocket event contains a certain message value entity

Availability: HTTP, WebSocket

### Fields

Message Value - The message value entity to check

Identifier - The key of the property within the message value entity to check. Only available for certain [Message Values](MessageValues.html) (e.g. request header). Supports variable tags.

## In Scope

If the URL is in the suite-wide scope

Availability: HTTP, WebSocket

### Fields

URL - The URL to check. If added to a HTTP rule, this field can be left blank to use the current request's URL. Supports variable tags.

## Matches Text

If a value (text, variable, or HTTP/WebSocket message value entity) matches a value

Availability: HTTP, WebSocket

### Fields

Use Message Value - Match on a [Message Value](MessageValues.html) (HTTP/WebSocket event entity). Otherwise, use the specified text.

Source Message Value - The HTTP/WebSocket event entity to check. Only available if `Use Message Value` is selected.

Source Identifier - The property of the HTTP/WebSocket entity to check. Only available for certain [Message Values](MessageValues.html) (e.g. request header). Supports variable tags.

Source Identifier Placement - Placement of the value to get if there are multiple (i.e. First, Last). Only available for certain [Message Values](MessageValues.html) (e.g. request header).

Source Text - The text to use as the value to check. Only available if `Use Message Value` is not selected. Supports variable tags.

Source Value Type - Declare that the value is Text, JSON (node), HTML (element), or Params (value). See [Value Types and Paths](Thens.html/#value-types-and-paths) for more details.

Source Value Path - Specify a JSONPath for JSON, a CSS selector for HTML, or a param name for Params to get a value from within the original value and then use this value instead. See [Value Types and Paths](Thens.html/#value-types-and-paths) for more details. Only available if `Source Value Type` is JSON, HTML, or Params. Supports variable tags.

Match Type - Match the text using Equals, Contains, Begins With, Ends With, Regex, Less Than, Less Than Or Equal, Greater Than, or Greater Or Equal.

Match Text - The text to match the value against. Supports variable tags.

Ignore Case - If selected, use case-insensitive comparison.

## Message Type

If the WebSocket message type is text or binary

Availability: WebSocket

### Fields

Message Type - Text or Binary

## MIME Type

If the HTTP response body is reported to match specified MIME types.

Availability: HTTP

### Fields

Response MIME Type - HTML, Script, CSS, JSON, SVG, Other XML, Other Text, Image, Out Binary, and/or Unknown.

## Proxy Name

If received by a certain Burp proxy listener

Availability: HTTP

### Fields

Proxy Name - The Burp proxy listener interface (e.g. 127.0.0.1:8080)

## Repeat

Repeat a group of When constraints for each item in a list

Availability: HTTP, WebSocket

### Fields

Number of Following Whens Included - The number of When items immediately following this one that are a part of the repeat group. They will not run independently of the repeat group.

Success Criteria - `Any Match`: Repeat for each item in the list until the When constraints in the group successfully match during any iteration. If so, report success. Otherwise, report failure; `All Match`: Repeat for each item in the list ensuring that the When constraints in the group successfully match during all iterations. If so, report success. Otherwise, report failure;

List Variable Source - List variants of the Global, Event, or Session scope.

List Variable Name - The name of the variable to repeat for each item of it. Supports variable tags.

Item Event Variable Name - The name of the single item Event variable to store the current item of the list for each repeat iteration. Supports variable tags.
