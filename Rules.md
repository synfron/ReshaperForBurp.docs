# Rules

Rules allow you to set actions to perform (called Thens) if an HTTP or WebSocket message (event) received by Burp Suite meets certain criteria (called Whens). Rules are processed in order. If the Rule is set to `Auto-Run`, the Rule will be run automatically when an HTTP or WebSocket event is received, otherwise, it must be specifically triggered. Rules must be `Enabled` to run at all.

HTTP events are processed by Rules under the HTTP Rules tab. WebSocket events are processed by Rules under the WebSocket Rules tab.

<!-- TOC -->

- [Rules](#rules)
	- [Whens](#whens)
	- [Thens](#thens)
	- [Common Fields](#common-fields)
	- [Debugging](#debugging)

<!-- /TOC -->

## Whens

Check if an event message meets certain criteria. See [Whens](Whens.html) for a full list of options.

## Thens

Perform actions if the When criteria are met. See [Thens](Thens.html) for a full list of options.

## Common Fields

### Additional When Fields

Use OR Condition - By default, all Whens must report as a successful match for any Thens in the Rule to be evaluated. Once one When reports failure, none of the remaining Whens in the Rule are evaluated. However, if this is checked, the current When will be evaluated even if the previous When reported failure. If this When reports success, the failure of the previous When is ignored.

Negate Result - If checked, a successful match will be reported as a failure, and an unsuccessful match will be reported as a success.

### Footer Fields

Auto-Run - If checked, the Rule will be evaluated for every event Reshaper is enabled to handle. If unchecked, the Rule will only run if explicitly triggered by a Then Run Rule.

Enabled - If unchecked, the Rule is marked inactive and will not be evaluated under any condition.

Save - Any changes to Rules in the UI do not become live and are not persisted until the Save button is clicked. Upon hitting the Save button, all fields are validated to ensure value requirements are met. If validation issues are found, details of the issues are displayed, and the changes will remain unsaved.

## Debugging

Rules can be debugged by enabling event diagnostics (_Settings > General > Enable Event Diagnostics_) to debug all Rules or by right-clicking the specific Rules you want to debug in the Rules list and selecting `Toggle Debug Logging` in the context menu. This will log details about the actions the Rule(s) have taken for each event (request, response, or WebSocket message) processed, including the result of When constraint checks, and the values that were used in Whens and Thens.

Example Diagnostic Output:

```
Request: http://example.com/
	Rule: Test
		    When Event Direction('Request' equals 'Request') - PASS
		AND When Matches Text('example.com' contains 'example') - PASS
		    Then Set Value(destinationMessageValue='Request Header' destinationIdentifier='special' input='Mine')
		    Then Highlight('orange')
	End Rule
End Request

Response: http://example.com/
	Rule: Test
		    When Event Direction('Response' equals 'Request') - FAIL
	End Rule
End Response
```
