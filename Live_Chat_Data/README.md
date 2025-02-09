## SQL Query Analysis of Chatbot Interaction History

### Overview
This section details an SQL query executed in a Spark job environment to analyze chatbot interaction history. The query retrieves and summarizes interaction counts grouped by communication channel.

![Description of Image](Images/pic1.png)

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

## SQL Query Analysis of Agent Interactions

### Overview
This section describes an SQL query that retrieves the count of **agent interactions** by communication channel from the `cognigy_chatbot_chathistory` table. The query filters the data to include only interactions where the **source** is labeled as `'agent'`. The results are grouped by **channel** and ordered by **agent interaction count** in descending order.


![Description of Image](Images/pic2.png)

### Key Insights from the Query Results
- **Channel**: Displays the names of channels where agent interactions took place (e.g., `webchat2`, `whatsapp`, `webchat3`).
- **Agent Interaction Count**: Shows the total number of interactions that involved an agent for each channel.
  - `webchat2` has the highest number of agent interactions with **5,937** interactions.
  - `whatsapp` follows with **290** agent interactions.
  - `webchat3` has significantly fewer agent interactions, with only **15** interactions.

### Interpretation
This dataset provides insights into which channels are most frequently used for **agent interactions**. 
- `webchat2` stands out as the primary channel for agent involvement.
- Other channels, such as `whatsapp` and `webchat3`, have **relatively fewer** interactions requiring human intervention.
- Understanding these trends can be valuable in **evaluating channel effectiveness** and determining where human support is most needed in chatbot interactions.







we 
