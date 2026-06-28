# Retail Sales Performance Dashboard — Power BI

Sales performance dashboard for a Brazilian electronics retailer covering **€3.7B in gross revenue** across **1.3M transactions** (2010–2022). Built with a star schema data model and advanced DAX measures including time intelligence and dynamic metrics.

---

## 🎯 Key Business Questions

- How is net revenue performing vs the previous year?
- Which categories, brands and products drive the most revenue?
- How is revenue split between Internet and physical store channels?
- Where are margins being eroded by discounts?
- Which products are growing or declining YoY?

---

## 📐 Data Model — Star Schema

Fact table `fato_vendas` connected to 4 dimension tables.

| Table | Type | Description |
|---|---|---|
| fato_vendas | Fact | Sales transactions (Date, Channel, Client, Product) |
| Dim_produto | Dimension | Product catalogue with category, subcategory and brand |
| Dm_calendario | Dimension | Custom calendar table for time intelligence |
| Dm_canal | Dimension | Sales channel (Internet vs Physical Store) |
| Dim_cliente | Dimension | Customer data |

---

## 🧠 DAX Measures

Measures organised into 4 folders:

**00 — Medidas Diversas**
Core aggregations: Net Revenue, Gross Revenue, Discount, Margin, Quantity

**01 — Performance**
- `Receita Líquida = ...`
- `Margem % = DIVIDE([Margem], [Receita Líquida], 0)`
- `Share % = DIVIDE([Receita Líquida], CALCULATE([Receita Líquida], ALL(...)), 0)`

**03 — Inteligência de Tempo**
- `Ano Anterior = CALCULATE([Receita Líquida], SAMEPERIODLASTYEAR(Dm_calendario[Data]))`
- `YoY % = DIVIDE([Receita Líquida] - [Ano Anterior], [Ano Anterior], 0)`

**05 — Medidas Dinâmicas**
- Metric selector via `Aux_Medidas` table — allows switching between Revenue, Margin, Discount and Quantity using a single slicer

---

## 📋 Dashboard Pages

- **Capa** — Landing page with navigation
- **Resumo** — Main KPIs (Net Revenue, Discount, Margin + YoY), revenue trend by month vs prior year, channel split (Internet vs Physical Store), revenue by brand, and category breakdown table with Share % and YoY
- **Decomposição** — Hierarchical decomposition tree: Total → Category → Subcategory → Brand → Product. Drillable to individual SKU level
- **Tabela** — Full transaction-level table with Date, Channel, Product, Quantity, Discount and Gross Revenue

---

## 💡 Key Findings

- **Samsung** is the top brand at €63.3M, followed by **Apple** at €40.6M (2015)
- **Informática** is the largest category (39% share), followed by **Eletrodomésticos** (31.2%)
- Channel split is near-even: **Internet 50% vs Physical Store 50%**
- **Games** and **Televisores** show negative YoY growth (-9.4% and -3.2%) while **Celulares** and **Eletrodomésticos** grow +2.8% and +2.5%
- **Eletroportáteis** is the smallest category at 1.7% share with declining trend (-5.6% YoY)

---

## 🛠️ Tools & Technologies

`Power BI` `DAX` `Power Query` `Star Schema` `Time Intelligence`

---

## 📂 Repository Structure

```
├── V1_-_estrela.pbix      # Power BI report file
└── README.md
```
