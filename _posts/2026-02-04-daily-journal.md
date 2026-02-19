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



