---
layout: default
---

## Abstract

End-users can potentially style and customize websites by editing them through in-browser developer tools. Unfortunately, end-users lack the knowledge needed to translate high-level styling goals into low-level code edits. We present <span style="color:{{site.syscolor}}">Stylette</span>, a browser extension that enables users to change the style of websites by expressing goals in natural language. By interpreting the user’s goal with a large language model and extracting suggestions from our dataset of 1.7 million web components, <span style="color:{{site.syscolor}}">Stylette</span> generates a palette of CSS properties and values that the user can apply to reach their goal. A comparative study (N=40) showed that <span style="color:{{site.syscolor}}">Stylette</span> lowered the learning curve, helping participants perform styling changes 35% faster than those using developer tools. By presenting various alternatives for a single goal, the tool helped participants familiarize themselves with CSS through experimentation. Beyond CSS, our work can be expanded to help novices quickly grasp complex software or programming languages.

------

## System

<span style="color:{{site.syscolor}}">Stylette</span> enables end-users to change the visual design of any website by simply clicking on a component and saying what change they want to see. The system interprets the user’s natural language request <span style="color:#0075b9">**(b)**</span> and clicked component <span style="color:#0075b9">**(a)**</span> to present a *palette* <span style="color:#0075b9">**(c)**</span> that consists of multiple CSS properties that could be changed to satisfy the request and various suggestions extracted from a large-scale dataset. <span style="color:{{site.syscolor}}">Stylette</span> is implemented as a Chrome Extension.

{: .sys-img}
![Figure shows that the user has selected the a subtitle in the CHI 2022 website and, underneath the subtitle, it shows hovering Stylette. Stylette shows a the transcription box with the text "tone down the text" and the style palette underneath the transcription box. The style palette is described further in Figure 3.](/assets/img/system.png)

### Palette

{: .img-left}
![The style palette shows different properties as columns and different value suggestions for each property as rows within each column.](/assets/img/palette.png)

{: .text-right}
For each property, the *palettes* presents: <br/><br/>
<span style="color:#0075b9">**(a)**</span> The current value. <br/>
<span style="color:#0075b9">**(b)**</span> The default or original value before any changes. <br/>
<span style="color:#0075b9">**(c)**</span> A list of suggested values. <br/> 
<span style="color:#0075b9">**(d)**</span> For numerical values, suggested values that are either larger or smaller than the current value based on the system's prediction.<br/>
<span style="color:#0075b9">**(e)**</span> Arrows next to a suggested value to see other similar suggestions. <br/>
<span style="color:#0075b9">**(f)**</span> If the user clicks on the "+" button, more suggestions are shown.<br/>
<span style="color:#0075b9">**(g)**</span> If the user clicks on the current value, widgets are revealed for the user to manually set values.

------

## Pipeline

We present a computational pipeline that processes the two input modalities, <span style="color:#f17104">voice</span> and <span style="color:#00a1ff">click</span>, to generate the *palettes*.

{: .sys-img}
![Diagram of the computational pipeline shows on the left a user making a voice request and clicking on a web component. On the top, it shows how the voice request is processed by transcribing with Google Cloud Speech-to-Text, concatenated with pseudo-tokens, inputted into GPT-Neo with Trained P-Tuning to finally generate and extract predicted CSS properties and change direction. On the bottom, it show how the component clicked by the user is captured and then inputted to a Variational Autoencoder model to extract an embedding vector. This embedding vector is then compared with cosine similarity to other embeddings in the Web Component dataset to identify the property values of similar components from which values are grouped and sampled to provide suggestions to the user.](/assets/img/pipeline.png)

<div class="md-div text-left" style="vertical-align: top">
  <span style="color:#f17104"><b>NLP Pipeline</b></span><br/><br/>
  <b>Architecture</b><br/>
  <ol>
   <li>Transcribe request using an STT API.</li>
   <li>Concatenate with pseudo-tokens. </li>
   <li>Input to GPT-Neo model to generate CSS properties.</li>
   <li>Concatenate remaining pseudo-tokens. </li>
   <li>Input to GPT-Model to generate change direction.</li>
   <li>Extract direction and CSS properties.</li>
  </ol>
  <b>Dataset</b><br/>
  <ul>
    <li>300 triplets of vague natural language requests, CSS property sets, and change directions.  </li>
    <li>Manually crafted and automatically augmented. </li>
    <li>Used to train the pseudo-tokens for the P-Tuning technique.</li>
  </ul>
</div>

<div class="md-div text-right" style="vertical-align: top">
  <span style="color:#00a1ff"><b>CV Pipeline</b></span><br/><br/>
  <b>Architecture</b><br/>
  <ol>
   <li>Screenshot the clicked component. </li>
   <li>Input to trained VAE model to encode the screenshot as a 512-dimensional vector. </li>
   <li>Compare vector to the vector representations of all components in dataset.</li>
   <li>Extract CSS property values of most similar components in dataset. </li>
   <li>Group values and sample values from the groups.</li>
  </ol>
  <b>Dataset</b><br/>
  <ul>
    <li>1.7 million components, includes their CSS properties and screenshot image. </li>
    <li>Automatically extracted from 7,565 websites. </li>
    <li>Used to train the VAE model and to extract CSS value suggestions.</li>
  </ul>
</div>

------

## Results

Through a between-subjects study (N=40), we compared <span style="color:{{site.syscolor}}">Stylette</span> to Chrome DevTools through two tasks: (1) a well-defined task and (2) an open-ended task.

{: .img-left}
![Bar chart on the left shows that the self-confidence of Stylette participants initially increased, but decreased later during the study. Bar chart on the right shows that self-confidence of DevTools participants increased initially and also slightly increased later in the study. Specific self-confidence ratings are included in the text.](/assets/img/comprehensive.png)

{: .text-right}
Self-confidence increased significantly after Task 1 for both conditions. But, self-confidence decreased significantly only for <span style="color:{{site.syscolor}}">Stylette</span> participants after Task 2.<br/><br/>
The study revealed that <span style="color:{{site.syscolor}}">Stylette</span>'s interpretation of users' vague requests could help them quickly learn how to use CSS. Once users had acquired the knowledge, however, ML-related flaws could significantly limit their interactions. 


------

## CHI 2022 Paper &nbsp;&nbsp;<span style="background-color:{{site.syscolor}}33; padding: 4px 0; border-radius: 8px">&nbsp;<i class="fa-solid fa-medal" style="margin-right: 4px"></i>Honorable Mention Award&nbsp;</span>

[Camera-ready PDF][1]

## Bibtex
<pre>
@inproceedings{10.1145/3491102.3501931,
  author = {Kim, Tae Soo and Choi, DaEun and Choi, Yoonseo and Kim, Juho},
  title = {Stylette: Styling the Web with Natural Language},
  year = {2022},
  isbn = {9781450391573},
  publisher = {Association for Computing Machinery},
  address = {New York, NY, USA},
  url = {https://doi.org/10.1145/3491102.3501931},
  doi = {10.1145/3491102.3501931},
  booktitle = {Proceedings of the 2022 CHI Conference on Human Factors in Computing Systems},
  numpages = {17},
  keywords = {Web Design; Natural Language Interface; End-User Programming; Machine Learning},
  location = {New Orleans, LA, USA},
  series = {CHI '22}
}
</pre>

------

{: .logos}
[![Logo of KIXLAB](/assets/img/kixlab_logo.png)](https://kixlab.org)
[![Logo of KAIST](/assets/img/kaist_logo.png)](https://kaist.ac.kr)

{: .center .acknowledgement}
This work was supported by IITP grant funded by the Korea government (MSIT) and the KAIST-NAVER Hypercreative AI Center.


[1]:https://kixlab.github.io/website-files/2022/chi2022-stylette-paper.pdf
