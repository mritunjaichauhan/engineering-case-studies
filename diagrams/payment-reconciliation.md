# Payment Reconciliation

```text
User starts credit purchase
        |
        v
Create local purchase record
        |
        v
Razorpay checkout
        |
        +-----------------------------+
        |                             |
        v                             v
Client confirmation path       Razorpay webhook event
                                      |
                                      v
                              Validate signature
                                      |
                                      v
                              Store webhook event
                                      |
                                      v
                              Select authoritative purchase
                                      |
                                      v
                              Apply status-priority logic
                                      |
                                      v
                              Fulfill credits idempotently

Background safety net:
scheduled cron -> find stale created purchases -> reconcile with payment/webhook state
```

## Design Notes

- Payment systems must tolerate duplicate events, delayed events, out-of-order events, and partial client failures.
- Webhooks should be persisted before fulfillment logic so failures can be inspected and retried.
- Fulfillment should be idempotent; a payment event must not grant credits twice.
- A reconciliation cron protects against edge cases where the checkout succeeds but app state is stale.
