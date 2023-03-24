## Draw nodes and arcs on geo map

### Create basic data
```
locations=["Los Angeles","Dallas","Miami", "Atlanta"]
lats = [34.07,32.96,25.878, 33.97]
longs = [-117.93,-97.01,-80.33, -84.53]
```


### Draw Nodes
```
import plotly.graph_objects as go
# Draw nodes
size_scale = [40,20,30,20] # size of the node
color_scale = [8,10,2,6] # we can set colors between cmin, cmax
fig = go.Figure(data=go.Scattergeo(
    lat = lats, # list or series from dataframe
    lon = longs, 
    text = locations, #list of names
    marker = dict(
        opacity = 0.9, 
        size = size_scale, # use different sizes
        color = color_scale,
        autocolorscale = True,
        cmin=0, cmax = 10, #range for color scale
        colorbar_title="Population",
        colorbar_thickness=5,
    )
))
```

### Draw Arcs
```
# Draw arcs
arcs = [[0,1],[1,2],[0,2], [0,3], [3,2], [1,3]]
colors=['blue','green','red','blue','black','yellow']
widths = [4,1,4,4,1,1]
for i,arc in enumerate(arcs): #for each arc
    from_loc = arc[0]
    to_loc = arc[1]
    fig.add_trace( # draw a line
        go.Scattergeo(
            locationmode = 'USA-states',
            lon = [longs[from_loc], longs[to_loc]], #set start
            lat = [lats[from_loc], lats[to_loc]], # set end
            mode = 'lines', #line
            line = dict(width = widths[i],color = colors[i]), #set arc width
            opacity = 0.6,
        )
    )
```


### Draw map
```
fig.update_layout(
    showlegend = False,
    height=500,
    width=1000,
    margin={"r":0,"t":0,"l":0,"b":0},
    geo = dict(
        scope = 'usa',
        projection_type='albers usa',
        showland = True,
        bgcolor="rgb(255, 255, 255)",
        landcolor = "rgb(212, 212, 212)",
        subunitcolor = "rgb(133, 212, 122)",
        #countrycolor = "rgb(255, 128, 255)",
        showsubunits = True,
    ),
    title='USA Map with Nodes and Edges',
)
```
