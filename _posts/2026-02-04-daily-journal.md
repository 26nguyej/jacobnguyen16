---
title: "Capstone"
date: 2026-02-04
categories:
  - Journal
tags:
  - Yearbook Project
  - Data Extraction
  - YAML
  - Claude
  - GitHub
---
# Description
For my capstone project, I worked on helping design an automated data extraction and analysis tool that collects and organizes information from past Charlotte Latin yearbooks and converts it into a digital database. The goal of the project is to reduce the amount of manual work required to search through decades of yearbooks while also preserving this information in a format that can be easily accessed in the future.

I joined the class during the second semester, so Mr. Dubick and Max had already started developing the project before I became involved. Because of this, I first had to learn how their existing system and workflow functioned so I could contribute to improving and expanding the tool.

I chose this project because it allowed me to apply the coding concepts I have been learning to a real-world problem while helping create something useful for the Charlotte Latin community.

A successful version of this project would be able to automatically extract relevant data from past yearbook PDFs, clean and standardize the information, and output it in a structured format that can be easily analyzed. The system should reduce the amount of manual work required by organizing large amounts of data quickly and accurately.

Another important goal is creating a searchable AI database that stores the extracted information. Ultimately, success for this project means developing a tool that saves time, improves accuracy, and can continue to be used in future years as more yearbook data is added to the digital database.

# Extraction Workflow
## Yearbook Data Extraction Workflow

### Step 1 — Page Classification
The system first scans every page of a yearbook PDF and labels its content (for example: grade rosters, sports teams, faculty pages, etc.).  
This creates a structured map of the entire yearbook so the system knows where different types of information are located.

**Output:**  
`page_classifications.json`

A quick manual check is performed to ensure the page types were classified correctly before continuing.

#### Example of Page Classification File
<img width="642" height="295" alt="pageclassificationscreenshot" src="https://github.com/user-attachments/assets/d8e7405e-62e0-4489-a63e-5531edaa2966" />

---

### Step 2 — YAML Configuration Generation
The page classification file is converted into a structured configuration file that defines how the extraction pipeline should process the yearbook.

This configuration includes:
- Page ranges for each section
- Expected record counts
- Extraction rules for each page type

**Output:**  
`parallel.yml`

#### Example of .yml contents:
<img width="602" height="484" alt="Screenshot 2026-03-07 at 8 35 20 PM" src="https://github.com/user-attachments/assets/db157898-3cd5-4a2a-a90f-a81f6b329bb9" />


---

### Step 3 — Automated Data Extraction
The orchestrator runs the main extraction pipeline and automatically performs several processes:

- **Data Extraction** – pulls names and structured information from the yearbook pages  
- **Name Parsing** – separates names into first, middle, and last names  
- **Confidence Scoring** – assigns a reliability score to each parsed name  
- **Automation Checks** – creates a cleaned dataset ready for matching

**Outputs:**
- Raw extracted records  
- Parsed names with confidence scores  
- Cleaned dataset ready for identity matching

---

### Step 4 — Name Review (Optional Human Review)
If any names are flagged with low confidence, they are manually reviewed using a lightweight editing interface.

This step ensures that unusual name formats or parsing errors are corrected before continuing.

#### Simple Yearbook Editor html:
<img width="1273" height="765" alt="simpleeditorscreenshot" src="https://github.com/user-attachments/assets/00e69ca7-b73d-456b-b379-688efa8e61d1" />

---

### Step 5 — Matching Pipeline
The system attempts to match names from sports teams, clubs, and activities back to their corresponding student or faculty record.

The matching pipeline uses multiple strategies, including:

- Nickname matching  
- Middle name matching  
- Fuzzy last-name matching  
- Grade-level matching  
- Faculty matching

**Outputs:**
- Enriched records with activity participation
- A list of unmatched names that require review

---

### Step 6 — Matching Corrections (Human Review)
Any unmatched records are reviewed manually to identify the correct person in the dataset.

Common corrections include:
- Abbreviated names
- Alternate spellings
- Teachers appearing in activity sections

The corrections are saved for automatic integration into the dataset.

#### Match Review Editor html:
<img width="1273" height="765" alt="simpleeditorscreenshot" src="https://github.com/user-attachments/assets/37300e1d-8346-4ae4-953c-e2dcadce6090" />

---

### Step 7 — Apply Corrections
Manual corrections are merged into the dataset, producing a finalized set of structured person records for that yearbook.

**Output:**  
`PersonRecords_Final.json`

---

### Step 8 — Schema Transformation
The finalized records are converted into a standardized archival schema used for long-term storage and analysis.

Examples of structured data created in this step include:

- Sports participation
- Club membership
- Leadership roles
- Faculty coaching roles
- Board or trustee positions

**Output:**  
`Target_Schema.json`

#### Target Schema Example:
<img width="398" height="539" alt="targetSchemaScreenshot" src="https://github.com/user-attachments/assets/4e74e75c-5613-437f-8b38-ce2273d893fe" />

---

### Step 9 — Cross-Year Identity Resolution
The final step links individuals across multiple yearbooks to create persistent identities.

This allows the system to recognize when the same person appears in different years (for example as a student, athlete, or later as faculty).

The result is a unified dataset with stable person identifiers that can power a searchable historical database.

# Tools 
## Software Tools
- **Python** – Primary programming language used to build the data extraction, processing, and automation scripts.

- **VS Code** – Development environment used for writing, testing, and debugging the code.

- **GitHub** – Version control platform used to manage project files, track changes, and support collaboration.

- **Claude AI** – AI tool used to assist with parsing, analyzing, and structuring extracted data during parts of the workflow.

# Challenges
One of the main challenges that I faced early on was getting the hang of the complex and intricate pipeline processes involved with the extraction. It was especially difficult to understand the actions of the Python scripts and certain terminal actions when using Claude Code, and I had to repeatedly ask Claude to explain to me what it was doing. Moreover, in the early stages of the process, before we made improvements, Gemini's extraction of the page numbers and name counts was inaccurate or skewed, which I had to remedy by manually going through the pdf and visually checking each metadata point. A challenge that went on throughout the process is that even though we got 90-96% accuracy on the extractions, those few data points and names would be either extracted incorrectly or the spellings were inconsistent throughout parts of the yearbook. This made it difficult to match certain students in the person records with sports and activities in the matching pipeline. Moreover, there is no fix for the case where certain coaches who were not a part of the official school faculty are not in the personnel records. 

# Daily Journal

### March 6, 2026
Today I presented the extraction pipeline to my classmates, detailing each step and answering questions when asked.

### March 5, 2026
Today I listened to my classmates presentations, evaluating them on numerous categories and waited for my turn to present.

### March 4, 2026
Started the CLS1993 yearbook extraction pipeline. Downloaded the final PDF (297 pages, with printed pages 11 and 13 missing), copied it into the project, and ran CP1 (page classification), which
  completed with no LOW confidence pages — 280 HIGH, 17 MEDIUM across all 297 pages. The YAML config was auto-generated and reviewed: fixed the teacher prefix (TCH → TEA), added the late arrivals page (PDF p.287) 
  to the upper school section so those students aren't missed, and skipped an informal friend group photo (PDF p.283) that isn't a real club. Also clarified that the missing pages don't affect the pipeline since
  it works on PDF page positions, not printed numbers. The orchestrator extraction (CP3) is queued for the next session.
  
### March 3, 2026
Today we merged main into my branch to make sure I had all the latest pipeline scripts and data, then knocked out Steps 7 and 8 for CLS1978 and CLS1979. For 1978 I only had 2 real corrections (Beth Godwin and   
  Eddie Cooke), and for 1979 I found 26 corrections across 17 names — mostly initials, nicknames, and spelling variants like Buck Bryant, E. Fox, and D. Van Pelt. We also fixed 4 issues in the CLS1991 YAML config
  after comparing it against the actual PDF — moved page 98 to Middle School, page 109 to Upper School, added Grade 4 to the grade breakdown, and corrected the teacher prefix from TCH to TEA. 1991 is now ready to 
  run. I also started a quick fuzzy match pass on CLS1985 but ran out of time before finishing it. Everything got committed and pushed to Jacob_Branch. When I got home, I also had some time to put in extra work and complete the 1991 and 1992 yearbook extractions all through schema transformation. 

### February 27, 2026
Today, I updated the ReadMe file for my branch first, making sure the next scripts were added into the process. Then, I looked over the 1991 pdf to make sure the page numbers line up, and created the yaml in the background with Claude, while continuing the 1990 extraction I started the other day. I ran into an issue with missing name extractions in the 1990 extraction from last time, and Claude resolved the error, which had to do with grade division in the yearbook file. Then, I completed the 1990 extraction with manual review and matching with activities all up until before making the target schema. I plan to begin the 1991 extraction next time after manually reviewing the yaml file I created and beginning the orchestrator.

### February 26, 2026
Today I worked on digitizing the 1990 Charlotte Latin School yearbook as part of an ongoing 
  data extraction pipeline. Before running the automated extraction, I reviewed the           
  auto-generated YAML configuration file to verify page numbers, section mappings, and data
  classifications. During the review, I identified an autograph page that had been
  misclassified as a student roster and removed it from the config. I then ran the extraction
  pipeline, which processes the yearbook PDF using AI to extract student, faculty, sports, and
   activity records. When the pipeline returned unexpectedly low counts for middle and upper
  school students, I diagnosed the root cause — incomplete grade breakdown entries in the
  config were causing the extractor to skip most pages — and fixed the YAML so the full
  extraction can complete in the next session.

### February 24, 2026
Got the 1990 yearbook set up today — the old PDF had skewed page numbers, so I prepped a clean
  version and got it into the pipeline. ran the automated page classifier on all 272 pages (took
   about 16 min), which scanned every page with AI vision to figure out what's on each one —
  class rosters, sports teams, clubs, faculty, etc., from which it auto-generated the YAML config
  that drives the whole extraction pipeline. ended up with 33 sports teams, 11 activity clubs,
  and all the student/faculty sections mapped out. The next step is reviewing the YAML and then
  running the orchestrator to actually extract all the records.

### February 23, 2026
Today, I caught up with Mr. Dubick about the work he had completed over the weekend, catching myself up to speed on new scripts and updates he had made to the extraction protocol. I learned that he implemented universal IDs for each student to eventually be able to reference across multiple years' yearbooks in a chatbot. After going over the updates and pulling them from the main branch, I investigated an error in the 1990 yearbook formatting on the pdf and found out that 2 pages were missing, the title page was not counted as a page, and that there was a small half page section numbering 1-16 that all skewed the page numbers in relation to the pdf page numbers. I worked on editing this pdf for use and also reading over what Claude summarized for the new updates to the workflow.

### February 20, 2026
Today I finished the full extraction pipeline for the 1983 Charlotte Latin School yearbook. I used the match review   
  editor to manually resolve unmatched names from the sports and activities sections, then applied the corrections and
  generated the final output — 1,125 person records with sports and club memberships fully linked. I also caught and    
  fixed a bug in the transform script along the way. At the end of the day, I synced my branch with my Mr. Dubick's latest 
  updates, which included faster parallel processing, smarter name matching, and better error handling across the       
  pipeline.

### February 19, 2026
 Today I worked on automating parts of our yearbook digitization pipeline to reduce the amount of manual work required 
  per yearbook. I started by reviewing a document I'd put together analyzing where human time was being spent, then     
  focused on what we called "Contact Point 2" — the name review step. I wrote a post-processing function that           
  automatically detects and upgrades compound names like "Van Der Berg" or "Mary Beth" that our AI was flagging as
  low-confidence even when the split was clearly correct. I also automated the creation of the edited records file so it
   no longer requires manually opening a browser-based editor just to save a copy, and added a terminal summary that
  tells you at the end of every run exactly which names still need human review — so you know instantly whether you even
   need to open the editor at all. After testing the changes against real data from nine yearbooks, I documented
  everything in a handoff doc and committed it to GitHub. I also mapped out the implementation plan for Contact Point 1,
   which is the bigger automation — using our existing DPT-2 vision AI to automatically classify every page of a new
  yearbook PDF and generate a draft YAML config, cutting what's currently a 2-3 hour manual setup process down to about
  40 minutes of review.

### February 18, 2026
We met with Mrs. Handford to walk her through the processes we have been executing so far in the yearbook project for her to get a good idea of where we are at. She also gave us some insight into her line of work and what she does for a living, as well as improvements that we can make to the process, such as working with the IT department to implement AWS to cloud store files and speed up our orchestration process. She said that she is currently working with them to give us access to that. Then, we read over the handoff document that Mr. Dubick gave us to update our landing AI models to the current DPT-2 because the old models are being deprecated soon.

### February 11, 2026
Investigated the impact of Landing AI's upcoming DPT-1 model deprecation on our yearbook extraction pipeline. Identified that all 16 parallel extraction scripts rely on Landing AI's agentic_doc.parse() API, which defaults to DPT-1 server-side — meaning the Feb 17 technology change and Mar 31 shutdown would affect every extractor. Confirmed that downstream phases (name splitting, fuzzy matching, manual corrections) are unaffected. Cross-referenced findings with a teammate's independent analysis, then combined both into a unified 7-step migration plan covering SDK updates, server-side configuration, version pinning, baseline testing, and validation. Delivered the final plan as a formatted PDF for the team.

### February 10, 2026
Today I began and finished the namesplitting for the 1983 metadata extraction, and then used the simple yearbook editor html to manually review names. There were 4 errors, and they were all resolved by me before being saved to an edited JSON file. After manually reviewing, I began the matching pipeline, which completed, and the next step is to use the matching review editor to match the activities and sports to the students.

### February 6, 2026
I completed verifying the metadata for the 1983 yearbook and began the extraction process, which took a long time. Then, I used claude to once gain generate the .yml file for the orchestrator to run the xtraction scripts. I was able to begin the extraction phase and complete it, generating a new file with records of names. 

### February 5, 2026
Today, I continued verifying the metadata for the 1983 yearbook by cross referencing the pdf scan with the sheets extracted by gemini. I got about halfway through it today. 

### February 4, 2026  
Today was our first day back after having Monday and Tuesday off due to snow. I focused on finishing the 1981 extraction matching and generating the final file, then began working on the 1983 extraction. Most of my time was spent visually cross-referencing the 1983 metadata with the PDF scan to ensure that the name counts were accurate.

### February 2-3 
No class due to snow days

### January 29, 2026
 Today I opened the simple yearbook editor to review the name-split results for the 1981 yearbook. Went
   through the low-confidence names, fixed the ones I could confirm were errors, and saved the edited
  file. Started looking at the matching pipeline next but ran out of time before finishing.

### January 28, 2026  
Today was our first day back in class since last week due to a snow day on Monday and drop day on Tuesday. I received the API key from Mr. Dubick and configured it in Claude Code to run the name-splitting script on the extracted data. After completing name splitting, I was ready to integrate the data into the simple yearbook editor HTML. However, I ran out of time because the name-splitting process took a significant amount of time to complete.

### January 26, 2026
 No class — snow day.

### January 23, 2026
Today I went through the YAML config for the 1981 yearbook and manually compared the page counts
  against the actual PDF to make sure everything lined up. Cross-referencing page by page takes a while
  but it's important to catch anything off before running extraction. Also started looking into getting
  the API key set up so I can run name splitting next time.

### January 22, 2026  
Today, I used Claude to generate the `.yml` file for the 1981 yearbook metadata so the orchestrator could run the extraction scripts. I completed the extraction phases up through name splitting. Tomorrow, I plan to screen the data by manually comparing the YAML file counts against the actual PDF, and then create an API key to use Claude’s Haiku model for name splitting.

### January 21, 2026  
Today, Mr. Dubick allowed Max and me to sign up for a Claude Pro account so we could run Claude Code locally in our terminals. This significantly streamlined our workflow, as we were now able to create our own branches of the GitHub repository and work on the project simultaneously from home. I spent most of the class figuring out how to properly clone the repository and set up Claude Code on my laptop. By the end of the period, everything was configured successfully, and I organized the project locally within a GitHub folder on my computer.

### January 20, 2026  
Today, Max and I used Mr. Dubick’s laptop to run Claude Code and begin the data extraction process using the 1980 yearbook metadata to create a `.yml` file. This took most of the class period because Claude had to revisit and fix several errors, and the orchestrator program was unable to pull data from Middle School activities or sports. By the end of class, we had Claude generate a summary of the day’s activities so Mr. Dubick could review our progress later, and we pushed the new files to the GitHub repository.

### January 9, 2026
 Built out the Gantt chart today, mapping each remaining task against the calendar for the rest of the
  semester. Having it laid out visually made it a lot easier to see where things were tight and where
  there was more breathing room.

### January 8, 2026
 Walked Mr. Dubick through the task analysis and project plans today and got his approval to move
  forward. He had a few notes on the timeline but was generally on board with the direction.
  
### January 7, 2026
 Created a task analysis breaking down what still needs to get done and roughly how long each task will
   take. Helped clarify where the priorities are for the rest of the semester and where the biggest time
   sinks are going to be.

### January 6, 2026
  Worked through the status report today and filled out the design specifications, bill of materials,
  and functional requirements page. This gave us a clear picture of what components we need and how
  everything is supposed to work together.

### January 5, 2026
Today I updated the engineering GitHub page to make sure it was current with where the project stands
  heading into the new semester. Cleaned up the layout and made sure all sections accurately reflected
  our current progress.
