# Multimodal EEG ECG Framework for Evaluating Emotional Valence and Arousal Using the DREAMER Dataset
## 1. Introduction
Affective information processing is a fundamental cognitive mechanism through which humans evaluate environmental stimuli and adjust attention, behavior, and physiological states. According to Russell’s Circumplex Model of Affect, emotions can be described along two orthogonal dimensions: valence, referring to the degree of pleasantness, and arousal, referring to the intensity of physiological activation. Examining how neural and cardiac signals change during emotional evaluation is therefore important for understanding human affective responses and improving human-computer interaction.

<img width="739" height="388" alt="image" src="https://github.com/user-attachments/assets/d5cc5939-8d6e-4daa-b5cf-be67fbc22fd5" />

This project investigates these responses using the DREAMER dataset, which provides synchronized electroencephalogram (EEG) and electrocardiogram (ECG) recordings during audio-visual emotion elicitation. To clearly compare affective dimensions, two contrasting conditions were selected: calm, representing high valence and low arousal, and fear, representing low valence and high arousal. A focused analysis was conducted on two participants, and only the final 60 seconds of each stimulus recording were extracted to capture periods in which the target emotions were expected to be fully elicited.

Two physiological mechanisms were examined. Emotional valence was assessed using EEG-derived Frontal Alpha Asymmetry (FAA), calculated from alpha power in the F3 and F4 frontal channels. Based on Davidson’s Approach-Withdrawal Model, stronger relative left-frontal activation indicates positive affect, whereas right-frontal dominance reflects negative affect. Autonomic arousal was evaluated using ECG-derived Heart Rate Variability (HRV), including RMSSD and the LF/HF ratio. RMSSD reflects parasympathetic regulation, while LF/HF indicates autonomic balance. By integrating EEG and ECG features, this project provides an interpretable multimodal framework for characterizing emotional responses to dynamic visual stimuli.

<img width="754" height="123" alt="image" src="https://github.com/user-attachments/assets/83955075-e445-487e-919e-18cf883ab427" />

## 2. Data Description

<details>
<summary>Data Source</summary>
  
Raw EEG and ECG signals are sourced from the DREAMER dataset.

- Kaggle: https://www.kaggle.com/datasets/phhasian0710/dreamer/data
- Katsigiannis, S., & Ramzan, N. (2018). DREAMER: A database for emotion recognition through EEG and ECG signals from wireless low-cost off-the-shelf devices. *IEEE Journal of Biomedical and Health Informatics*, 22(1), 98–107. https://doi.org/10.1109/JBHI.2017.2688959
</details>

<details>
<summary>Recording Device Info</summary>

| Item | Description |
|------|-------------|
| Signals recorded | EEG and ECG |
| EEG device | Emotiv EPOC wireless EEG headset |
| EEG channels | 14 channels |
| EEG sampling rate | 128 Hz |
| ECG device | Shimmer2 ECG sensor |
| ECG channels | 2 channels |
| ECG sampling rate | 256 Hz |
| Emotion labels | Participants rated valence, arousal, and dominance after each stimulus |

</details>

<details>
<summary>Original Purpose</summary>

The data were originally collected to evaluate whether low-cost, wireless, wearable EEG/ECG devices can be used for affective computing and emotion recognition.

</details>

## 3. Data Preprocessing

<details>
<summary>Visual Inspection & Artifact Identification</summary>

### Participant 3 — Stimuli 15 (Calm)
*EEG: 323.42 µV/cm | ECG: 200 µV/cm*

**Eye Blink Artifact**
At 14–15s, a sharp transient deflection is observed predominantly in frontal channels (AF3, F7, F3, FC5, AF4, F4, F8), with minimal effect on posterior channels (P8, O1, O2). Eye blinks should only appear in frontal leads without spreading to posterior regions.

![Pipeline Graph](figures/eyeblink.png)

---

### Participant 4 — Stimuli 4 (Fear)
*EEG: 334.48 µV/cm | ECG: 253.04 µV/cm*

**Sweat Artifact & Electrode Disconnection**
At ~9–12s, a slow bilateral baseline drift is observed across multiple channels (~3s duration, < 0.5 Hz) with no specific topographic pattern — consistent with sweat artifact. Channel F7 shows a flat line throughout, indicating electrode disconnection. At ~12s, an abrupt return to baseline is observed, likely due to a brief head movement.

![Pipeline Graph](figures/sweat.png)

</details>

<details>
<summary>Spectral & Time-Series Proof</summary>

Time-series signals and Power Spectral Density (PSD) before and after preprocessing (bandpass filtering + artifact removal):

![Pipeline Graph](figures/EEG_time.png)
![Pipeline Graph](figures/EEG_PSD.png)
![Pipeline Graph](figures/ECG_PSD.png)

</details>

## 4. NeuroPype Pipeline

![Pipeline Graph](figures/pipeline.png)
https://drive.google.com/file/d/1cDDj1-EVk4VkKCEZEuVvr-xp128mZdFV/view?usp=drive_link

<details>
<summary> How to Run </summary>
  
1. Open **NeuroPype Pipeline Designer**
2. Load `pipeline/HIP_FinalProject_Group10_Pipeline.pyp`
3. Update the file path in the **ParameterPort** node to your local `.edf` file
4. Run the pipeline

</details>
