# MQTT-Based Multiplayer Board Game

This project implements a multiplayer board game using MQTT as the communication protocol. The game involves players moving on a grid and attempting to eliminate each other using a special power. The last player standing wins.

## Game Rules

1. **Grid Size**: The game is played on a 500x500 grid, with cells numbered from 0 to 499.
2. **Players**: N players join the game.
3. **Movement**: Each player can occupy any cell on the grid. No two players can occupy the same cell at the same time.
4. **Teleportation**: Players can teleport to any location on the grid.
5. **Power Activation**: Each player has a power that, when activated, can kill any player in adjacent or neighboring cells.
6. **Power Clash**: If two players have their powers activated simultaneously and are in adjacent cells, nothing happens.
7. **Objective**: The game continues until only one player is left, who is declared the winner.

## Input

1. Each player is provided with an input file named `player-x.txt` (e.g., `player-1.txt`), where `x` is the player's number.
2. The first line in each file contains the total number of players, `N`.
3. Subsequent lines contain three numbers: `<x_coordinate, y_coordinate, power_status>`, where:
   - `x_coordinate` and `y_coordinate` represent the player's position on the grid.
   - `power_status` indicates whether the player's power is activated (`0` for not activated, `1` for activated).
4. The input files provide sufficient data for the game to finish.

### Sample Input

For a game with 2 players where Player 1 wins:

#### `player-1.txt`
2 2 2 0 3 7 0 10 5 1 4 7 0 6 8 1

#### `player-2.txt`
2 5 3 1 7 2 0 11 5 1 10 3 1 6 7 0


## Game Flow

1. **Connecting to the Server**: Each player connects to the MQTT broker (acting as the game server) and waits until all other players have joined.
2. **Game Start**: The game starts once all players are connected.
3. **Updating Status**: Each player periodically updates their location and power status to the server.
4. **Subscriptions**: Players subscribe to the location and power status of all other players to keep track of their positions.
5. **Elimination**: A player checks if any other player is adjacent with an activated power while their own power is not activated. If so, the player is eliminated and disconnects from the server after updating necessary information.
6. **Player Death Announcement**: All players are notified when a player is killed and who the killer is, reducing the number of alive players.
7. **Winning the Game**: When only one player is left, they are declared the winner and the game ends.

## Implementation Details

- The game is implemented in Python, leveraging the Paho MQTT Python client library for communication with the HiveMQ broker.
- Each player and the server run as separate processes that communicate over MQTT topics.

## Prerequisites

- Python 3.8 or higher
- Paho MQTT Python client library
- HiveMQ broker (either local or cloud)

```bash
sudo apt update
sudo apt install python3 python3-pip
pip3 install paho-mqtt
wget https://www.hivemq.com/releases/hivemq-4.5.0.zip
unzip hivemq-4.5.0.zip
cd hivemq-4.5.0/bin
./run.sh


## Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/debika-samanta/mqtt-board-game-hivemq.git
   cd mqtt-board-game-hivemq
   


