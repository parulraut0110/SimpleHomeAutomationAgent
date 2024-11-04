```python

class HomeAutomationAgent:
    def __init__(self):
        self.temperature = 22  # Default room temperature in °C
        self.lights_on = False
        self.security_armed = True
        self.occupancy = False  # True if home is occupied
        self.time_of_day = 'day'  # 'day' or 'night'
        self.doors_open = False  # Track if doors are open

    def update_sensors(self, temperature, occupancy, time_of_day, doors_open):
        self.temperature = temperature
        self.occupancy = occupancy
        self.time_of_day = time_of_day
        self.doors_open = doors_open

    def control_heating(self):
        if self.temperature < 20:
            return "Turning on heating."
        elif self.temperature > 25:
            return "Turning off heating."
        return "No heating adjustment needed."

    def control_lighting(self):
        if not self.occupancy:
            self.lights_on = False
            return "Turning off lights; no occupancy detected."
        if self.time_of_day == 'night':
            self.lights_on = True
            return "Turning on lights; it's dark."
        self.lights_on = False
        return "Turning off lights; it's daytime."

    def control_security(self):
        if not self.occupancy or self.doors_open:
            return "Alarm triggered! Doors are open and nobody is home."
        return "Security system is armed; doors are locked."

    def run(self):
        outputs = []
        outputs.append(self.control_heating())
        outputs.append(self.control_lighting())
        outputs.append(self.control_security())
        return outputs


def main():
    agent = HomeAutomationAgent()
    
    while True:
        # Get user input for sensor readings
        try:
            time_of_day = input("Enter the time of day (day/night): ").strip().lower()
            occupancy = input("Is the home occupied? (yes/no): ").strip().lower() == 'yes'
            doors_open = input("Are the doors/windows open? (yes/no): ").strip().lower() == 'yes'
            temperature = float(input("Enter the current temperature (°C): "))
            
            # Update sensor readings
            agent.update_sensors(temperature, occupancy, time_of_day, doors_open)
            outputs = agent.run()
            
            # Print the outputs
            for output in outputs:
                print(output)
        except ValueError:
            print("Invalid input, please try again.")

        # Check if the user wants to continue
        if input("Do you want to update the readings again? (yes/no): ").strip().lower() != 'yes':
            break


if __name__ == "__main__":
    main()
    
    
    


```
