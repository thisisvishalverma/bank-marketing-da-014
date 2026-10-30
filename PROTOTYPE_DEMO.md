# Faculty demonstration guide (3–5 minutes)

1. Start the app with `streamlit run app.py` and open the local browser link.
2. On **Overview**, point out the four KPI cards. Explain that response rate is `yes` subscriptions divided by valid target records in the current filtered set.
3. Change one sidebar filter, such as `contact` or `job`. Show the KPI values and charts updating from the filtered records. Restore the filter to all values afterward.
4. Change **Compare response rate by segment** to education or month. Use hover details to show record and response counts behind each rate.
5. Point out the contact-frequency chart and the channel/month/weekday comparisons. Mention that `campaign` counts the number of contacts during this campaign, including the last contact.
6. Open **Findings & recommendations**. Explain the minimum group-size rule (30 records), and that the results are observations used to propose controlled experiments, not causal claims.
7. Open **Data & methodology** to show cleaning notes, the target definition, the post-contact limitation for `duration`, and the UCI dataset source.
8. Expand **Preview filtered records** on Overview to demonstrate that the charts use actual rows from the data.

Suggested closing: “This prototype is an exploratory analysis. Any campaign change based on these historical associations should be tested on a comparable audience before rollout.”

