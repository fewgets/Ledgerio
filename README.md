<!-- Ledgerio · README by Usama Shahid (fewgets) -->
<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0D1117,55:0F3D3E,100:36FFC7&height=230&section=header&text=Ledgerio&fontSize=60&fontColor=FFFFFF&fontAlignY=36&desc=Intelligent%20point-of-sale%20and%20business%20ledger%20for%20wholesale&descSize=17&descAlignY=58&animation=fadeIn" width="100%" alt="Ledgerio"/>

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=22&duration=3000&pause=700&color=36FFC7&center=true&vCenter=true&width=720&height=60&lines=Sales%2C+Stock+and+Credit+in+One+App;Smart+Daily+Business+Insights;Native+Windows+Speed+with+.NET+10" alt="Typing SVG"/>

<p>
  <img src="https://img.shields.io/badge/C%23-512BD4?style=for-the-badge&logo=dotnet&logoColor=white" alt="C#"/>
  <img src="https://img.shields.io/badge/.NET%2010-512BD4?style=for-the-badge&logo=dotnet&logoColor=white" alt=".NET 10"/>
  <img src="https://img.shields.io/badge/WPF-0C54C2?style=for-the-badge&logo=windows&logoColor=white" alt="WPF"/>
  <img src="https://img.shields.io/badge/Supabase-3ECF8E?style=for-the-badge&logo=supabase&logoColor=white" alt="Supabase"/>
  <img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white" alt="PostgreSQL"/>
  <img src="https://img.shields.io/badge/xUnit-5E2D79?style=for-the-badge&logo=dotnet&logoColor=white" alt="xUnit"/>
</p>

</div>

---
> 💼 **Project showcase.** Ledgerio is a production app built for a wholesale footwear business, so the
> source code is private. This page explains what it does and how it is built.

## 📌 Overview

**Ledgerio** is a native **Windows point-of-sale and business-ledger application** for wholesale
and distribution businesses. It replaces paper registers and spreadsheets with one fast desktop app
that manages **customers (debit parties), suppliers (credit parties), stock, bank accounts and staff
salaries**, then turns all of that data into **daily insights, analytics and printable PDF reports**.

It started as a Python (CustomTkinter) app and was **rebuilt from the ground up in C# / WPF on .NET 10**
for a faster, fully native feel, with **full functional parity** checked against the original.

---

## ✨ Features

### 🧾 Sales and Customer Ledger (Debit)
- Multi-item **orders** with live price preview, stock deduction and per-item recovery if one fails
- Customer accounts with **city → province** mapping and Active / Defaulted status
- Running balances, payments (cash, online, slip, cheque), returns and discounts
- Reports: **single party, city-wise, province-wise, and old / overdue accounts** (overdue rows highlighted)

### 🏭 Supplier Ledger (Credit)
- Supplier accounts and purchase entries with automatic debit/credit detection
- Latest balances, single-party and whole-ledger PDF reports

### 📦 Stock Management
- Add, update, edit and delete articles, with **low-stock highlighting**
- Full **stock movement log**: daily *added vs. sold* activity report
- Configurable stock fields and printable stock sheets

### 🏦 Banks and 👥 Staff
- Bank accounts with transaction history
- Staff directory, monthly salaries, bonuses, deductions and **advances to recover**
- One-click **PDF salary slips**

### 📊 Smart Dashboard and Analytics
- **"Today" strip:** sales today vs. yesterday, cash vs. credit sales, payments received, returns, discounts
- **Automatic insight lines** in plain language (good news ✅ or needs attention ⚠️)
- **Top debtors** list showing who owes most and how long since their last entry
- Analytics by any date range with automatic daily / weekly / monthly grouping, **best sellers** and period-over-period change

### 🎨 Experience
- **12 colour themes** (Sage, Teal, Navy, Leather, Graphite, Obsidian, Emerald, Luxe…), light and dark
- **Customisable keyboard shortcuts** (`Ctrl + key`) for every main action
- Searchable drop-downs, toast notifications, skeleton loaders, smooth scrolling
- PDF reports on the business **letterhead**, saved and auto-numbered automatically

### 🔐 Security
- **Login lockout:** 5 failed attempts lock the account for 1 hour (enforced on the server)
- Hashed passwords and role-based access

---

## 🏗️ Architecture

A clean, layered **MVVM** solution. Business rules have **zero dependency** on the UI or the database,
so either can be swapped without touching the logic.

```mermaid
flowchart TB
    UI[🖥️ ElegantFootwear.App<br/>WPF · MVVM · DI · themes]
    SVC[⚙️ Services<br/>Debit · Credit · Stock · Staff · Bank<br/>Analytics · Insights · PDF reports · Auth]
    IF[📐 DataAccess.Interfaces<br/>repository contracts]
    DA[🗄️ DataAccess.Supabase<br/>repository implementations]
    CORE[📦 Core<br/>domain models · ServiceResult]
    DB[(☁️ Supabase<br/>PostgreSQL)]

    UI --> SVC
    SVC --> IF
    DA -.implements.-> IF
    DA --> DB
    SVC --> CORE
    UI --> CORE
```

| Project | Responsibility |
|---|---|
| `Core` | Domain models (parties, transactions, stock, staff, banks) and result types |
| `DataAccess.Interfaces` | Repository contracts |
| `DataAccess.Supabase` | Implementations using the official Supabase C# client |
| `Services` | 100% of the business rules, analytics, insights and PDF generation |
| `App` | WPF views and view models, navigation, theming, dependency injection |
| `Tests` | xUnit + Moq unit tests |

---

## 📈 By the Numbers

| | |
|---|---|
| 🖥️ Screens | **30+** (dashboard, 10 debit, 7 credit, 6 stock, banks, staff, analytics, reports, settings) |
| 🧪 Unit tests | **110** xUnit tests covering the highest-risk logic |
| 🎨 Themes | **12** |
| 📄 PDF report types | **10+** ledgers, stock sheets and salary slips |

**Tested logic includes:** stock replace-vs-add semantics, stock-movement logging, the
quantity/price vs. manual-amount conflict rule, login lockout, analytics grouping, dashboard insights,
salary calculations, PDF generation and keyboard-shortcut conflicts.

---

## 🧰 Tech Stack

| Layer | Technology |
|---|---|
| Language / Runtime | C#, .NET 10 |
| UI | WPF, MVVM, Microsoft.Extensions.DependencyInjection / Hosting |
| Database | Supabase (PostgreSQL) via `supabase-csharp` |
| PDF | PdfSharpCore, SixLabors.ImageSharp |
| Testing | xUnit, Moq |
| Previous version | Python, CustomTkinter, ReportLab |

---

## 📂 Source Code

Ledgerio is a client product, so the source code is private.
**Want a similar system for your business, or a demo?** Get in touch below.

---

## 📜 License

© 2026 Usama Shahid. All rights reserved. This repository is a project showcase; the source code is private.

---

## 🤝 Let's Work Together

<div align="center">

**Have an idea, a freelance project, or want to collaborate on something in AI?**
I'm always open to collaborations, freelance work and full-time opportunities.

<a href="mailto:shaikhusama541@gmail.com?subject=Collaboration%20-%20Ledgerio">
  <img src="https://img.shields.io/badge/Email-shaikhusama541%40gmail.com-36FFC7?style=for-the-badge&logo=gmail&logoColor=white&labelColor=0D1117" alt="Email"/>
</a>
<a href="https://www.linkedin.com/in/-usamashahid/">
  <img src="https://img.shields.io/badge/LinkedIn-Usama%20Shahid-36FFC7?style=for-the-badge&logo=linkedin&logoColor=white&labelColor=0D1117" alt="LinkedIn"/>
</a>
<a href="https://github.com/fewgets">
  <img src="https://img.shields.io/badge/GitHub-fewgets-36FFC7?style=for-the-badge&logo=github&logoColor=white&labelColor=0D1117" alt="GitHub"/>
</a>

<br/><br/>

⭐ **If you like this project, please give it a star. It really helps!** ⭐

<br/>

<h3>"Run your business on numbers, not guesswork."</h3>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:36FFC7,55:0F3D3E,100:0D1117&height=150&section=footer&animation=twinkling" width="100%" alt="footer"/>

</div>
