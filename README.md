# LeetCode 2353 - Design a Food Rating System
# Author: Your Name - Student ID

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

    def changeRating(self, food: str, newRating: int) -> None:
        cuisine = self.food_to_cuisine[food]
        self.food_to_rating[food] = newRating
        heapq.heappush(self.cuisine_heap[cuisine], (-newRating, food))

    def highestRated(self, cuisine: str) -> str:
        heap = self.cuisine_heap[cuisine]
        while heap:
            neg_r, food = heap[0]
            if -neg_r == self.food_to_rating[food]:
                return food
            heapq.heappop(heap)
        return ""
