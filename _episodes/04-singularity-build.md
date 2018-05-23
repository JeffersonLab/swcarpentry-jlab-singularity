---
title: "Building docker containers"
teaching: 5
exercises: 5
questions:
- "How do I create my own containers?"
objectives:
- "Understand how to build a recipe for a docker container."
keypoints:
- "Although using containers with singularity does not require superuser privileges, creating containers still does."
- "Dockerfiles are recipes for docker containers."
- "By storing Dockerfiles in a GitHub repository we gain version both tracking and cloud building."
---

## Creating docker containers

So, you want to build your own docker containers? Excellent. You may be able
to distribute your simulation or analysis code to others more easily without
the need to support a wide range of platforms.

Writing a
