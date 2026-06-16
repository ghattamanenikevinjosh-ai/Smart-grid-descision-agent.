# Smart-grid-descision-agent.
# ============================
# SMART GRID DECISION AGENT
# CFAI PROJECT
# ============================

import random
import pandas as pd
import matplotlib.pyplot as plt

# ---------------------------------
# CO1: Agent Model using OOP
# ---------------------------------
class SmartGridAgent:

    def __init__(self):
        # CO1: State Representation
        self.energy_data = []
        self.decisions = []

    # ---------------------------------
    # CO1: Data Collection Function
    # ---------------------------------
    def generate_data(self, hours=24):

        for hour in range(hours):

            demand = random.randint(200, 900)
            solar = random.randint(50, 400)
            wind = random.randint(30, 250)

            self.energy_data.append({
                "Hour": hour,
                "Demand": demand,
                "Solar": solar,
                "Wind": wind
            })

    # ---------------------------------
    # CO5: Prediction Under Uncertainty
    # ---------------------------------
    def predict_demand(self):

        for record in self.energy_data:

            predicted = (
                record["Demand"] +
                random.randint(-30, 30)
            )

            record["Predicted_Demand"] = predicted

    # ---------------------------------
    # CO2 + CO4
    # Heuristic Decision Making
    # Utility Based Selection
    # ---------------------------------
    def analyze_grid(self):

        for record in self.energy_data:

            renewable = (
                record["Solar"] +
                record["Wind"]
            )

            demand = record["Predicted_Demand"]

            if renewable >= demand:

                decision = "Renewable Energy"

            elif renewable >= demand * 0.6:

                decision = "Hybrid Energy"

            else:

                decision = "Conventional Backup"

            self.decisions.append(decision)

    # ---------------------------------
    # CO6: Fault Detection
    # ---------------------------------
    def fault_detection(self):

        print("\nFAULT REPORT\n")

        for record in self.energy_data:

            if record["Demand"] > 850:

                print(
                    f"Overload Alert at Hour "
                    f"{record['Hour']}"
                )

            if record["Solar"] < 60:

                print(
                    f"Low Solar Production "
                    f"at Hour {record['Hour']}"
                )

    # ---------------------------------
    # CO3: Constraint Satisfaction
    # Resource Scheduling
    # ---------------------------------
    def load_balancing(self):

        print("\nLOAD BALANCING\n")

        for record in self.energy_data:

            demand = record["Demand"]

            if demand > 800:

                print(
                    f"Hour {record['Hour']} : "
                    f"Shift Non-Critical Load"
                )

            elif demand < 300:

                print(
                    f"Hour {record['Hour']} : "
                    f"Store Extra Energy"
                )

            else:

                print(
                    f"Hour {record['Hour']} : "
                    f"Normal Operation"
                )

    # ---------------------------------
    # CO4: Utility Evaluation
    # ---------------------------------
    def calculate_efficiency(self):

        total_demand = 0
        total_renewable = 0

        for record in self.energy_data:

            total_demand += record["Demand"]

            total_renewable += (
                record["Solar"] +
                record["Wind"]
            )

        efficiency = (
            total_renewable /
            total_demand
        ) * 100

        print("\nSYSTEM EFFICIENCY")
        print(
            f"Renewable Usage : "
            f"{efficiency:.2f}%"
        )

    # ---------------------------------
    # CO6: Explainable AI Report
    # ---------------------------------
    def display_report(self):

        df = pd.DataFrame(
            self.energy_data
        )

        df["Decision"] = (
            self.decisions
        )

        print("\nSMART GRID REPORT")
        print(df)

        return df

    # ---------------------------------
    # CO6: Performance Visualization
    # ---------------------------------
    def plot_graph(self, df):

        plt.figure(figsize=(10,5))

        plt.plot(
            df["Hour"],
            df["Demand"],
            marker='o',
            label="Demand"
        )

        plt.plot(
            df["Hour"],
            df["Predicted_Demand"],
            marker='s',
            label="Prediction"
        )

        plt.xlabel("Hour")
        plt.ylabel("Power MW")
        plt.title(
            "Demand Prediction Graph"
        )

        plt.legend()
        plt.grid(True)

        plt.show()

    # ---------------------------------
    # Complete Agent Execution
    # ---------------------------------
    def run(self):

        self.generate_data()

        self.predict_demand()

        self.analyze_grid()

        self.fault_detection()

        self.load_balancing()

        self.calculate_efficiency()

        df = self.display_report()

        self.plot_graph(df)


# ---------------------------------
# Main Program
# ---------------------------------
if __name__ == "__main__":

    print("=" * 50)
    print("SMART GRID DECISION AGENT")
    print("=" * 50)

    agent = SmartGridAgent()

    agent.run()
