I modelled this question after how some implementations
of hash tables use open addressing to resolve collisions.

There is not really much to this question if you follow the instructions


Python Codeish
```
TAKEN = -1
size = 100
parking_spots = [TAKEN] * 100 

def hash_license_plate(plate):
    return plate % size

colissions = 0
for plate in read_license_plates():
    spot = hash_license_plate(plate)
    peek = parking_spots[spot]
    while peek != TAKEN:
        collisions += 1
        spot = (spot + 1) % size
        peek = parking_spots[spot]
    parkings_spots[spot] = plate

result = colission * size
```