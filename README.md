# EV-Battery-SOC-Estimation-Using-Kalman-Filter
Modeling and simulation of Lithium-Ion battery State of Charge (SOC) estimation using Kalman Filter algorithm in MATLAB/Simulink for EV Battery Management System applications.

Project Overview
This project presents the modeling and simulation of State of Charge (SOC) estimation for a Lithium-Ion battery using a Kalman Filter algorithm. Accurate SOC estimation is critical for Battery Management Systems (BMS) in electric vehicles to ensure safe operation, improved battery life, and reliable energy management.
The system is developed in MATLAB/Simulink using a battery equivalent circuit model and a discrete Kalman Filter estimator.

Objective

To estimate battery SOC accurately under dynamic load conditions using:

•	Battery mathematical modeling
•	Current and voltage measurement
•	State-space modeling
•	Kalman Filter algorithm

System Architecture

The Simulink model consists of the following major blocks:

1️⃣ Battery Model Block

A first-order equivalent circuit model (ECM) is used, consisting of:
•	Open Circuit Voltage (OCV)
•	Internal resistance (R0)
•	RC polarization network
This model represents real lithium-ion battery behavior.

2️⃣Current Input Block

The battery current profile is provided as input:
•	Positive current → Discharging
•	Negative current → Charging
This simulates real EV driving cycles.

3️⃣ Coulomb Counting Block (Reference SOC)

SOC reference calculation:
SOC(t)=SOC(0)−1Q∫I(t)dt
Where:
•	Q = Battery capacity (Ah)
•	I(t) = Battery current
This gives baseline SOC but accumulates error over time.

4️⃣State-Space Model Block

Battery system is converted into discrete state-space form:
x(k+1)=Ax(k)+Bu(k)+w(k)
 y(k)=Cx(k)+Du(k)+v(k) 
Where:
•	x(k) = States (SOC & polarization voltage)
•	u(k) = Input current
•	y(k) = Output voltage
•	w(k), v(k) = Noise

5️⃣Kalman Filter Block

The Kalman Filter performs two main steps:
Prediction Step
Predicts next SOC value using battery model.
Update Step
Corrects predicted SOC using measured terminal voltage.
Kalman Gain:
K=PC^T(CPC^T+R)−1 
Updated state:
x=xpred+K(y−ypred) 
This reduces estimation error.


Working Principle

The battery current is applied to the battery model, generating terminal voltage and internal states. The Kalman Filter predicts the SOC using the mathematical model and then compares the predicted voltage with the actual measured voltage. Based on the error, it updates the SOC estimate using the Kalman gain.
Unlike Coulomb Counting, which accumulates integration errors, the Kalman Filter continuously corrects the SOC using voltage feedback, improving long-term accuracy.
Thus, the system operates as a closed-loop SOC estimator suitable for real-world EV applications

Simulation Results

The following outputs were analyzed:
•	True SOC
•	Coulomb Counting SOC
•	Kalman Estimated SOC
•	SOC Error

Observations:

✔ Kalman Filter SOC closely tracks true SOC
✔ Reduced steady-state error
✔ Better performance under dynamic load
✔ Improved robustness to noise
Method            	Accuracy	      Drift Error    	Noise Immunity
Coulomb Counting	   Medium           High              Low
Kalman Filter	        High            Low	              High


Tools Used

•	MATLAB
•	Simulink
•	Discrete State-SpaceModeling
•	Kalman Filter Algorithm
			
EV Application

This SOC estimation method is suitable for:
•	EV Battery Management Systems
•	Energy management strategies
•	Range prediction systems
•	Safety monitoring
