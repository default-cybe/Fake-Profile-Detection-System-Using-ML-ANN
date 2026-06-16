# Model

The classifier is a feed-forward neural network (Keras / TensorFlow) trained on
labelled social-media profiles. The trained model is stored as:

- `fpd/model.json`: the network architecture
- `fpd/model.h5`: the trained weights

## Input features

The network takes eight numeric features per profile:

| # | Feature | Description |
|---|---------|-------------|
| 1 | `status` | number of posts / tweets |
| 2 | `followers` | follower count |
| 3 | `friends` | following count |
| 4 | `fav` | favourites / pinned-content signal |
| 5 | `lang_num` | language indicator |
| 6 | `listed_count` | number of lists the account appears on |
| 7 | `geo` | whether the profile exposes a location (0/1) |
| 8 | `pic` | whether the profile has a non-default picture (0/1) |

## Output

A single value in `[0, 1]`, thresholded at `0.5`: `>= 0.5` → fake, otherwise
real.
