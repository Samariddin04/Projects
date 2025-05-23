# Amazon.com Fulfillment

Your job is to determine the most cost effective way to deliver 10,000 orders on a particular day from three fulfillment centers given the current placement of inventory, the cost to process and ship each order from each fulfillment center, and the cost of transshipping items among fulfillment centers to provide sufficient inventory for each fulfillment center to ship the items it will fulfill. To do so, your solution must specify which of the three fulfillment centers will process each order and how many units of each item need to be transshipped among the fulfillment centers. No fulfillment center can fulfill any order unless its current inventory level plus the inventory transshipped to it meets or exceed the order quantity for every item in every order.

# The Data

The data represent a context with 3 fulfillment centers, 10,000 items, and 10,000 orders. The data are provided in the form of four text files that can be read into a Python program as a numpy arrays using the np.genfromtxt(filename) command, where filename is the path to the file that contains the data.

• order_10000_10000.txt: A 10,000×10,000 array where each of the 10,000 rows contains the order quantities for each order. Each of 10,000 columns represents the 10,000 possible items that could be ordered. A value of 2, for example, in row 987 and column 7 indicates that order 987 includes a quantity of 2 of item 7.

• tshp10000_3_3.txt: This file contains the data for a three-dimensional array that is ultimately 10000×3×3. The first dimension corresponds to the 10,000 items and the remaining dimensions give data for each item in terms of how much it costs to ship one unit of the item between each possible combination of fulfillment centers. For example, a 5 in position (97, 1, 2) in this array indicates that it costs $5 to transship one unit of item 97 from Fulfillment Center 1 to Fulfillment Center 2. Three-dimensional numpy arrays cannot be stored directly in text files, and so the data in this file is one-dimensional. It, therefore, needs to be reshaped into its appropriate dimensions. For the data for 10000 items, the code to input this data into a Python variable named tshp would be this:

import numpy as np
tshp = np.genfromtxt('tshp10000_3_3.txt')
tshp = tshp.reshape(10000,3,3)

• inv10000_10000_3.txt: A 3×10,000 where each row contains the number of units of inventory available for each of 10,000 items at each of the 3 fulfillment centers. A value of 20, for example, in row 2 and column19, indicates that Fulfillment Center 2 has 20 units of item 19.

• ship_cost10000_10000_3.txt: this file represents data for the cost of shipping each order from each fulfillment center. This is an array with a number of rows equal to the number of orders and a number of columns equal to the number of fulfillment centers.

Each order may have a different shipping cost depending on the center’s proximity to the customer.
While these files are somewhat large, smaller input files representing 100 items and 100 orders are provided also for development purposes. Additionally, although not reflected in a data file, each fulfillment center can handle, at most, 5,000 orders in a day.
