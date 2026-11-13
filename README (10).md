# Topic 13: IF Node & Conditional Logic

## Overview
This n8n workflow demonstrates how to evaluate incoming order values with an IF node and route each item to a different downstream action.

## Workflow name
`Topic 13 IF Node Workflow`

## Workflow structure
1. Manual Trigger
2. Mock Orders
3. Check Order VIP Status (IF)
4. True branch: Set VIP
5. False branch: Set Regular

## Test data
The Mock Orders node supplies two separate order items:

| Customer | Order Value |
|---|---:|
| Alice | 150 |
| Bob | 75 |

## IF condition
- Value 1: `{{ $json.orderValue }}`
- Data type: Number
- Operator: Greater Than or Equal
- Value 2: `100`

Orders with a value greater than or equal to 100 go through the True output. Other orders go through the False output.

## Expected results
| Customer | Order Value | Branch | Status |
|---|---:|---|---|
| Alice | 150 | True | VIP |
| Bob | 75 | False | Regular |

## Implementation note
In this n8n setup, the Edit Fields node's JSON mode expected a single object and rejected an array of order objects. To supply the two separate test items, the `Mock Orders` node was implemented with a Code node that returns two n8n items. The Code node only creates mock input data; it does not evaluate the condition or perform the routing. All conditional evaluation is handled by the IF node.

## How to run
1. Open `Topic 13 IF Node Workflow`.
2. Click **Test workflow**.
3. Open `Set VIP` and verify that Alice is the only item, with `status` set to `VIP`.
4. Open `Set Regular` and verify that Bob is the only item, with `status` set to `Regular`.

## Completion
The workflow was executed successfully and saved. The observed branch outputs matched the expected results.
