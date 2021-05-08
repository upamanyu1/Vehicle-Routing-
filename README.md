In the Vehicle Routing Problem (VRP), the goal is to find optimal routes for multiple vehicles visiting a set of locations.One answer is the routes with the least total distance. However, if there are no other constraints, the optimal solution is to assign just one vehicle to visit all locations, and find the shortest route for that vehicle. This is essentially the same problem as the TSP.

A better way to define optimal routes is to minimize the length of the longest single route among all vehicles. This is the right definition if the goal is to complete all deliveries as soon as possible. The VRP example below finds optimal routes defined this way.we'll describe other ways of generalizing the TSP by adding constraints on the vehicles, including:

Capacity constraints: the vehicles need to pick up items at each location they visit, but have a maximum carrying capacity.
Time windows: each location must be visited within a specific time window.Capacitated Vehicle Routing Problem with Time Windows (and optional orders).
   This is a sample using the routing library python wrapper to solve a
   CVRPTW problem.
   A description of the problem can be found here:
   http://en.wikipedia.org/wiki/Vehicle_routing_problem.
   The variant which is tackled by this model includes a capacity dimension,
   time windows and optional orders, with a penalty cost if orders are not
   performed.
   To help explore the problem, two classes are provided Customers() and
   Vehicles(): used to randomly locate orders and depots, and to randomly
   generate demands, time-window constraints and vehicles.
   Distances are computed using the Great Circle distances. Distances are in km
   and times in seconds.
   A function for the displaying of the vehicle plan
   display_vehicle_output
   The optimization engine uses local search to improve solutions, first
   solutions being generated using a cheapest addition heuristic.
   A class that generates and holds customers information.
        Randomly normally distribute a number of customers and locations within
        a region described by a rectangle.  Generate a random demand for each
        customer. Generate a random time window for each customer.
        May either be initiated with the extents, as a dictionary describing
        two corners of a rectangle in latitude and longitude OR as a center
        point (lat, lon), and box_size in km.  The default arguments are for a
        10 x 10 km square centered in Sheffield).
        Args: extents (Optional[Dict]): A dictionary describing a rectangle in
        latitude and longitude with the keys 'llcrnrlat', 'llcrnrlon' &
        'urcrnrlat' & 'urcrnrlat'  center (Optional(Tuple): A tuple of
        (latitude, longitude) describing the centre of the rectangle.  box_size
        (Optional float: The length in km of the box's sides.  num_stops (int):
        The number of customers, including the depots that are placed normally
        distributed in the rectangle.  min_demand (int): Lower limit on the
        randomly generated demand at each customer.  max_demand (int): Upper
        limit on the randomly generated demand at each customer.
            min_tw: shortest random time window for a customer, in hours.
            max_tw: longest random time window for a customer, in hours.
        Examples: To place 100 customers randomly within 100 km x 100 km
        rectangle, centered in the default location, with a random demand of
        between 5 and 10 units:  >>> customers = Customers(num_stops=100,
        box_size=100, ...                 min_demand=5, max_demand=10)
        alternatively, to place 75 customers in the same area with default
        arguments for demand:  >>> extents = {'urcrnrlon': 0.03403, 'llcrnrlon':
        -2.98325, ...     'urcrnrlat': 54.28127, 'llcrnrlat': 52.48150} >>>
        customers = Customers(num_stops=75, extents=extents)
               A Class to create and hold vehicle information.
    The Vehicles in a CVRPTW problem service the customers and belong to a
    depot. The class Vehicles creates a list of named tuples describing the
    Vehicles.  The main characteristics are the vehicle capacity, fixed cost,
    and cost per km.  The fixed cost of using a certain type of vehicles can be
    higher or lower than others. If a vehicle is used, i.e. this vehicle serves
    at least one node, then this cost is added to the objective function.
    Note:
        If numpy arrays are given for capacity and cost, then they must be of
        the same length, and the number of vehicles are inferred from them.
        If scalars are given, the fleet is homogeneous, and the number of
        vehicles is determined by number.
    Args: capacity (scalar or numpy array): The integer capacity of demand
    units.  cost (scalar or numpy array): The fixed cost of the vehicle.  number
    (Optional [int]): The number of vehicles in a homogeneous fleet.
    
    On running the program we get the output for the shortest path that a vehicle should follow without not exceeding the load carrying capacity are
    The Objective Value is 1275
Route 0: 2 Load(0) Time(0:00:00, 0:00:00) ->  34 Load(0) Time(3:51:51, 4:27:17) ->  13 Load(4) Time(6:26:28, 7:01:54) ->  10 Load(11) Time(8:25:41, 9:32:13) ->  43 Load(21) Time(17:20:40, 17:36:03) ->  39 Load(33) Time(18:53:14, 19:08:37) ->  45 Load(43) Time(22:24:23, 1 day, 0:00:00) ->  EndRoute 0. 

Route 1: 18 Load(0) Time(0:00:00, 0:00:00) ->  26 Load(0) Time(8:48:10, 8:53:03) ->  11 Load(1) Time(9:02:34, 9:07:27) ->  19 Load(9) Time(9:53:08, 9:58:01) ->  4 Load(18) Time(13:27:01, 16:10:07) ->  25 Load(30) Time(16:51:23, 19:34:29) ->  37 Load(31) Time(19:22:02, 21:41:57) ->  44 Load(40) Time(21:40:05, 1 day, 0:00:00) ->  EndRoute 1. 

Route 2: 5 Load(0) Time(0:00:00, 0:00:00) ->  1 Load(0) Time(4:08:01, 4:47:12) ->  21 Load(2) Time(7:00:32, 7:39:43) ->  38 Load(12) Time(9:15:21, 9:54:32) ->  42 Load(20) Time(10:40:17, 11:19:28) ->  16 Load(29) Time(13:06:41, 16:14:40) ->  22 Load(30) Time(19:05:05, 23:10:04) ->  45 Load(37) Time(19:55:01, 1 day, 0:00:00) ->  EndRoute 2. 

Route 3: Empty 

Route 4: Empty 

Route 5: 20 Load(0) Time(0:00:00, 0:00:00) ->  36 Load(0) Time(3:05:45, 7:01:35) ->  33 Load(2) Time(9:05:28, 9:07:13) ->  24 Load(8) Time(12:14:48, 12:16:33) ->  40 Load(11) Time(14:04:27, 14:06:12) ->  14 Load(14) Time(15:01:57, 15:03:42) ->  0 Load(28) Time(18:12:38, 20:26:25) ->  29 Load(34) Time(21:46:13, 1 day, 0:00:00) ->  EndRoute 5. 

Route 6: 6 Load(0) Time(0:00:00, 0:00:00) ->  35 Load(0) Time(2:14:41, 4:34:18) ->  47 Load(12) Time(4:47:26, 7:07:03) ->  46 Load(26) Time(7:18:22, 9:37:59) ->  31 Load(40) Time(10:04:22, 12:23:59) ->  7 Load(49) Time(11:25:30, 13:45:07) ->  8 Load(60) Time(13:00:41, 15:19:55) ->  12 Load(72) Time(14:16:12, 16:35:26) ->  49 Load(73) Time(14:31:44, 16:50:58) ->  20 Load(77) Time(15:34:23, 1 day, 0:00:00) ->  EndRoute 6. 

Route 7: 45 Load(0) Time(0:00:00, 0:00:00) ->  3 Load(0) Time(2:32:10, 3:19:19) ->  9 Load(6) Time(4:08:33, 4:55:42) ->  15 Load(17) Time(5:52:02, 6:39:11) ->  28 Load(23) Time(7:03:33, 7:50:42) ->  41 Load(36) Time(8:25:26, 12:52:09) ->  32 Load(45) Time(14:48:26, 16:58:57) ->  17 Load(54) Time(20:01:58, 20:43:54) ->  23 Load(63) Time(23:18:04, 1 day, 0:00:00) ->  EndRoute 7. 


dropped nodes: 
Vehicle 0 is used True
Vehicle 1 is used True
Vehicle 2 is used True
Vehicle 3 is used False
Vehicle 4 is used False
Vehicle 5 is used True
Vehicle 6 is used True
Vehicle 7 is used True

The pictoral representation of different paths are as 
![Figure_1](https://user-images.githubusercontent.com/40518603/117528093-15ef1780-afee-11eb-8b77-bc60f0ba8440.jpeg)
