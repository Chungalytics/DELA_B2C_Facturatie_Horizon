# Qollabi_Analyse_Tool


# Inhoudstabel

- [Doelstelling](#doelstelling)
- [Gegevensbronnen](#gegevensbronnen)
- [Fasen](#fasen)
- [Data Cleaning](#data-cleaning)
  - [Transform the Data](#transform-the-data)
- [Analyse](#analyse)
  - [Bevindingen](#bevindingen)
  - [Validatie](#validatie)
  - [Ontdekking](#ontdekking)
- [Aanbevelingen](#aanbevelingen)
  - [Potentiële ROI](#potentiële-roi)
  - [Potentiële acties](#potentiële-acties)
- [Conclusie](#conclusie)

# Doelstelling 

- What is het doel?

Het facturatieproces voor Horizon in kaart brengen.

## User story 

Maandelijks krijgen wij een excel lijst van Horizon door. Op basis van deze lijst moeten we bepalen wat we gaan betalen.
Hierbij moeten wij meerdere bronnen consulteren om dit inzichtelijk te hebben.

# Gegevensbronnen

Welke bronnen hebben we allemaal die belang hebben bij de facturatie?

Query 1 - Excel file van horizon
Query 2 - Excel lijst voor de analyse

# Fasen

1 Data Gathering
2 Data Cleaning

# Data Gathering

Kopieer Query 1 naar een tabblad "RAW Horizon" in een nieuw bestand 02 - Verwerkingslijst

# Data Processing

1  Insert table uit "RAW Horizon" in Power Query.
2  Hernoem de tabel naar "01 - Lijst Verzekeringen" 
3  PQ: Controleer de periode van de maand
4  PQ: Verwijder alle dubble mailadressen 
5  PQ: Add Conditional Column: = Table.AddColumn(#"Removed Duplicates", "Feedback leeftijd", each if [age] > 68 then "Niet Factureren - Leeftijd" else null)
6  PQ: Verwijder kolom "buy_intent" & "sent_to"
7  PQ: Insert table met alle leads: "02 - CRM Leads"
8  PQ: New Query - Combine - Merge Queries as New: "01 - Lijst Verzekeringen" / "02 - CRM Leads" op basis van mailadres.
9  PQ: Merge1: Expand all columns buiten email
10 PQ: Add column: = Table.ReorderColumns(#"Added Conditional Column",{"email_client", "age", "date", "Feedback leeftijd", "Feedback", "02 - CRM Leads.Lead Number", "02 - CRM Leads.Created On", "02 - CRM Leads.Created By", "02 - CRM Leads.Lead Type", "02 - CRM Leads.Owner", "02 - CRM Leads.Customer Lifecycle Status (Parent Contact for lead) (Contact)", "02 - CRM Leads.Assigned Agent", "02 - CRM Leads.Source", "02 - CRM Leads.Type", "02 - CRM Leads.Postal Code", "02 - CRM Leads.Lead Provider", "02 - CRM Leads.Description", "02 - CRM Leads.Status", "02 - CRM Leads.Status Reason", "02 - CRM Leads.Status (Qualifying Opportunity) (Opportunity)", "02 - CRM Leads.Status Reason (Qualifying Opportunity) (Opportunity)", "02 - CRM Leads.Yomi Full Name", "02 - CRM Leads.Yomi First Name", "02 - CRM Leads.Yomi Middle Name", "02 - CRM Leads.Yomi Last Name", "02 - CRM Leads. Full Name (Parent Contact for lead) (Contact)", "02 - CRM Leads.Owner (Parent Contact for lead) (Contact)", "02 - CRM Leads.Abandonded Step", "02 - CRM Leads.Producer Account", "02 - CRM Leads.Status (Producer Account) (Producer Account)", "02 - CRM Leads.Intermediary (Producer Account) (Producer Account)", "02 - CRM Leads.Lead Generator (Producer Account) (Producer Account)", "02 - CRM Leads.Phone (Home/Office)", "02 - CRM Leads.Phone (Mobile)", "02 - CRM Leads.Date of Birth (Parent Contact for lead) (Contact)", "02 - CRM Leads.Language", "02 - CRM Leads.Postal Code (Parent Contact for lead) (Contact)", "02 - CRM Leads.City", "02 - CRM Leads.Lead Provider Reference", "02 - CRM Leads.Rating", "02 - CRM Leads.Assignment Status", "02 - CRM Leads.Postal Code (lookup)", "02 - CRM Leads.Country"})
11 PQ: Reorder columns
12 Copy all info out of Merge1 





# Ontwerp

Lijst kopiëren naar map sharepoint: C:\Users\cwong\Dela\INS - Sales Support - Test B2C structuur\07. Lead Management\03. Facturation\Verzekeringen & Assurances\202501
Data "01 - Lijst Verzekeringen" omzetten in een tabel
PQ: Inladen tabel "01 - Lijst Verzekeringen"
PQ: Sorteren "age" descending ==> Geen 68+ of Alles van de correcte maand?
verwijder kolommen age / sent_to / buy_intent
verwijder dubbels mailadres
Download: "All Leads B2C/B2B - Analyse leads"
PQ: Inladen alle leads CRM
Merge Mailadressen met CRM alle leads
Merge statussen in CRM

Indien geen leadnummer ==>status: No lead received 
1e controle dubbele leads van verzekeringen.be in CRM
![image](https://github.com/user-attachments/assets/ae37a609-e6a2-4236-97e3-fc7fb8b59ebe)


