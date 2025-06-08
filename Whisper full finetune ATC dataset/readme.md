!pip install datasets>=2.6.1
!pip install librosa
!pip install evaluate>=0.30
!pip install jiwer
pip uninstall torch torchvision torchaudio -y
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
pip install torchvision
pip install torch
pip install transformers


Finetuning of all parameters of Whisper using an application specific dataset (Air traffic control- ATC)
