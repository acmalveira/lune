# Pipedream Workflow — Lead Information

## Purpose

This workflow retrieves the complete lead record from Google Sheets and returns the structured information through an HTTP response.

It is used to provide the Presentation and Closing agent with the lead data collected and processed by the pipeline.

## Workflow

```text
Trigger
  ↓
find_row
  ↓
return_http_response
```

## 1. Trigger

Receives an HTTP request.

The workflow expects the lead email in:

```text
{{steps.trigger.event.body.email}}
```

The email is used as the lookup key for the lead record.

## 2. find_row

Searches the lead database in Google Sheets.

Configuration:

- Drive: My Drive
- Spreadsheet: Dados coletados do Agente 01
- Worksheet: Leads
- Column: C
- Search value: `{{steps.trigger.event.body.email}}`
- Export Row: TRUE

The complete row is returned so that the response step can expose the lead information as structured data.

## 3. return_http_response

Returns HTTP status code `200`.

The response body is a JSON object with:

- `success`
- `dados`

The `dados` object maps the values retrieved from the lead row to named fields.

### Returned fields

| Field | Source |
|---|---|
| `data_hora` | row[0] |
| `nome_do_lead` | row[1] |
| `email_do_lead` | row[2] |
| `empresa_negocio` | row[3] |
| `segmento` | row[4] |
| `porte_do_negocio` | row[5] |
| `objetivo_com_o_site` | row[6] |
| `recursos_desejados` | row[7] |
| `nivel_de_maturidade_digital` | row[8] |
| `canal_de_origem` | row[9] |
| `perfil` | row[10] |
| `interesse` | row[11] |
| `quadrante` | row[12] |
| `classificacao_final` | row[13] |
| `comentario_do_agente` | row[14] |
| `whatsapp` | row[15] |
| `diagnostico_validado` | row[16] |
| `funcionalidades_prioritarias` | row[17] |
| `argumentos_personalizados` | row[18] |
| `validacao_final` | row[19] |
| `proposta_enviada` | row[21] |
| `justificativa_da_proposta` | row[22] |
| `email_ao_lead` | row[23] |
| `link_da_imagem_proposta` | row[25] |

The response is wrapped by the value retrieved from `row[25]`, as shown in the Pipedream configuration:

```text
{{steps.find_row.$return_value[0].row[25]}}{
  "success": true,
  "dados": {
    ...
  }
}
```

## Data Flow

Lead email → Google Sheets lookup → Complete lead record → Structured HTTP response → Presentation and Closing agent

## External Service

- Google Sheets
- Pipedream Webhook / HTTP response

## Security and sanitization

The repository version does not include Google account credentials, OAuth tokens, private webhook secrets, or other authentication credentials.

The Google Sheets spreadsheet and worksheet names are preserved because they describe the implementation structure. Account credentials are intentionally omitted.

