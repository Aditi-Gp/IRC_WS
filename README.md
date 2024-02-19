# IRC_WS
Includes Behavior tree for autonomous expedition using py_tree_ros, capture panorama for every change in 15 degrees for 100 degrees,  detect angle between waypoint and yaw.,  Run 5 Esp32 cams at once, Capture image  when service is called

![alt text]([https://www.canva.com/design/DAF9NRP2380/_M2eM9W4Zm1YE0XXk61ypg/view?utm_content=DAF9NRP2380&utm_campaign=share_your_design&utm_medium=link&utm_source=shareyourdesignpanel]

## Behavior Tree Structure
AutEx (Selector)\
nbsp; |-- Sequence_1 (Sequence)\
\t|\t|-- Launch All Nodes
\t|\t|-- Set Datum
\t|\t|-- Fallback_16 (Selector)
\t|\t|\t|-- Launch Zed2i
\t|\t|\t|-- RetryUntilSuccess35
\t|\t|-- Fallback_17 (Selector)
\t|\t|\t|-- Launch arrow detection node
\t|\t|\t|-- RetryUntilSuccess37
\t|\t|-- Fallback_2 (Selector)
\t|\t|\t|-- Start Rosbag
\t|\t|\t|-- RetryUntilSuccess2
\t|\t|-- Fallback_3 (Selector)
\t|\t|\t|-- Always Fail Decorator
\t|\t|\t|-- Sequence_3 (Sequence)
\t|\t|\t|\t|-- Fallback_6 (Selector)
\t|\t|\t|\t|\t|-- ArrowDetectionCondition
\t|\t|\t|\t|\t|-- Sequence_6 (Sequence)
\t|\t|\t|\t|\t|\t|-- Generate waypoints if arrow not detected
\t|\t|\t|\t|\t|\t|-- Move Wheels
\t|\t|\t|\t|\t|\t|-- ArrowDetectionCondition
\t|\t|\t|\t|\t|\t|-- Fallback_7 (Selector)
\t|\t|\t|\t|\t|\t|\t|-- ArrowVisitedCondition
\t|\t|\t|\t|\t|\t|\t|-- Look for another arrow
\t|\t|\t|\t|-- Fallback_8 (Selector)
\t|\t|\t|\t|\t|-- Always Fail
\t|\t|\t|\t|\t|-- Sequence_7 (Sequence)
\t|\t|\t|\t|\t|\t|-- Find tf of arrow
\t|\t|\t|\t|\t|\t|-- Generate waypoints towards arrow
\t|\t|\t|\t|\t|\t|-- Move Wheels
\t|\t|\t|\t|\t|\t|-- Follow Waypoints
\t|\t|\t|\t|\t|\t|-- Fallback_19 (Selector)
\t|\t|\t|\t|\t|\t|\t|-- DistanceConditionArrow
\t|\t|\t|\t|\t|\t|\t|-- Turn to align
\t|\t|\t|\t|-- Fallback_9 (Selector)
\t|\t|\t|\t|\t|-- Sequence_8 (Sequence)
\t|\t|\t|\t|\t|\t|-- Stop wheels
\t|\t|\t|\t|\t|\t|-- Start 10 sec timer
\t|\t|\t|\t|-- Fallback_10 (Selector)
\t|\t|\t|\t|\t|-- Recheck tf of arrow
\t|\t|\t|\t|\t|-- RetryUntilSuccess14
\t|\t|\t|\t|-- Fallback_11 (Selector)
\t|\t|\t|\t|\t|-- Save GPS Coordinates
\t|\t|\t|\t|\t|-- RetryUntilSuccess16
\t|\t|\t|\t|-- Fallback_12 (Selector)
\t|\t|\t|\t|\t|-- Spot turn
\t|\t|\t|\t|\t|-- RetryUntilSuccess12
\t|\t|\t|\t|-- Fallback_13 (Selector)
\t|\t|\t|\



Note: Obstacle Avoidance and path planning is executed using waypoint navigation
