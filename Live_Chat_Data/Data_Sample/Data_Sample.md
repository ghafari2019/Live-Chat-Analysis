# Used Filters in Session ID Selection

## **1. Exclusion of Test Channels**

The following condition ensures that **test/mock channels** are excluded from the dataset:

```sql
AND LOWER(chathistory.channel) NOT IN ('e2eteam4', 'adminconsole')
```

- This filters out sessions where the **channel** is `e2eteam4` or `adminconsole`, which are used for testing purposes.

## **2. Exclusion of Mock Input Text**

The following condition removes sessions with **mock input text** used for testing:

```sql
AND LOWER(chathistory.input_text) != 'enablemock'
```

- This ensures that sessions where `input_text` is `'enablemock'` are excluded from the analysis.

## **3. Session Filtering Based on Interaction Count**

The query applies a filter to select **sessions within a specific interaction range**:

```sql
HAVING interaction_count BETWEEN 50 AND 200
```

- This ensures that only sessions with **50 to 200 interactions** are included in the analysis, focusing on **substantive interactions** while avoiding excessively short or long sessions.

## **4. Exclusion of WhatsApp Channels**

The query explicitly excludes **WhatsApp interactions** to ensure that the dataset remains clean and relevant:

```sql
AND LOWER(session_channel) != 'whatsapp'
```

- This guarantees that sessions originating from **WhatsApp** are not included in the results, reducing noise and ensuring consistent analysis.




```sql
WITH highest_interaction_sessions AS (
  SELECT 
    chathistory.session_id,
    COUNT(CASE WHEN LOWER(chathistory.source) IN ('agent', 'notify') THEN 1 END) AS interaction_count
  FROM odp_customer_service_analytics_p.standardized.cognigy_chatbot_chathistory chathistory
  WHERE LOWER(chathistory.channel) NOT IN ('e2eteam4', 'adminconsole')  -- Exclude test channels
    AND LOWER(chathistory.input_text) != 'enablemock'  -- Exclude mock input text
  GROUP BY chathistory.session_id
  HAVING interaction_count > 0 AND interaction_count BETWEEN 50 AND 200  -- Filter interactions between 50 and 200
),
filtered_sessions AS (
  SELECT DISTINCT session_id
  FROM highest_interaction_sessions
  WHERE session_id IN (
    SELECT session_id
    FROM odp_customer_service_analytics_p.trusted.cognigy_chatbot_handover_history
    WHERE LOWER(session_channel) != 'whatsapp'  -- Exclude WhatsApp sessions
  )
)
SELECT 
  his.session_id,
  his.interaction_count AS agent_interaction_count
FROM highest_interaction_sessions his
JOIN filtered_sessions fs ON his.session_id = fs.session_id
ORDER BY his.interaction_count DESC;
```








