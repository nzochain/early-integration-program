# NZOChain — Early Integration Program

**Documentação pública e exemplos de integração REST da infraestrutura de segurança Web3 NZOChain.**

Explore, integre e construa com a NZOChain — análise de risco de carteiras, contratos e transações via API REST.

> **Percurso principal:** [site NZOChain](https://nzochain.com/) → [página Early Integration](https://nzochain.com/early-integration/) → este repositório para guias técnicos.  
> O GitHub é o destino complementar de documentação — não substitui a página local do programa.

Este repositório público é o primeiro conjunto oficial de documentação e exemplos para equipas que pretendem testar e integrar a NZOChain em wallets, dApps, protocolos, exchanges e outros produtos Web3.

> **Âmbito:** apenas documentação, exemplos de integração e recursos públicos.  
> **Não** é uma publicação do código-fonte proprietário, backend ou infraestrutura privada da NZOChain.  
> Nesta fase **não** existe licença open source. Visibilidade pública não concede direitos de reutilização da propriedade intelectual da NZOChain.

**Versão:** 1.1.0 · **Data:** 2026-11-07

Idioma técnico principal deste repositório: [README.md](./README.md) (inglês).

---

## Estado do produto (resumo)

A NZOChain disponibiliza análise de risco via API REST e aplicação B2C.

- **RiskScore atual:** heurísticas, regras de avaliação e sinais de segurança de múltiplas fontes. Não utiliza um modelo de IA/ML treinado.
- **Scans:** on-demand; re-scan agendado é opt-in (intervalo de 6 horas quando disponível/ativado). Não é monitorização contínua nem em tempo real.
- **Redes suportadas pelo motor de scan identificado:** Ethereum, BNB Chain, Polygon, Arbitrum.
- **SDK oficial:** não publicado. Integração via REST API.

Detalhes: [PRODUCT-STATUS.md](./PRODUCT-STATUS.md)

---

## Preços B2B (referência)

| Plano | Preço/mês | API calls/mês | Simulações/mês |
|---|---:|---:|---:|
| Free | $0 | 1.000 | 0 |
| Starter | $49 | 25.000 | 100 |
| Growth | $149 | 100.000 | 2.000 |
| Business | $499 | 500.000 | 10.000 |
| Enterprise | Custom | Contrato | Contrato |

Detalhes de quotas, overage e planos B2C: [PRICING.md](./PRICING.md)

---

## Quickstart

1. Criar conta em https://developers.nzochain.com/
2. Gerar API Key (nunca publicar no GitHub)
3. Chamar `POST https://api.nzochain.com/api/v1/wallets/risk` com header `X-API-Key`
4. Interpretar `riskScore`, `riskLevel` e `decision`

Guia completo: [QUICKSTART.md](./QUICKSTART.md)

---

## Guias técnicos

| Tema | Documento |
|---|---|
| Integrações | [integrations/README.md](./integrations/README.md) |
| Casos de uso | [use-cases/](./use-cases/) |
| Autenticação | [api/authentication.md](./api/authentication.md) |
| Redes | [api/supported-networks.md](./api/supported-networks.md) |
| Rate limits | [api/rate-limits-and-errors.md](./api/rate-limits-and-errors.md) |
| Webhooks | [api/webhooks.md](./api/webhooks.md) |

---

## Early Integration Program

Programa para equipas que desejam integrar, experimentar e validar os serviços de segurança da NZOChain — com documentação, exemplos e acompanhamento técnico conforme disponibilidade.

O programa centra-se em integração técnica e validação. Não inclui financiamento, quotas especiais além do plano Free publicado, SLA ou parceria comercial automática.

Detalhes: [EARLY-INTEGRATION-PROGRAM.md](./EARLY-INTEGRATION-PROGRAM.md)

Página: https://nzochain.com/early-integration/

---

## QuickNode Startup Program

A NZOChain foi aceite no QuickNode Startup Program, passando a integrar um ecossistema que apoia empresas em fase inicial a construir produtos e infraestrutura Web3. Este marco reforça a ligação ao ecossistema de developers enquanto continuamos a desenvolver infraestrutura de segurança para wallets, aplicações e protocolos.

Detalhes: [QUICKNODE-STARTUP-PROGRAM.md](./QUICKNODE-STARTUP-PROGRAM.md)

---

## Plano de auditoria

A NZOChain pretende realizar uma auditoria de segurança independente durante o primeiro semestre de 2027. A concretização deste objetivo dependerá da disponibilidade de financiamento, do crescimento da receita recorrente ou de um evento de liquidez que torne o investimento sustentável. A auditoria ainda não foi contratada nem agendada.

Detalhes: [SECURITY-AND-ROADMAP.md](./SECURITY-AND-ROADMAP.md)

---

## Links oficiais

- Website: https://nzochain.com/
- Developer Portal: https://developers.nzochain.com/
- Documentação: https://docs.nzochain.com/
- API: https://api.nzochain.com/
- App B2C: https://app.nzochain.com/
- GitHub: https://github.com/nzochain/early-integration-program

## Contacto

**Email:** contact@nzochain.com  
**Assunto sugerido:** `NZOChain Early Integration Program`
