<h1>ExpNo 1 :Developing AI Agent with PEAS Description</h1>
<h3>Name: Saravanan N</h3>
<h3>Register Number/Staff Id: TSML006</h3>


<h3>AIM:</h3>
<br>
<p>To find the PEAS description for the given AI problem and develop an AI agent.</p>
<br>
<h3>Theory</h3>
<h3>Medicine prescribing agent:</h3>
<p>Such this agent prescribes medicine for fever (greater than 98.5 degrees) which we consider here as unhealthy, by the user temperature input, and another environment is rooms in the hospital (two rooms). This agent has to consider two factors one is room location and an unhealthy patient in a random room, the agent has to move from one room to another to check and treat the unhealthy person. The performance of the agent is calculated by incrementing performance and each time after treating in one room again it has to check another room so that the movement causes the agent to reduce its performance. Hence, agents prescribe medicine to unhealthy.</p>
<hr>
<h3>PEAS DESCRIPTION:</h3>
<table>
  <tr>
    <td><strong>Agent Type</strong></td>
    <td><strong>Performance</strong></td>
     <td><strong>Environment</strong></td>
    <td><strong>Actuators</strong></td>
    <td><strong>Sensors</strong></td>
  </tr>
    <tr>
    <td><strong>Medicine prescribing agent</strong></td>
    <td><strong>Treating unhealthy, agent movement</strong></td>
     <td><strong>Rooms, Patient</strong></td>
    <td><strong>Medicine, Treatment</strong></td>
    <td><strong>Location, Temperature of patient</strong></td>
  </tr>
</table>
<hr>
<H3>DESIGN STEPS</H3>
<h3>STEP 1:Identifying the input:</h3>
<p>Temperature from patients, Location.</p>
<h3>STEP 2:Identifying the output:</h3>
<p>Prescribe medicine if the patient in a random has a fever.</p>
<h3>STEP 3:Developing the PEAS description:</h3>
<p>PEAS description is developed by the performance, environment, actuators, and sensors in an agent.</p>
<h3>STEP 4:Implementing the AI agent:</h3>
<p>Treat unhealthy patients in each room. And check for the unhealthy patients in random room</p>
<h3>STEP 5:</h3>
<p>Measure the performance parameters: For each treatment performance incremented, for each movement performance decremented</p>

## PROGRAM:
### DEVELOPED BY : G.KIRAN
### REGISTER NUMBER : 212223040095
```python
import random

class Patient:
    def __init__(self, room_name):
        self.room = room_name
        self.temperature = random.uniform(97.0, 102.0)  # random patient temp

    def is_unhealthy(self):
        return self.temperature > 98.5

    def treat(self):
        """Prescribe medicine and set to healthy temperature"""
        if self.is_unhealthy():
            self.temperature = 98.0
            return True
        return False


class MedicinePrescribingAgent:
    def __init__(self, rooms, patients):
        self.rooms = rooms
        self.patients = patients
        self.location = rooms[0]  # start in Room A
        self.performance = 0

    def sense(self, room):
        """Check patient's temperature in current room"""
        patient = self.patients[room]
        return patient.temperature

    def act(self):
        """Main decision-making and action loop"""
        while True:
            treated_any = False
            for room in self.rooms:
                # Move to the room if not already there
                if self.location != room:
                    print(f"Agent moving from {self.location} → {room}")
                    self.location = room
                    self.performance -= 1  # movement penalty

                # Sense patient's state
                temp = self.sense(room)
                print(f"[{room}] Patient temperature: {temp:.1f}")

                # If unhealthy → treat
                if temp > 98.5:
                    if self.patients[room].treat():
                        print(f"💊 Treated patient in {room}")
                        self.performance += 10
                        treated_any = True
                else:
                    print(f"✅ Patient in {room} is healthy")

            # Stop if all patients healthy
            if all(not p.is_unhealthy() for p in self.patients.values()):
                print("\nAll patients are healthy. Stopping agent.")
                break

            # If treated someone, continue loop to re-check
            if treated_any:
                print("Re-checking rooms...\n")
            else:
                print("No unhealthy patients found. Stopping agent.")
                break


if __name__ == "__main__":
    # Define environment: 2 rooms with patients
    rooms = ["Room A", "Room B"]
    patients = {room: Patient(room) for room in rooms}

    # Show initial patient states
    print("Initial patient states:")
    for r, p in patients.items():
        print(f"{r}: {p.temperature:.1f}")

    # Run agent
    agent = MedicinePrescribingAgent(rooms, patients)
    agent.act()

    print(f"\nFinal Performance Score: {agent.performance}")
```
# OUTPUT

<img width="780" height="342" alt="image" src="https://github.com/user-attachments/assets/ab2290e3-5746-46e7-9b2e-460ceb30eb10" />


# RESULT : 


Thus the Developing AI Agent with PEAS Description was implemented using python programming.
