# VoiceStar: Robust, Duration-controllable TTS that can Extrapolate

## 1. Env setup
### Download models
#### Linux
```bash
# under VoiceStar root dir
wget -O ./pretrained/encodec_6f79c6a8.th https://huggingface.co/pyp1/Encodec_VoiceStar/resolve/main/encodec_4cb2048_giga.th?download=true
wget -O ./pretrained/VoiceStar_840M_30s.pth https://huggingface.co/pyp1/VoiceStar/resolve/main/VoiceStar_840M_30s.pth?download=true
wget -O ./pretrained/VoiceStar_840M_40s.pth https://huggingface.co/pyp1/VoiceStar/resolve/main/VoiceStar_840M_40s.pth?download=true
```

#### Windows
```bash
# under VoiceStar root dir
curl -O ./pretrained/encodec_6f79c6a8.th https://huggingface.co/pyp1/Encodec_VoiceStar/resolve/main/encodec_4cb2048_giga.th?download=true
curl -O ./pretrained/VoiceStar_840M_30s.pth https://huggingface.co/pyp1/VoiceStar/resolve/main/VoiceStar_840M_30s.pth?download=true
curl -O ./pretrained/VoiceStar_840M_40s.pth https://huggingface.co/pyp1/VoiceStar/resolve/main/VoiceStar_840M_40s.pth?download=true
```
Or manually download encodec here: https://huggingface.co/pyp1/Encodec_VoiceStar/blob/main/encodec_4cb2048_giga.th and VoiceStar weights here https://huggingface.co/pyp1/VoiceStar/tree/main.  Place them into the `pretrained` folder

### Env Setup:
Highly recommend you use `uv` to set this repository up. It handles package dependencies etc all for you. You do need python on your computer first for pip but afterwards you can use uv
```bash
# The following is needed so torch index doesn't mess things up: --index-strategy unsafe-best-match 
pip install uv
uv sync --index-strategy unsafe-best-match
```

* avoid warnings likes
[WARNING] words_mismatch.py:88 || words count mismatch on 200.0% of the lines (2/1)
```python
# go to .venv/Lib/site-packages/phonemizer/backend/espeak/words_mismatch.py
# pass the warning like this
    def _resume(self, nmismatch: int, nlines: int):
        """Logs a high level undetailed warning"""
        pass
        # if nmismatch:
        #     self._logger.warning(
        #         'words count mismatch on %s%% of the lines (%s/%s)',
        #         round(nmismatch / nlines, 2) * 100, nmismatch, nlines)
```

## 2. Inference
### command line example
check signature of `run_inference` func in `inference_commandline.py` for adjustable hyperparameters
```bash
# under root dir
uv run inference_commandline.py `
  --reference_speech "./demo/5895_34622_000026_000002.wav" `
  --target_text "I cannot believe that the same model can also do text to speech synthesis too! And you know what? this audio is 8 seconds long." `
  --target_duration 8
```

### Gradio
```bash
uv run inference_gradio.py
```

## License
Code license: MIT

Model Weights License: CC-BY-4.0 (as Emilia dataset we used is under this license)

This is a fork of https://github.com/jasonppy/VoiceStar