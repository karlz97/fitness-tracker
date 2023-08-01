[![GitHub repo size](https://img.shields.io/github/repo-size/TheNewThinkTank/fitness-tracker?style=flat&logo=github&logoColor=whitesmoke&label=Repo%20Size)](https://github.com/TheNewThinkTank/fitness-tracker/archive/refs/heads/main.zip)
# Fitness-Tracker

[![Documentation Status](https://readthedocs.org/projects/fitness-tracker/badge/?version=latest)](https://fitness-tracker.readthedocs.io/en/latest/?badge=latest)
![CI](https://github.com/TheNewThinkTank/Fitness-Tracker/actions/workflows/fitness-tracker-wf.yml/badge.svg) [![codecov](https://codecov.io/gh/TheNewThinkTank/Fitness-Tracker/branch/main/graph/badge.svg?token=CKAX4A3JQF)](https://codecov.io/gh/TheNewThinkTank/Fitness-Tracker)

<!-- ![simulation-wf](https://github.com/TheNewThinkTank/Fitness-Tracker/actions/workflows/simulation-wf.yml/badge.svg) -->

## Intro

Full stack fitness tracking application using TinyDB and FastAPI.
Add weight-training logs continuously to db.json and query the data through the browser.
Visually inspect your progression through dates and exercises

## Architecture Diagram
![architecture](img/architecture.png)

## Getting started

First, clone the project:<br>
`git clone https://github.com/TheNewThinkTank/Fitness-Tracker.git`

### Upload your workouts

- Add your workout log to the `data` folder under the correct workout date
- Edit `src/orchestration/real_flow.sh`: Specify the `WORKOUT_DATE` and `TRAINING_PROGRAM` values
- Execute `bash src/orchestration/real_flow.sh` which will insert your log(s) into the TinyDB database

### Analyze your data

Run FastAPI web app with Docker from CLI:
`docker-compose up`<br>
then visit the URL: http://localhost:8080/docs

Alternatively,

```BASH
docker build -t ftimage .
docker run -d -p 8000:8000 --name ftcontainer ftimage
```

### Update docs

```BASH
cd docs
make clean
sphinx-apidoc -o ./source ../src
make html
```

## Features

- FastAPI app "Fitness-Tracker", with TinyDB backend, exposed through Docker container
- Program logging (Located in folder: logs)
- Plotting (with the Seaborn library. Located in folder: img)
- Documentation (auto-generated by Sphinx and hosted on readthedocs):  
  https://fitness-tracker.readthedocs.io/en/latest/index.html#
- Multiple unit test suites (Pytest)
- BDD (Behavior Driven Development, using the Behave framework)
- Multiple GitHub Actions workflows
- Data quality validation (Great Expections)
- Package dependency management (Poetry)
- KPI tracking: 1-Rep-Max estimation (Epley and Brzycki formulas)
- Realistic workout data simulation (with naturally progressing trend over time)
- Catalogue of musclegroups, corresponding exercises and suggested weight ranges (for simulations)

## Examples

[training plots etc.](examples/EXAMPLES.md)

### Similar projects
If you liked this fitness tracker then you might also be interested in
the [workout-generator](https://github.com/TheNewThinkTank/workout-generator) Django project,<br>
the [nutrition-planner](https://github.com/TheNewThinkTank/nutrition-planner) Streamlit project, with associated development guide:<br>
[medium](https://medium.com/@GustavCollinRasmussen/build-a-nutrition-app-on-streamlit-8c4f01229989),<br>
the [athlete](https://github.com/TheNewThinkTank/athlete) project,<br>
or the [Dojo](https://gitlab.com/sports-tracking/dojo) martial arts project
which can be found on GitLab and is a Rust & TypeScript based general purpose martial arts desktop application

<!--
## Upcoming features
- deploy and host containerized app on Raspberry Pi
- Add muscle groups to log file name
- ML models (Scikit Learn)
- Bodily strength-ratio tracking (determine baseline, ideal-ranges, and compare the two)
- Dashboard
- Add key exercises (benchpress, squat, deadlift) to dashboard
- Hosting on PyPi (automated deploy with GitHub Actions)
- Identify musclegroups and exercises with best or worst progression
- Add cardio tracking (integrate app with Strava)
-->

### TODOs
- [ ] quality control for TS and JS
- [x] YAML support

### Known Issues
* Google Drive on macOS Ventura 13.4.1 spontaneously switches local mounting point between
`/Users/<USER>/Google Drive/` and
`/Users/<USER>/Library/CloudStorage/GoogleDrive-<EMAIL>/`, or fails to sign in.<br>
[Fix](tech_support/macos_ventura_google_drive.md)
* Mounting directories directly from Google Drive is not supported by Docker Compose. Docker Compose can only mount directories that are accessible on the local filesystem.
