# 🎓 OMR Training & Software Institutes – Analysis & Insights Dashboard

A data analytics project that studies computer training and software institutes along the **Old Mahabalipuram Road (OMR) corridor in Chennai, Tamil Nadu**. Institute data was collected and organised in Excel, modelled as a relational dataset, and visualised in an interactive **Power BI** dashboard.

![OMR Dashboard](images/dashboard.png)

---

## 📌 Project Overview

Students and working professionals along OMR have dozens of training institutes to pick from, but no single place to compare them. This project brings that information together to answer questions such as:

- Which areas and zones of OMR have the most training institutes?
- Which course categories (Programming, Data Science, Testing, Cloud, etc.) are most widely offered?
- How do institutes compare on Google rating, review count and placement support?
- Which courses are the most in demand, based on enquiries?
- How do institutes promote themselves (website, Instagram presence, activity)?

## 📊 Dataset at a Glance

| Item | Count |
|---|---|
| Institutes | 68 |
| Areas covered | 13 (Adyar/Madhya Kailash → Mahabalipuram) |
| OMR zones | 3 (North, Central, South) |
| Course categories | 10 |
| Course catalogue | 50 courses |
| Institute–course rankings | 363 |

**Areas covered:** Madhya Kailash (Adyar), Taramani, Perungudi, Kandanchavadi, Thoraipakkam, Karapakkam, Sholinganallur, Semmancheri, Navalur, Siruseri, Kelambakkam, Mahabalipuram, Kottivakkam.

**Data collection:** institute details (name, address, phone, website, rating, review count) were gathered from Google Maps using the [Apify Google Maps Scraper](https://apify.com/compass/crawler-google-places), then cleaned, de-duplicated and enriched manually with course, trainer, promotion, placement and enquiry information.

## 🗂️ Data Model

The workbook `data/OMR_Institutes_Final_Data.xlsx` contains the following sheets:

| Sheet | Description |
|---|---|
| `Area` | Area master list with OMR zone |
| `Institude` | Institute master: address, phone, website, established year, Google rating & review count, top courses |
| `Course_Category` | Course category master |
| `Institute_course` | Course catalogue (course → category) |
| `Course` | Top-ranked courses offered by each institute |
| `Trainer` | Trainer name, subject, qualification, experience, certification |
| `Promotion` | Website, Instagram link, followers, last-post activity |
| `Review` | Rating, review count, platform |
| `Placement` | Placement support, interview prep, resume support, placement %, companies reported |
| `Enquiry` | Enquiry date, source, student type, status |
| `Trainer_Details_Dammy` | Sample trainer records (kept for reference) |

**Relationships (star-style model):**

```
Area ──< Institute ──< Trainer
                   ├──< Promotion
                   ├──< Review
                   ├──< Placement >── Course
                   ├──< Enquiry   >── Course
                   └──< Course (institute–course ranking)

Course_Category ──< Course
```

## 📈 Dashboard (Power BI)

The report file is `powerbi/omr_project.pbix` (open with **Power BI Desktop**). It includes:

- **KPI cards** – headline metrics for institutes, courses and ratings
- **Bar / column charts** – institutes by area and zone, course and category comparisons
- **Donut chart** – distribution across course categories
- **Slicers** – filter by institute, location, course category and more
- **Detail tables** – institute-level drill-down

The full page-by-page design (Executive Overview, Institute, Course, Trainer, Promotion & Review, Placement & Enquiry) is described in [`docs/OMR_Power_BI_Dashboard_Design.docx`](docs/OMR_Power_BI_Dashboard_Design.docx).

## 🛠️ Tools & Technologies

- **Microsoft Power BI Desktop** – data modelling and dashboard
- **Microsoft Excel** – data storage, cleaning and validation
- **Apify (Google Maps Scraper)** – data collection
- **DAX / Power Query** – measures and transformations

## 📁 Repository Structure

```
omr-training-institutes-analysis/
├── data/
│   └── OMR_Institutes_Final_Data.xlsx     # Cleaned dataset (11 sheets)
├── powerbi/
│   └── omr_project.pbix                   # Power BI report
├── docs/
│   ├── OMR_Plan.docx                      # Project plan, sheet design & work allocation
│   └── OMR_Power_BI_Dashboard_Design.docx # Dashboard page design
├── images/
│   └── dashboard.png                      # Dashboard screenshot
├── .gitignore
└── README.md
```

## 🚀 How to Use

1. Clone or download this repository:
   ```bash
   git clone https://github.com/<your-username>/omr-training-institutes-analysis.git
   ```
2. Open `powerbi/omr_project.pbix` in **Power BI Desktop**.
3. If Power BI asks for the data source, go to **Home → Transform data → Data source settings** and point it to `data/OMR_Institutes_Final_Data.xlsx` on your machine, then click **Refresh**.
4. Use the slicers to explore institutes, locations and course categories.

## 📝 Data Notes

- Ratings and review counts reflect Google Maps at the time of collection (September 2026) and will change over time.
- Some fields (for example certain trainer details and placement figures) come from partial public information. Where information was not publicly available it is marked as *Not Mentioned* or *Not verified* rather than estimated.
- Please verify details directly with an institute before making any enrolment decision.

## 👥 Team

Project planning and execution were shared across **Armash**, **Sofia** and **Nivethitha** over a 7-day plan covering data structure, collection, entry, validation and Power BI reporting (see `docs/OMR_Plan.docx`).

## 🔮 Future Improvements

- Add fee, duration and mode (online/offline) analysis per course
- Automate data refresh from Google Maps
- Add sentiment analysis on review text
- Publish the report to Power BI Service with a public link

---

⭐ If you found this project useful, consider giving the repository a star!
