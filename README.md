<div align="center">
      <h1> <img src="https://raw.githubusercontent.com/default-cybe/Fake-Profile-Detection-System-Using-ML-ANN/main/Logo/logo.png" width="80px"><br/>Fake Profile Detection System Using ML(ANN)</h1>
     </div>
<p align="center"> <a href="https://github.com/default-cybe" target="_blank"><img alt="" src="https://img.shields.io/badge/Website-EA4C89?style=normal&logo=dribbble&logoColor=white" style="vertical-align:center" /></a> <a href="https://twitter.com/default_yt_" target="_blank"><img alt="" src="https://img.shields.io/badge/Twitter-1DA1F2?style=normal&logo=twitter&logoColor=white" style="vertical-align:center" /></a> <a href="https://www.instagram.com/kaivalya_ahir" target="_blank"><img alt="" src="https://img.shields.io/badge/Instagram-E4405F?style=normal&logo=instagram&logoColor=white" style="vertical-align:center" /></a> <a href="https://www.linkedin.com/in/kaivalya-ahir/" target="_blank"><img alt="" src="https://img.shields.io/badge/LinkedIn-0077B5?style=normal&logo=linkedin&logoColor=white" style="vertical-align:center" /></a> </p>

# Description

A Django web app that flags likely-fake social media profiles using a small
neural network (ANN). You feed it a profile's public metrics (follower and
following counts, post count, whether it has a profile picture, that kind of
thing) and it tells you whether the account looks real or fake. It can pull
those numbers from a Twitter or Instagram username, or you can just type the
eight features in by hand.

# How it works

The model is a Keras/TensorFlow ANN trained on labelled profile data and saved
as `fpd/model.json` (architecture) + `fpd/model.h5` (weights). At request time
the app collects eight numeric features, feeds them to the network, and
thresholds the output at 0.5 to decide real vs. fake. See
[`MODEL.md`](MODEL.md) for the feature list.

- **Twitter**: pulls public metrics via the Twitter API v2 (`tweepy`).
- **Instagram**: pulls public metrics via `instaloader`.
- **Manual**: enter the eight features directly on the detect page.

# Tech used

![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54) ![TensorFlow](https://img.shields.io/badge/TensorFlow-%23FF6F00.svg?style=for-the-badge&logo=TensorFlow&logoColor=white) ![Keras](https://img.shields.io/badge/Keras-%23D00000.svg?style=for-the-badge&logo=Keras&logoColor=white) ![NumPy](https://img.shields.io/badge/numpy-%23013243.svg?style=for-the-badge&logo=numpy&logoColor=white) ![Django](https://img.shields.io/badge/django-%23092E20.svg?style=for-the-badge&logo=django&logoColor=white)

# Running locally

You need Python and (for the social lookups) a Twitter API bearer token and/or
Instagram credentials.

```bash
git clone https://github.com/default-cybe/Fake-Profile-Detection-System-Using-ML-ANN.git
cd Fake-Profile-Detection-System-Using-ML-ANN

python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt

cp .env.example .env            # then fill in your keys
export $(grep -v '^#' .env | xargs)   # load env vars (or use python-dotenv)

python manage.py migrate
python manage.py runserver
```

Open `http://127.0.0.1:8000/`.

# Configuration

All secrets are read from the environment, nothing is hardcoded. See
[`.env.example`](.env.example):

| Variable | Purpose |
|---|---|
| `DJANGO_SECRET_KEY` | Django secret key |
| `DJANGO_DEBUG` | `True`/`False` |
| `DJANGO_ALLOWED_HOSTS` | comma-separated hosts |
| `TWITTER_BEARER_TOKEN` | Twitter API v2 bearer token |
| `IG_USERNAME` / `IG_PASSWORD` | Instagram login (optional) |

# Notes

The social-media APIs used here change often; if a lookup fails, the manual
feature-entry path still works for demonstrating the model.
