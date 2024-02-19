# IRC_WS
Includes Behavior tree for autonomous expedition using py_tree_ros, capture panorama for every change in 15 degrees for 100 degrees,  detect angle between waypoint and yaw.,  Run 5 Esp32 cams at once, Capture image  when service is called

![alt text]([https://www.canva.com/design/DAF9NRP2380/_M2eM9W4Zm1YE0XXk61ypg/view?utm_content=DAF9NRP2380&utm_campaign=share_your_design&utm_medium=link&utm_source=shareyourdesignpanel]

## Behavior Tree Structure
AutEx (Selector)
&nbsp;|-- Sequence_1 (Sequence)
&nbsp;|&nbsp;|-- Launch All Nodes
&nbsp;|&nbsp;|-- Set Datum
&nbsp;|&nbsp;|-- Fallback_16 (Selector)
&nbsp;|&nbsp;|&nbsp;|-- Launch Zed2i
&nbsp;|&nbsp;|&nbsp;|-- RetryUntilSuccess35
&nbsp;|&nbsp;|-- Fallback_17 (Selector)
&nbsp;|&nbsp;|&nbsp;|-- Launch arrow detection node
&nbsp;|&nbsp;|&nbsp;|-- RetryUntilSuccess37
&nbsp;|&nbsp;|-- Fallback_2 (Selector)
&nbsp;|&nbsp;|&nbsp;|-- Start Rosbag
&nbsp;|&nbsp;|&nbsp;|-- RetryUntilSuccess2
&nbsp;|&nbsp;|-- Fallback_3 (Selector)
&nbsp;|&nbsp;|&nbsp;|-- Always Fail Decorator
&nbsp;|&nbsp;|&nbsp;|-- Sequence_3 (Sequence)
&nbsp;|&nbsp;|&nbsp;|&nbsp;|-- Fallback_6 (Selector)
&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|-- ArrowDetectionCondition
&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|-- Sequence_6 (Sequence)
&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|-- Generate waypoints if arrow not detected
&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|-- Move Wheels
&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|-- ArrowDetectionCondition
&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|-- Fallback_7 (Selector)
&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|-- ArrowVisitedCondition
&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|-- Look for another arrow
&nbsp;|&nbsp;|&nbsp;|&nbsp;|-- Fallback_8 (Selector)
&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|-- Always Fail
&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|-- Sequence_7 (Sequence)
&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|-- Find tf of arrow
&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|-- Generate waypoints towards arrow
&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|-- Move Wheels
&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|-- Follow Waypoints
&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|-- Fallback_19 (Selector)
&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|-- DistanceConditionArrow
&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|-- Turn to align
&nbsp;|&nbsp;|&nbsp;|&nbsp;|-- Fallback_9 (Selector)
&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|-- Sequence_8 (Sequence)
&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|-- Stop wheels
&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|-- Start 10 sec timer
&nbsp;|&nbsp;|&nbsp;|&nbsp;|-- Fallback_10 (Selector)
&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|-- Recheck tf of arrow
&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|-- RetryUntilSuccess14
&nbsp;|&nbsp;|&nbsp;|&nbsp;|-- Fallback_11 (Selector)
&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|-- Save GPS Coordinates
&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|-- RetryUntilSuccess16
&nbsp;|&nbsp;|&nbsp;|&nbsp;|-- Fallback_12 (Selector)
&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|-- Spot turn
&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|-- RetryUntilSuccess12
&nbsp;|&nbsp;|&nbsp;|&nbsp;|-- Fallback_13 (Selector)
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
