# Remaking Hitchcock's 1963 film _The Birds_

🗂️ **Project Files: [[Google Drive Files for this Project](https://drive.google.com/drive/folders/1GDVN3x3jcEExj150KVBS02H0M8h5oB02?usp=drive_link)]**

This project is inspired by Joanna Zylinska's work [_The Gift of the World (Oedipus on the Jetty)_](https://www.nonhuman.photography/perception-machine), a remake of [_La Jetée_](https://www.youtube.com/watch?v=DQ4jFYTTjAU).

_La Jetée_ is a 1962 French science fiction featurette directed by Chris Marker and associated with the Left Bank artistic movement. Constructed almost entirely from still photos, it tells the stable time loop story of a post-nuclear war experiment in time travel. It is 28 minutes long and shot in black and white. [1] To create this work, Zylinska generated the new script by feeding selected lines from _La Jetée_'s original script to GPT-2, which took the film in an unexpected new direction by rewriting the very masculine story of salvation present in _La Jetée_ as a gender-fluid polyvocal counter-apocalypse.[2] To produce the film, she combined a variety of photorealistic AI models such as GANs, Diffusion, and CLIP. [3]

![Zylinska (2023), Composite of frames from A Gift of the World (Oedipus on the Jetty), [Photofilm, 2021]. © Zylinska, 2023 (Cortesía de la Autora)](Zylinska-2023-Composite-of-frames-from-A-Gift-of-the-World-Oedipus-on-the-Jetty.png)
Zylinska (2023), Composite of frames from A Gift of the World (Oedipus on the Jetty), [Photofilm, 2021]. © Zylinska, 2023 (Cortesía de la Autora) [4]

For Zylinska, the editing process was intuitive and consisted of her own visual and corporeal responses to both the script and the GAN images, which she references as a dream-like state, where neural networks find patterns in images not so much in a logical preprogrammed way but rather by using previous data and memories as prompts for making new connections between data points and for generating new data. In this work, she finds herself dreaming _with_ but also _against_ the AI algorithm underpinning the model. The "counterdream" aspect was critical given the sociopolitical limitations of AI technology, which have been well documented by feminist and decolonial cultural critics, revealing not only gender and racial bias but also the exclusionary and unjust logic underlying many of its founding principles. Not to mention its extractivism when it comes to both human and natural resources. Zylinska was curious about what AI would do to the source material, while intentionally serving as both a dream catcher and analyst in the creation process. [5]

When I came across Zylinska's project, I thought it was interesting how GPT-2 flipped the gender narrative of the original film, which shifted the premise of the film dramatically. The abstract images created by StyleGAN was also very interesting. Human faces were re-interpreted with these kidneys-liked eyees. Inspired by this, I chose to experiment with Hitchcock's _The Birds_, a film from a similar era with a male-centric storyline lacking female perspectives, perpetuating sexist stereotypes, and depicting violence against women. I also wanted to see if any biases would be reflected in the AI-generated outcomes.

## Approach & Process

### Text Generation
🗂️ **Project Files: [[Google Colab Notebook 01_new_script_generation](https://colab.research.google.com/drive/10OAtNJP5Rr8oz06NzSipFfAx3OBJ-5w7?authuser=1#scrollTo=GpisUfhuJli_)] | [[Google Colab Notebook 02_new_script_genreation_by_finetuning](https://drive.google.com/file/d/1KpFxMCUrMBQ0LSmCBP6Ko_5EnITU4CkA/view?usp=sharing)]
🤖 **Model used:**

For this part of the project, I adapted the Class 5 notebooks to create, prepare a new dataset and generate a new script. 

I first created a dataset by taking [the original 1962 film script] (http://www.script-o-rama.com/movie_scripts/b/the-birds-script-screenplay.html) and adapted the class notebook. 

With the code from the class notebook, a separate tokenization was not needed, but since I was curious about the tokenization process, I tokenized the film script using [Andrej Karpathy's minibpe repo](https://github.com/karpathy/minbpe). Here is the [[output](https://drive.google.com/drive/folders/1jCvXqMzpysmWJ-UuEMF0c4-JZHcbfewu?usp=drive_link)] from the tokenizer process, and here is the [[Google Colab notebook 00_tokenize_script](https://drive.google.com/file/d/1pWiDtswiTl1T_0vfRmgdLPGf84bn4ucg/view?usp=drive_link)].

## Generating a new short film based on the scripts generated

Prior to this step, I used the Class 5 Notebook codes to created a dataset based on Hitchcock's 1962 film _The Birds_ and to generate four versions of scripts by finetuning the GPT2 model (files `output_GPT2_v3` through `v6`).

Then, I collated the four versions into one PDF and asked ChatGPT 4o to generate a new script:

"The PDF contains a few different versions of a short film draft. Please clean up this short film draft and rewrite it to make it coherent for today's audience."

After the initial generation, I asked GPT4o to elaborate further:

"This is very intriguing, can you keep writing?"

The final draft of the film script can be found in the  `output_scripts` folder >> `final_script_generated_by_gpt4o`

Here, I tried setting up the [StyleGAN-T model] (https://github.com/autonomousvision/stylegan-t) to generate a new short film but failed because of package conflicts.

### StyleGAN-T Genereation
🗂️ **Project File: [Google Colab Notebook 03 (https://colab.research.google.com/drive/1ntrxQQxkczMidhcOKD5hhbnj5KnA4sod?usp=sharing)]**
🤖 **Model used:**

Here, I tried to run the generated script through the [StyleGAN-T](https://github.com/autonomousvision/stylegan-t/blob/main/README.md) model, which combines transformers with StyleGAN. However, I ran into a lot of issues with dependencies and packages conflicts. After 2+ hours of debugging and trying various ways of installing different packages, I decided to try other methods. 

### CLIP Text Encoding
🗂️ **Project Files:**
🤖 **Model used: [CLIP (https://github.com/openai/CLIP)]**



### CLIP-Guided Diffusion
🗂️ **Project Files:**
🤖 **Model used: [[CLIP-Guided Diffusion by EleutherAI](https://www.eleuther.ai/artifacts/clip-guided-diffusion)]**

I had a lot of issues locating the latent vector to map my text encoding from CLIP to StyleGAN2's latent space due to dependencies being updated and becoming conflicted with each other. After researching, I found the CLIP-Guided Diffusion model by EleutherAI to successfully generate images with text prompts. 

This particular model is adapted from [Katherine Crowson(https://twitter.com/RiversHaveWings)]'s [work (https://github.com/crowsonkb/clip-guided-diffusion)]. It uses [OpenAI's 256x256 unconditional ImageNet diffusion model (https://github.com/openai/guided-diffusion)] together with [CLIP (https://github.com/openai/CLIP)] to connect text prompts with images. 

### Image Interpolation
🗂️ **Project Files:**

Each image takes about 9 minutes to generate. In the interest of on-time delivery of this project, I generated the first scene (first 10 prompts) of the script and interpolated the 10 images by adapting the code from the Class 7 notebook.

Full list of prompts: https://docs.google.com/document/d/1CxwlhFuR-utL1xmJVt2GeadrJO1squYzX-DkUVv6Cv0/edit?usp=sharing 

## Results & Evaluation

# Bibliography
1. La Jetée. (2024, June 6). In Wikipedia. https://en.wikipedia.org/wiki/La_Jet%C3%A9e
2. Talking to Joanna Zylinska. Artificial intelligence in artistic creation., Jose Vertedor, December 2023 - Umática. Revista sobre Creación y Análisis de la Imagen.
3. The Perception Machine, Joanna Zylinska, 2023, page 136 - Massachusetts Institute of Technology.
4. Vertedor-Romero, J.A.. (2023). Editorial. AI-driven art: la inteligencia artificial en el arte y el diseño. UMÁTICA. Revista sobre Creación y Análisis de la Imagen. 9-20. 10.24310/umatica.2023.v5i6.18315. 
5. The Perception Machine, Joanna Zylinska, 2023, page 139-140 - Massachusetts Institute of Technology.
