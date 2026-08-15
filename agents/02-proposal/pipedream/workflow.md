# Pipedream Workflow — Proposal

## Purpose

This workflow processes the visual proposal generated for a qualified lead.

It retrieves the lead record, updates proposal-related information, locates the proposal image in Google Drive, uploads the image to Cloudinary, records the resulting URL, sends an email to the lead, and returns an HTTP response.

## Workflow

Trigger → find_row → update_cell_Proposta → update_cell_Justificativa → list_files → hash → custom_request → update_cell1 → send_email → update_cell → return_http_response

## Steps

### 1. Trigger

Receives the workflow request through an HTTP webhook.

Input data used by subsequent steps includes:

- email
- proposta_enviada
- justificativa

### 2. find_row

Searches the Google Sheets lead database.

Configuration:

- Spreadsheet: Dados coletados do Agente 01
- Worksheet: Leads
- Search column: C
- Search value: lead email received by the trigger
- Export Row: enabled

The returned row is used by subsequent steps to identify the lead and retrieve related data.

### 3. update_cell_Proposta

Updates the proposal status in the lead record.

- Spreadsheet: Dados coletados do Agente 01
- Worksheet: Leads
- Row: retrieved from find_row
- Column: V
- Value: proposta_enviada from the trigger

### 4. update_cell_Justificativa

Updates the justification associated with the proposal.

- Spreadsheet: Dados coletados do Agente 01
- Worksheet: Leads
- Row: retrieved from find_row
- Column: W
- Value: justificativa from the trigger

### 5. list_files

Searches Google Drive for the proposal image.

Configuration:

- Drive: My Drive
- Parent folder: retrieved from the lead record
- Returned fields: id, mimeType, name, webContentLink, webViewLink
- File filter: .png
- Filter type: CONTAINS
- Trashed: FALSE

The resulting file identifier is used by the Cloudinary upload step.

### 6. hash

Generates the Cloudinary request signature.

The step:

1. generates a Unix timestamp;
2. defines the upload folder as propostas;
3. creates the Cloudinary signing string;
4. generates the signature using SHA-1;
5. returns timestamp, signature and folder.

The Cloudinary API secret is supplied through a protected Pipedream property and is not stored in this repository.

**Note:** this SHA-1 signature is part of the Cloudinary API authentication process. It is not the SHA-256/SHA-512 hash required for the UNIFEI software registration.

### 7. custom_request

Uploads the proposal image to Cloudinary.

Configuration:

- HTTP method: POST
- Content type: multipart/form-data
- File: retrieved from Google Drive
- API key: supplied through the workflow configuration
- Timestamp: returned by hash
- Signature: returned by hash
- Folder: propostas

The response provides the Cloudinary secure URL.

Credentials and private configuration values are intentionally excluded from this repository.

### 8. update_cell1

Stores the Cloudinary URL in the lead record.

- Spreadsheet: Dados coletados do Agente 01
- Worksheet: Leads
- Row: retrieved from find_row
- Column: Z
- Value: secure_url returned by custom_request

### 9. send_email

Sends the proposal notification to the lead.

Configuration:

- Recipient: lead email received by the trigger
- Subject: Sua proposta personalizada está pronta! 💡✨
- Body type: HTML

The message:

- addresses the lead by name;
- informs that the visual proposal is ready;
- references the lead's registered email;
- directs the lead to the presentation and closing agent;
- provides the proposal access link;
- closes with the Bamboo Tec signature.

The workflow uses an authenticated Gmail connection. Account credentials are not stored in this repository.

### 10. update_cell

Records the result of the email operation.

- Spreadsheet: Dados coletados do Agente 01
- Worksheet: Leads
- Row: retrieved from find_row
- Column: X
- Value: the first Gmail label ID returned by send_email

### 11. return_http_response

Returns the final HTTP response.

- Status code: 200

Response fields:

- status — Gmail status
- summary — Gmail summary
- mensagem — confirmation that the email was sent
- imagem_no_cloudinary — Cloudinary secure URL

## Data Flow

Lead email → Google Sheets → Lead record → Proposal data → Google Drive → Proposal PNG → Cloudinary → Secure proposal URL → Google Sheets → Gmail → HTTP response

## External Services

The workflow integrates with:

- Google Sheets
- Google Drive
- Cloudinary
- Gmail
- Pipedream

## Security

The repository does not contain:

- API secrets
- OAuth credentials
- private account credentials
- authentication tokens
- private webhook secrets

Credentials remain managed by the respective platforms and Pipedream's encrypted credential system.

