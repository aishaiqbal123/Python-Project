# Python-Project
import matplotlib.pyplot as plt

Gravitational_acceleration = 9.81 
Air_density = 1.225 

Initial_mass = float(input("Enter the initial mass of the rocket (kg): "))
Fuel_mass = float(input("Enter the fuel mass (kg): "))
Thrust = float(input("Enter the thrust provided by the rocket engine (N): "))
Burn_rate = float(input("Enter the fuel burn rate (kg/s): "))
Coffecient_of_drag = cd = float(input("Enter the drag coefficient (typically between 0.1 and 0.5): "))
Cross_section_Area = float(input("Enter the cross-sectional area of the rocket (m^2): "))

dt = float(input("Enter the time step for simulation (seconds, e.g., 0.1): "))

Initial_time = 0  
Altitude = 0  
velocity = 0  
mass = Initial_mass 

time_data = []
altitude_data = []
velocity_data = []
acceleration_data = []

# Simulation loop
while Altitude >= 0:
    weight = mass * Gravitational_acceleration
    drag = 0.5 * Air_density * velocity** 2 * Coffecient_of_drag * Cross_section_Area

    # Calculate net force
    if Fuel_mass > 0:
        net_force = Thrust - drag - weight
        Fuel_mass -= Burn_rate * dt
        mass -= Burn_rate * dt
    else:
        net_force = - drag - weight 

    acceleration = net_force / mass
    velocity += acceleration * dt
    Altitude += velocity * dt

    # Store data for plotting
    time_data.append(Initial_time)
    altitude_data.append(Altitude)
    velocity_data.append(velocity)
    acceleration_data.append(acceleration)

    Initial_time += dt

    # Break if the rocket has hit the ground
    if Altitude < 0:
        break

# Plot results
plt.figure(figsize=(10, 6))

# Altitude plot
plt.subplot(3, 1, 1)
plt.plot(time_data, altitude_data)
plt.title("Rocket Flight Simulation")
plt.ylabel("Altitude (m)")

# Velocity plot
plt.subplot(3, 1, 2)
plt.plot(time_data, velocity_data)
plt.ylabel("Velocity (m/s)")

# Acceleration plot
plt.subplot(3, 1, 3)
plt.plot(time_data, acceleration_data)
plt.xlabel("Time (s)")
plt.ylabel("Acceleration (m/s^2)")

plt.tight_layout()
plt.show()
