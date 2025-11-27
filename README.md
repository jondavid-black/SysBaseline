# SysBaseline

Project Management & Systems Engineering as Code. Maintain your content, requirements, plans, and issues directly in your git repository.

## 📋 Overview

SysBaseline provides a suite of git-native tools designed for Project Management as Code (PMaC) and Systems Engineering as Code (SEaC).
It bridges the gap between high-level program management, system engineering, and development tasks needed to implement them.

It rejects the idea that your critical engineering data should live in a proprietary database.
Instead, SysBaseline treats your lifecycle as structured YAML data that lives alongside your source code.

The suite includes two primary tools:

sbl: A utility for initializing and maintaining the repository structure.

sblweb: A local web server that provides a modern UI for managing requirements, boards, and traceability matrices, along with a REST API for integration.

## ✨ Key Features

Everything as Code: All data (PM artifacts and SE artifacts) is stored in human-readable, machine-parsable YAML.

Git-Native History: Use git diff to see how requirements evolved.

Local Web Interface: Use sblweb to visualize relationships and Kanban boards without leaving your local environment.

Offline First: No cloud dependency. If you can commit code, you can update the system architecture.

API Integration: sblweb exposes a local API for CI/CD gating and custom reporting.

## 🚀 Quick Start

1. Installation

SysBaseline is available on PyPI. Installing the package provides both sbl and sblweb.

# via pipx (Recommended)
pipx install sysbaseline

# Verify installation
sbl --version
sblweb --version


2. Initialize a Repository

Go to your project root and use sbl to scaffold the directories:

cd my-project
sbl init


This creates the standard directory structure:

.sysbaseline/
  └── config.yaml      # Project settings

plans/                 # Project Management (PM) Artifacts
  ├── issues/
  └── milestones/

mbse/                  # Model-Based Systems Engineering (MBSE) Artifacts
  ├── requirements/
  └── designs/


3. Launch the Web Experience

Start the local web server to interact with your artifacts through a clean UI:

sblweb start
# Serving UI at http://localhost:8080
# Serving API at http://localhost:8080/api/v1


Open your browser to http://localhost:8080 to create requirements, manage issues, and view traceability matrices.

4. Manual Usage (The "As Code" Way)

Because SysBaseline uses standard YAML, you can also create artifacts manually using your favorite text editor or IDE.

Example: Creating a Requirement Manually

Create a file at mbse/requirements/REQ-100.yaml:

id: REQ-100
statement: System must handle 10k concurrent users.
type: performance
status: draft
verification: test


Example: Creating an Issue Manually

Create a file at plans/issues/ISSUE-101.yaml:

id: ISSUE-101
title: Optimize database connection pool
status: open
priority: high
trace:
  - REQ-100  # Links this task to the requirement above


5. Commit to Git

Once you have added content via sblweb or your editor, commit the artifacts just like code:

git add .sysbaseline plans mbse
git commit -m "feat: added REQ-100 and associated implementation task"
