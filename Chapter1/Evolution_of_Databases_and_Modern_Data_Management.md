**1.1 Evolution of Data Storage Systems**

- Data storage technology has evolved continuously to meet growing requirements for data capacity, processing speed, structural flexibility, and availability.
- ```
  Paper / Manual Files (Pre-1960s)
          │
          ▼
  Flat File Systems (1960s)
            │
            ▼
  Hierarchical & Network Data Models (1960s–1970s)
            │
            ▼
  Relational Database Management Systems - RDBMS (1970s–1990s)
            │
            ▼
  Object-Oriented & Object-Relational Databases (1990s)
            │
            ▼
  NoSQL & Big Data Frameworks (2000s)
            │
            ▼
  Distributed, Cloud & NewSQL Databases (2010s–Present)
  ```
- Era 1: Manual Systems & Paper Files (Pre-1960s)
  - Before electronic computing, data was recorded physically in ledgers, folders, and filing cabinets.
  - Key Characteristics: Physical paper-based indexing and storage.
  - Limitations:
  - High physical space requirements.
  - Slow data retrieval and manual searching.
  - Susceptible to physical damage, loss, or human filing error.

- Era 2: Flat File Systems (1960s)
  - With early electronic computers, data was stored in simple, flat text or binary files directly on magnetic tapes and early hard disks.
  - Key Characteristics: Basic OS-level file management (.txt, .csv style structures) managed by custom application programs.
  - Limitations:
  - Data Redundancy & Inconsistency: The same data was repeated across multiple files, leading to sync issues.
  - Data Dependence: Application code was tightly coupled with the physical data format.
  - Lack of Concurrent Access: Multiple users could not read/write simultaneously without file corruption risks.
  - Poor Security & Integrity: No built-in role access control or validation rules.

- Era 3: Hierarchical and Network Database Models (1960s–1970s)
  - To overcome flat-file limitations, early structured database management systems were created.
  - Hierarchical Model (e.g., IBM IMS):
  - Organizes data in a tree structure (parent-child relationship).
  - Limitation: Each child can have only one parent. Complex many-to-many relationships were difficult to represent.
  - Network Model (e.g., CODASYL, IDS):
  - Organizes data as a graph structure.
  - Limitation: Allowed a child record to have multiple parents (many-to-many relationships).
  - However, navigation required low-level physical pointers, making query code complex to write and maintain.

 - Era 4: Relational Database Management Systems - RDBMS (1970s–1990s)
  - Introduced by Edgar F. Codd in 1970, the relational model revolutionized data management.
  - Core Concept: Data is organized into 2D tables (called relations) consisting of rows (tuples) and columns (attributes).
  - Key Innovations:
  - SQL (Structured Query Language): Declarative language for querying and defining data.
  - ACID Properties: Guarantees Atomicity, Consistency, Isolation, and Durability for transactional applications.
  - Normalization: Rules to remove data redundancy and ensure data integrity.
  - Examples: Oracle, MySQL, PostgreSQL, IBM DB2, Microsoft SQL Server.

- Era 5: Object-Oriented & Object-Relational Databases (1990s)
  - As Object-Oriented Programming (OOP) languages (Java, C++) gained popularity,
  - a gap emerged between object-oriented code and tabular SQL databases (known as the Object-Relational Impedance Mismatch).
  - Object-Oriented DBMS (OODBMS): Stored complex objects directly with methods, inheritance, and encapsulation (e.g., ObjectStore).
  - Object-Relational DBMS (ORDBMS): Hybrid systems extending traditional RDBMS to support user-defined types and complex objects (e.g., PostgreSQL).

- Era 6: NoSQL and Big Data Systems (2000s)
  - The rise of the World Wide Web, social media, e-commerce, and mobile devices produced massive volumes of structured,
  - semi-structured, and unstructured data. Traditional RDBMS struggled to scale horizontally across commodity hardware.
  - Key Characteristics:
  - Schema-flexible or schema-less storage. 
  - Designed for Horizontal Scaling (Scaling Out) across distributed clusters.
  - Trade-off: Priority given to high availability and partition tolerance over strict ACID guarantees (BASE model).
  - Key Paradigms: Document Stores, Key-Value Stores, Column-Family Stores, Graph Databases.
  - Examples: MongoDB, Apache Cassandra, Redis, Neo4j, Apache Hadoop / HDFS.
 
- Era 7: Cloud, Distributed SQL & Modern Engines (2010s–Present)
  - Modern enterprise architecture relies on globally distributed, auto-scaling cloud databases.
  - Cloud-Native Databases & DBaaS: Managed platforms offering auto-scaling, replication, and zero-maintenance overhead
  - (e.g., Amazon Aurora, Snowflake, Google Cloud BigQuery).
  - NewSQL / Distributed SQL: Systems designed to provide the horizontal scalability of NoSQL alongside the ACID guarantees and
  - SQL compatibility of traditional RDBMS (e.g., Google Cloud Spanner, CockroachDB).


**1.2 Limitations of Traditional RDBMS in Big Data and Cloud Environments**

1. Vertical Scaling (Scale-Up) Bottleneck
  - Monolithic Architecture: Traditional RDBMS systems (like MySQL or Oracle) are primarily designed to run on a single machine.
  - Resource Ceiling: To handle larger workloads, you must scale vertically by adding more CPU, RAM, or SSDs to a single server.
  - This rapidly hits a hard hardware ceiling and becomes exponentially expensive.
  - Lack of Seamless Horizontal Scaling: Scaling horizontally (scale-out across multiple commodity nodes) is extremely difficult in relational databases
  - because join operations and ACID transactions across network-distributed nodes incur heavy latency.

2. Rigid Schema Requirements
  - Schema-on-Write: RDBMS requires predefined schemas (tables, column types, constraints) before inserting data.
  - Inflexibility with Unstructured Data: Big Data consists largely of semi-structured and
  - unstructured data (JSON documents, logs, social media posts, sensor streams, media files).
  - Enforcing a rigid tabular schema on rapidly changing or unpredictable data leads to continuous, costly schema migrations and downtime.

3. ACID Properties vs. High Availability (CAP Theorem Constraints)
  - Strict ACID Compliance: RDBMS prioritizes Atomicity, Consistency, Isolation, and Durability.
  - The CAP Theorem Trade-off: The CAP theorem states that a distributed system can simultaneously guarantee only two of three properties:
  - Consistency, Availability, and Partition Tolerance.
  - Availability Degradation: RDBMS architectures favor strong consistency.
  - In a cloud/distributed setting where network partitions (P) occur,
  - maintaining strict consistency forces the system to sacrifice availability (A),
  - leading to potential system downtime or timeouts.
  - 1. ACID Properties (ॲसिड प्रॉपर्टीज)

    - ACID ही अशी तत्त्वे आहेत जी RDBMS मध्ये प्रत्येक Transaction (व्यवहार) सुरक्षित आणि अचूक राहावा यासाठी वापरली जातात.
    - Atomicity (ऑटोमिसीटी - All or Nothing): व्यवहार एकतर पूर्णपणे यशस्वी होतो किंवा अजिबात होत नाही.
    - उदाहरण: बँक ट्रान्सफर करताना तुमच्या खात्यातून पैसे कट झाले पण समोरच्याला मिळाले नाहीत, तर सिस्टीम पूर्ण व्यवहार रद्द (Rollback) करते.
    - Consistency (कन्सिस्टन्सी - डेटाची अचूकता): व्यवहाराच्या आधी आणि नंतर डेटाबेसचे सर्व नियम लागू राहतात. डेटा कधीही चुकीच्या किंवा अपूर्ण स्थितीत राहत नाही.
    - Isolation (आयसोलेशन - अलिप्तता): एकाच वेळी अनेक व्यवहार चालू असतील, तर ते एकमेकांमध्ये अडथळा आणत नाहीत. प्रत्येक व्यवहार स्वतंत्रपणे पूर्ण होतो.
    - Durability (ड्युरेबिलिटी - टिकाऊपणा): एकदा व्यवहार यशस्वी (Commit) झाला की लाईट गेली किंवा सर्व्हर क्रॅश झाला तरी तो डेटा कायमस्वरूपी सुरक्षित राहतो.
      
  - 2. CAP Theorem (कॅप थिअरी)

    - कोणत्याही Distributed System मध्ये (जिथे डेटा एकापेक्षा जास्त कॉम्प्युटर्सवर पसरलेला असतो) खालील ३ पैकी फक्त २च गोष्टी एका वेळी पूर्णपणे मिळवता येतात:
    - C - Consistency (कन्सिस्टन्सी): सर्व कॉम्प्युटर्सवर एकाच वेळी अगदी नवीन आणि एकसारखाच डेटा दिसणे.
    - A - Availability (अव्हेलेबिलिटी): सिस्टीम कधीही बंद न पडणे; प्रत्येक रिक्वेस्टला नेहमी प्रतिसाद (Response) मिळणे.
    - P - Partition Tolerance (पार्टिशन टॉलरन्स): कॉम्प्युटर्समधील नेटवर्क वायर तुटली किंवा संपर्क तुटला तरी सिस्टीम चालू राहणे.

  - 3. Availability Degradation (लास्ट पॉईंटचे सोप्या भाषेत स्पष्टीकरण)हा मुद्दा RDBMS मधील Consistency ($C$) आणि Availability ($A$) मधील संघर्ष समजून सांगतो.
    - मुख्य अडचण: RDBMS (उदा. MySQL, Oracle) हे Strict Consistency ($C$) वर काम करतात.
    - त्यांना डेटा चुकीचा दाखवलेला अजिबात चालत नाही.नेटवर्क तुटल्यास काय होते? समजा, क्लाउडवर २ सर्व्हर्स आहेत (Server X आणि Server Y).
    - त्यांच्यातील नेटवर्क केबल तुटली (Network Partition - $P$).
    - RDBMS चा निर्णय: अशा वेळी जर एखाद्या युजरने Server X वर नवीन डेटा अपडेट केला, तर तो Server Y पर्यंत पोहोचू शकत नाही.
    - परिणाम (Availability Degradation): RDBMS विचार करतो — "मी युजरला जुना किंवा चुकीचा डेटा दाखवण्यापेक्षा सिस्टीम बंद ठेवेन किंवा एरर दाखवेन."
    - यामुळे सिस्टीम Consistency साध्य करण्यासाठी Availability चा त्याग करते (Sacrifice Availability).
    - सोपे उदाहरण: ATM नेटवर्क डाऊन असताना बँक तुम्हाला पैसे काढू देत नाही (Availability थांबवते), कारण तुमच्या खात्यातील शिल्लक चुकीची अपडेट होऊ नये (Consistency महत्त्वाची असते).
      
 4. High Latency on Complex Joins at Scale
  - Expensive Join Operations: RDBMS relies on relational algebra and normalized structures to eliminate redundancy.
  - Performance Drop: Joining multiple massive tables (spanning terabytes or petabytes) across distributed networks requires significant cross-node data shuffling,
  - degrading query performance and causing high latency.
     - १. Normalization आणि Joins चे महत्त्व (Relational Algebra)
     - डेटाचे तुकडे करणे: RDBMS मध्ये डेटाची पुनरावृत्ती (Redundancy) टाळण्यासाठी डेटा Normalized केला जातो,
     - म्हणजेच वेगवेगळ्या टेबल्समध्ये विभागला जातो (उदा. Users टेबल वेगळे, Orders टेबल वेगळे, Payments टेबल वेगळे).
     - JOIN ची गरज: जेव्हा आपल्याला संपूर्ण माहिती हवी असते (उदा. कोणत्या युजरने काय खरेदी केले?), तेव्हा या सर्व टेबल्सवर JOIN ऑपरेशन चालवावे लागते.
     - २. Distributed Architecture मध्ये काय घडते? (Data Shuffling)
     - वेगवेगळ्या कॉम्प्युटर्सवर डेटा: Big Data किंवा Cloud मध्ये डेटा इतका मोठा असतो (Terabytes/Petabytes) की तो एकाच कॉम्प्युटरवर बसत नाही. तो शेकडो सर्व्हर्समध्ये (Nodes) विभागून साठवला जातो.
     - Network Data Shuffling: समजा, Users चा डेटा Node A वर आहे आणि Orders चा डेटा Node B वर आहे.
     - जेव्हा आपण JOIN क्वेरी रन करतो, तेव्हा Node A आणि Node B ला नेटवर्कवरून एकमेकांना डेटा पाठवावा लागतो. यालाच Data Shuffling म्हणतात.
     - ३. Performance Drop आणि High Latency (मंद गती)
     - नेटवर्कचा अडथळा: RAM किंवा Hard Disk मधून डेटा वाचण्यापेक्षा नेटवर्कवरून (Cable/Wi-Fi) डेटा एका सर्व्हरकडून दुसऱ्या सर्व्हरकडे ट्रान्सफर होण्यासाठी खूप जास्त वेळ लागतो.
     - परिणाम: जेव्हा डेटा पेटाबाईट्समध्ये (PB) असतो आणि नेटवर्कवर लाखो रेकॉर्ड्सची देवाणघेवाण सुरू होते, तेव्हा:
     - क्वेरीचा रिस्पॉन्स मिळायला सेकंदांऐवजी मिनिटे किंवा तास लागतात (High Latency).
     - संपूर्ण सिस्टीमचा स्पीड अत्यंत मद होतो (Performance Drop).
     - सोपे वास्तववादी उदाहरण (Real-World Analogy)
     - RDBMS प्रकार: तुमच्याकडे एकाच खोलीत ३ फायली (Tables) ठेवल्या आहेत. तुम्हाला माहिती गोळा करायला ५ सेकंद लागतात.
     - Big Data (Distributed Joins) प्रकार: १ फाइल पुण्यात आहे, २ री मुंबईत आहे आणि ३ री नागपूरला आहे.
     - JOIN करून उत्तर बनवण्यासाठी तिन्ही शहरांतून माणसे प्रवास करून एका जागी भेटतील आणि डेटा गोळा करतील. या प्रवासात जाणारा वेळ म्हणजेच High Latency!

     -  ```
        Normalization (नॉर्मलायझेशन) म्हणजे काय?
        Normalization ही डेटाबेस डिझाइन करण्याची अशी एक पद्धत (Technique) आहे, ज्याद्वारे टेबल्समधील Data Redundancy (डेटाची अनावश्यक पुनरावृत्ती) कमी केली जाते आणि Data Integrity (डेटाची अचूकता) टिकवून ठेवली जाते.
        सोप्या भाषेत सांगायचे तर: एकाच मोठ्या आणि विस्कळीत टेबलचे छोटे-छोटे, अर्थपूर्ण टेबल्स बनवणे आणि त्यांना Primary Key - Foreign Key ने जोडणे म्हणजेच Normalization.
        - Normalization का केले जाते? (Problems Avoided)
        - जर एकाच टेबलमध्ये सर्व डेटा भरला, तर ३ मुख्य अडचणी (Anomalies) येतात:
        - Insertion Anomaly: नवीन माहिती भरायची असल्यास नको असलेली माहितीही सक्तीने भरावी लागते.
        - Deletion Anomaly: एक रेकॉर्ड डिलीट केला की त्यासोबत दुसरी महत्त्वाची माहितीही आपोआप डिलीट होते.
        - Update Anomaly: एकच नाव किंवा पत्ता अनेक ठिकाणी असेल, तर तो अपडेट करताना सर्व ठिकाणी बदलावा लागतो. एका जागी बदलायचा राहिला तर डेटा चुकीचा होतो.
        
        - Normalization कसे काम करते? (Steps / Normal Forms)
        - डेटा नॉर्मलाइज करण्यासाठी त्याला टप्प्याटप्प्याने नियम लावले जातात, ज्यांना Normal Forms (NF) म्हणतात.
        
        - 1. First Normal Form (1NF) – Atomic Values (तुकडे करणे)
        - नियम: टेबलच्या कोणत्याही कॉलममध्ये एकापेक्षा जास्त व्हॅल्यूज (Multiple Values / Sets) नसाव्यात. प्रत्येक सेलमध्ये फक्त एकच (Atomic) व्हॅल्यू असावी.
        - कसे काम करते? कॉमा (,) देऊन लिहिलेले फोन नंबर किंवा सब्जेक्ट्स वेगळ्या रो (Rows) मध्ये किंवा वेगळ्या टेबलमध्ये विभागले जातात.
        - 2. Second Normal Form (2NF) – Remove Partial Dependency
        - नियम: टेबल आधी 1NF मध्ये असावे, आणि नॉन-प्रायमरी की (Non-Key) कॉलम्स हे पूर्ण Primary Key वर अवलंबून असावेत (Partial Dependency नसावी).
        - कसे काम करते? जर एखादा कॉलम Primary Key च्या फक्त अर्ध्या भागावर अवलंबून असेल, तर तो कॉलम कापून एक नवीन टेबल बनवले जाते.
        - 3. Third Normal Form (3NF) – Remove Transitive Dependency
        - नियम: टेबल आधी 2NF मध्ये असावे, आणि नॉन-प्रायमरी की कॉलम हा दुसऱ्या नॉन-प्रायमरी की कॉलमवर अवलंबून नसावा (A -> B आणि B -> C असेल तर A -> C ही थेट अवलंबून राहणे काढून टाकणे).
        ```
 5. Cost and Deployment Complexity in Cloud Infrastructure
    - Licensing & Infrastructure Costs: Enterprise RDBMS systems often carry high licensing costs and
    - require expensive high-end storage infrastructure (SAN/NAS).
    - Cloud Elasticity Challenges: Cloud-native applications require dynamic, rapid auto-scaling (scaling up and down on demand).
    - Traditional RDBMS instances cannot easily partition, replicate, and re-balance data dynamically without manual intervention and downtime.      

------------------
```
  1.3 Structured vs Semi-Structured vs Unstructured Data
  In modern data management, data is broadly classified into three categories based on its organizational structure and format.
  
  1. Structured Data
  Definition: Data that conforms to a fixed, predefined schema (Schema-on-Write).
  
  Format: Organized strictly in two-dimensional tables consisting of rows and columns.
  
  Querying & Access: Highly organized and easily queried using standard Structured Query Language (SQL).
  
  Storage Systems: Relational Database Management Systems (RDBMS) like MySQL, PostgreSQL, Oracle, and MS SQL Server.
  
  Examples: Bank transaction logs, student marksheets, inventory catalogs, CSV files, and Excel spreadsheets.
  
  2. Semi-Structured Data
  Definition: Data that does not follow a rigid table structure but contains tags, markers, or key-value pairs (self-describing structure).
  
  Format: Hierarchical or graph-based data formats that allow field flexibility per record.
  
  Querying & Access: Processed using dedicated parsers, execution engines, or NoSQL query languages.
  
  Storage Systems: Document Databases (MongoDB), Key-Value Stores (Redis), and Native XML Databases.
  
  Examples: JSON documents, XML files, YAML files, and system log files.
  
  3. Unstructured Data
  Definition: Data that completely lacks a predefined data model, schema, or structural framework.
  
  Format: Qualitative media files, documents, and continuous binary streams; accounts for 80% to 90% of all enterprise Big Data.
  
  Querying & Access: Cannot be queried using SQL; requires advanced analytics, Machine Learning (ML), Natural Language Processing (NLP), and search indexing engine pipelines.
  
  Storage Systems: Data Lakes, Cloud Object Storage (Amazon S3, Azure Blob Storage), and Distributed File Systems (HDFS).
  
  Examples: MP4 video files, JPEG/PNG images, PDF documents, social media feeds, audio files, and email bodies.
```
----------
 
