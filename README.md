# face-recog-experiments repo.

To install requirements to run notebook demo_notebook.ipynb:
pip install -r requirements.txt

Install Openface manually: https://cmusatyalab.github.io/openface/setup/

Steps to train face recognition on new people:
Pull the docker container
1) docker pull bamos/openface
2) Make volume mount to keep training images
3) docker run -v /home/shrutigupta/Documents/face-recog-experiments/data_images:/root/openface/training-images -p 9001:9000 -p 8000:8000 -t -i bamos/openface /bin/bash
4) cd /root/openface/
5) ls training-images/
6) ./util/align-dlib.py ./training-images/ align outerEyesAndNose ./aligned-images/ --size 96
7) ./batch-represent/main.lua -outDir ./generated-embeddings/ -data ./aligned-images/
8) ./demos/classifier.py train ./generated-embeddings/
9) ./demos/classifier.py infer ./generated-embeddings/classifier.pkl ./training-images/ayushman/ayush19.jpg

References:
Side-Profile-Detection: https://github.com/nawafalageel/Side-Profile-Detection
Face-Matching: https://github.com/ageitgey/face_recognition
