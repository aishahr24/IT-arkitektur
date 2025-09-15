# HaaV – Fælles sprog (Ubiquitous Language)

- **“Ordre”** = *entitet* der repræsenterer et køb (Kunde ↔ Medlem). Indeholder ordrelinjer, totaler, status.  
  (Det er ikke en proces; processen hedder **Køb vare** / **Checkout**.)

- **“Produkt”** = *entitet* som kan være fysisk vare eller service. Tilhører ét Medlem.  
  (Katalog er en *samling* af Produkter – ikke en kopi af data.)

- **“Betaling”** = *entitet* der beskriver transaktion hos betalingsudbyder (autoriseret, gennemført, refunderet).  
  Betaling er ikke det samme som Ordrestadie – en Ordre kan være “Shipped”, selvom betalingen var gennemført tidligere.

- **“Kunde” vs. “Medlem”**  
  Kunde = køber på platformen. Medlem = sælger/udbyder. (Roller og data adskilles for at undgå forveksling.)

- **“Udbetaling”** = *proces + dataresultat* hvor platformen sender penge til Medlem på baggrund af gennemførte Ordrer.

- **Status-begreber**  
  Ordre.Status: `Created → Paid → Fulfillment → Completed/Cancelled`  
  Betaling.Status: `Authorized → Captured → Refunded/Failed`
