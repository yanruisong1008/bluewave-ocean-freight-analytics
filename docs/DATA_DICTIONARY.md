# Data Dictionary

## Shipments (`data/raw/shipments/shipments_YYYY-MM.csv`)

One row per shipment (booking). Files are split by booking month.

| Column | Type | Description |
|---|---|---|
| ShipmentID | Text | Unique shipment reference (BW + 6 digits) |
| BookingDate | Date | Date the customer booked the shipment |
| CustomerID | Text | Links to Customers sheet |
| CarrierName | Text | Ocean carrier (**name only, not code — needs cleaning**) |
| OriginPort | Text | UN/LOCODE of port of loading |
| DestinationPort | Text | UN/LOCODE of port of discharge |
| ContainerType | Text | Links to ContainerTypes sheet |
| ContainerQty | Whole number | Number of containers |
| Incoterm | Text | Trade term (FOB, CIF, EXW, DDP) |
| ETD / ATD | Date | Estimated / actual time of departure (ATD blank if not yet sailed) |
| ETA / ATA | Date | Estimated / actual time of arrival (ATA blank if still in transit) |
| FreightCost_USD | Decimal | Cost paid to the carrier |
| Revenue_USD | Decimal | Amount billed to the customer |
| Status | Text | Booked, In Transit, Delivered |
| DelayReason | Text | Filled when the shipment arrived more than 1 day late or was rolled |

## Master Data (`data/raw/master_data.xlsx`)

| Sheet | Key | Columns |
|---|---|---|
| Carriers | CarrierCode | CarrierName, Alliance |
| Ports | PortCode | PortName, Country, Region, PortRole (Origin / Destination) |
| Customers | CustomerID | CustomerName, Industry, SalesRegion, AccountManager, Tier |
| ContainerTypes | ContainerType | Description, TEU_Factor, Category (Dry / Reefer) |

## Budget (`data/raw/budget_2026.xlsx`)

Wide layout: one row per DestinationRegion × Metric (TEU, Revenue_USD), one column per month.

## Invoices (`data/raw/invoices.csv`)

One row per customer invoice, exported from the billing system. Links to Shipments by ShipmentID. Only shipments already delivered to the door appear.

| Column | Type | Description |
|---|---|---|
| InvoiceID | Text | Unique invoice number |
| ShipmentID | Text | Links to Shipments |
| CustomerID | Text | Links to Customers sheet |
| DoorDeliveredDate | Date | Cargo delivered to the customer's door (after ATA + drayage) |
| InvoiceSubmittedAt | Date-time | Invoice submitted to customer (blank = not yet invoiced) |
| InvoicePaidAt | Date-time | Payment received (blank = unpaid) |
| InvoiceAmount | Decimal | Billed amount |
| Currency | Text | Always USD |
| PaymentTermsDays | Whole number | Payment term after submission (45) |
| InvoiceStatus | Text | Not Invoiced, Open, Overdue, Disputed, Paid |
| DisputeFlag | Text | Y if the customer disputed the invoice |

**Business rules:** invoice must be submitted within 30 days of door delivery; customer must pay within 45 days of submission.

## Intentional Data Quality Issues

These are planted on purpose so the Power Query work reflects real operations data.

| # | Issue | Where |
|---|---|---|
| 1 | Carrier names vary in spelling, casing, suffixes and leading/trailing spaces, and must be mapped to CarrierCode | Shipments |
| 2 | Two monthly files come from a European system: semicolon delimiter, dd/mm/yyyy dates, decimal comma | `2025-08`, `2026-03` |
| 3 | Some port codes are lower case | Shipments |
| 4 | Some freight costs are stored as text with `$` and thousand separators | Shipments |
| 5 | Exact duplicate rows | Shipments |
| 6 | Blank rows at the end of some files | Shipments |
| 7 | Report-style title rows above the real header | Customers sheet |
| 8 | Months stored as columns (needs unpivoting) | Budget |
| 9 | Blank ATD/ATA are valid (not yet sailed / in transit), not errors | Shipments |
| 10 | Invoice dates carry a time stamp and must be converted to dates before calculating day differences | Invoices |
| 11 | Blank InvoiceSubmittedAt / InvoicePaidAt are valid (not yet invoiced / unpaid), not errors | Invoices |
