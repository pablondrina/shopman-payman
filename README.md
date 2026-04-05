# shopman-payman

Gestão de pagamentos para Django. Payment intents com lifecycle completo, transações imutáveis, suporte a múltiplos gateways (PIX, cartão, counter), e protocols para integração com qualquer provedor.

Part of the [Django Shopman](https://github.com/pablondrina/django-shopman) commerce framework.

## Domínio

- **PaymentIntent** — intenção de pagamento vinculada a um pedido. Status: pending → authorized → captured → failed/cancelled/refunded. Suporta PIX, cartão, counter (caixa), e external (marketplace).
- **PaymentTransaction** — movimentação financeira imutável (capture, refund, chargeback). Audit trail completo com gateway_id.

## PaymentService

| Método | O que faz |
|--------|-----------|
| `create_intent(order_ref, method, amount_q)` | Cria intenção de pagamento |
| `authorize(intent_ref)` | Autoriza (reserva no gateway) |
| `capture(intent_ref)` | Captura (efetiva cobrança) |
| `cancel(intent_ref)` | Cancela intent pendente |
| `refund(intent_ref, amount_q)` | Estorno total ou parcial |

## Protocols

O Payman define `GatewayIntent` protocol — qualquer gateway (EFI, Stripe, PagSeguro) implementa este contrato. O framework resolve o gateway via adapter pattern.

## Instalação

```bash
pip install shopman-payman
```

```python
INSTALLED_APPS = [
    "shopman.payman",
]
```

## Development

```bash
git clone https://github.com/pablondrina/django-shopman.git
cd django-shopman && pip install -e packages/payman
make test-payman  # ~233 testes
```

## License

MIT — Pablo Valentini
