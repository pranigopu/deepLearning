# PAPER PRESENTATION
As a part of the deep learning for audio and music course, we students have to present a paper of our choice (either live or in video, with a live Q & A in either case). My chosen paper is "Piano Skills Assessment" by Paritosh Parmar, Jaiden Reddy and Brendan Morris (link: https://arxiv.org/abs/2101.04884). I chose this paper due to the following reasons:

- My experience in piano assessment (as a student)
- The relevance of such an application (ex. personal performance evaluation to help self-improvement)
- The interesting complexity of the problem of automating musical evaluation

---

# Presentation notes
> **Reference**: [Presentation Slides](./Presentation%20Slides.pdf)

## SLIDE 2: Driving goals & questions
The velocity of the music (notes per second) can be detected auditorily. Lot of performance aspects (ex. arpeggio, playing speed, cadences, hand movements) can be detected visually. The presence of multiple notes at once with cadences that correspond to cadences included in the grade level syllabi above would be recognizable both through auditory and visual analysis.

## SLIDE 7: Data acquisition
No overlap between training and test sets.

## SLIDE 8: Closer look at key scored attributes
Levels 1-9 represent pre-collegiate certification/skill level, while level 10 represents a collegiate or post-collegiate mastery. The primary evaluation of player skill (by a human evaluator, for annotation) is through the technique required for the most difficult song they are able to play. In this way, song level generally indicates player skill.

## SLIDE 9: Mitigating small dataset size
This (i.e. training the data on clips instead of whole videos) would be necessary in any case (even for a larger dataset), since CNNs have difficulty processing long videos

## SLIDE 10: Sampling schemes
It is unfeasible to use all the clips of a performance for training, hence we sample some clips from the whole video. (a) Contiguous sampling scheme is wherein each sample gets a set of contiguous segments. (b) Uniformly distributed sampling scheme is wherein each sample gets uniformly-spaced segments from across the performance video.

## SLIDE 14: Visual branch - Network type used
_What can be learnt from visual analysis and how?_ The lack of certain skills would not give any indication as to the level of a pianist, but the presence of certain skills would immediately indicate a very high level of technical achievement. For example, professional pianists who must play at high speeds may play eight note intervals with their first and third fingers, which is incredibly difficult for the average pianist. To be able to take these into account, we need to process clips rather than single frames; hence, we need 3DCNN not 2DCNN.

## SLIDE 15: Visual branch - Feature processing method
Prior work in AQA has shown averaging to work well and it also enables end-to-end training. RNN based aggregation would not enable end-to-end training when used with 3DCNNs due to large number of parameters and consequent overfitting. Therefore, we choose to use averaging as our aggregation scheme to obtain whole sample-level video features from clip-level features.

## SLIDE 16: Aural branch - Network type used
_What can be learnt from auditory analysis?_ A significant amount of information can be detected from audio as well. The velocity of the music (notes per second) can be detected auditorily, which is a simple yet valuable tool to judge the technical skill required for a piece. The presence of multiple notes at once with cadences that correspond to cadences included in the grade level syllabi above would be recognizable both through auditory and visual analysis.

## SLIDE 18: Multimodal branch
Cross-modality contamination is the case wherein features processed from one mode of information affect the parameters used to process features from a different mode of information (aural features and their effect on the multimodal features may affect the parameters for processing features from the visual branch and vice versa). Each modality must be processed independently, due to separate properties and processing requirements!

## SLIDE 20: Objective function (considerations & components)…
KEY CONSIDERATION! Unlike a typical classification problem, in our player-level prediction problem, the distance between categories has meaning. For example, for a ground-truth player-level of 5, although predicted levels of 2 and 6 are both incorrect, a predicted level of 6 is “less wrong” than predicted level of 2.

**Precedent for using L1 distance**: <br> Paritosh Parmar and Brendan Tran Morris, “What and how well you performed? A multitask learning approach to action quality assessment,” in Proceedings of the IEEE Conference on Computer Vision and Pattern, Recognition, 2019, pp. 304–313.

## SLIDE 23: Experimentation questions
CV $\implies$ Computer Vision, ML $\implies$ Machine Learning.

## SLIDE 26: Implementation details for visual branch
Overfitting is a more significant danger due to the small dataset. Hence, they use a large dataset that is based on a similar domain (action recognition) as the one the visual branch is dealing with.

## SLIDE 27: Implementation details for aural branch
**ImageNet**:

The ImageNet project is a large visual database designed for use in visual object recognition software research. More than 14 million images have been hand-annotated by the project to indicate what objects are pictured and in at least one million of the images, bounding boxes are also provided. ImageNet contains more than 20,000 categories, with a typical category, such as "balloon" or "strawberry", consisting of several hundred images.

**ResNet**:

A residual neural network (ResNet) is an artificial neural network (ANN) that utilizes skip connections (shortcuts) to jump over some layers to help prevent overfitting. Typical ResNet models are implemented with double or triple layer skips that contain nonlinearities (ReLU) and batch normalization in between.

## SLIDE 30: Understanding the results
Trivial local or static cues refer to cues obtained by averaging consequent clips in some small time-interval, such as certain kinds of small movements (ex. flourishing motions), certain phrases, etc.

## SLIDE 33: Limitations
Distance is relevant! Better to mark 9 as 7 than 3.

---

# Preparation notes made before the presentation slides
## Driving questions
- Can a computer assess piano player's skill level?
- Visual analysis or auditory analysis? What about both?
- How to sample shorter clips to best reflect player performance
    -**CONTEXT**: Long videos are difficult for CNNs to process

## Key considerations for data & training
### Dataset
**NOTE**: _The dataset contains both visual and auditory data._

- Feature selection w.r.t. method of evaluation
- Data collection method
- Mitigation of small dataset size (as data collection method led to small dataset)
- Sampling schemes (both were used and compared to each other)
    - Uniform
    - Contiguous
     
**NOTE**: Sampling schemes relate to how clips must be sampled from longer videos to best reflect the player's performance. Relevant quote from the paper: <br> _"Since current CNNs have difficulty processing long [video] videos, how can shorter clips be sampled to best reflect the players skill level?"_

### Training
**NOTE**: _Consider the data representation and CNN structure used for each branch._

- Branches
    - Visual branch
    - Aural branch <br>**CONCEPTS TO LEARN**: _Averaging function_
    - Multimodal branch <br>**CONCEPTS TO LEARN**: _Cross-modality contamination_
- Objective function
    - Difference from usual classification problems
    - Defining distance component of the objective function
     
### Dataset details
Relevant quote: <br> _"In this paper, automated determination of piano playing skill level based on a 10 point scale using a new multimodal PIano Skills Assessment (PISA) dataset (Fig. 1) that accounts for both visual and auditory evidence."_

2 key attributes in PISA dataset: (1) player skill and (2) music difficulty

---

**QUESTION 1**: How are the above attributes measured?

**ANSWER 1**: <br>  (1) _"The primary evaluation of player skill is through the technique required for the most difficult song they are able to play. In this way, song level generally indicates player skill."_ The technique is graded based on skill-level as defined in the syllabus by Music Teachers National Association (MTNA). (2) _"The methodology for determining the song level (SL) of difficulty of a piano piece utilized multiple syllabi. A 10 point grading system was used for piece difficulty."_ As with player skill, music difficulty was graded based on the skill-level as defined in various syllabi; cross referrencing was done as needed.

---

**QUESTION 2**: How was the training and testing data acquired and annotated?

**ANSWER 2**: <br>  (1) Acquiring the data: _"We had to rely on a trained pianist to collect videos from YouTube, analyze them, and determine each player’s skill level (as described above). As such, scaling up the dataset is difficult. We collected a total of 61 total piano performances."_ <br> (2) Annotating the data: _"For each piano performance, we provide the following annotations: 1) player skill level; 2) song difficulty level; 3) name of the song; 4) a bounding box around the pianist’s hands"_ <br> (3) Delineating the testing and training data: _"Out of the 61 total piano performances, we use 31 (516 samples) as our training set and 30 (476 samples) as our test set. Note that no overlap exists between train and test sets."_

---

**QUESTION 3** (follow-up of previous): How was the small dataset size mitagated?

**ANSWER 3**: <br>  _"To mitigate small dataset size, we create multiple unique, non-overlapping samples, each of size of 16 frames. In this way, we have a total of 992 unique samples."_ Hence, they divide the videos into small, equally-sized clips; the model is to be trained not on whole videos but on clips. This would be necessary in any case (even for a larger dataset), since CNNs have difficulty processing long videos (however, for larger datasets, we may only take a few clips per video, rather than use the whole video).

---

**QUESTION 4**: How are the samples taken (relates to question 3)?

**ANSWER 4**: <br>  Samples are taken in 2 different ways (leading to 2 different use-cases): (a) contiguous sampling scheme and (b) uniformly distributed sampling scheme. A sampling scheme is a detailed description of what data will be obtained and how this will be done. Each performance - measured in frames - is divided into small, equally-sized segments (equally-sized means having the same number of frames). A sample is the set of segments considered as a whole (i.e. as a single input for the CNN). Sampling scheme, thus, defines the method by which the segments are picked for each sample. (a) Contiguous sampling scheme is wherein each sample gets a set of contiguous segments. (b) Uniformly distributed sampling scheme is wherein each sample gets uniformly-spaced segments from across the performance video.

> REFERENCE: (To understand what a sample scheme is) https://itl.nist.gov/div898/handbook/ppc/section3/ppc332.htm

**NOTE**: _The 2 different use-cases based on the 2 different sampling schemes are both explored and compared to each other in experimentation._

## Key considerations for experimentation
**Questions for experiments**:

- Is it possible to determine the pianist’s skill level using machine learning/computer vision?
- What is the better sampling strategy: contiguous or uniform distribution?
- Is a multimodal assessment better than a unimodal asssessment?
    - Hence, the paper involves both unimodal and multimodal approaches
