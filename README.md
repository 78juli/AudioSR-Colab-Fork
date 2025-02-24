
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/78juli/AudioSR-Colab-Fork/blob/main/AudioSR_Colab_Fork.ipynb)

Edit:
Changed the Inference cell input to take many comma (and space) separated files to process one after the other





----------------------------------------------------------------------------------------------------------------------------------------------

#support the original project:
[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/Q5Q811R5YI)  
# AudioSR-Colab-Fork v0.5

Colab adaptation of AudioSR, with some tweaks:

v0.5
- input audio is resampled accordingly to 'input_cutoff' (instead of lowpass filtering)
- each processed chunk is normalised at same LUFS level than input chunk (fix the volume drop issue)

v0.4
- code rework, inference.py created for local CLI usage.

v0.3
- added : multiband ensemble option to use original audio below the given cutoff frequency and the generated audio above.
- fixed : other than .wav input error while saving the final audio

v0.2
- added a chunking feature to process input of any length
- added stereo handling, stereo input channels will be splitted and processed independantly (dual mono) and then reconstructed as stereo audio.
- added overlap feature to smooth the transitions between chunks (don't use high values because AudioSR is not 100% phase accurate and this will create weird phase cancellations accross the overlapping regions)

---
Local usage:
Install AudioSR and requirements/edited inference file:
```
git clone https://github.com/haoheliu/versatile_audio_super_resolution.git
cd versatile_audio_super_resolution
pip install cog huggingface_hub unidecode phonemizer einops torchlibrosa transformers ftfy timm librosa
pip install -r requirements.txt
wget https://raw.githubusercontent.com/jarredou/AudioSR-Colab-Fork/main/inference.py
```
CLI example
```
python inference.py --input "{input_file_path}" \
                    --output "{output_folder}" \
                    --ddim_steps 50 \
                    --guidance_scale 3.5 \
                    --seed 0 \
                    --chunk_size 10.24 \
                    --overlap 0.04 \
                    --multiband_ensemble True \
                    --input_cutoff 14000
```

---

Original work [AudioSR: Versatile Audio Super-resolution at Scale](https://github.com/haoheliu/versatile_audio_super_resolution) by Haohe Liu, Ke Chen, Qiao Tian, Wenwu Wang, Mark D. Plumbley
```
@article{liu2023audiosr,
  title={{AudioSR}: Versatile Audio Super-resolution at Scale},
  author={Liu, Haohe and Chen, Ke and Tian, Qiao and Wang, Wenwu and Plumbley, Mark D},
  journal={arXiv preprint arXiv:2309.07314},
  year={2023}
}
```
