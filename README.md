# 🎨🤖 Image Generation Pipeline with Streamlit

This project is an implementation and submission of an AI-based image processing pipeline utilizing **Stable Diffusion**, ranging from Jupyter Notebook-based experiments to interactive web interface deployment using **Streamlit** and **Ngrok**.

---

## 📺 Demo Video
[![Watch the video](https://img.youtube.com/vi/NjAjpmqKMAU/hqdefault.jpg)](https://youtu.be/NjAjpmqKMAU)

---

## ✨ 1. Key Project Features

* **Text-to-Image Generation:** Generates high-quality images from text prompts using Stable Diffusion v1.5.
* **Hyperparameter & Scheduler Tuning:** Experiments and comparisons of *Guidance Scale (CFG)*, *Inference Steps*, and *Schedulers* (Euler A, DPM++, DDIM).
* **Image-to-Image (Inpainting & Outpainting):** Refining, modifying specific areas (*Manual & Automasking* using CLIPSeg), and expanding image canvases (*Zoom-Out Outpainting*).
* **Base + Refiner Pipeline:** Enhances final image detail output.
* **Interactive Web App (Streamlit):** Web-based user interface featuring *Tab Generation* and *Tab Edit*, GPU memory management, and instant public publishing support using Ngrok.

---

## 🛠️ 2. Dependencies & Installation

## **A. Pipeline Notebook**
```bash
!pip uninstall -y torchao
!pip install -q --upgrade diffusers transformers accelerate
!pip install -q "pillow<11.0.0"
!pip install -q "torch>=2.4.1" "torchvision>=0.19.1" "diffusers>=0.31.0" "transformers>=4.45.0" accelerate --force-reinstall
```


## **B. Streamlit & Web App Dependencies**

```bash
!pip install -q pyngrok
!pip install -q streamlit
!pip install -q torch
!pip install -q diffusers
!pip install -q transformers
!pip install -q streamlit-drawable-canvas==0.8.0

```

---

## 🧠 3. Core Logic (`logic.py`)

The core operation module of the model includes cached model loading, GPU memory management (`flush_memory`), scheduler configuration, and Inpainting and Outpainting processing functions:

* **Model Loader:** Loads `stable-diffusion-v1-5` (Text-to-Image) and `stable-diffusion-inpainting` (Inpainting/Outpainting) to the GPU device (`cuda`).


* **Scheduler Options:** Supports `Euler A`, `DPM++`, and `DDIM`.


* **Inpainting & Outpainting Pipeline:** Manages image masking areas, multiple-of-8 resolution adjustments, and Background Blur effects for outpainting.



---

## 💻 4. Running the Streamlit Application (`app.py`)

The Streamlit app is designed with Sidebar Controls to configure generation parameters and interactive tabs for generating and editing:

* **Parameters Sidebar:**
* **Quality Steps:** Slider (15 - 50 steps).


* **Creativity (CFG):** Slider (1.0 - 20.0).


* **Seed Control:** Numeric input for reproducibility.


* **Scheduler & Batch Size:** Selection of scheduler methods and batch image count (1 - 4).




* **Generation Tab (`tab_gen`):**
* Enter *Prompt* and *Negative Prompt*.


* Click **Initialize Generation** to process and display the image grid results.




* **Edit Tab (`tab_edit`):**
* **Inpainting (Edit Object):** Scribble/draw a mask on specific areas, then enter a *New Prompt* and modification *Strength*.


* **Outpainting (Zoom Out):** Automatically expands the canvas to add a new background using prompt descriptions.





---

## 🌐 5. Deployment Using Ngrok

To run and publish the Streamlit application publicly locally/in Colab using Ngrok:

```python
from pyngrok import ngrok
import subprocess

auth_token = "YOUR_NGROK_AUTH_TOKEN"
ngrok.set_auth_token(auth_token)
subprocess.Popen(["streamlit", "run", "app.py"])

public_url = ngrok.connect(8501).public_url
print(public_url)

```

---



