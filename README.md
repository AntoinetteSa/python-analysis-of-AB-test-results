# python-analysis-of-AB-test-results
End-to-end A/B test analysis in Python: historical power analysis (MDE), data cleansing of logging anomalies, and conversion window modeling. Features cumulative CVR evaluation and statistical validation via Z-test.


[🇺🇸 English Version](#-english-version) | [🇺🇦 Українська версія](#-українська-версія)
________________________________________

## 🌍 English Version

### 📌 Project Overview
This project evaluates the performance of a product experiment (A/B test) that introduced a pinned low-balance reminder in the user chat interface to boost the first-to-payment conversion rate ($CVR$). 

### 🛠️ Tech Stack
* **Python** (Pandas, NumPy)
* **Statistical Analysis & Power Calculations:** `statsmodels` (Z-test for proportions, `NormalIndPower`, `proportion_effectsize`)
* **Data Visualization:** Matplotlib, Seaborn

### 📂 Repository Structure
* `проект_a_b_тестування.ipynb` — interactive Jupyter Notebook with charts and execution steps.
* `проект_a_b_тестування.py` — production Python script for clean automated execution.

---

### 📊 Executive Business Summary

#### 1. Experimental Results
Metrics evaluated strictly within a valid 3-day conversion window (after filtering out logging anomalies):
* **Control Group (Current Interface):** 11.17% CVR (25,631 users, 2,864 payments)
* **Treatment Group (Pinned Reminder):** 11.70% CVR (25,856 users, 3,026 payments)
* **Performance Impact:** Absolute increase of **+0.53%**, resulting in a relative lift of **+4.74%** compared to the Control baseline.

#### 2. Statistical Validity
* A two-sided Z-test for proportions returned a **p-value = 5.92%**, which exceeds the critical significance threshold ($\alpha = 0.05$).
* **Business Implication:** The observed +4.74% lift is not yet statistically reliable. There is a 5.92% probability that this variance is driven by random traffic fluctuations. 
* Cumulative dynamic trends show both groups achieved steady plateaus, but the performance gap is currently too narrow to confirm success with 95% confidence.

#### 3. Final Product Decision & Next Steps
* **Experiment Status: Inconclusive / Neutral.** A full feature roll-out is paused to protect the product from unverified updates.
* **Core Action:** Prolong the experiment for exactly **7 calendar days**. Because the test is on the verge of significance ($5.92\% \approx 5\%$) and the trend lines are perfectly stable, accumulating a slight amount of additional traffic will provide the statistical power needed to confidently confirm the lift and justify roll-out costs.

#### 4. Risk Safeguards
During the extended testing week, the team will monitor two guardrail metrics:
1. **Average Order Value (AOV):** To ensure the reminder does not shift purchasing behavior toward the cheapest credit packages, maintaining overall revenue growth.
2. **User Retention:** To verify that the persistent UI banner does not cause fatigue or increase churn among non-paying audiences.

________________________________________

## 🇺🇦 Українська версія

### 📌 Короткий опис проєкту
Цей проєкт присвячений оцінці результатів продуктового експерименту (A/B тесту) щодо впровадження закріпленого нагадування про низький баланс у чаті з метою збільшення конверсії в першу оплату ($CVR$).

### 🛠️ Використовувані технології
* **Python** (Pandas, NumPy)
* **Статистичний аналіз та розрахунок потужності:** `statsmodels` (Z-test для пропорцій, `NormalIndPower`, `proportion_effectsize`)
* **Візуалізація даних:** Matplotlib, Seaborn

### 📂 Структура репозиторію
* `проект_a_b_тестування.ipynb` — інтерактивний ноутбук Jupyter із графіками та покроковим кодом.
* `проект_a_b_тестування.py` — чистий скрипт Python для автоматизованого запуску.

---

### 📊 Бізнес-резюме результатів експерименту

#### 1. Результати тестування
Показники конверсії, розраховані строго в межах валідного 3-денного вікна дозрівання (після повного очищення даних від технічних збоїв логування):
* **Контрольна група (Поточний інтерфейс):** 11.17% CVR (25,631 користувач, 2,864 оплати)
* **Тестова група (Закріплене нагадування):** 11.70% CVR (25,856 користувачів, 3,026 оплат)
* **Бізнес-ефект:** Абсолютний приріст конверсії склав **+0.53%**, що відповідає відносному підняттю метрики (Lift) на **+4.74%** відносно бази.

#### 2. Статистична надійність
* Двосторонній Z-тест для пропорцій зафіксував значення **p-value = 5.92%**, що перевищує критичний бізнес-поріг похибки ($\alpha = 0.05$).
* **Значення для бізнесу:** Отриманий приріст у +4.74% наразі не є статистично значущим. Існує 5.92% ймовірності того, що зафіксована різниця є результатом випадкових коливань трафіку.
* Графік кумулятивної динаміки підтверджує, що метрики обох груп вийшли на стабільне плато, проте поточний відрив тестової лінії від контрольної занадто вузький для однозначного підтвердження успіху.

#### 3. Фінальне продуктове рішення
* **Статус тесту: Невизначений / Нейтральний.** Повний запуск фічі на 100% користувачів призупинено задля захисту продукту від непідтверджених змін.
* **Подальший крок:** Продовжити експеримент строго на **7 календарних днів**. Оскільки тест знаходиться на самій межі значущості ($5.92\% \approx 5\%$), а тренд кумулятивної конверсії ідеально стабільний, додатковий обсяг трафіку дозволить дотиснути потужність тесту та прийняти остаточне, математично обґрунтоване рішення.

#### 4. Контроль бізнес-ризиків
Протягом додаткового тижня тестування команда фокусується на двох захисних метриках:
1. **Середній чек (AOV):** Перевірка, чи не зміщує нагадування фокус продажів у бік найдешевших пакетів кредитів, руйнуючи загальний дохід (Revenue).
2. **Retention у чатах:** Моніторинг активності, щоб виключити ризик роздратування та відтоку (Churn) аудиторії через новий елемент інтерфейсу.
