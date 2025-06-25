# **Approach, Techniques & Challenges**

This project focuses on player re-identification and tracking in soccer videos using object detection and multi-object tracking (MOT) techniques.

---

## **🛠 Methods & Techniques Explored**

### 1. **YOLOv11 for Object Detection**

* Utilized a fine-tuned version of **Ultralytics YOLOv11** to detect players and the ball in each frame.
* Chosen for its real-time performance and reliable detection accuracy.

### 2. **Multi-Object Tracking (MOT) Algorithms Tried**

I experimented with several popular tracking methods to achieve consistent player ID assignment:

| Method         | Outcome/Reason for Rejection                                                                                                             |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| **SORT**       | Simple and fast, but struggled with ID consistency when players re-enter the frame after occlusion or going out of view.                 |
| **Deep SORT**  | Introduced appearance features but still produced inconsistent tracking, especially during complex scenes.                               |
| **BoT-SORT**   | Improvement over SORT by adding Re-ID logic, but initial tuning was tricky and results were unstable without adjustments.                |
| **ByteTrack**  | Known for handling crowded scenes, but tracking IDs fluctuated significantly due to limited frame-to-frame association in this scenario. |
| **Fast Track** | Fast but compromised tracking stability and was unsuitable for the re-identification requirement of this task.                           |

---

## **💡 Final Working Solution**

After evaluating various techniques, I implemented the solution using **BoT-SORT**, which provided:

✅ Better ID consistency for players re-entering the frame.
✅ Real-time tracking performance compatible with YOLOv11.
✅ Simulated realistic re-identification without the need for paid Re-ID APIs.

---

## **⚠️ Limitations & Challenges**

* I **do not have access to paid Re-ID APIs or proprietary models**, which limited the re-identification capabilities to freely available trackers.
* Some advanced Re-ID models (e.g., OSNet) were considered, but setting up reliable pipelines within time and resource constraints was not feasible.
* Tracking in high-occlusion or player-overlapping scenarios remains challenging with the current setup.

---

## **✅ Conclusion**

Despite these challenges, I successfully implemented a working re-identification and tracking pipeline using:

* **YOLOv11 for detection**
* **BoT-SORT for tracking & re-identification**
