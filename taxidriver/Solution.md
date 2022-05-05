This question can be tricky to solve efficently but since the input size is small enough, we can just brute force it with
some minor optimizations.

From the start we explore every possible trip that we have enough fuel to complete.
Once we take a trip we remove it from the available trips and try every possible trip from this point.
We keep track of the best result from all trips and return what made the most.


Pseudo Code
```


function explore(position, trip. available_trips, fuel, money_made) {

    distance_to_trip = distance(position, trip)
    distance_of_trip = distance(trip.start, trip.end)

    total_distance = distance_to_trip + distance_of_trip
    remaining_fuel = fuel - total_distance


    most_money = money_made

    if remaining_fuel > 0 {

        for trip_option in available_trips {

            trips_minus_this_one = available_trips.filter(t => t != trip_option)

            made = explore(trip.end, 
                    trip_option, 
                    trips_minus_this_one, 
                    remaining_fuel,
                    money_made + trip_profit(trip))

            most_money = max(most_money, made)
        }
    }
    return most_money
}


starting_cordinate = (0,0)
available_trips = trips()

max_profit = 0
for trip in trips {
    trips_minus_this_one = trips.filter(t => t != trip)

    profit = explore(starting_cordinate, trip, trips_minus_this_one, fuel, 0)
    max_profit = max(profit, max_profit)
}