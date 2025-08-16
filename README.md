## Problem Statement

In the rapidly evolving landscape of sustainable transportation, the availability and strategic placement of electric vehicle (EV) charging infrastructure are paramount. Tesla's Supercharger network plays a critical role in supporting the adoption of EVs. This project addresses the challenge of optimizing the Tesla Supercharger network by analyzing its dataset to identify geographic and temporal trends, and pinpoint potential charging gaps across the USA. Understanding these patterns and gaps is crucial for efficient network expansion and ensuring seamless long-distance travel for Tesla owners, thereby contributing to the broader goal of sustainable mobility.

## Data Source

The dataset used in this project contains information about Tesla Supercharger locations. The data was obtained from a publicly available source, though the specific URL is not included in this README.

The analysis in this project utilized the following relevant features from the dataset:

- **Supercharger:** A unique identifier for each location.
- **Street Address:** The physical address of the station.
- **City:** The city where the station is located.
- **State:** The state where the station is located.
- **Zip:** The ZIP code associated with the station.
- **Country:** The country where the station is located (primarily USA for this analysis).
- **Stalls:** The number of charging stalls available.
- **kW:** The power rating in kilowatts.
- **GPS:** The GPS coordinates (latitude and longitude).
- **Elev(m):** The elevation in meters.
- **Open Date:** The date the Supercharger station was opened.
- **Latitude:** The geographical latitude coordinate (derived from GPS).
- **Longitude:** The geographical longitude coordinate (derived from GPS).

## Methodology

This project followed a structured analytical approach to gain insights into the Tesla Supercharger network and optimize station placement. The key phases of the analysis included:

### Data Cleaning

This phase involved preparing the raw dataset for analysis. Key activities included:
- Handling missing values in relevant columns such as 'State', 'Zip', 'kW', and 'Open Date'.
- Filtering the dataset to focus on Supercharger locations within the USA.
- Dropping irrelevant columns that do not contribute to the analysis.

### Exploratory Data Analysis (EDA)

EDA was conducted to understand the distribution and characteristics of the Supercharger data. This involved:
- Generating descriptive statistics for numerical features like 'Stalls', 'kW', and 'Elev(m)'.
- Visualizing the distribution of numerical variables using histograms.
- Analyzing the frequency of categorical variables, particularly the distribution of Superchargers across different states.

### Time Series Analysis

Time series analysis was performed to identify temporal trends in the opening of Supercharger stations. This involved:
- Converting 'Open Date' to datetime objects.
- Resampling the data to analyze the number of Superchargers opened per month and year.
- Visualizing the temporal trends using line plots to understand the growth and fluctuations in network expansion.

### Geospatial Analysis

Geospatial analysis was used to visualize the spatial distribution of Supercharger locations and identify potential coverage gaps. This involved:
- Extracting Latitude and Longitude from the 'GPS' column.
- Creating interactive maps to display Supercharger locations across the USA.
- Analyzing the concentration of stations in different regions to understand the existing network coverage.

### Optimization

An optimization model was formulated and solved to identify optimal locations for new Supercharger stations with the objective of minimizing the total distance between stations while considering constraints on the number of stations to be built. This involved:
- Filtering data for a specific region (California) and time frame.
- Calculating the distance matrix between potential station locations.
- Defining decision variables, objective function (minimizing total distance), and constraints (minimum and maximum number of stations).
- Using a linear programming approach to solve the optimization problem.
- Identifying and visualizing the optimal locations based on the model's solution.

## Optimization Model

The optimization model aims to minimize the total distance between newly built EV supercharging stations in California, subject to constraints on the number of stations.

### Sets and Indices

$x \in \text{Newly Built Charging Stations}=\{\text{1}, \text{0}\}$

$d \in \text{Distance}=\{\text{Location i}, \text{Location j}\}$

### Decision Variables

$\text{x}_{i} \in \mathbb{1, 0}$: Whether a charging station is newly built at location $i$.

$\text{d}_{i,j} \in \mathbb{D}^{+}$: Distance between the newly built location $i$ and $j$.

### Objective Function

- **Distance**: Minimize the total distance between newly built EV supercharging stations.

\begin{equation}
\text{Minimize} \quad Z = \sum_{i = \text{1}} \sum_{j = \text{1}} {\text{D}*{i,j}*\text{x}*{i} *\text{x}_{j}}
\end{equation}

### Constraints

- **Station Constraint**: For each station $i$ selected in the route, number of stations $x_i$, should be between the minimum and maximum number of charging stations.

\begin{equation}
\text{Min Charging Stations} \leq \sum_{\text{i=1}}{\text{$x_i$}} \leq \text{Max Charging Stations}
\end{equation}

- **Non-Binary Constraint**: Ensure that each new location is either selected or not:

\begin{equation}
{x_i \in \text{0,1}}{} \quad \forall i \in \text{1, 2, ..., N}
\end{equation}

## Results and Findings

This project yielded several key insights from the analysis of the Tesla Supercharger network data:

**Exploratory Data Analysis (EDA):**
- Descriptive statistics revealed that the majority of Supercharger stations have a relatively low number of stalls and are located at lower elevations. The distribution of kW values shows peaks at certain power capacities.
- The frequency analysis of categorical variables highlighted the uneven distribution of Superchargers across states, with California having a significantly higher number of stations compared to others.

**Time Series Analysis:**
- The temporal analysis of Supercharger openings indicated a notable surge in new station constructions around 2020, followed by a decrease in the subsequent years. This suggests a period of rapid expansion followed by a slowdown.

**Geospatial Analysis:**
- The interactive map visualization clearly showed a higher concentration of Supercharger stations on the East and West coasts of the USA, with sparser coverage in the central regions. This highlights potential charging gaps in the middle of the country.

**Optimization Model Results:**
- The optimization model, aimed at minimizing the total distance between newly built stations in California, successfully identified optimal locations for a specified number of new charging stations within the range of 208 to 727 stations.
- The optimal solution resulted in an objective value of approximately 3.24 million, with an optimality gap of around 9.99%.
- The analysis of the selected optimal locations revealed a strong concentration of recommended new stations in major metropolitan areas such as San Francisco, Los Angeles, and San Diego.
- This concentration in high-demand urban centers suggests that the optimization model prioritizes serving areas with potentially higher EV density.
- Visualizing the optimal locations and their nearest neighbors showed that placing stations in these metropolitan areas can significantly reduce the distance between charging points, potentially minimizing the travel distance for EV drivers to access a Supercharger. In these areas, the distance between stations was reduced by a minimum of around 20 miles, potentially bringing charging within a more convenient range for most drivers in the state.

## Conclusion

This project provided valuable insights into the Tesla Supercharger network in the USA. Through comprehensive data cleaning, exploratory data analysis, time series analysis, and geospatial visualization, we identified significant trends in station distribution and temporal expansion. The analysis highlighted the concentration of Superchargers in coastal states, particularly California, and revealed a period of accelerated network growth around 2020.

The optimization model successfully demonstrated how to strategically place new charging stations in California to minimize the total distance between them, thereby enhancing accessibility for EV drivers. The results suggest that focusing new infrastructure development in high-demand metropolitan areas can significantly reduce the distance to charging stations, contributing to a more convenient and efficient charging experience.

This work has the potential to inform Tesla's strategic planning for future Supercharger network expansion, helping to identify underserved areas and optimize resource allocation. By minimizing the distances between charging stations, the project contributes to the broader goal of promoting sustainable mobility and accelerating the adoption of electric vehicles.

Future work could involve incorporating additional factors into the optimization model, such as population density, traffic flow, and the presence of other EV charging networks. Extending the analysis to other countries and exploring different optimization objectives, such as maximizing coverage or minimizing waiting times, would also provide further valuable insights.
