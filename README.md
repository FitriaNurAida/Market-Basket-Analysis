## Introduction<br><br>
Welcome to the **Market Basket Analysis (MBA)** module! As future business leaders and analysts, understanding customer purchasing behavior is critical. MBA, also known as **Association Rules** Mining, is a key technique in data mining that helps **discover relationships between items** in large datasets, often used in retail to determine **which products are frequently bought together**.<br><br>
This module will cover the theoretical foundations of Association Rules and provide a practical exercise using Python and a common dataset.<br><br>
## Core Concepts<br><br>
Market Basket Analysis seeks to find rules of the form $\mathbf{A \Rightarrow B}$, meaning: "If item A is bought, then item B is likely to be bought as well."The strength of these rules is measured by three key metrics: <br><br>
<img width="749" height="627" alt="image" src="https://github.com/user-attachments/assets/549dbc90-a01b-4fd4-9ca5-ee93935414ca" />
<br> <br>
#### 🛒 Transaction Data Table
| Transaction ID | Items Purchased |
| :---: | :--- |
| 1 | Milk, Bread, Diapers |
| 2 | Eggs, Milk, Diapers |
| 3 | Bread, Eggs |
| 4 | Milk, Diapers |
| 5 | Bread, Milk, Diapers |
| 6 | Eggs |
| 7 | Milk, Bread |
| 8 | Milk, Eggs, Diapers |
| 9 | Bread, Diapers |
| 10 | Bread, Milk |
| **Total:** | **10 Transactions** |

<br> <br>
### 1. Support <br>
Support is an indication of how frequently a collection of items (an itemset) appears in the total transactions. It is the probability of seeing all the items in the itemset. Think of it as the **popularity** of a product or a combination of products.
<br><br>
$$\text{Support} (A \Rightarrow B) = \frac{\text{Number of transactions containing } A \text{ and } B}{\text{Total number of transactions}}$$ <br><br>
This metric is used to identify itemsets that are common enough to be relevant and meaningful. A low minimum support threshold will yield too many trivial rules, while a high threshold might miss important, but less frequent, ones. <br>
For example : Measures the popularity of both Bread and Milk being bought together.<br><br>
$$\text{Support}(\text{Bread} \implies \text{Milk}) = \text{Support}(\text{Bread} \cup \text{Milk}) = 0.4$$<br><br>
Interpretation: 40% of all transactions contain both Bread and Milk.<br><br>
**Priority Business Case** : Store Layout/Product Placement, Inventory Management, General Product Bundling
<br><br>
### 2. Confidence<br>
Confidence measures of how often items in B appear in transactions that already contain A. It is the **conditional probability** $P(B|A)$.<br><br>
$$\text{Confidence} (A \Rightarrow B) = \frac{\text{Support} (A \cap B)}{\text{Support} (A)}$$<br><br>
This metric measures the reliability/power of the rule. "If a customer buys $A$, how likely are they to also buy $B$?".<br>
For example : Measures the probability of buying Milk given that Bread was purchased, P(Milk|Bread).<br><br>
$$\text{Confidence}(\text{Bread} \implies \text{Milk}) = \frac{\text{Support}(\text{Bread} \cup \text{Milk})}{\text{Support}(\text{Bread})} = \frac{0.4}{0.6} \approx 0.667$$<br><br>
Interpretation: If a customer buys Bread, there is a 66.7% chance they will also buy Milk.<br><br>
**Priority Business Case** : Cross-Selling, Website/App Recommendations
<br><br>
### 3. Lift<br>
Lift measures the **strength** of a rule over the random co-occurrence of A and B. It tells us how much more likely item B is to be purchased given that item A is purchased, while controlling for how popular B is overall.<br><br>
$$\text{Lift} (A \Rightarrow B) = \frac{\text{Confidence} (A \Rightarrow B)}{\text{Support} (B)} = \frac{\text{Support} (A \cap B)}{\text{Support} (A) \times \text{Support} (B)}$$<br><br>
Metrics:<br>
$\text{Lift} = 1$: The purchase of A has no effect on the purchase of B (A and B are independent).<br>
$\text{Lift} > 1$: The purchase of A increases the probability of purchasing B (positively associated). This is the desired outcome for a useful association rule.<br>
$\text{Lift} < 1$: The purchase of A decreases the probability of purchasing B (negatively associated).<br>
For example : Measures how much stronger the rule is than expected by chance.<br><br>
$$\text{Lift}(\text{Bread} \implies \text{Milk}) = \frac{\text{Confidence}(\text{Bread} \implies \text{Milk})}{\text{Support}(\text{Milk})} = \frac{0.667}{0.7} \approx 0.95$$<br><br>
Interpretation: Since the $\text{Lift} (0.95)$ is less than 1, this means that while the confidence is high, the association is slightly negative. Buying Bread actually makes it slightly less likely the customer will buy Milk, compared to the overall popularity of Milk. In simple terms, Milk is popular (70%) that the rule isn't adding much predictive value.
<br><br>
**Priority Business Case** : Promotional Strategy
<br><br>

## What is Apriori Algorithm?
The Apriori Algorithm is a classic and foundational algorithm used for Market Basket Analysis to discover frequent itemsets and derive association rules. It operates based on the key principle that any subset of a frequent itemset must also be frequent. This property significantly reduces the search space, making the algorithm efficient for large datasets.<br><br>
<img width="800" height="535" alt="image" src="https://github.com/user-attachments/assets/e364d269-61f5-402d-854c-c551ef3f3f14" />
