---
title = "ATS-Friendly Resume"
date = 2025-09-14
draft = true
---

# The Perfect ATS-Friendly Resume

For and after my Accenture internship ended, I had to create multiple versions of my resume and update it constantly. I started using [Enhancv](https://enhancv.com/) for their free templates, but they came with branding at the bottom. To fix that, I'd upload the PDF to [ILovePDF](https://www.ilovepdf.com/edit-pdf), add a blank white image on top of the branding, and download it. The resume looked pretty and not unprofessional with the branding removed, but it wasn't great practice. The ATS score was only [66/100](https://app.enhancv.com/resume-checker/report/68c85d8dda9e82e2909d00a9?isWithGenerateSummary=false) - pretty low.

I tried to solve this by building a simple HTML ATS-friendly [resume maker](https://github.com/emaniaditya/ATS_Friendly_Resume_Maker), inspired by my classmate's [project](https://github.com/Anjalisahu4644/ATS_Friendly_Resume_Maker). It had input fields, and when you clicked "Generate," it printed to PDF and downloaded. But when I migrated from HTML to React, alignment was off, things were hardcoded, and options were limited. Along with a [not so great half built project](https://emaniaditya.github.io/ATS_Friendly_Resume_Maker).

![LibreOffice Resume](/static/img/libre-resume-template.png)

That's when I decided to go old school and do it in a word doc, like my friend who was using Canva. I thought hers was image-based but was wrong and the [low](https://app.enhancv.com/resume-checker/report/68c85f01b94defcb9a7cb888?isWithGenerateSummary=false) ATS score might be because of some missing sections. On my laptop, I used LibreOffice (since that's ubuntus doc editor), and to my surprise, they had pre-built resume templates. I customized one and exported to PDF.

My current resume scores 98/100 on ATS checkers and is made with LibreOffice. It's text-based, customizable, free, and reliable.

![98-ats](/static/img/ats-98.png)

I've uploaded the PDF and raw .docx to [GitHub](https://github.com/emaniaditya/resume) for others to download and customize.

Crux - simple tools like LibreOffice beat fancy apps. If you're struggling with ATS resumes, try it!
