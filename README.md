# IRC_WS
Includes Behavior tree for autonomous expedition using py_tree_ros, capture panorama for every change in 15 degrees for 100 degrees,  detect angle between waypoint and yaw.,  Run 5 Esp32 cams at once, Capture image  when service is called

![alt text]([https://www.canva.com/design/DAF9NRP2380/_M2eM9W4Zm1YE0XXk61ypg/view?utm_content=DAF9NRP2380&utm_campaign=share_your_design&utm_medium=link&utm_source=shareyourdesignpanel]

## Behavior Tree Structure
AutEx (Selector)
|-- Sequence_1 (Sequence)
|   |-- Launch All Nodes
|   |-- Set Datum
|   |-- Fallback_16 (Selector)
|   |   |-- Launch Zed2i
|   |   |-- RetryUntilSuccess35
|   |-- Fallback_17 (Selector)
|   |   |-- Launch arrow detection node
|   |   |-- RetryUntilSuccess37
|   |-- Fallback_2 (Selector)
|   |   |-- Start Rosbag
|   |   |-- RetryUntilSuccess2
|   |-- Fallback_3 (Selector)
|   |   |-- Always Fail Decorator
|   |   |-- Sequence_3 (Sequence)
|   |       |-- Fallback_6 (Selector)
|   |       |   |-- ArrowDetectionCondition
|   |       |   |-- Sequence_6 (Sequence)
|   |       |       |-- Generate waypoints if arrow not detected
|   |       |       |-- Move Wheels
|   |       |       |-- ArrowDetectionCondition
|   |       |       |-- Fallback_7 (Selector)
|   |       |           |-- ArrowVisitedCondition
|   |       |           |-- Look for another arrow
|   |       |-- Fallback_8 (Selector)
|   |       |   |-- Always Fail
|   |       |   |-- Sequence_7 (Sequence)
|   |       |       |-- Find tf of arrow
|   |       |       |-- Generate waypoints towards arrow
|   |       |       |-- Move Wheels
|   |       |       |-- Follow Waypoints
|   |       |       |-- Fallback_19 (Selector)
|   |       |           |-- DistanceConditionArrow
|   |       |           |-- Turn to align
|   |       |-- Fallback_9 (Selector)
|   |       |   |-- Sequence_8 (Sequence)
|   |       |       |-- Stop wheels
|   |       |       |-- Start 10 sec timer
|   |       |-- Fallback_10 (Selector)
|   |       |   |-- Recheck tf of arrow
|   |       |   |-- RetryUntilSuccess14
|   |       |-- Fallback_11 (Selector)
|   |       |   |-- Save GPS Coordinates
|   |       |   |-- RetryUntilSuccess16
|   |       |-- Fallback_12 (Selector)
|   |       |   |-- Spot turn
|   |       |   |-- RetryUntilSuccess12
|   |       |-- Fallback_13 (Selector)
|   |       |   |-- Generate waypoints in direction of arrow
|   |       |   |-- RetryUntilSuccess20
|   |       |-- Fallback_14 (Selector)
|   |       |   |-- Sequence_9 (Sequence)
|   |       |       |-- TimerCondition
|   |       |       |-- Move Wheels
|   |       |-- Fallback_15 (Selector)
|   |           |-- Follow Waypoints
|   |           |-- RetryUntilSuccess24
|   |   
|-- Sequence_2 (Sequence)
|   |-- Reboot system
|   |-- Always Fail


Note: Obstacle Avoidance and path planning is executed using waypoint navigation
