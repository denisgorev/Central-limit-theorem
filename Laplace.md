
# Центральная предельная теорема


```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import scipy.stats as sts
%matplotlib inline
import math
```

Распределе́ние Лапла́са (двойно́е экспоненциа́льное) — в теории вероятностей это непрерывное распределение случайной величины, при котором плотность вероятности есть:

$$ f(x) = \frac{\alpha}{2}  e^{\alpha|x - \beta|},\;     -\infty < x < \infty, $$
$$где\; \alpha>0 - параметр\; масштаба,\;  -\infty < \beta < \infty - \;параметр \;сдвига$$
$$математическое \;ожидание = \beta, \;дисперсия = \frac{2}{\alpha^2}$$

более подробно тут: 
https://en.wikipedia.org/wiki/Laplace_distribution




```python
#Задаем параметры распределения

alpha = 1
betta = 0

#Расчет среднего, дисперсии и среднеквадратичного отклонения

disp_laplace = 2/ alpha**2 #дисперсия
mean_lapace = betta #матожидание
sigma_laplace = math.sqrt(disp_laplace) #среднеквадратичное отклонение

print("Матожидание: ", mean_lapace)
print("Дисперсия: ", disp_laplace)
```

    Матожидание:  0
    Дисперсия:  2.0
    


```python
laplas_rv = sts.laplace(betta, alpha) # задаем случайную величину

x = np.linspace(-4,4,1000) #определяем массив точек для построения плотности распределения

pdf = laplas_rv.pdf(x) #теоритическая плотность распределения

sample = laplas_rv.rvs(1000) #генерируем случайную выборку в 1000 значений

#построение гистограммы
plt.hist(sample, bins=35, density=True, label='hist')
plt.plot(x, pdf, label='theoretical Laplace')
plt.legend(loc='upper right')
plt.ylabel('$f(x)$/number of samples')
plt.xlabel('$x$') 
```




    Text(0.5, 0, '$x$')




![png](output_4_1.png)


## Оценка распределения выборочного среднего при n = 5


```python
a=np.array([]) #задали массив
n = 5

#цикл генерации выборок и средних значений, в итоге получаем 1000 значений средних n=5
i=1
while i < 1000:
    a = np.append(a, sum(laplas_rv.rvs(n))/n)
    i+=1
  
x = np.linspace(-4, 4, 100)#определяем массив точек для построения плотности распределения
 
sigma = math.sqrt(disp_laplace/n) #сигма для нормального распределения выборки средних
norm_rv = sts.norm(mean_lapace, sigma)#определяем нормальное распределение с характеристиками распределения Лапласа
pdf = norm_rv.pdf(x)#нормальная плотность распределения
plt.plot(x, pdf, label='theoretical normal')#график нормальной плотности распределения
plt.hist(a, bins=25, density=True, label='hist') #гистограмму массива средних при n=5
plt.ylabel('number of samples')
plt.xlabel('$x$')
plt.legend(loc='upper right')

```




    <matplotlib.legend.Legend at 0x2517ab01160>




![png](output_6_1.png)


## Оценка распределения выборочного среднего при n = 30


```python
a=np.array([]) #задали массив
n = 30

#цикл генерации выборок и средних значений, в итоге получаем 1000 значений средних n=30
i=1
while i < 1000:
    a = np.append(a, sum(laplas_rv.rvs(n))/n)
    i+=1
    
x = np.linspace(-4, 4, 100)#определяем массив точек для построения плотности распределения

sigma = math.sqrt(disp_laplace/n) #сигма для нормального распределения выборки средних
norm_rv = sts.norm(mean_lapace, sigma)#определяем нормальное распределение с характеристиками распределения Лапласа
pdf = norm_rv.pdf(x)#нормальная плотность распределения
plt.plot(x, pdf, label='theoretical normal')#график нормальной плотности распределения
plt.hist(a, bins=30, density=True, label='hist') #гистограмму массива средних при n=30
plt.legend(loc='upper right')
plt.ylabel('number of samples')
plt.xlabel('$x$')
```




    Text(0.5, 0, '$x$')




![png](output_8_1.png)


## Оценка распределения выборочного среднего при n = 100


```python
a=np.array([]) #задали массив
n = 100

#цикл генерации выборок и средних значений, в итоге получаем 1000 значений средних n=100
i=1
while i < 1000:
    a = np.append(a, sum(laplas_rv.rvs(n))/n)
    i+=1
    
x = np.linspace(-4, 4, 100)#определяем массив точек для построения плотности распределения

sigma = math.sqrt(disp_laplace/n) #сигма для нормального распределения выборки средних
norm_rv = sts.norm(mean_lapace, sigma)#определяем нормальное распределение с характеристиками распределения Лапласа
pdf = norm_rv.pdf(x)#нормальная плотность распределения
plt.plot(x, pdf, label='theoretical normal')#график нормальной плотности распределения
plt.hist(a, bins=10, density=True, label='hist') #гистограмму массива средних при n=100
plt.legend(loc='upper right')
plt.ylabel('number of samples')
plt.xlabel('$x$')
```




    Text(0.5, 0, '$x$')




![png](output_10_1.png)


## Оценка распределения выборочного среднего при n = 150


```python
a=np.array([]) #задали массив
n = 150

#цикл генерации выборок и средних значений, в итоге получаем 1000 значений средних n=150
i=1
while i < 1000:
    a = np.append(a, sum(laplas_rv.rvs(n))/n)
    i+=1
    
x = np.linspace(-4, 4, 100)#определяем массив точек для построения плотности распределения

sigma = math.sqrt(disp_laplace/n) #сигма для нормального распределения выборки средних
norm_rv = sts.norm(mean_lapace, sigma)#определяем нормальное распределение с характеристиками распределения Лапласа
pdf = norm_rv.pdf(x)#нормальная плотность распределения
plt.plot(x, pdf, label='theoretical normal')#график нормальной плотности распределения
plt.hist(a, bins=20, density=True, label='hist') #гистограмму массива средних при n=150
plt.legend(loc='upper right')
plt.ylabel('number of samples')
plt.xlabel('$x$')
```




    Text(0.5, 0, '$x$')




![png](output_12_1.png)


При решении данной задачи использовалась непрерывная функция распределения Лапласа. 
Были построены гистограмы для n=5, n=30, n=100, n=150
Были измерены необходимые значения - среднее и дисперсия. Для каждой гистаграммы построены функции нормального распределения

Функция плотности распределения Лапласа является симметричной, функция сходится быстро. Совпадение нормального распределения и гистограмы по выборочным средним наблюдается уже при n=5.


```python

```
