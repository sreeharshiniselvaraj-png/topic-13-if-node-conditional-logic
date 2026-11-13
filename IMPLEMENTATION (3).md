# Topic 13: IF Node & Conditional Logic — Implementation

## 1. Workflow details
- Workflow name: `Topic 13 IF Node Workflow`
- Trigger: Manual Trigger (`When clicking "Test workflow"`)
- Input node: `Mock Orders`
- Conditional node: `Check Order VIP Status`
- True branch node: `Set VIP`
- False branch node: `Set Regular`

## 2. Mock input data
The `Mock Orders` node returns two separate items:

```javascript
return [
  {
    json: {
      customerName: "Alice",
      orderValue: 150
    }
  },
  {
    json: {
      customerName: "Bob",
      orderValue: 75
    }
  }
];
```

This code only constructs the mock input items. It does not calculate eligibility or route items.

## 3. IF node configuration
Configure one condition:
- Value 1 (Expression): `{{ $json.orderValue }}`
- Type: Number
- Operator: Greater Than or Equal
- Value 2: `100`

Expected routing:
- True output: Alice (150)
- False output: Bob (75)

## 4. Downstream node configuration

### Set VIP
Add a String field:
- Field name: `status`
- Value: `VIP`

Keep the other input fields in the output.

### Set Regular
Add a String field:
- Field name: `status`
- Value: `Regular`

Keep the other input fields in the output.

## 5. Execution procedure
1. Open the workflow.
2. Click **Test workflow**.
3. Inspect the `Set VIP` output.
4. Confirm Alice has `orderValue` 150 and `status` VIP.
5. Inspect the `Set Regular` output.
6. Confirm Bob has `orderValue` 75 and `status` Regular.
7. Save the workflow.

## 6. Expected output

### Set VIP
```json
[
  {
    "customerName": "Alice",
    "orderValue": 150,
    "status": "VIP"
  }
]
```

### Set Regular
```json
[
  {
    "customerName": "Bob",
    "orderValue": 75,
    "status": "Regular"
  }
]
```

## 7. Environment-specific note
The trainer guide suggests entering an array of objects in the Edit Fields node's JSON mode. In the n8n environment used for this exercise, that field expected a single object and returned a `jsonOutput expects a object` validation error. The workflow therefore uses a Code node for mock data generation only. The IF node remains responsible for all conditional logic, and the two downstream Edit Fields nodes implement the branch actions.
