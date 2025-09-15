# HaaV – Subdomæner (Core / Support / Generic) og Boundaries

## Kategorisering
- **Core (kerne)**
    - **Commerce / Ordering**: oprette kurv, checkout, ordrer, ordrelinjer, priser, kampagner.
    - **Catalog / Product**: produktdata, kategorier, søgning, lager/kapacitet pr. medlem.

- **Support (støtte)**
    - **Fulfillment / Logistics**: forsendelse, tracking, leveringsaftaler, returhåndtering.
    - **Payouts**: afregning/udbetaling til Medlem baseret på færdigbehandlede ordrer.

- **Generic (generisk)**
    - **Payments**: integration til betalingsudbydere (Stripe/Nets/etc.).
    - **Identity & Access**: login, roller, rettigheder (Kunde, Medlem, Admin).
    - **Notifications**: e-mail/SMS/push-beskeder.

## Forslag til afgrænsede kontekster (bounded contexts)
- **ProductContext** (Core: Catalog/Product) – ejer produktdata. Egen DB.
- **OrderContext** (Core: Commerce/Ordering) – ejer Ordre og Ordrelinjer. Egen DB.
- **PaymentContext** (Generic) – ejer Betalinger/Transaktioner. Egen DB. Event: `PaymentCaptured`, `PaymentRefunded`.
- **FulfillmentContext** (Support) – forsendelse, returlogik. Events: `OrderShipped`, `ReturnRequested`.
- **PayoutContext** (Support) – batch-afregninger til Medlem. Event: `PayoutExecuted`.
- **IdentityContext** (Generic) – kunder/medlemmer/roller, tokens.

## Simpelt context-map (tekst)

[Customer App] ──REST──> (OrderContext) ──events──> (FulfillmentContext)
│                         └─events──> (PaymentContext)
└─REST──> (ProductContext)

(ProductContext) ──queries──> (Search/ReadModel)
(OrderContext) <──events── (PaymentContext: PaymentCaptured)
(PayoutContext) <──events── (OrderContext: OrderCompleted)

- Hver kontekst ejer sin **egen database**.
- Kommunikation: **REST** til synkrone kald (læse/kommandere), **events** til asynkrone reaktioner.
