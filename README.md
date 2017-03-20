# README

The Web Task Framework is designed to make it easy to define and administer web-based psychological tasks. Think of it roughly as a hosted type of Experiment Factory. It focus is traditionally-recruited research participants rather than a tight integration with Amazon's Mechanical Turk (although it should work with MTurk).

## Overview

The software is divided into two parts: a **researcher-facing** view and a **participant-facing** view.

### The Researcher View

Here, you'll set up and configure your batteries of instruments, and test them. In addition, you'll be able to generate URLs for participants to complete your assessments, and download the data. It should also be possible to see where participants are in completing a battery, and see basic QA data.

There's also an instrument library — administrators can build instruments and import them into the system (either by a specially-arranged .zip file or a git repository, I don't know which right now).

Adding an instrument to a battery automatically creates a **copy** of the instrument. This way, if administrators modify instruments, it won't affect existing batteries.

### The Participant View

The participant view is much simpler. It'll track participants either:

* By generated identifier in URL
* by identifier/password login
* totally anonymously (eg, no researcher-provided identifier)

From there, it'll take participants directly through the battery of tasks.

Note that other than this identifier, the software explicitly avoids saving identifiable information, to make data sharing as easy as possible and minimize the risks of security breaches. Mainly, this is IP address. (Should this include dates? Dates are real useful.)

## Glossary of terms

* **researcher** — a person involved in setting up and/or administering batteries of instruments.
* **participant** — a person who completes assessments and provides data
* **battery** — a sequence of instruments, ready for data collection
* **instrument** — a single psychological task
* **parameter** — something that changes the behavior of an instrument and is easily changed by a researcher
* **library** — the full set of instruments in the system
* **assessment** — the data for one instrumenta and one participant
* **measurement** — the fundamental unit of data in the system

## Technical stuff

Server-side, this is a pretty standard app. Rails 5, ruby 2.4. The one somewhat unusual requirement a modern version of PostgreSQL — I believe at least 9.4. Run 9.6 though, don't cheap out. We're making use of the json functionality in the relational database rather than dropping the data into mongodb or something.

The researcher view assumes shiny new browsers running on desktop computers. Like, we'll use grid layout(!), assume proper javascript, and so on. Shiny af.

The participant view will be much more conservative — all *required* components should work on old, terrible browsers (say, IE6). Which instruments work on what platforms will solely depend on the design of individual instruments.