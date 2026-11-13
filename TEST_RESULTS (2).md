# Topic 13: IF Node & Conditional Logic — Test Results

## Test environment
- Platform: n8n Cloud
- Workflow: `Topic 13 IF Node Workflow`
- Trigger: Manual Trigger
- Condition: `{{ $json.orderValue }}` is greater than or equal to `100`

## Test data
| Item | Customer | Order Value | Expected branch | Expected status |
|---|---|---:|---|---|
| 1 | Alice | 150 | True | VIP |
| 2 | Bob | 75 | False | Regular |

## Test case results

| Test ID | Validation | Expected result | Observed result | Status |
|---|---|---|---|---|
| TC-001 | Workflow naming | `Topic 13 IF Node Workflow` | Workflow renamed as required | PASS |
| TC-002 | Mock order input | Two separate items: Alice and Bob | Two items returned by Mock Orders | PASS |
| TC-003 | IF condition configuration | Numeric `orderValue >= 100` | Dynamic expression and numeric comparison configured | PASS |
| TC-004 | True branch routing | Alice (150) reaches Set VIP | One item: Alice | PASS |
| TC-005 | False branch routing | Bob (75) reaches Set Regular | One item: Bob | PASS |
| TC-006 | VIP output mapping | `status` = `VIP` | Set VIP configured with required status field | PASS |
| TC-007 | Regular output mapping | `status` = `Regular` | Set Regular configured with required status field | PASS |
| TC-008 | Item-by-item evaluation | Each item routed independently | Alice and Bob split across separate outputs | PASS |
| TC-009 | End-to-end execution | Workflow completes without errors | Complete workflow executed successfully | PASS |
| TC-010 | Save workflow | Workflow saved | User confirmed workflow saved | PASS |

## Verified output

### True branch — Set VIP
```json
[
  {
    "customerName": "Alice",
    "orderValue": 150,
    "status": "VIP"
  }
]
```

### False branch — Set Regular
```json
[
  {
    "customerName": "Bob",
    "orderValue": 75,
    "status": "Regular"
  }
]
```

## Overall result
**PASS** — The observed results match the trainer's expected routing: Alice's order value of 150 meets the threshold and is assigned VIP; Bob's order value of 75 is below the threshold and is assigned Regular.

## Implementation note
The `Mock Orders` node uses a Code node solely to generate two separate input items because the Edit Fields JSON editor in the tested environment expected a single object and rejected an array. The Code node does not evaluate the condition. Numeric comparison and routing are performed by the n8n IF node.
