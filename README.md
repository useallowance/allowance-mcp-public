# Allowance MCP

<p>
  <a href="https://useallowance.com">
    <img src="assets/allowance-logo-green-bg.jpg" alt="Allowance" width="96">
  </a>
</p>

[Allowance](https://useallowance.com) is a payment security layer for AI agents. It lets humans approve scoped purchases on their phone while agents complete checkout with limited-use payment credentials instead of the human's real card.

Allowance MCP exposes that flow to MCP clients: agents can request approval for a specific purchase, receive a scoped virtual card after approval, complete checkout, and report receipts and final charged amounts back into an audit trail.

This repository is the public listing and configuration home for the hosted Allowance MCP server. The implementation repository is private.

![Allowance MCP social preview](assets/social-card.png)

## Hosted Server

- Server URL: `https://mcp.useallowance.com`
- Transport: `streamable-http`
- Official registry name: `com.useallowance/allowance-mcp`
- Official registry URL: `https://registry.modelcontextprotocol.io/v0.1/servers/com.useallowance%2Fallowance-mcp/versions/latest`
- Company site: `https://useallowance.com`
- Discovery metadata: `https://useallowance.com/.well-known/mcp.json`
- Product docs: `https://useallowance.com/mcp`

## Authentication

Allowance MCP uses OAuth. Connect your MCP client to `https://mcp.useallowance.com` and complete the Allowance OAuth flow when prompted.

After OAuth completes, MCP clients send the issued bearer token on tool calls. Users should not create or paste standalone API keys for normal MCP use. Do not commit tokens, card credentials, or checkout PII.

## Core Flow

1. The agent creates an allowance request for a specific purchase.
2. The human approves, denies, or lets the request expire on their phone.
3. If approved, the agent completes checkout with scoped payment credentials or waits for Allowance remote fulfillment.
4. The agent reports success or failure, including receipt and charged amount details when available.

Human phone approval is the spending authorization. After approval, agents should not ask for another final confirmation unless the realized total exceeds the approved cap, checkout requires unavailable information, or the item materially differs from the approved request.

## What Allowance Controls

- Spend scope: merchant, amount cap, purchase reason, and expiration.
- Payment exposure: agents get limited payment credentials instead of the human's real card.
- Checkout data: approved contact, shipping, and billing fields are available only when needed for checkout.
- Auditability: requests, approvals, card issuance, purchase attempts, receipts, and failures are recorded.
- Revocation: humans can pause or revoke allowances instead of leaving broad payment access with an agent.

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
