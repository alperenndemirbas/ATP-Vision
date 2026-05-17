# ATP Vision — Basketball Shot Analysis

ATP Vision is a computer vision system that automatically analyzes basketball free-throw videos from a single fixed camera. It processes raw training footage and produces an annotated video output with biomechanical metrics, consistency scoring, and a visual report — no manual tagging required.

---

## Demo

https://github.com/user-attachments/assets/47a58dd7-325e-48d3-aac0-e02a678f8045

---

## What It Does

- Detects every shot in the video automatically — start, release moment, and end
- Slows down the release frame window to highlight the critical moment
- Draws angle arcs on elbow and knee joints at the moment of release
- Calculates elbow angle, knee angle, and squat depth per shot
- Scores each shot against the player's own session median for consistency analysis
- Generates a visual report (shot table + form bars) appended to the video output

## How It Works

| Component | Role |
|---|---|
| YOLO11m (fine-tuned) | Ball, rim, and net detection — custom-labeled dataset |
| MediaPipe Pose | Skeleton extraction, joint angle calculation |
| Shot trigger algorithm | Detects shot start via upward ball movement + shoulder threshold |
| Release scoring | Multiplicative score: normalized elbow angle × wrist-to-ball proximity |
| Squat detection | Rolling 0.5s window minimum knee angle before shot |
| Slow-motion rendering | Frame buffering around release ± window, written at 2x |

## Stack

`Python` `OpenCV` `YOLO11 / Ultralytics` `MediaPipe` `NumPy` `ffmpeg`
