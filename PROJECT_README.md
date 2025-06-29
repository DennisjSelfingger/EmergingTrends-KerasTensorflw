# Pirate Treasure Hunt - Deep Q-Learning Implementation

## Project Overview

This project implements a deep Q-learning algorithm to train an intelligent pirate agent to find treasure in a maze environment. The pirate learns optimal pathfinding strategies through reinforcement learning, using exploration and exploitation to navigate from any starting position to the treasure location.

## Project Structure

### Core Files
- **TreasureHuntGame.ipynb** - Main Jupyter notebook containing the complete implementation
- **TreasureMaze.py** - Environment class that defines the maze, game mechanics, and agent interactions
- **GameExperience.py** - Experience replay system for storing and retrieving training episodes

### Key Components

#### 1. Environment Setup
- 8x8 maze represented as a numpy array
- Walls (0) and free spaces (1) define the navigable environment
- Treasure located at bottom-right corner (7,7)
- Pirate can move in four directions: LEFT, UP, RIGHT, DOWN

#### 2. Deep Q-Learning Algorithm
The core implementation includes:
- **Neural Network Model**: Sequential model with dense layers and PReLU activation
- **Experience Replay**: Stores episodes for batch training
- **Epsilon-Greedy Strategy**: Balances exploration vs exploitation
- **Q-Value Approximation**: Neural network predicts optimal actions for each state

#### 3. Training Process
- Agent starts from random positions each epoch
- Collects experiences through environment interaction
- Trains neural network on batched historical experiences
- Tracks win rate and adjusts exploration rate dynamically

## Implementation Details

### Neural Network Architecture
```python
model = Sequential()
model.add(Dense(maze.size, input_shape=(maze.size,)))
model.add(PReLU())
model.add(Dense(maze.size))
model.add(PReLU())
model.add(Dense(num_actions))
model.compile(optimizer='adam', loss='mse')
```

### Key Parameters
- **Epochs**: Up to 15,000 training iterations
- **Epsilon**: Exploration factor (starts at 0.1, reduces to 0.05 when win rate > 90%)
- **Memory**: Stores up to 1,000 episodes for experience replay
- **Data Size**: 50 experiences used per training batch

### Success Criteria
- Achieve 100% win rate across all possible starting positions
- Pass completion check ensuring optimal paths from every free cell
- Agent must consistently find treasure regardless of starting location

## How to Run

1. **Setup Environment**
   ```bash
   pip install numpy keras matplotlib
   ```

2. **Run the Notebook**
   - Open `TreasureHuntGame.ipynb` in Jupyter
   - Execute all cells in sequence
   - Monitor training progress through epoch outputs

3. **Training Output**
   ```
   Epoch: 001/999 | Loss: 0.0234 | Episodes: 145 | Win count: 12 | Win rate: 0.120 | time: 2.3 seconds
   ```

4. **Test Trained Model**
   - Completion check validates performance across all starting positions
   - Single game test demonstrates pathfinding from (0,0) to treasure

## Key Features

### Intelligent Agent Capabilities
- **Adaptive Learning**: Improves pathfinding through trial and error
- **Memory Utilization**: Leverages past experiences for better decision making
- **Exploration Balance**: Dynamically adjusts between learning and exploring
- **Optimal Navigation**: Finds shortest paths after successful training

### Visualization
- Real-time maze visualization showing:
  - Pirate position (dark gray)
  - Treasure location (light gray)  
  - Visited cells (medium gray)
  - Walls and free spaces

## Technical Approach

### Reinforcement Learning Concepts
- **State**: Current maze position represented as flattened array
- **Action**: Movement direction (LEFT, UP, RIGHT, DOWN)
- **Reward**: Positive for reaching treasure, negative for hitting walls
- **Q-Values**: Predicted future rewards for state-action pairs

### Deep Q-Learning Workflow
1. Initialize neural network and experience replay memory
2. For each epoch:
   - Reset environment with random starting position
   - Execute actions using epsilon-greedy policy
   - Store experiences (state, action, reward, next_state)
   - Train network on sampled experiences
   - Update win rate and adjust exploration

## Expected Results

A successfully trained agent will:
- Achieve 100% win rate within 1000-3000 epochs
- Navigate efficiently from any starting position
- Demonstrate learned optimal pathfinding strategies
- Pass all completion checks consistently

## Educational Value

This project demonstrates:
- **Reinforcement Learning**: Core concepts of Q-learning and value approximation
- **Neural Networks**: Deep learning for function approximation
- **Game AI**: Intelligent agent development for navigation tasks
- **Algorithm Implementation**: Translating theoretical concepts into working code

## Troubleshooting

### Common Issues
- **Slow Convergence**: Adjust epsilon, learning rate, or network architecture
- **Memory Errors**: Reduce max_memory or data_size parameters
- **Training Stuck**: Verify maze has valid paths to treasure
- **Low Win Rate**: Increase training epochs or adjust exploration strategy

### Performance Tips
- Monitor loss values to ensure network is learning
- Win rate should steadily increase over time
- Completion check confirms robust learning across all scenarios
- Visualization helps debug pathfinding behavior

---

*This implementation showcases practical application of deep reinforcement learning for solving navigation and pathfinding challenges in constrained environments.*
