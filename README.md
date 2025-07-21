ShotSense: Real-Time Basketball Feedback with Gemini & OpenCV

This project uses MediaPipe, OpenCV, and Gemini AI to analyze basketball videos and provide real-time, shot-by-shot feedback on jump shots, layups, and 3-pointers.

WHAT IT DOES:

Detects and tracks the basketball player using MediaPipe Pose

Reads structured shot feedback data from ball.json

Displays:

Player tracking arrow and name

Shot statistics (made/missed)

Coaching feedback like a real trainer

Outputs a high-resolution annotated video

Example feedback:
"You're pushing that ball, not shooting it — get your elbow under, extend fully, and follow through."

HOW IT WORKS:

final_ball.mov: used for fast pose tracking (low resolution)

final_ball.mp4: used for high-quality visual overlays

ball.json: contains all shot data (timestamp, type, result, feedback)

ball.py: core processor and visualizer

final.mp4: output video with overlays and annotations

FILES:

ball.json: Shot metadata and Gemini feedback

ball.py: Main script that overlays visual feedback

final_ball.mov: Low-res input video for pose detection

final_ball.mp4: High-res input video for display and export

final.mp4: Output video with annotations

.env (optional): Store your Gemini API key securely

HOW TO RUN:

Install dependencies:
pip install opencv-python mediapipe numpy python-dotenv google-generativeai

Make sure the following files are in the same folder:

ball.json

final_ball.mov

final_ball.mp4

Run the script:
python ball.py

The final video will be saved as final.mp4

EXAMPLE ball.json FORMAT:
{
"shots": [
{
"timestamp_of_outcome": "0:07.5",
"result": "missed",
"shot_type": "Jump shot (around free-throw line)",
"feedback": "You're pushing that ball, not shooting it...",
"total_shots_made_so_far": 0,
"total_shots_missed_so_far": 1,
"total_layups_made_so_far": 0
}
]
}

REAL-TIME GEMINI INTEGRATION (OPTIONAL):
To make it work live:

Use cv2 to grab 1 frame per second

Send the image to Gemini using the Vision API

Prompt:
"You are a basketball coach. Analyze this image and return JSON: {timestamp, result, shot_type, feedback}"

Append Gemini’s JSON output to shot_data['shots']

Use existing rendering logic to overlay feedback in real-time

ENV SETUP (OPTIONAL):
Create a .env file to store your Gemini API key:
GOOGLE_API_KEY=your_gemini_key

Then in Python:
from dotenv import load_dotenv
load_dotenv()
api_key = os.getenv("GOOGLE_API_KEY")

FFMPEG TIP:
If you only have final_ball.mp4, you can generate final_ball.mov using:
ffmpeg -i final_ball.mp4 -vf scale=640:-1 final_ball.mov

FUTURE IOS APP IDEA:
This system can evolve into a real-time mobile coaching app that:

Uses the iPhone camera to track shots

Sends video frames to Gemini AI

Gives real-time, coach-style feedback

Generates highlight reels with auto-edited overlays

CREDITS:

Gemini by Google for AI feedback

MediaPipe for pose tracking

OpenCV for visual rendering

Inspired by @FarzaTV’s Gemini + basketball demo on Twitter/X

