---
title: "Daily Journal: Yearbook Metadata & Extraction Work"
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

### January 28, 2026  
Today was our first day back in class since last week due to a snow day on Monday and drop day on Tuesday. I received the API key from Mr. Dubick and configured it in Claude Code to run the name-splitting script on the extracted data. After completing name splitting, I was ready to integrate the data into the simple yearbook editor HTML. However, I ran out of time because the name-splitting process took a significant amount of time to complete.

### January 22, 2026  
Today, I used Claude to generate the `.yml` file for the 1981 yearbook metadata so the orchestrator could run the extraction scripts. I completed the extraction phases up through name splitting. Tomorrow, I plan to screen the data by manually comparing the YAML file counts against the actual PDF, and then create an API key to use Claude’s Haiku model for name splitting.

### January 21, 2026  
Today, Mr. Dubick allowed Max and me to sign up for a Claude Pro account so we could run Claude Code locally in our terminals. This significantly streamlined our workflow, as we were now able to create our own branches of the GitHub repository and work on the project simultaneously from home. I spent most of the class figuring out how to properly clone the repository and set up Claude Code on my laptop. By the end of the period, everything was configured successfully, and I organized the project locally within a GitHub folder on my computer.

### January 20, 2026  
Today, Max and I used Mr. Dubick’s laptop to run Claude Code and begin the data extraction process using the 1980 yearbook metadata to create a `.yml` file. This took most of the class period because Claude had to revisit and fix several errors, and the orchestrator program was unable to pull data from Middle School activities or sports. By the end of class, we had Claude generate a summary of the day’s activities so Mr. Dubick could review our progress later, and we pushed the new files to the GitHub repository.



