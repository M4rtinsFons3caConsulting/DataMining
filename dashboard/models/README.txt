This folder stores our trained model, to use them follow this methodology.

### STORE AND LOAD SCRIPT

import joblib
import os

class ClusteringSolutionManager:
    def __init__(self, storage_dir="clustering_solutions"):
        self.storage_dir = storage_dir
        os.makedirs(self.storage_dir, exist_ok=True)

    def save_solution(self, solution, file_name):
        """Save the clustering solution to a .pkl file."""
        file_path = os.path.join(self.storage_dir, file_name)
        joblib.dump(solution, file_path)
        print(f"Solution saved to {file_path}")

    def load_solution(self, file_name):
        """Load the clustering solution from a .pkl file."""
        file_path = os.path.join(self.storage_dir, file_name)
        if not os.path.exists(file_path):
            raise FileNotFoundError(f"No such file: {file_path}")
        solution = joblib.load(file_path)
        print(f"Solution loaded from {file_path}")
        return solution

    def list_solutions(self):
        """List all saved clustering solutions."""
        return [f for f in os.listdir(self.storage_dir) if f.endswith('.pkl')]

## EXAMPLE USAGE

if __name__ == "__main__":
    # Create a manager instance
    manager = ClusteringSolutionManager()

    # Example clustering solution (replace with your own clustering result)
    clustering_result = {"labels": [0, 1, 1, 0], "centroids": [[1, 2], [3, 4]]}

    # Save the clustering solution
    manager.save_solution(clustering_result, "example_solution.pkl")

    # List saved solutions
    print("Available solutions:", manager.list_solutions())

    # Load the solution back
    loaded_solution = manager.load_solution("example_solution.pkl")
    print("Loaded solution:", loaded_solution)

