# Topic 13: IF Node & Conditional Logic — Requirements

## 1. Objective
Demonstrate how the n8n IF node evaluates a numeric condition and routes each incoming item to a True or False output.

## 2. Scope

### In scope
- Add and configure an IF node.
- Compare a dynamic input expression with a numeric threshold.
- Use a numeric comparison operator.
- Route matching and non-matching items to separate downstream Edit Fields nodes.
- Verify item-by-item routing using multiple input records.

### Out of scope
- Complex AND/OR condition groups.
- Nested IF routing.
- Switch node routing.
- Custom JavaScript condition evaluation.

## 3. Prerequisites
- Completion of Topics 1–12.
- Basic understanding of comparison operators and Boolean branching.
- Access to an n8n workspace.

## 4. Functional requirements

| ID | Requirement | Priority |
|---|---|---|
| REQ-001 | Workflow includes an IF node to split data routing. | High |
| REQ-002 | IF node uses a basic numeric comparison operator. | High |
| REQ-003 | Condition references preceding-node data through `{{ $json.orderValue }}`. | High |
| REQ-004 | Items with orderValue greater than or equal to 100 use the True branch. | High |
| REQ-005 | Items with orderValue below 100 use the False branch. | High |
| REQ-006 | True and False outputs connect to distinct downstream Edit Fields nodes named `Set VIP` and `Set Regular`. | High |
| REQ-007 | Workflow executes successfully with different input items and routes them correctly. | High |

## 5. Technical requirements

| ID | Requirement | Implementation / validation |
|---|---|---|
| TR-001 | Numeric values are compared as numbers, avoiding alphabetical string comparison. | Test data uses numeric orderValue values (150 and 75); numeric comparison is configured in the IF node. |
| TR-002 | Each input item is evaluated independently and routed to one of two output arrays. | Two input items are supplied; Alice reaches True and Bob reaches False. |

## 6. Test data
- Alice: `orderValue` = 150
- Bob: `orderValue` = 75
- Threshold: 100

## 7. Acceptance criteria
- Alice is the only item in `Set VIP`, with `status` = `VIP`.
- Bob is the only item in `Set Regular`, with `status` = `Regular`.
- The complete workflow executes without errors and is saved.

## 8. Implementation note
The n8n Edit Fields node in the tested environment rejected an array in its JSON output field because it expected one object. Therefore, a Code node named `Mock Orders` was used only to emit two mock input items. It does not contain conditional evaluation logic. The IF node performs all comparisons and routing.
