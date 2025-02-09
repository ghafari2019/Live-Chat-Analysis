## SQL Query Analysis of Chatbot Interaction History

### Overview
This section details an SQL query executed in a Spark job environment to analyze chatbot interaction history. The query retrieves and summarizes interaction counts grouped by communication channel.

### SQL Query Explanation
- The query extracts data from the `cognigy_chatbot_chathistory` table within the `odp_customer_service_analytics_n.standardized` database.
- It counts the number of interactions per **channel** (e.g., web chat, voice gateway) and orders the results in descending order based on interaction count.

### Columns in the Query Result
- **Channel**: Represents the communication platform used for chatbot interactions (e.g., `e2team4`, `webchat2`, `rest`).
- **Count**: Shows the number of chatbot interactions per channel.

### Insights from Query Results
- The results help identify which channels are most frequently used for chatbot interactions.
- The table is sorted by interaction count, showing `e2team4` as the most used channel with **1,094,049** interactions and `webchat3` as the least used with **9,088** interactions.
- These insights can help evaluate the effectiveness and popularity of different communication channels for customer engagement.
