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
        #print('Neighbour of Vertex ',i, j,vertex)
        rt=j+1
        up=i+1
        lt=j-1
        dn=i-1
        #print('i and j',i,j)
# Checking Connecting Vertex on Left
        if(lt>=0):
            neighbour[vertex].append(vertices[i][lt])
# Checking Connecting Vertex towards Up
        if(up<yLength):
            neighbour[vertex].append(vertices[up][j])
# Checking Connecting Vertex towards Down
        if(dn>=0):
            neighbour[vertex].append(vertices[dn][j])
# Checking Connecting Vertex on Right
        if(rt<xLength):
            neighbour[vertex].append(vertices[i][rt])

# Checking Connecting Vertex towards Right-Up
        if(up<yLength and rt<xLength):
            neighbour[vertex].append(vertices[up][rt])
# Checking Connecting Vertex towards Left-Up
        if(up<yLength and lt>=0):
            neighbour[vertex].append(vertices[up][lt])
# Checking Connecting Vertex towards Right-Dn
        if(dn>=0 and rt<xLength):
            neighbour[vertex].append(vertices[dn][rt])
# Checking Connecting Vertex towards Left-Dn
        if(dn>=0 and lt>=0):
            neighbour[vertex].append(vertices[dn][lt])

#print(neighbour)
# Depth First algorithm
stack=[]
visited=[]
for obs in range(len(xObstacleState)):
    visited.append(vertices[yObstacleState[obs]][xObstacleState[obs]])
    
visited.append(0)
counter=0
stack.append(0) #start with Zeroth vertex (First)
print('Stack ', stack)
while stack:
    counter=counter+1
    current=stack.pop()
    #print('Stack after pop', stack)
    #Take last element of the stack out and 
    #check for all the neighbours of the current Vertex(Node)
    #print('Iteration No. ', counter, 'Current Node to Explore ', current)
    #print('Visited ',visited)
    movePossibility=0
    for neighbourElements in neighbour[current]:
        #print('Neighbour Node', neighbourElements)
        if not neighbourElements in visited:
            stack.append(neighbourElements)
            #print('stack ',stack)
            movePossibility=1          
        if not current in visited:
            visited.append(current) #if (if not in) returns false
        if current in goalState:
            goalReached=1
            break
    if(goalReached==1):
        print('Goal Reached')
        break
    if(movePossibility==0):
        print('No New Movement Possible')
        break
#print('Vertices \n',vertices)
print('DFS path \n',visited)
xPath=[]
yPath=[]
plt.figure(1,figsize=(5,4))
plt.ion()
plt.show()
for nodeCounter in range(len(xObstacleState),len(visited)):
    node=visited[nodeCounter]
    currentState=np.where(vertices==node)
    yCoord=currentState[0]
    xCoord=currentState[1]
    xPath.append(xCoord)
    yPath.append(yCoord)
    #print('Index of',node,xCoord,yCoord)
    goal=np.where(vertices==goalState)
    yGoal=goal[0]
    xGoal=goal[1]
    plt.clf()
    plt.plot(xGoal,yGoal,'go')
    plt.plot(xObstacleState,yObstacleState,'ro')
    plt.plot(xPath,yPath,'ko')
    plt.text(xCoord, yCoord, str(str(xCoord[0])+","+str(yCoord[0])), style='italic')
    plt.plot(xCoord,yCoord,'bo')
    plt.ylim((-1,yLength))
    plt.xlim((-1,xLength))
    plt.pause(0.2)
