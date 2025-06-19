# itis_TSN_ScientificName

# 🐟 ITIS SQLite Database Processing

This project uses the **ITIS.sqlite** file from the [Integrated Taxonomic Information System (ITIS)](https://www.itis.gov/downloads) to build a clean reference list of species, combining scientific names and common names for organisms — with a focus on valid entries in the **Animal kingdom**.

---

## 📦 What is ITIS?

The **ITIS.sqlite** file is the SQLite version of the Integrated Taxonomic Information System (ITIS). It provides standardized taxonomic information on:

- Animals
- Plants
- Fungi
- Microbes

This includes scientific names, common names, hierarchical relationships, synonym tracking, and authorship details.

---

## 🗂️ Key Tables in ITIS.sqlite

| Table Name          | Description                                                               |
|---------------------|---------------------------------------------------------------------------|
| `taxonomic_units`   | Core table with TSN (Taxonomic Serial Number), scientific name, rank, and status. |
| `vernaculars`       | Common names associated with TSNs (e.g., `"walleye"` → TSN `168507`).     |
| `hierarchy`         | Parent-child relationships (e.g., genus to species).                      |
| `synonym_links`     | Links between valid TSNs and their synonyms.                              |
| `taxon_authors_lkp` | Authorship information for scientific names.                              |
| `kingdoms`          | List of biological kingdoms (e.g., Animalia, Plantae).                    |

---

## 🧪 Data Processing Steps

This project focuses on extracting relevant entries for the **Animal Kingdom** (where `kingdom_id = 5`) that are:

- **Valid** (`usage = 'valid'`)
- **In English** (`language = 'English'`)

### ✅ Steps:

1. **Filter `taxonomic_units`**  
   - Only rows where:
     - `kingdom_id = 5` (Animalia)
     - `usage = 'valid'`

2. **Join with `vernaculars`**  
   - For each `TSN`, collect **all English common names**
   - Use `'/ '.join()` to concatenate multiple names into a single string per TSN

3. **Final Output Columns**  
   - `TSN`
   - `Scientific Name`
   - `Common Names in English` (all joined with `/ `)

---

