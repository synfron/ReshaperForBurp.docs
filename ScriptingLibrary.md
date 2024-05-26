# Scripting Library

Extra Javascript library APIs usable in `ThenRunScript` scripts.

* auto-gen TOC:
{:toc}

## Reshaper.

### event.

#### getMessageValue(messageValueKey, messageValueIdentifier)

Get a [Message Value](MessageValues.html) from the current event.

Parameters:

messageValueKey - Key of the [Message Value](MessageValues.html).

messageValueIdentifier - The identifier for the [Message Value](MessageValues.html) if applicable. 

#### setMessageValue(messageValueKey, messageValueIdentifier, value)

Set a [Message Value](MessageValues.html) of the current event.

Parameters:

messageValueKey - Key of the [Message Value](MessageValues.html).

messageValueIdentifier - The identifier for the [Message Value](MessageValues.html) if applicable.

value - The new value.

#### getMessageValueKeys()

Get all [Message Value](MessageValues.html) keys.

#### setRuleResponse(ruleResponse)

Set whether further processing of Thens or Rules should continue after this script finishes executing. This provides the same functionality as Then Break.

Continue - Continue processing as normal.</br>
BreakThens - Skip running any further Thens of the current Rule.</br>
BreakRules - Skip running any further Thens and Rules for this event.

Parameters:

ruleResponse - "Continue" | "BreakThens" | "BreakRules"

#### runThen(thenType, thenData)

Run a Then action.

Parameters:

thenType - BuildHttpMessage, Break, DeleteValue, DeleteVariable, Drop, Highlight, Log, ParseHttpMessage, SendRequest, SendTo, SetEventDirection, SetValue, or SetVariable

thenData - Object containing the properties for the Then action. See below. Note, the fields that are used or required for each type match the display of fields in the UI.

BuildHttpMessage
```
{
    dataDirection: "Request" | "Response"
    starterHttpMessage: string
    messageValueSetters: [{
        destinationMessageValue: string
        destinationIdentifier: string
        sourceText: string
    }]
    destinationVariableSource: "Event" | "Global" | "Session" | "Event List" | "Global List" | "Session List"
    destinationVariableName: string
    itemPlacement: "First" | "Last" | "Index" | "AddFirst" | "AddLast" | "All"
    delimiter: string
    index: number
}
```
Comment
```
{
    text: string
}
```
Delete Value
```
{
    messageValue: MessageValueKey
    identifier: string
    identifierPlacement: "First" | "Last" | "All"
}
```
Delete Variable
```
{
    targetSource: "Event" | "Global" | "Session" | "Event List" | "Global List" | "Session List"
    variableName: string
    itemPlacement: "First" | "Last" | "Index" | "All"
    index: number
}
```
Drop
```
{
    dropMessage: boolean
}
```
Evaluate
```
{
    x: string
    operation: "Add" | "Subtract" | "Multiply" | "DivideBy" | "Increment" | "Decrement" | "Mod" | "Abs" | "Round" | "Not" | "Equals" | "NotEquals" | "Contains" | "GreaterThan" | "GreaterThanOrEquals" | "LessThan" | "LessThanOrEquals"
    y: string
    destinationVariableSource: "Event" | "Global" | "Session" | "Event List" | "Global List" | "Session List"
    destinationVariableName: string
    itemPlacement: "First" | "Last" | "Index" | "AddFirst" | "AddLast" | "All"
    delimiter: string
    index: number

}
```
Extract
```
{
    text: string
    extractorType: "Regex" | "Json" | "CssSelector" | "XPath" | "Chunk"
    extractor: string
    listVariableSource: "Event List" | "Global List" | "Session List"
    listVariableName: string
    delimiter: string
    itemPlacement: "AddFirst" | "AddLast" | "Overwrite"
}
```
Generate
```
{
    generationOption: "Uuid" | "Words" | "Password" | "Bytes" | "Integer" | "IpAddress" | "Timestamp"
    "UnixTimestamp"
    generator: { 
        version: "V3" | "V4" | "V5"
        namespace: string
        name: string
     } | {
        generatorType: "Word" | "Sentence" | "Paragraph"
        count: number
        separator: string
     } | {
        minLength: number
        maxLength: number
        characterGroups: [
            "LowercaseLetters" | "UppercaseLetters" | "Numbers" | "Symbols"
        ]
     } | {
        length: number
        encoding: string
     } | {
        minValue: number
        maxValue: number
        base: number
     } | {
        version: "V4" | "V6"
     } | {
        format: string
        minTimestamp: string
        maxTimestamp: string
     } | {
        format: string
        minTimestamp: string
        maxTimestamp: string
     }
    destinationVariableSource: "Event" | "Global" | "Session" | "Event List" | "Global List" | "Session List"
    destinationVariableName: string
    itemPlacement: "First" | "Last" | "Index" | "AddFirst" | "AddLast" | "All"
    delimiter: string
    index: number
}
```
Highlight
```
{
    color: "None" | "Red" | "Orange" | "Yellow" | "Green" | "Cyan" | "Blue" | "Pink" | "Magenta" | "Gray"
}
```
Intercept
```
{
    interceptResponse: "UserDefined" | "Disable" | "Intercept"
}
```
Log
```
{
    text: string
}
```
ParseHttpMessage
```
{
    dataDirection: "Request" | "Response"
    httpMessage: string
    messageValueGetters: [{
        sourceMessageValue: MessageValueKey
        sourceIdentifier: string
        destinationVariableSource: "Event" | "Global" | "Session" | "Event List" | "Global List" | "Session List"
        destinationVariableName: string
        itemPlacement: "First" | "Last" | "Index" | "AddFirst" | "AddLast" | "All"
        delimiter: string
        index: number
    }]
}
```
ReadFile
```
{
    filePath: string
    encoding: string
    breakAfterFailure: string
    captureAfterFailure: string
    captureVariableSource: "Event" | "Global" | "Session" | "Event List" | "Global List" | "Session List"
    captureVariableName: string
    itemPlacement: "First" | "Last" | "Index" | "AddFirst" | "AddLast" | "All"
    delimiter: string
    index: string
}
```
SaveFile
```
{
    filePath: string
    text: string
    encoding: string
    fileExistsAction: "None" | "Append" | "Overwrite"
}
```
SendMessage
```
{
    dataDirection: "Server" | "Client"
    messageType: "Text" | "Binary"
    message: string
}
```
SendRequest
```
{
    request: string
    url: string
    protocol: "http" | "https"
    address: string
    port: number
    waitForCompletion: boolean
    failAfter: number
    failOnErrorStatusCode: boolean
    breakAfterFailure: boolean
    captureOutput: boolean
    captureAfterFailure: boolean
    captureVariableSource: "Event" | "Global" | "Session" | "Event List" | "Global List" | "Session List"
    captureVariableName: string
    itemPlacement: "First" | "Last" | "Index" | "AddFirst" | "AddLast" | "All"
    delimiter: string
    index: number
}
```
SendTo
```
{
    sendTo: "Comparer" | "Intruder" | "Repeater" | "Spider" |  "Browser" | "Organizer" | "Decoder" | "SiteMap"
    overrideDefaults: boolean
    host: string
    port: number
    protocol: "http" | "https"
    request: string
    response: string
    comment: string
    highlightColor: "None" | "Red" | "Orange" | "Yellow" | "Green" | "Cyan" | "Blue" | "Pink" | "Magenta" | "Gray"
    value: string
    url: string
}
```
SetEncoding
```
{
    encoding: string
}
```
SetEventDirection
```
{
    dataDirection: "Request" | "Response"
}
```
SetValue
```
{
    text: string
    useMessageValue: boolean
    sourceMessageValue: MessageValueKey
    sourceIdentifier: string
    sourceIdentifierPlacement: "First" | "Last"
    sourceMessageValueType: "Text" | "JSON" | "XML" | "Params"
    sourceMessageValuePath: string
    useReplace: boolean
    regexPattern: string
    replacementText: string
    destinationMessageValueType: "Text" | "JSON" | "XML" | "Params"
    destinationMessageValuePath: string
    destinationMessageValue: MessageValueKey
    destinationIdentifier: string
}
```
SetVariable
```
{
    text: string
    useMessageValue: boolean
    sourceMessageValue: MessageValueKey
    sourceIdentifier: string
    sourceIdentifierPlacement: "First" | "Last"
    sourceMessageValueType: "Text" | "JSON" | "XML" | "Params"
    sourceMessageValuePath: string
    useReplace: boolean
    regexPattern: string
    replacementText: string
    destinationMessageValueType: "Text" | "JSON" | "XML" | "Params"
    destinationMessageValuePath: string
    targetSource: "Event" | "Global" | "Session" | "Event List" | "Global List" | "Session List"
    variableName: string
    itemPlacement: "First" | "Last" | "Index" | "AddFirst" | "AddLast" | "All"
    delimiter: string
    index: number
}
```
Transform
```
{
    transformnOption: "Base64" | "Escape" | "JwtDecode" | "Case" | "Hash" | "Hex" | "Integer" | "Trim"
    transformer: { 
        action: "Encode" | "Decode"
        variant: "Standard" | "Url"
        encoding: string
     } | {
        entityType: "Html" | "Xml" | "Json" | "Url"
        action: "Escape" | "Unescape"
     } | {
        segment: "Header" | "Payload" | "Signature"
     } | {
        phraseCase: "LowerCase" | "UpperCase" | "FlatCase" | "CamelCase" | "PascalCase" | "SnakeCase" | "ConstantCase" | "DashCase" | "CobolCase" | "TitleCase" | "SentenceCase"
     } | {
        hashType: "Sha1" | "Sha256" | "Sha512" | "Sha256V3" | "Sha512V3" | "Md5"
     } | {
        action: "FromText" | "ToText"
        encoding: string
     } | {
        sourceBase: number
        targetBase: number
     } | {
        trimOption: "Start" | "End" | "StartAndEnd"
        characters: string
     }
    destinationVariableSource: "Event" | "Global" | "Session" | "Event List" | "Global List" | "Session List"
    destinationVariableName: string
    itemPlacement: "First" | "Last" | "Index" | "AddFirst" | "AddLast" | "All"
    delimiter: string
    index: number
}
```

### variables.

#### deleteEventVariable(name)

Delete an event variable.

Parameters:

name - Variable name.

#### deleteGlobalVariable(name)

Delete an global variable.

Parameters:

name - Variable name.

#### deleteSessionVariable(name)

Delete an session variable.

Parameters:

name - Variable name.

#### getEventVariable(name)

Get the value of an event variable.

Parameters:

name - Variable name.

#### getGlobalVariable(name)

Get the value of a global variable.

Parameters:

name - Variable name.

#### getSessionVariable(name)

Get the value of a session variable.

Parameters:

name - Variable name.

#### setEventVariable(name, value)

Set the value of an event variable.

Parameters:

name - Variable name.

value - The new value.

#### setGlobalVariable(name, value)

Set the value of a global variable.

Parameters:

name - Variable name.

value - The new value.

#### setSessionVariable(name, value)

Set the value of a session variable.

Parameters:

name - Variable name.

value - The new value.
