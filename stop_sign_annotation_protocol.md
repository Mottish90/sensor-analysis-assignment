

**One quick note before getting into the instructions themselves:**  
 If it were up to me, I would have trimmed the videos and shared only the *relevant* subclips with the annotation team — for example, a short clip showing the entire approach to each stop sign, including the car reaching the sign and entering the junction.

As it stands, I’ll write the instructions based on the full videos provided in the assignment, without modifying the data.

*For instance, the video `893f22ef-668d-40c3-8715-7b92ab8d952a.mp4` doesn’t seem helpful here, since the collision kind of ruins the point of this training.*

**Detailed Annotation Instructions**

### **1\. Clip-Level Information**

For each video clip, provide the following:

* **Clip name(str)** – the name of the video file.

* **Time of day(str)** – either `Day` or `Night`.

* **Weather(str)** – labeled as `Clear` if the weather conditions are good and visibility is not affected. Otherwise, use `Not clear` (e.g., rain, fog, glare).

---

### **2\. Stop Sign Encounter-Level Information**

These annotations should be made for every relevant stop sign encounter **in the clip** (there may be multiple per clip). An encounter is considered relevant **only if the ego car reaches and enters the junction area**. If the car doesn’t enter the junction, skip the encounter.

#### **Frame Range(int)**

* **Start Frame** – the frame in which the stop sign becomes clearly visible.

* **End Frame** – the frame in which the ego vehicle is still within the junction.

  * *If the vehicle doesn't enter the junction (e.g., due to a collision), skip this annotation.*

#### **Behavior(str)**

Label the driver’s behavior when approaching the stop sign with one of the following:

* **Full stop** – the vehicle stops completely in a safe position before entering the junction.

* **Late full stop** – the vehicle does come to a full stop, but too close to or inside the junction, creating risk.

* **Near full stop** – the driver significantly slows down, but doesn’t come to a full stop.

* **Risky approach** – the driver barely slows down or doesn’t slow down at all before entering the junction.

#### **Vehicles in Junction(boolean)**

Indicate whether other vehicles are present or approaching the junction area (excluding the ego vehicle):

* **True** – at least one other vehicle is approaching or already inside the junction.

* **False** – the ego car is the only vehicle interacting with the junction.

#### **Driving Direction(str)**

Specify the movement of the driver as it exits the junction:

* **Left** – the vehicle turns left.

* **Right** – the vehicle turns right.

* **Straight** – the vehicle continues straight through the junction.

#### **Road Connection Type(str)**

Specify the types of the road the ego vehicle is coming from and the perpendicular road it crosses or enters when going straight or turning.

* **One-way to one-way**

* **One-way to two-way**

* **Two-way to one-way**

* **Two-way to two-way**

**Annotation file example:**

All options written above should be lower case and use ‘\_’ instead of spaces.  
In the following only one relevant encounter was found.

{  
‘clip\_name’: ’893f22ef-668d-40c3-8715-7b92ab8d952a.mp4’, ‘tod’: ‘day’,   
‘weather’: ‘not\_clear’,  
‘encounters’: {‘1’: {‘start’: 200, ‘end’: 350, ‘behaviour’: ‘near\_full\_stop’,                             \_\_\_\_\_\_\_\_\_\_\_\_\_\_ ’vehichles\_in\_junction’: False, ‘driving\_direction’: ‘straight’,      
                             ‘road\_connection\_type’: ‘2way\_to\_2way’  
					   }  
					   }   
}

For any questions please feel comfortable to reach out.  
Thanks a lot in advance.

**Assumptions and other Issues:**

One important assumption I made is that the data comes from a right-hand traffic country (where vehicles drive on the right side of the road). If we want to make the labeling more general and applicable across regions, we could redefine the **driving direction** labels as:

* **Simple** — a turn that crosses the least number of lanes (e.g., right turn in right-hand traffic, left turn in left-hand traffic).

* **Complex** — a turn that crosses multiple lanes (e.g., left turn in right-hand traffic, right turn in left-hand traffic).

* **Straight** — continuing forward through the intersection.

This approach removes the dependency on local traffic orientation and makes the annotation schema more universal.

Another thing I’ve been thinking about is the weather label — I’m not sure how relevant it really is, or if *“Clear”* vs *“Not clear”* gives enough detail. It might help to define what exactly counts as *“Not clear”* and whether it impacts the results.

Of course, with a task like labeling behavior, there’s always some room for interpretation. For example, what counts as “risky.” I did my best to explain everything as clearly and specifically as possible to reduce any ambiguity.

**Short Explanation of my Work:**

I did my best to consider the factors that might influence a driver’s behavior when approaching a stop sign. I believe the categories I chose are fairly self-explanatory, and I think there’s real potential in analyzing the relationship between these behaviors and the influencing factors. This kind of analysis could help train a model to predict when a risky driver is likely to act unsafely at a stop sign — whereas a safe driver would likely behave consistently across similar situations.