# Data Cleaning Change Log — Morocco Electricity Consumption

**Project:** AnalystLab Africa — Week 5, Data Analytics track  
**Scope:** Data inspection, cleaning and preparation only. No consumption analysis, charts, correlations, forecasting or business recommendations were performed.

## 1. Source files

- `powerconsumption.csv` — original input; left unchanged.
- `powerconsumption_datadictionary.csv` — reviewed for field descriptions; left unchanged.

## 2. Inspection results

- Source records: **52,416**
- Original columns: **9**
- Date-time coverage: **2017-01-01 00:00** to **2017-12-30 23:50**
- Timestamp uniqueness: **52,416 unique timestamps**; no duplicates.
- Timestamp order and cadence: **all records strictly ordered and all 52,415 intervals are exactly 10 minutes**.
- Missing cells: **0** across all original columns.
- Duplicate full rows: **0**.
- Invalid/non-finite numeric cells: **0**.
- Negative numeric measurements: **0**.
- Numeric zero values: **0**.

## 3. Changes made to the prepared copy

| Field / area | Change | Reason |
|---|---|---|
| Datetime | Re-formatted from `M/D/YYYY H:MM` to `YYYY-MM-DD HH:MM:SS` | Standard, unambiguous, sortable datetime representation; all values parsed successfully. |
| Year | Added | Required time attribute for Data Analytics preparation. |
| Month | Added as integer 1–12 | Required time attribute. |
| Day | Added as integer 1–31 | Required time attribute. |
| Hour | Added as integer 0–23 | Required time attribute. |
| DayOfWeek | Added as weekday name | Required day-of-week attribute. |
| Date | Added as `YYYY-MM-DD` | Date-only attribute for grouping and filtering. |
| Original numeric columns | Values and precision preserved as supplied | No demonstrated invalid numeric values required correction. |
| Original rows | All retained | No blank, duplicate, malformed, or invalid records were identified. |

## 4. Outlier review — flagged, not altered

The following counts are based on the conventional 1.5 × IQR rule. An IQR flag is only a statistical review signal; it does not prove a measurement is erroneous. These records were **not deleted, capped, winsorised, or replaced**.

| Column | Lower fence | Upper fence | Below lower fence | Above upper fence |
|---|---:|---:|---:|---:|
| Temperature | 1.690000 | 35.610000 | 0 | 142 |
| Humidity | 23.675000 | 116.035000 | 291 | 0 |
| WindSpeed | -7.177500 | 12.170500 | 0 | 0 |
| GeneralDiffuseFlows | -479.245000 | 798.907000 | 0 | 2,315 |
| DiffuseFlows | -151.195000 | 252.317000 | 0 | 4,571 |
| PowerConsumption_Zone1 | 9813.144454 | 53806.542424 | 0 | 0 |
| PowerConsumption_Zone2 | 5381.338801 | 36313.144751 | 0 | 7 |
| PowerConsumption_Zone3 | 387.165945 | 34366.261105 | 0 | 1,191 |

## 5. Data-dictionary issues requiring clarification

- The dictionary describes `GeneralDiffuseFlows` and `DiffuseFlows` as atmospheric emissions-gas measurements. Those definitions are not sufficiently clear for this electricity/environment dataset, and the assignment itself warns that their physical meaning should be checked. Field names and values were therefore preserved; no reinterpretation was applied.
- The dictionary labels the zone fields as **kWh**, while the assignment explicitly says to verify what each 10-minute reading represents and not to assume it is interval energy. The unit/measurement interpretation remains unresolved and should be confirmed with the programme/data provider before aggregation or unit-based claims.
- The wind-speed unit is listed as km/h in the dictionary. This was retained as source metadata, not independently verified.

## 6. Output files

- `powerconsumption_cleaned.csv` — prepared dataset with 15 columns and all 52,416 source records.
- `powerconsumption_cleaning_log.md` — this inspection summary and change log.

## 7. Important notes

- The source ends on **30 December 2017**, matching the period stated in the assignment; no rows were fabricated for 31 December.
- Apart from standardising the timestamp representation and adding the six requested time attributes, original measurement values were not changed.
- The original source CSV and data dictionary remain unchanged.
