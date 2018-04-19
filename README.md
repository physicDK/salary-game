# salary-game
#BANG
n = 1000
v = np.ones(n)
w = np.array(v)
x = w*40
y = x.tolist()


from random import randint

for i in range(100000):
    a = randint(1, n)
    b = randint(1, n)
    if a != b:
        coin = randint(0,1)
        if coin==0 and y[a-1] != 0:
            y[a-1] -= 10
            y[b-1] += 10
        elif coin==1 and y[b-1] != 0:
            y[a-1] += 10
            y[b-1] -= 10

plt.hist(y,15)
plt.show()           
    
#print y





from scipy import optimize

import collections, numpy

a= numpy.array(y)
unique, counts = numpy.unique(a, return_counts=True)
q = dict(zip(unique, counts))


names = ['id','data']
formats = ['f8','f8']
dtype = dict(names = names, formats=formats)
qarray = np.array(list(q.items()), dtype=dtype)
qarray.sort()

xd =np.asarray([i[0] for i in qarray])
yd =np.asarray([i[1] for i in qarray])

print xd
print qarray


x_data = xd
y_data = yd
def test_func(b, a):
    return a * np.exp(-b/40)

popt, pcove = optimize.curve_fit(test_func, x_data, y_data)

plt.plot(x_data, test_func(x_data, *popt),'g--',tuple(popt))
plt.show()

popt
