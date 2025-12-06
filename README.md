# video_frames_sorting
This is a repository to sort video frames based on SIFT descriptors.

The main steps for reconstructing the video are:
- **Features extraction:**

For each frame, features are extracted using SIFT descriptors. Frames may be resized beforehand to accelerate this step. SIFT descriptors are invariant to rotation, scale, and translation, allowing features to be detected even when objects move or the camera viewpoint changes.

- **Computing similarity features between frames:**

Using the extracted features, a similarity score is computed to identify the most likely neighboring frames.
First, the number of matching SIFT descriptors between two frames is determined. This is an important criterion, as frames containing the same objects typically share many common features.
However, the number of shared features alone is not sufficient. To refine the similarity measure, we also compute the median displacement of the matched features. Smaller displacements increase the likelihood that the frames are true neighbors.

- **Frames sorting and filtering:**

Based on the similarity scores, an algorithm is used to reorder the frames.
Starting from a randomly selected frame, we iteratively append its most similar neighbor to build a sequence. When we encounter a frame that is more similar to the first frame of the sequence than to the last, we assume we have reached one end of the original video. At that point, we reverse direction and begin adding frames to the front of the sequence instead of the back.
