dataset for Ritz & Shenhav 'Orthogonal neural encoding of targets and distractors supports multivariate cognitive control'. 

Undergraduate participants performed a color-motion decision-making task (random dot kinematogram) during fMRI (N=29, 90min scan). 
Alternating runs of color-response (hard, longer runs, data of primary interest) and motion-response (easy, shorter runs). 
At the end of the session, participants performed color/motion localizers (see paper).
For event timing, download code & behavioral files here: https://github.com/shenhavlab/PACT_fMRI_public/tree/main/0_behavior



# Run types
sub-80xx_ses-01_task-RDMmotion_run-xx_bold.nii.gz
	- Participants repond to majority motion direction, ignoring color (easy)

sub-80xx_ses-01_task-RDMcolor_run-xx_bold.nii.gz
	- Participants repond to majority color, ignoring color (hard)

sub-80xx_ses-01_task-RDMlocalizer_run-xx_bold.nii.gz
	- Color and motion localizers (for order, see behavioral files)





See manuscript for full details (available at https://harrisonritz.github.io; publication forthcoming).
Relevant methods section:

# Participants
Twenty-nine individuals (17 females, Age: M = 21.2, SD = 3.4) provided informed consent and participated in this experiment for compensation ($40 USD; IRB approval code: 1606001539). All participants had self-reported normal color vision and no history of neurological disorders. Two participants missed one Attend-Color block (see below) due to a scanner removal, and one participant missed a motion localizer due to a technical failure, but all participants were retained for analysis. This study was approved by Brown University’s institutional review board.

# Task
The main task closely followed our previously reported behavioral experiment 10. On each trial, participants saw a random dot kinematogram (RDK) against a black background. This RDK consisted of colored dots that moved left or right, and participants responded to the stimulus with button presses using their left or right thumbs. 

In Attend-Color blocks (six blocks of 150 trials), participants responded depending on which color was in the majority. Two colors were mapped to each response (four colors total), and dots were a mixture of one color from each possible response. Dots colors were approximately isolument (uncalibrated RGB: [239, 143, 143], [191, 239, 143], [143, 239, 239], [191, 143, 239]), and we counterbalanced their assignment to responses across participants. 

In Attend-Motion blocks (six blocks of 45 trials), participants responded based on the dot motion instead of the dot color. Dot motion consisted of a mixture between dots moving coherently (either left or right) and dots moving in a random direction. Attend-Motion blocks were shorter because they acted to reinforce motion sensitivity and provide a test of stimulus-dependent effects.

Critically, dots always had color and motion, and we varied the strength of color coherence (percentage of dots in the majority) and motion coherence (percentage of dots moving coherently) across trials. Our previous experiments have found that in Attend-Color blocks, participants are still influenced by motion information, introducing a response conflict when color and motion are associated with different responses 10. Target coherence (e.g., color coherence during Attend-Color) was linearly spaced between 65% and 95% with 5 levels, and distractor congruence (signed coherence relative to the target response) was linearly spaced between -95% and 95% with 5 levels. In order to increase the salience of the motion dimension relative to the color dimension, the display was large (~10 degrees of visual angle) and dots moved quickly (~10 degrees of visual angle per second). 

Participants had 1.5 seconds from the onset of the stimulus to make their response, and the RDK stayed on the screen for this full duration to avoid confusing reaction time and visual stimulation (the fixation cross changed from white to gray to register the response). The inter-trial interval was uniformly sampled from 1.0, 1.5, or 2.0 seconds. This ITI was relatively short in order to maximize the behavioral effect, and because efficiency simulations showed that it increased power to detect parametric effects of target and distractor coherence (e.g., relative to a more standard 5 second ITI). The fixation cross changed from gray to white for the last 0.5 seconds before the stimulus to provide an alerting cue.

# Procedure
Before the scanning session, participants provided consent and practiced the task in a mock MRI scanner. First, participants learned to associate four colors with two button presses (two colors for each response). After being instructed on the color-button mappings, participants practiced the task with feedback (correct, error, or 1.5 second time-out). Errors or time-out feedback were accompanied with a diagram of the color-button mappings. Participants performed 50 trials with full color coherence, and then 50 trials with variable color coherence, all with 0% motion coherence. Next, participants practiced the motion task. After being shown the motion mappings, participants performed 50 trials with full motion coherence, and then 50 trials with variable motion coherence, all with 0% color coherence. Finally, participants practiced 20 trials of the Attend-Color task and 20 trials of Attend-Motion tasks with variable color and motion coherence (same as scanner task).

Following the twelve blocks of the scanner task, participants underwent localizers for color and motion, based on the tasks used in our previous experiments 30. Both localizers were block designs, alternating between 16 seconds of feature present and 16 seconds of feature absent for seven cycles. For the color localizer, participants saw an aperture the same size as the task, either filled with colored squares that were resampled every second during stimulus-on (‘Mondrian stimulus’), or luminance-matched gray squares that were similarly resampled during stimulus-off. For the motion localizer, participants saw white dots that were moving with full coherence in a different direction every second during stimulus-on, or still dots for stimulus-off. No responses were required during the localizers.


# MRI sequence 
We scanned participants with a Siemens Prisma 3T MR system. We used the following sequence parameters for our functional runs: field of view (FOV) = 211 mm × 211 mm (60 slices), voxel size = 2.4 mm3, repetition time (TR) = 1.2 sec with interleaved multiband acquisitions (acceleration factor 4), echo time (TE) = 33 ms, and flip angle (FA) = 62°. Slices were acquired anterior to posterior, with an auto-aligned slice orientation tilted 15° relative to the AC/PC plane. At the start of the imaging session, we collected a high-resolution structural MPRAGE with the following sequence parameters: FOV = 205 mm × 205 mm (192 slices), voxel size = 0.8 mm3, TR = 2.4 sec, TE1 = 1.86 ms, TE2 = 3.78 ms, TE3 = 5.7 ms, TE4 = 7.62, and FA = 7°. At the end of the scan, we collected a field map for susceptibility distortion correction (TR = 588ms, TE1 = 4.92 ms, TE2 = 7.38 ms, FA = 60°).

# fMRI preprocessing
We preprocessed our structural and functional data using fMRIprep (v20.2.6; 122 based on the Nipype platform 123. We used FreeSurfer and ANTs to nonlinearly register structural T1w images to the MNI152NLin6Asym template (resampling to 2mm). To preprocess functional T2w images, we applied susceptibility distortion correction using fMRIprep, co-registered our functional images to our T1w images using FreeSurfer, and slice-time corrected to the midpoint of the acquisition using AFNI. We then registered our images into MNI152NLin6Asym space using the transformation that ANTs computed for the T1w images, resampling our functional images in a single step. For univariate analyses, we smoothed our functional images using a Gaussian kernel (8mm FWHM, as dACC responses often have a large spatial extent). For multivariate analyses, we worked in the unsmoothed template space (see below).

