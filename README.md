# .Effgithub
import matplotlib.pyplot as plt
import time
import random

def huz_bub_sort(lst):
    start = time.perf_counter_ns()
    passflag = True
    while passflag == True:
        count = 0
        for i in range(len(lst)-1):
            if lst[i] > lst[i+1]:
                lst [i] , lst [i+1] = lst[i+1] , lst[i]
                count += 1
        if count == 0:
            passflag = False
    end = time.perf_counter_ns()
    timings = (end - start) / 1e+9
    return timings

def most_eff_bubble_sort(lst):
    start = time.perf_counter_ns()
    n = len(lst)
    swapped = True
    while swapped:
        swapped = False
        for i in range(1, n):
            if lst[i - 1] > lst[i]:
                lst[i - 1], lst[i] = lst[i], lst[i - 1]
                swapped = True
    end = time.perf_counter_ns()
    timings = (end - start) / 1e+9
    return timings

def least_eff_bubble_sort(lst):
    start = time.perf_counter_ns()
    n = len(lst)
    for i in range(n):
        for j in range(n - 1):
            if lst[j] > lst[j + 1]:
                lst[j], lst[j + 1] = lst[j + 1], lst[j]
    end = time.perf_counter_ns()
    timings = (end - start) / 1e+9
    return timings


def rand_lst(number):
    lst = [random.randint(1,10000) for i in range(number)]
    return lst

def eff_plot(repeat = 10):
    y_values = [1000, 2000, 3000, 4000, 5000, 6000, 7000, 8000, 9000, 10000]
    huz_lst , most_lst , least_lst = [] , [] , []
    huz_add , most_add , least_add = 0 , 0 , 0
    for values in y_values:
        for i in range(repeat):
            huz_add += huz_bub_sort(rand_lst(i))
            most_add += most_eff_bubble_sort(rand_lst(i))
            least_add += least_eff_bubble_sort(rand_lst(i))
        huz_lst.append((huz_add / repeat))
        most_lst.append((most_add / repeat))
        least_lst.append((least_add / repeat))
    plt.plot(most_lst, y_values , 'o-' , label = 'most' , marker = 'o' , markerfacecolor = 'black' , markeredgecolor = 'black' , markersize = 4)
    plt.plot(huz_lst, y_values , 'o-' , label = 'huz' , marker = 'o' , markerfacecolor = 'black' , markeredgecolor = 'black' , markersize = 4)
    plt.plot(least_lst, y_values , 'o-' , label ='least' , marker = 'o' , markerfacecolor = 'black' , markeredgecolor = 'black' , markersize = 4)
    plt.xlabel('Average Time Taken in seconds')
    plt.ylabel('Number of random items')
    plt.title('Efficiency of each variation of bubble sorts')
    plt.legend()
    plt.show()

eff_plot()
