---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}

Education
======
* B.Sc. in Information Systems, GPA 87  
  * Open University of Israel  
  * Focus: Software Engineering, Data Structures, AI fundamentals

* Graduate Diploma Program (in progress)  
  * Preparing for M.Sc. in Computer Science  
  * Focus: Linear Algebra, Algorithms, Embedded Systems

Experience
======
* 2022–2024: CUDA / C++ Developer  
  * Opteamizer (acquired by Deloitte)  
  * Worked on high-performance GPU code for real-time image processing  
  * Tools: C++, CUDA, OpenCV, TensorRT, Jetson

* 2024–2025: AI & Robotics Projects (Independent)  
  * Built multi-camera DeepStream-based tracking systems  
  * Integrated ASR/NLP/TTS agents with robotics (Jetson NX, ROS)  
  * Optimized video processing with GStreamer + CUDA pipelines

Skills
======
* **Programming**: C++, Python, CUDA, Bash  
* **AI / CV Frameworks**: PyTorch, TensorRT, DeepStream, OpenCV  
* **Hardware**: NVIDIA Jetson (Xavier, Orin NX), Raspberry Pi, STM32  
* **Video / Audio**: GStreamer, FFmpeg, Hifi-GAN, Tacotron2  
* **Web / Tools**: Git, Docker, PostgreSQL (with pgvector), FastAPI

Projects & Publications
======
<ul>{% for post in site.publications reversed %}
  {% include archive-single-cv.html %}
{% endfor %}</ul>

Talks & Presentations
======
<ul>{% for post in site.talks reversed %}
  {% include archive-single-talk-cv.html %}
{% endfor %}</ul>

Teaching & Mentorship
======
<ul>{% for post in site.teaching reversed %}
  {% include archive-single-cv.html %}
{% endfor %}</ul>

Service and Leadership
======
* Led independent open-source contributions on GitHub  
* Created demo content for LinkedIn on AI & robotics  
* Maintains multiple developer boards for community-based testing
