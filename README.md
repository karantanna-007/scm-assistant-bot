# SCM Assistant Bot — Trinamix Hiring Task TX-JrAI-003
 

## Stack Used
- **Platform**: Flowise Cloud (flowiseai.com)
- **LLM**: Groq API — llama-3.3-70b-versatile (free)
- **Embeddings**: HuggingFace Inference — sentence-transformers/all-MiniLM-L6-v2
- **Vector Store**: Qdrant Cloud — policy_knowledge collection (384 dimensions, cosine)
- **CSV Analysis**: Flowise CSV Agent (Pandas-based)
- **Architecture**: Agent with two workers (policy_retriever + supplier_data_analyst)
 
## Chunk Configurations Tried
 
### Configuration 1 (Final)
- Chunk Size: 1000 | Overlap: 200 | Result: ~19 chunks | 15,018 characters
 
### Configuration 2 (Experiment)
- Chunk Size: 700 | Overlap: 100 | Result: ~25 chunks | 15,018 characters
 
Config 1 was chosen for the final build because larger chunks retain more
policy context per retrieval, reducing the chance of a rule being split mid-sentence.
 
## Q&A Results
 
**Q1:** Which Tier-3 suppliers have an active disruption flag, and what response level applies?
**A1:** The 24 Tier-3 suppliers with active disruptions are: Archipelago PCB Corp, Bogota Pack Ltda, Bohai Electronics, Buenos Aires Pack, Cerromax Mineria, DaNang Metal Works, Deccan Polymer Mfg, Deltaforge Vietnam, Dravex Components India, Helios Pack Greece, Lima Polymer SA, Longhua Polymer Works, Maghreb Castworks, MeKong Pack Co, Orinoco Pack SAPI, Patagonia Alloys SRL, Plataforma Metales SA, Quetzal Textiles, Sahyadri Alloy Tech, Sibertek Molding, Varna Electronics EAD, Visayas Textile Co, Vistula Pack Sp, Yucatan Polymer Mfg. All are High Risk. According to the policy (Section 9), these suppliers require a Level 3 response, which includes immediate escalation to the CPO, activation of an alternate supplier for at least 40% of the volume within 10 business days, and a full root-cause analysis (RCA) within 15 business days.
 
**Q2:** Which suppliers qualify for the annual Volume Rebate Program and how many are there?
**A2:** There are 25 suppliers that qualify for the annual Volume Rebate Program. These suppliers meet the criteria of having an On-Time Delivery (OTD) rate of 93% or higher, a Defect Rate below 0.5%, and a Sustainability Score of 85 or higher. The list of qualifying suppliers includes Berliner Pack GmbH, BlueMesa Polymers, Borealis Composites, and others. The Volume Rebate Program is outlined in Section 4.2 of the supply chain governance policy, which states that Tier-1 suppliers who meet the eligibility criteria will receive an annual volume rebate of 2.5% of their total annual invoice value.
 
**Q3:** Which region has the highest total PO value, and does it breach the concentration limit?
**A3:** The region with the highest total PO value is APAC, with a total spend of $131,620,356.14, which accounts for 37.0% of the total PO spend. This does not breach the concentration limit of 45% as per Policy §5.3.
 
**Q4:** Which suppliers are on Supplier Watch List (SWL) status and what does it restrict?
**A4:** There are 24 suppliers on the Supplier Watch List (SWL) status, with Compliance Scores below 60. These suppliers are restricted to 20% of their prior quarter volume for new POs, as per Policy §3.4. The suppliers on the SWL include Archipelago PCB Corp, Bogota Pack Ltda, Bohai Electronics, and others.
 
**Q5:** Which product category has the highest average defect rate and does it exceed Tier-2 limit?
**A5:** The product category with the highest average defect rate is Packaging Materials, with an average defect rate of 1.909%. This is below the Tier-2 limit of 2.50% as per Policy §3.2.
 
## What I Would Improve
- Replace CSV Agent with a FastAPI microservice for deterministic, 100% accurate filtering
- Add metadata filtering in Qdrant to retrieve by policy section number
- Add a Redis Record Manager to prevent duplicate embeddings on re-upsert
- Upgrade embeddings to BAAI/bge-base-en-v1.5 for better semantic precision
- Add evaluation dataset with RAGAS framework to measure retrieval quality
