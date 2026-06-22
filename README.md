# Allowance MCP

Allowance MCP lets AI agents request scoped human approval for purchases, receive limited virtual cards, complete checkout, and report receipts without seeing the human's real card.

This repository is the public listing and configuration home for the hosted Allowance MCP server. The implementation repository is private.

## Hosted Server

- Server URL: `https://mcp.useallowance.com`
- Transport: `streamable-http`
- Official registry name: `com.useallowance/allowance-mcp`
- Official registry URL: `https://registry.modelcontextprotocol.io/v0.1/servers/com.useallowance%2Fallowance-mcp/versions/latest`
- Discovery metadata: `https://useallowance.com/.well-known/mcp.json`
- Product docs: `https://useallowance.com/mcp`

## Authentication

Allowance MCP requires an Allowance connection token:

```text
Authorization: Bearer ak_...
```

Connection tokens are issued through Allowance setup/OAuth. Do not commit tokens, card credentials, or checkout PII.

## Core Flow

1. The agent creates an allowance request for a specific purchase.
2. The human approves, denies, or lets the request expire on their phone.
3. If approved, the agent completes checkout with scoped payment credentials or waits for Allowance remote fulfillment.
4. The agent reports success or failure, including receipt and charged amount details when available.

Human phone approval is the spending authorization. After approval, agents should not ask for another final confirmation unless the realized total exceeds the approved cap, checkout requires unavailable information, or the item materially differs from the approved request.

## Tools

- `send_allowance_request`
- `poll_allowance_request`
- `wait_for_allowance_request`
- `get_allowance_request`
- `list_allowance_requests`
- `cancel_allowance_request`
- `get_contact_details`
- `get_allowance_shipping_address`
- `get_allowance_billing_address`
- `issue_allowance_card`
- `complete_purchase_auth`
- `report_purchase_success`
- `report_purchase_failure`
- `list_allowance_purchase_attempts`
- `get_allowance`
- `wait_for_remote_fulfillment`
- `reply_to_remote_fulfillment_message`
- `list_allowances`
- `pause_allowance`
- `revoke_allowance`
- `list_supported_merchants`
- `check_merchant`

## Security Model

Allowance is designed so agents spend with scoped authorization instead of receiving the human's real card. Approvals, limits, receipts, and audit trails are enforced by Allowance.

If you find a security issue, email `security@useallowance.com`.
