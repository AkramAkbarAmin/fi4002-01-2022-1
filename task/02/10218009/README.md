# 10218009
Akram Akbar Amin


## materi sebelumnya
+ Basic Python
+ Rekursif
+ Grafik, Module, Function
+ Lorenz
+ Grafik Metode Euler
+ Predator-prey
+ Pegas Teredam
+ Bandul Pegas
+ Monte Carlo
+ Discrete Fourier Transform
+ Sistem Rantai Membentang


## materi paling menarik
+ Grafik Metode Euler dan Runge Kutta orde 4 - Pengaplikasian materinya dapat menyelesaikan berbagai problem fisis

## materi paling membosankan
+ Sistem Rantai Membentang - Materinya susah untuk dipahami


## materi yang sudah dipahami
+ Basic Python
+ Rekursif
+ Grafik, Module, Function
+ Lorenz
+ Grafik Metode Euler
+ Predator-prey
+ Pegas Teredam
+ Bandul Pegas
+ Monte Carlo


## materi yang belum dipahami
+ Discrete Fourier Transform
+ Sistem Rantai Membentang


## contoh program
+ Buat suatu contoh program dalam Python dan sertakan di sini dengan hasil keluarnnya.

```python
# contoh program python
#pers panas 2D 

import numpy as np
import matplotlib.pyplot as plt


axis_size = 100     #ukuran 1D grid
side_length = 10    #panjang pelat 10 (cm)
dx = side_length/axis_size   #step ruang
axis_points = np.linspace(0,10,axis_size)   #titik grid ruang 

#grid waktu
T = 1.0                                       #total waktu (s)
k = 1.011                                     #difusivitas termal pelat cm^2/s.
dt = ((1/axis_size)**2)/(2*k)                 #ukuran time step memastikan disktritisasi stabil 
n = int(T/dt)                                 #jumlah time step

#maks suhu
max_temp = 100


# kondisi awal 2D dengan Gaussian (puncak di tengah)

def temp_init(x,y,c,m_temp):
    return m_temp*np.exp(-((x-side_length/2)**2 + (y-side_length/2)**2)/c**2)

#buat meshgrid
X, Y = np.meshgrid(axis_points, axis_points)

#standar deviasi
c = 2

#T awal
U = temp_init(X, Y, c, max_temp)

#set BC pada t=0
#ujung bawah paling panas
U[:,0] = 25
U[:,-1] = 150
U[0,:] = 5
U[-1,:] = 300

#nilai batas
B1 = U[:,0]
B2 = U[:,-1]
B3 = U[0,:]
B4 = U[-1,:]

#awal
plt.imshow(U, cmap ='hot', vmin = 0, vmax = max_temp, extent= [0,10,0,10])
plt.tick_params(axis='both', which='major', labelsize=16)
plt.xlabel('ujung pelat horizontal (cm)', fontsize = 16)
plt.ylabel('ujung pelat vertikal (cm)', fontsize = 16)
plt.title('peta suhu awal')
plt.show()

#pers laplace 
def laplacian(Z,d_ex):
    Ztop = Z[0:-2,1:-1]
    Zleft = Z[1:-1,0:-2]
    Zbottom = Z[2:,1:-1]
    Zright = Z[1:-1,2:]
    Zcenter = Z[1:-1,1:-1]
    return (Ztop + Zleft + Zbottom + Zright - 4 * Zcenter) / d_ex**2

#selesaikan Pers diff

n=10000

for i in range(n):
    deltaU = laplacian(U,dx)
    Uc = U[1:-1,1:-1] #ambil nilai di dalam
    U[1:-1,1:-1] = Uc + dt * (k*deltaU)# + 0.01*np.random.randn()#update variabel 
    #syarat batas tidak berubah (steady state,Direchlet boundary conditions)
    U[:,0] = B1
    U[:,-1] = B2
    U[0,:] = B3
    U[-1,:] = B4

#tampilkan
plt.imshow(U,cmap = 'hot', vmin = 0, vmax = max_temp, extent= [0,10,0,10])
plt.tick_params(axis='both', which='major', labelsize=16)
plt.xlabel('ujung pelat horizontal (cm)', fontsize = 16)
plt.ylabel('ujung pelat vertikal (cm)', fontsize = 16)
plt.title('peta suhu akhir')
plt.show()


Hasilnya adalah

!(https://github.com/AkramAkbarAmin/fi4002-01-2022-1/blob/main/task/02/10218009/Pers%20panas%202D.png)
```


## cara perkuliahan
+ Tuliskan pendapat Anda mengenai cara perkuliahan selama ini dan cantumkan usulan untuk perkuliahan setelah UTS.


## topik sistem fisis
+ Tuliskan sistem fisis yang menarik bagi Anda untuk dikaji lebih dalam dan jelaskan alasannya mengapa.


## simulasi dan visualisasi
+ Apakah Anda tertarik dengan simulasi dan visualisasi? Jelaskan topik yang ingin Anda simulasikan / visualisasikan serta cantumkan alasannya dan perkiraan pusataka Python yang perlu digunakan.
