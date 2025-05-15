# Crowdfunding-Success-Prediction-for-Startup-Incubator

Crowdfunding has become a vital funding avenue for startups globally, allowing entrepreneurs to raise capital directly from backers via online platforms. In Turkey, a rapidly growing startup ecosystem, evidenced by a nearly 6-fold increase in investments from 2021 to 2024 ($4.7 billion) and the emergence of seven unicorns, highlights the potential of this mechanism. Turkey’s largest startup incubator supports early-stage ventures by refining business plans, connecting them with resources, and facilitating funding opportunities. However, the ecosystem faces a significant challenge: only 23.1% of crowdfunding campaigns succeed, and the national success rate of 28.7% remains below the threshold needed to reliably support startup growth.

This report presents a data-driven project to predict crowdfunding success and identify key factors contributing to the success, leveraging a dataset of 1,628 Turkish campaigns with 38 features. Through EDA, predictive modeling (including XGBoost and Decision Trees), and NLP analysis of campaign descriptions, we aim to equip the largest turkish startup incubator with actionable insights. The work addresses two key questions: Can we predict crowdfunding success rates for startups? And which factors drive success in Turkey’s ecosystem? The following sections detail our methodology, findings, and recommendations to enhance funding outcomes.

# **Business understanding** {#business-understanding}

### **Context and Motivation** {#context-and-motivation}

Turkey’s startup ecosystem is experiencing rapid growth, supported by government-led initiatives like the Turcorn 100 program and tax-incentivized technology development zones. Despite this, the incubator faces a critical hurdle: 56% of its startups struggle to secure follow-on funding after initial rounds. Traditional VC funding remains highly competitive and selective, leaving a large portion of early-stage ventures underfunded.

Crowdfunding offers a compelling alternative. It provides startups with access to early capital, customer validation, and brand visibility without ceding equity. However, only 28.7% of crowdfunding campaigns in Turkey succeed, mirroring the global success gap. For our team, Turkey’s largest incubator, closing this success gap could be a strategic and financial opportunity.

### **Crowdfunding in Turkey: A Localized Overview** {#crowdfunding-in-turkey:-a-localized-overview}

Crowdfunding in Turkey has emerged as a vital alternative financing mechanism, particularly for startups and small to medium-sized enterprises (SMEs) seeking to overcome traditional funding barriers. The process involves entrepreneurs presenting their projects on online platforms to solicit small contributions from a large number of individuals, collectively achieving their funding goals.

The Turkish crowdfunding landscape has been significantly shaped by regulatory developments. In 2017, amendments to the Capital Markets Law No. 6362 established a legal framework for equity-based crowdfunding, further detailed by the Capital Markets Board (CMB) through the Communiqué on Equity-Based Crowdfunding published in October 2019\. This regulatory environment has fostered the growth of various crowdfunding platforms across the country.

Notable platforms include Fongogo, Fonbulucu, and Burada with different focuses. These platforms serve as intermediaries, ensuring compliance with regulatory standards and providing the necessary infrastructure for campaign management. The typical crowdfunding process in Turkey encompasses the following stages:

1. Project Ideation and Planning: Entrepreneurs develop their business concepts and prepare detailed plans outlining their objectives and funding requirements.  
2. Campaign Submission and Approval: The project undergoes a review process to ensure it meets the necessary criteria and regulatory compliance by the platform.  
3. Campaign Launch: Upon approval, the campaign is launched on the platform, making it accessible to potential backers.  
4. Promotion and Engagement: Entrepreneurs actively promote their campaigns through various channels, including social media, to attract backers and maintain engagement.  
5. Fundraising Period: The campaign remains live for a predetermined duration, during which backers can contribute funds.  
6. Campaign Conclusion and Fund Allocation: If the funding goal is met, the collected funds are transferred to the entrepreneur, who will then deliver the rewards.

This structured approach, underpinned by a supportive regulatory framework and a growing number of dedicated platforms, has positioned crowdfunding as a significant enabler of entrepreneurial activity in Turkey.

![][image2]  
*A typical webpage of a crowdfunding campaign in Turkey*

### **Business Problem** {#business-problem}

Our incubator currently lacks a scalable, data-driven framework to assess and improve the crowdfunding readiness of its startups. With no clear roadmap for identifying high-potential campaigns or optimizing campaign design, promising ideas risk being lost in the noise.

---

### **Comparison and Evaluation** {#comparison-and-evaluation}

| Model | Accuracy | F1-Score (1) | ROC-AUC | PR-AUC |
| ----- | ----- | ----- | ----- | ----- |
| Decision Tree | 0.86 | 0.68 | 0.8251 | 0.5966 |
| LDA | 0.84 | 0.65 | \~0.80 | \~0.55 |
| SVM | 0.85\~ | 0.67\~ | 0.8683\~ | \~0.60 |
| **XGBoost** | **0.87** | **0.72** | **0.9153** | **0.8175** |
| Logistic Regression | 0.83\~ | 0.65 | \~0.84 | \~0.70 |

The best overall model is XGBoost, based on the highest F1, ROC-AUC, and PR-AUC scores.

#### **Key Takeaways:**

* XGBoost offers the best performance and interpretability via feature importances.  
* SVM performs competitively but is less interpretable.  
* Logistic Regression is fast, easy to implement, and a good linear benchmark.  
* Feature importance plots can drive real-world campaign strategies, e.g., choosing the right category or platform.

### **Text Processing Using NLP** {#text-processing-using-nlp}

It was explored how natural language used in project descriptions correlates with the success of crowdfunding campaigns. The goal was to extract interpretable linguistic features that provide insight into what kind of messaging resonates with backers.

#### **NLP Pipeline and Vectorization:**

To process the campaign descriptions, we employed a standard NLP pipeline:

* Text cleaning: Lowercasing, punctuation removal, and lemmatization.  
* Tokenization: Using nltk to split text into individual words.  
* Stopword removal: To discard common but uninformative words like “the”, “is”, and “and”.

The processed text was then converted into numerical features using a TF-IDF Vectorizer. TF-IDF (Term Frequency–Inverse Document Frequency) helps identify terms that are not only frequent but also discriminative across documents. It allows the model to focus on meaningful words rather than common ones.\\

