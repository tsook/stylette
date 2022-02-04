---
layout: default
---

## Abstract

Team members commonly collaborate on visual documents remotely and asynchronously. Particularly, students are frequently restricted to this setting as they often do not share work schedules or physical workspaces. As communication in this setting has delays and limits the main modality to text, members exert more effort to reference document objects and understand others' intentions. We propose <span style="color:{{site.syscolor}}">Winder</span>, a Figma plugin that addresses these challenges through *linked tapes*&mdash;multimodal comments of clicks and voice. Bidirectional links between the clicked-on objects and voice recordings facilitate understanding tapes: selecting objects retrieves relevant recordings, and playing recordings highlights related objects. By periodically prompting users to produce tapes, <span style="color:{{site.syscolor}}">Winder</span> preemptively obtains information to satisfy potential communication needs. Through a five-day study with eight teams of three, we evaluated the system's impact on teams asynchronously designing graphical user interfaces. Our findings revealed that producing linked tapes could be as lightweight as face-to-face (F2F) interactions while transmitting intentions more precisely than text. Furthermore, with preempted tapes, teammates coordinated tasks and invited members to build on each others' work.

------

## System

In <span style="color:{{site.syscolor}}">Winder</span>, users send *linked tapes*, which are recordings of their voice and clicks on objects on the UI design. The system generates bidirectional links between voice snippets and clicked-on objects to support navigation and understanding the receiver side.

The main components of the system's interface are (a) the top bar, (b) the list of linked tapes, and (c) the transcript space.

{: .sys-img}
![Winder next to the design for a screen of a mobile application](/assets/img/winder_main.png)

### Object Highlighting on Voice Playback

When the user plays a tape, <span style="color:{{site.syscolor}}">Winder</span> Winder displays the version of the document when the tape was recorded, and plays the voice audio while highlighting objects as they were clicked during recording.

{: .sys-img}
![An image of a salad in the UI design is highlighted while a recording appears to be playing in Winder.](/assets/img/winder_highlight.png)

### Inline Thumbnail Images on Voice Transcripts

{: .img-left}
![A transcript of a voice recording is shown with inline thumbnail images of UI design objects.](/assets/img/winder_transcript.png)

{: .text-right}
<span style="color:{{site.syscolor}}">Winder</span> provides automatic transcripts of the voice recordings (generated through speech-to-text). On the transcript, it embeds thumbnail images of the objects clicked during the recording inline with the words of the transcript.

### Object-based Search of Voice Recordings

If the user clicks on an object in the UI design, <span style="color:{{site.syscolor}}">Winder</span> retrieves all tapes in which that object was selected. For each tape, the segment of the tape’s transcript during which the object had been clicked on is shown.

{: .sys-img}
![A gray rectangle is clicked in the UI design. In Winder, a list of tapes shows a short snippets from transcripts and thumbnails of the gray rectangle.](/assets/img/winder_search.png)

------

## Results

Tapes recorded by participants in a five-day user study were analyzed and categorized. The results showed that participants used <span style="color:{{site.syscolor}}">Winder</span> for a variety of purposes&mdash;with most tapes used for "Describing" or "Justifying" design choices, or "Coordinating" work within a team.

{: .sys-img}
![Table showing descriptions and example snippets of each tape category. Additionally, the table shows the perentage of tapes that fit into that category.](/assets/img/results_type.png)

Participants mentioned how <span style="color:{{site.syscolor}}">Winder</span> increased their shared understanding, motivated them to work, and made them feel as if they were co-present.

{: .center .quote}
T2M1: *"The recordings left behind by my group members helped clarify some of the misunderstandings or confusions that I had."*

{: .center .quote}
T1M2: *"Understanding [my team members] actions and intentions was fun somehow and made me work harder."*

{: .center .quote}
T5M2: *"With the voice recordings and the feature that showed what the users clicked on as they talked, it was as if we were working together."*


------

## CHI 2021 Paper (Camera-ready)

[Link to the PDF][1]

## Bibtex
<pre>
@inproceedings{10.1145/3411764.3445686,
  author = {Kim, Tae Soo and Kim, Seungsu and Choi, Yoonseo and Kim, Juho},
  title = {Winder: Linking Speech and Visual Objects to Support Communication in Asynchronous Collaboration},
  year = {2021},
  isbn = {9781450380966},
  publisher = {Association for Computing Machinery},
  address = {New York, NY, USA},
  url = {https://doi.org/10.1145/3411764.3445686},
  doi = {10.1145/3411764.3445686},
  booktitle = {Proceedings of the 2021 CHI Conference on Human Factors in Computing Systems},
  pages = {1–17},
  numpages = {17},
  keywords = {Team Collaboration; Asynchronous Communication; Speech; Voice; Multimodal Input; Visual Document; User Interface Design},
  location = {Yokohama, Japan},
  series = {CHI ’21}
}
</pre>

------

{: .logos}
[![Logo of KIXLAB](/assets/img/kixlab_logo.png)](https://kixlab.org)
[![Logo of KAIST](/assets/img/kaist_logo.png)](https://kaist.ac.kr)

{: .center .acknowledgement}
This research was supported by the [KAIST](https://kaist.ac.kr) UP Program.


[1]:https://kixlab.github.io/website-files/2021/chi2021-Winder-paper.pdf
