
Step 0. Convert to numeric values
Step 1. Decide how many clusters you want to use ($k$)
Step 2. Assign initial centroid values for each cluster
	You can assign randomly; Some implementations pick $k$ random data points to serve as centroids
Step 3. Assign each data point to a cluster (nearest centroid)
Step 4. Compute the new centroid of each cluster (mean)
Repeat Steps 3 and 4 until the centroids no longer change (convergence)

---
# Exercise

K = 2; use Manhattan distance
Initial centroids:
- (9, 30)
- (0, 13)

Initial centroids: (Manhattan Distance)
$$|(9-0)|+|(30-13)|=26$$

| Temperature (x-axis) | Humidity (y-axis) |
| -------------------- | ----------------- |
| 1                    | 24                |
| 8                    | 30                |
| 7                    | 21                |
| 5                    | 14                |

