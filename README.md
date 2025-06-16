# 🎯 Did the New Landing Page Work? A/B Testing and Behavioral Insight in Real Data

![A-B Landing page](https://github.com/user-attachments/assets/b27beacc-a5a4-4ccb-90f7-bcab22e8a388)

> _What if your company redesigned its landing page and wanted to know whether it really made a difference? Would you rely on intuition — or data?_

This is the story of a simulated A/B test dataset, where we assess whether a new landing page led to better user engagement and conversions. But this isn't just about measuring clicks — we’ll explore behavior deeper by analyzing **session duration** too.

Let’s walk through the full lifecycle of this project — from data cleaning to statistical testing — and what it reveals about making evidence-based decisions.

---

## 🧪 The Scenario

You’ve been handed two datasets:`

1. **`ab_data.csv`** — contains user ID, landing page group (`control` or `treatment`), whether they converted, and their session duration (in `MM:SS.s` format).
2. **`countries.csv`** — a mapping of users to their countries.

You're tasked with answering:

> _Did the new landing page actually perform better? And how did it impact user behavior (measured by time spent on the page)?_

---

## 🔎 Step 1: Cleaning the Real-World Mess

Real-life data is rarely clean, and this dataset is no exception. We began by:

- Merging both datasets using `user_id`
- Removing duplicate and mismatched entries (e.g., `control` group users landing on `new_page`)
- Converting the odd `MM:SS.s`-style "timestamp" into a usable `session_duration` in seconds
- Dropping rows where the conversion failed (many were malformed)

```python
def duration_to_seconds(duration_str):
    try:
        mins, secs = duration_str.split(":")
        return int(mins) * 60 + float(secs)
    except:
        return np.nan
```

After cleaning, we had a solid foundation for A/B testing.

---

## 🧮 Step 2: Conversion Rate Comparison

We first asked the simplest question:

> _Did more people convert on the new page?_

Using a **t-test** to compare the `converted` variable between groups:

```python
T Statistics:  1.319, p-value: 0.189
```

📉 **Interpretation:**  
There was **no statistically significant difference** in conversion between the two groups.

### 📊 Placeholder: Conversion Rate Bar Plot

**![Conversion Rate by Group with 95% Confidence Interval](https://github.com/user-attachments/assets/428f9d0f-79a8-487c-8e24-b112308f1824)**

---

## ⏱️ Step 3: How Long Did Users Stay?

Conversions alone don’t tell the full story. What if users **engaged** more with the new design, even if they didn’t convert?

To test this, we compared the `session_duration` in seconds.

```python
T Statistics:  0.883, p-value: 0.377
```

📉 **Interpretation:**  
Users in the treatment group spent **less time** on the page, but again, **the difference wasn’t statistically significant**.

### 📊 Placeholder: Session Duration Barchart

**![Average Session Duration by Group (95% CI)](https://github.com/user-attachments/assets/1a50fe6a-ee7a-4d72-bcfb-877ae27f4078)**

---

## 📈 Country Level Insight

To dig deeper, We can analyze conversion rates by country and check if certain regions responded differently to the test.

### 📊 Placeholder: Bar Plot showing conversion rate by country

**![conversion rate by country](https://github.com/user-attachments/assets/89327f18-cf22-43bc-837c-dabcff1c3086)**

While visually subtle, we still didn’t find any meaningful behavioral shift.

## 📊 Placeholder: KDE Plot

**![Session Duration Distribution by Group](https://github.com/user-attachments/assets/e4e3fa55-f0c6-4c2a-8030-9cbd08dd0bfd)**

---

## 🧾 Conclusion

- **Conversion Rate:** There was **no statistically significant difference** between the two groups (_p = 0.189_).
- **Time on Page:** Users in the treatment group spent **less time**, but the difference was **not significant** (_p = 0.377_).

**🚫 In short: the new page didn’t win.**

---

## 🧠 What We Learned

- **A/B testing** is not just for checking "conversion wins" — it’s about understanding **how users behave**.
- Behavioral metrics like **time on page** can help interpret **why** a change may or may not be effective.
- Not every redesign leads to better performance. And that’s OK — it’s why we test.

---

## 💡 Final Takeaway

> “Without data, you're just another person with an opinion.” — W. Edwards Deming

A/B testing turns guesswork into strategy. Even when the result is _null_, it tells us something: maybe it’s time to try a different idea or revisit the design goals.

---

## 📂 Notebook + Dataset

You can find the full notebook and cleaned dataset in this repository.

---

## ✍️ About the Author

I'm an Electrical Engineer and a data science enthusiast passionate about turning raw data into real insight.  
Let’s connect on [LinkedIn](www.linkedin.com/in/ekikhalo-victor) or [Kaggle](https://www.kaggle.com/ehisvictor) and discuss data, analytics, and experiments!
