# Depth First for Robotic Applications
The code is written in Python 3.7
## Add Goal
goalState=[28] 
## Let Node number 28 is the Goal Node on the graph
goalReached=0
## Add Obstacle
xObstacleState=[2]
yObstacleState=[2]

## Creating Vertices for the Graph
## Vertex Number to Start from 1

    vertices=[[i]for i in range(xLength*yLength)]
    vertices=np.reshape(vertices,(yLength,xLength))

## Creating Neighbours for each Vertex of the Graph
## The Neighbour List is the option of the movement in reverse order
## Last element of the list is the first option for movement
neighbour=[[]for i in range(xLength*yLength)]
for i in range(0,yLength):
    for j in range(0, xLength):
        vertex=vertices[i][j]
        rt=j+1
        up=i+1
        lt=j-1
        dn=i-1
### Checking Connecting Vertex on Left
        if(lt>=0):
            neighbour[vertex].append(vertices[i][lt])
### Checking Connecting Vertex towards Up
        if(up<yLength):
            neighbour[vertex].append(vertices[up][j])
### Checking Connecting Vertex towards Down
        if(dn>=0):
            neighbour[vertex].append(vertices[dn][j])
### Checking Connecting Vertex on Right
        if(rt<xLength):
            neighbour[vertex].append(vertices[i][rt])
### Depth First algorithm
stack=[]
visited=[]
for obs in range(len(xObstacleState)):
    visited.append(vertices[yObstacleState[obs]][xObstacleState[obs]])
    
visited.append(0)
counter=0
stack.append(0) #start with Zeroth vertex (First)
print('Stack ', stack)

