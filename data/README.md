# Data

Deidentified behavioral features and model covariates analyzed in the
article. Each file has one row per participant × task (92 participants × 2
tasks = 184 rows) and contains exactly the observations that entered the
models. There are no missing values.

These files contain no names, dates, locations, recordings, transcripts, or
study record numbers. Participants are identified only by arbitrary codes
(`P001`–`P092`) that link rows across the three files. The video, audio, and
transcript data cannot be shared because they contain identifiable protected
health information.

## Common columns

All three files begin with these columns.

| Column | Description |
|---|---|
| `participant` | Participant code (`P001`–`P092`) |
| `source` | Recruitment source: `patient` (PTSD specialty clinic waitlist) or `control` (Prolific). Four participants recruited as patients did not meet PTSD criteria on the CAPS-5 and were analyzed as controls. |
| `ptsd` | Diagnostic group from the CAPS-5: `1` = PTSD, `0` = control |
| `demo_age` | Age in years |
| `demo_sex` | Sex: `Male` or `Female` |
| `demo_nonwhite` | Race other than White: `TRUE` or `FALSE` (one participant who selected "Hispanic" as their race is coded `TRUE`) |
| `task` | Behavioral task: `Account` (trauma account) or `Impact` (impact statement) |

## `verbal.csv`

Computed from automatic (Whisper) transcripts of the participant's speech in
each task.

| Column | Description |
|---|---|
| `WC` | Total word count |
| `i` | LIWC-22 first-person singular pronouns (% of words) |
| `we` | LIWC-22 first-person plural pronouns (% of words) |
| `emo_neg` | LIWC-22 negative emotion words (% of words) |
| `emo_pos` | LIWC-22 positive emotion words (% of words) |
| `allnone` | LIWC-22 all-or-none words (% of words) |
| `cogproc` | LIWC-22 cognitive process words (% of words) |
| `Perception` | LIWC-22 perception words (% of words) |
| `sentiment` | Sentiment rating of the transcript from Llama 3.3 70B (1 = very negative to 7 = very positive) |

LIWC-22 was run on transcript segments; word count is summed over segments
and each category percentage is averaged over segments. The models analyze
the category percentages divided by 100 (proportions) with ordered beta
regression.

## `vocal.csv`

Computed from the participant's audio stream in each task.

| Column | Description |
|---|---|
| `SD_Loudness` | Standard deviation of loudness (openSMILE eGeMAPSv2) |
| `SD_Pitch` | Standard deviation of fundamental frequency, in Hz (Praat) |
| `PSR` | Pseudo-syllable rate: voiced segments per second (openSMILE eGeMAPSv2) |
| `M_Voiced` | Mean length of voiced segments, in seconds (openSMILE eGeMAPSv2) |
| `M_Unvoiced` | Mean length of unvoiced segments, in seconds (openSMILE eGeMAPSv2) |
| `SD_Voiced` | Standard deviation of voiced segment lengths, in seconds (openSMILE eGeMAPSv2) |
| `SD_Unvoiced` | Standard deviation of unvoiced segment lengths, in seconds (openSMILE eGeMAPSv2) |
| `CPPS` | Smoothed cepstral peak prominence, in dB (Praat) |
| `H1H2` | Difference between the amplitudes of the first and second harmonics, in dB (Praat) |

## `visual.csv`

Computed from the participant's video in each task with OpenFace 2.0, then
averaged over frames.

| Column | Description |
|---|---|
| `AU04` | Mean intensity of AU4, brow lowerer (0–5) |
| `AU12` | Mean intensity of AU12, lip corner puller (0–5) |
| `AU15` | Mean intensity of AU15, lip corner depressor (0–5) |
| `AU17` | Mean intensity of AU17, chin raiser (0–5) |
| `AU20` | Mean intensity of AU20, lip stretcher (0–5) |
| `PoseX` | Mean head rotation about the X axis (OpenFace `pose_Rx`, pitch), in radians |
| `PoseY` | Mean head rotation about the Y axis (OpenFace `pose_Ry`, yaw), in radians |
| `DiffX` | Head motion: root mean square of successive frame-to-frame differences in `pose_Rx`, in radians |
| `DiffY` | Head motion: root mean square of successive frame-to-frame differences in `pose_Ry`, in radians |

The models analyze the AU intensities divided by 5 (proportions of the scale
maximum) with ordered beta regression.

## Reading the files

Read the files with base R's `read.csv()`, as the analysis code does, to
recover every stored value exactly. Other readers (e.g., `readr::read_csv()`)
can differ in the last binary digit of some values, which is enough to change
the MCMC draws slightly.

## License

CC BY 4.0; see [`LICENSE-CC-BY.md`](../LICENSE-CC-BY.md).
