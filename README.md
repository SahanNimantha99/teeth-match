# Teeth Match Capture

A research project tool built for a dental plaque study. The app speeds up and standardises taking and collecting patient photos before and after applying disclosing dye.

> **Research use only. This is not a medical device** and must not be used for diagnosis or treatment decisions.

## The problem

Photos taken before and after the dye must be from the same position and angle so they can be compared. The patient moves when the dye is applied, which makes the after-dye photos hard to line up. The app guides the user to match each after-dye photo to its before-dye benchmark.

## How it works

1. **Before dye:** take 6 benchmark photos, from the Up, Left and Right angles, each with the light on and then with the light off. For each benchmark you check the teeth area the app found and adjust the box if needed.
2. **Apply the dye.** The patient sits back in the same position, with the same retractor.
3. **After dye:** for each photo the app shows:
   - the benchmark teeth outline over the live camera
   - a live **Teeth match %**
   - directions such as "Move phone left", "Move closer or zoom in" or "Rotate phone clockwise"

   A photo counts as matched at **90% or more** (rotation also has to be within 2.5°). Matched photos are saved straight away. If a photo is not matched, you can retake it or keep it anyway. **Auto take** is optional and takes the photo by itself once the match holds for a moment.
4. **Finish:** the patient's 12 photos, the benchmark teeth masks and a match log (`capture_log.csv`) are saved as one ZIP.

## Benefits

- Faster capture
- Consistent photos for every patient
- A recorded match score for each photo
- Data that is ready for analysis or AI training

## Features

- A guided step-by-step flow (before dye → apply dye → after dye → finish)
- A dashboard that shows each patient's progress
- Resume unfinished patients, which are stored in the browser on the phone
- Retake any photo by tapping it
- Zoom (uses the camera's own zoom when the phone supports it, otherwise digital zoom)
- Teeth-only matching: only the teeth area is compared, using edges rather than colour, so the dye does not affect the match
- A match % display, with a guide that can be shown as an outline
- Safe saving: photos are never deleted until you confirm the ZIP is saved. A copy of the ZIP stays in the app, and the **Download again** button on the dashboard downloads it again. **Remove** deletes it for good.

## Privacy

Everything runs on the device. **No photos are uploaded.** The photos, matching and ZIP creation all stay in the phone's browser, and data leaves the phone only when you save or share the ZIP yourself.

## Run and deploy

The whole app is one file, `index.html`, with no build step. The ZIP library (JSZip) is included inside the file.

- **Deploy:** the app is hosted on GitHub Pages from this repository's `main` branch: <https://sahannimantha99.github.io/teeth-match/>. Push to `main` to update it.
- **Run locally:** serve the folder over HTTP, for example `python -m http.server 8000`, and open `http://localhost:8000`. The camera needs HTTPS or `localhost`, so test on a phone through the GitHub Pages link.

## Install on iPhone

1. Open the GitHub Pages link in **Safari**.
2. Tap **Share → Add to Home Screen**. The app appears as "Teeth Match".
3. Open it from the home screen and allow camera access when asked.
4. After finishing a patient, choose **Save to Files** (or Google Drive) in the share sheet. If the save was missed, use **Download again** on the dashboard.

## Project structure

```
teeth-match/
├── index.html   # the whole app: UI, camera, teeth matcher, storage, ZIP export
└── README.md
```

## Output files

Each patient produces `<PatientID>.zip`, which contains a folder named after the patient:

```
P001.zip
└── P001/
    ├── up_undyed.jpg              # benchmark, light on
    ├── up_undyed_teeth.png        # teeth mask for that benchmark
    ├── up_undyed_nolight.jpg      # benchmark, light off
    ├── up_undyed_nolight_teeth.png
    ├── up_dyed_light.jpg          # after dye, light on  (matched to up_undyed.jpg)
    ├── up_dyed_nolight.jpg        # after dye, light off (matched to up_undyed_nolight.jpg)
    ├── left_...                   # the same 6 files for Left
    ├── right_...                  # the same 6 files for Right
    └── capture_log.csv
```

File names follow the pattern `<angle>_<undyed|dyed>_<light|nolight>.jpg`, except that the light-on benchmark is just `<angle>_undyed.jpg`.

`capture_log.csv` has one row per photo with these columns: `file, captured_at, benchmark, matched, teeth_match_pct, edge_similarity, shift_x_pct, shift_y_pct, size_pct, rotation_deg, zoom, width, height`.

## Team

- **Project team:** _[names]_
- **Supervisors:** _[names]_
- **Institution:** University of Peradeniya, _[faculty / department]_
- **Contact:** _[email]_
