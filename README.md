# LeetCode 2353 - Design a Food Rating System
# Author: wilson muriithi

import heapq

class FoodRatings:
    def __init__(self, foods, cuisines, ratings):
        self.food_to_cuisine = {}
        self.food_to_rating = {}
        self.cuisine_heap = {}
        for f,c,r in zip(foods,cuisines,ratings):
            self.food_to_cuisine[f] = c
            self.food_to_rating[f] = r
            if c not in self.cuisine_heap:
                self.cuisine_heap[c] = []
            heapq.heappush(self.cuisine_heap[c], (-r, f))
