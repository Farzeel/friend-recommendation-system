# Social Network Recommendation System

## Project Description

This project implements a "People You May Know" recommendation system for a social network. It identifies potential friend recommendations for a given user based on two main factors:

1.  **Mutual Connections:** Recommending friends of friends who are not already direct friends.
2.  **Location Proximity:** Recommending users within a certain geographical distance using the Haversine formula.

The system combines scores from these two factors to generate a ranked list of recommendations.

## Features

* Load user and page data from a JSON file.
* Calculate the great-circle distance between two points using the Haversine formula.
* Find potential recommendations based on a combination of mutual friends and location.
* Includes a fallback mechanism to recommend based solely on mutual friends if location data is unavailable for the user.
* Allows adjusting the weighting of mutual connection scores and location scores.
* Display the names of the recommended users.

## Getting Started

### Prerequisites

* Python 3.x
* Standard Python libraries: `json`, `math`, `collections`

### Installation

1.  Clone this repository to your local machine:
    ```bash
    git clone https://github.com/Farzeel/friend-recommendation-system.git
    ```
2.  Navigate to the project directory:
    ```bash
    cd [your-repository-name]
    ```

## Usage

1.  **Prepare your data:** Ensure you have a JSON file named `massive_data.json` in the same directory as the Python script. The format of this file should match the structure described in the Data Format section below.
2.  **Run the script:** Execute the main Python script from your terminal:
    ```bash
    python your_main_script_name.py
    ```
    (Replace `your_main_script_name.py` with the actual name of your Python file containing the functions).

3.  **Configure:** You can modify the `user_id`, `mutual_weight`, and `location_weight` variables in the main execution block of the script to change the target user and the influence of mutual friends vs. location.

The script will print the list of recommended user IDs and their corresponding names.

## Code Structure

* `load_data(filename)`: Loads the user and page data from the specified JSON file.
* `calculate_distance(lat1, lon1, lat2, lon2)`: Calculates the distance between two points in kilometers using the Haversine formula.
* `find_people_you_may_know(user_id, data, max_distance, mutual_weight, location_weight)`: The core function that finds recommendations by combining mutual friend scores and location scores.
* `find_people_by_mutual_friends(user_id, friends)`: A fallback function to find recommendations based solely on mutual friends.
* `display_data(data, recommended_ids)`: Takes the recommended user IDs and returns a list of their names.

## Data Format

The input JSON file (`massive_data.json`) should have the following structure:

```json
{
    "users": [
        {
            "id": 1,
            "name": "User Name",
            "friends": [FriendID1, FriendID2, ...],
            "liked_pages": [PageID1, PageID2, ...],
            "location": {
                "latitude": Latitude,
                "longitude": Longitude,
                "city": "City Name"
            }
        },
        // ... more user objects
    ],
    "pages": [
        {
            "id": 101,
            "name": "Page Name"
        },
        // ... more page objects
    ]
}