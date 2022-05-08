---
title: "Aplicación del modelo lineal general"
author: "Vásquez V., C.R.A."
date: "2022-05-07"
subtitle: Recuento de escarabajos en un área
institute: InkaStats - Data Science Solutions S.A.C.
site: bookdown::bookdown_site
---

```{=html}
<style>
body {
text-align: justify}
</style>
```


# Reconocimiento de variables

Para crear un modelo de regresión lineal se tomó como variable dependiente al *Recuento de escarabajos en un área*. Las posibles variables predictoras fueron:

*Temperatura*: Temperatura (°C) ambiental.

*Altura*: Altura (msnsm) del ambiente.

*Humedad*: Humedad relativa (%) ambiental.

*Machos*: Genero predominante en el área (0 si predominan machos, 1 si hembras).

*Urbano*: 0 (No) si el conteo se hizo en un área no urbana, 1 (Sí) si el conteo se hizo en un área urbana.

# Análisis exploratorio y descriptivo

## Análisis descriptivo

Los datos cuenta con un total de 200 observaciones (n=200).

\changefontsizes{6pt}


```
Descriptive Statistics  
datos  
N: 200  

                    Altura   Humedad   Recuento   Temperatura
----------------- -------- --------- ---------- -------------
             Mean   255.54     81.85     196.93         20.50
          Std.Dev   133.68      7.04      72.10          4.93
              Min    25.00     70.29      67.00         12.00
               Q1   138.50     75.73     134.00         16.00
           Median   247.00     81.47     190.50         20.00
               Q3   368.50     88.04     255.50         24.00
              Max   495.00     94.78     333.00         30.00
              MAD   166.05      8.67      88.96          5.93
              IQR   228.50     12.28     120.75          8.00
               CV     0.52      0.09       0.37          0.24
         Skewness     0.18      0.12       0.15          0.10
      SE.Skewness     0.17      0.17       0.17          0.17
         Kurtosis    -1.19     -1.22      -1.13         -1.11
          N.Valid   200.00    200.00     200.00        200.00
        Pct.Valid   100.00    100.00     100.00        100.00
```

\changefontsizes{7pt}


```
  Temperatura       Altura         Humedad          Macho     Urbano      Recuento    
 Min.   :12.0   Min.   : 25.0   Min.   :70.29   Machos :160   No: 94   Min.   : 67.0  
 1st Qu.:16.0   1st Qu.:139.2   1st Qu.:75.75   Hembras: 40   Sí:106   1st Qu.:134.0  
 Median :20.0   Median :247.0   Median :81.47                          Median :190.5  
 Mean   :20.5   Mean   :255.5   Mean   :81.85                          Mean   :196.9  
 3rd Qu.:24.0   3rd Qu.:367.8   3rd Qu.:88.03                          3rd Qu.:254.8  
 Max.   :30.0   Max.   :495.0   Max.   :94.78                          Max.   :333.0  
```

## Gráficos exploratorios

<img src="bookdownproj_files/figure-html/unnamed-chunk-3-1.png" width="672" style="display: block; margin: auto;" />

<img src="bookdownproj_files/figure-html/unnamed-chunk-4-1.png" width="672" style="display: block; margin: auto;" />

<img src="bookdownproj_files/figure-html/unnamed-chunk-5-1.png" width="672" style="display: block; margin: auto;" />

<img src="bookdownproj_files/figure-html/unnamed-chunk-6-1.png" width="672" style="display: block; margin: auto;" />

<img src="bookdownproj_files/figure-html/unnamed-chunk-7-1.png" width="672" style="display: block; margin: auto;" />

# Modelo de regresión lineal multiple completo

## Resumen del modelo

A continuación presentamos el modelo completo:

$$Recuento=\beta_0+\beta_1*Temperatura+\beta_2*Altura+\beta_3*Humedad+\beta_4*Hembras+\beta_5*Urbano+\epsilon_i$$

\changefontsizes{5pt}


```

Call:
lm(formula = Recuento ~ ., data = datos)

Residuals:
     Min       1Q   Median       3Q      Max 
-13.4092  -3.1671  -0.4643   2.5792  12.7935 

Coefficients:
              Estimate Std. Error t value             Pr(>|t|)    
(Intercept)  25.232477   4.691091   5.379          0.000000214 ***
Temperatura   1.617856   0.072173  22.416 < 0.0000000000000002 ***
Altura        0.537264   0.003014 178.255 < 0.0000000000000002 ***
Humedad       0.007299   0.051288   0.142               0.8870    
MachoHembras -0.165017   0.989351  -0.167               0.8677    
UrbanoSí      1.248129   0.712726   1.751               0.0815 .  
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Residual standard error: 5.016 on 194 degrees of freedom
Multiple R-squared:  0.9953,	Adjusted R-squared:  0.9952 
F-statistic:  8185 on 5 and 194 DF,  p-value: < 0.00000000000000022
```

## Análisis de variancia


```
Analysis of Variance Table

Response: Recuento
             Df  Sum Sq Mean Sq    F value               Pr(>F)    
Temperatura   1    5306    5306   210.8877 < 0.0000000000000002 ***
Altura        1 1024231 1024231 40709.3013 < 0.0000000000000002 ***
Humedad       1       0       0     0.0164              0.89816    
Macho         1       1       1     0.0199              0.88785    
Urbano        1      77      77     3.0667              0.08149 .  
Residuals   194    4881      25                                    
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
```

# Selección de variables paso a paso

## Partición inicial de la base de datos

### Resumen de la base de datos de entrenamiento

\changefontsizes{6pt}


```
  Temperatura        Altura       Humedad          Macho     Urbano     Recuento    
 Min.   :12.00   Min.   : 25   Min.   :70.29   Machos :130   No:74   Min.   : 67.0  
 1st Qu.:16.00   1st Qu.:141   1st Qu.:77.21   Hembras: 31   Sí:87   1st Qu.:134.0  
 Median :21.00   Median :231   Median :81.58                         Median :190.0  
 Mean   :20.62   Mean   :255   Mean   :81.95                         Mean   :196.7  
 3rd Qu.:25.00   3rd Qu.:367   3rd Qu.:88.01                         3rd Qu.:254.0  
 Max.   :30.00   Max.   :495   Max.   :94.31                         Max.   :333.0  
```

### Resumen de la base de datos de prueba

\changefontsizes{6pt}


```
  Temperatura        Altura         Humedad          Macho    Urbano     Recuento    
 Min.   :12.00   Min.   : 57.0   Min.   :70.42   Machos :30   No:20   Min.   : 83.0  
 1st Qu.:16.00   1st Qu.:133.5   1st Qu.:74.67   Hembras: 9   Sí:19   1st Qu.:137.0  
 Median :20.00   Median :255.0   Median :80.38                        Median :195.0  
 Mean   :20.03   Mean   :257.6   Mean   :81.44                        Mean   :197.7  
 3rd Qu.:23.50   3rd Qu.:367.5   3rd Qu.:88.61                        3rd Qu.:250.0  
 Max.   :28.00   Max.   :494.0   Max.   :94.78                        Max.   :321.0  
```

### Verificación de la distribución de la variable respuesta (Recuento)

<img src="bookdownproj_files/figure-html/unnamed-chunk-12-1.png" width="672" style="display: block; margin: auto;" />

## Forward

### Resumen del modelo

\changefontsizes{5pt}


```

Call:
lm(formula = Recuento ~ Altura + Temperatura + Urbano, data = datos.train)

Residuals:
     Min       1Q   Median       3Q      Max 
-13.1978  -3.2243  -0.3167   2.4130  12.1485 

Coefficients:
            Estimate Std. Error t value            Pr(>|t|)    
(Intercept) 24.47646    1.88438  12.989 <0.0000000000000002 ***
Altura       0.53687    0.00290 185.140 <0.0000000000000002 ***
Temperatura  1.66862    0.07687  21.708 <0.0000000000000002 ***
UrbanoSí     1.68814    0.77633   2.175              0.0312 *  
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Residual standard error: 4.88 on 157 degrees of freedom
Multiple R-squared:  0.9955,	Adjusted R-squared:  0.9954 
F-statistic: 1.164e+04 on 3 and 157 DF,  p-value: < 0.00000000000000022
```

### AIC del modelo


```
[1] 973.239
```

### Coeficientes del modelo

\changefontsizes{5pt}

<img src="bookdownproj_files/figure-html/unnamed-chunk-15-1.png" width="672" style="display: block; margin: auto;" />

### VIF de las variables seleccionadas


```
     Altura Temperatura    UrbanoSí 
   1.008899    1.003479    1.012153 
```

### MSE del entrenamiento


```
[1] 23.21906
```

### Indicadores predictivos con la base de datos de entrenamiento


```
     RMSE  Rsquared       MAE 
4.8186162 0.9955231 3.7545822 
```

## Backward

### Resumen del modelo

\changefontsizes{5pt}


```

Call:
lm(formula = Recuento ~ Temperatura + Altura + Urbano, data = datos.train)

Residuals:
     Min       1Q   Median       3Q      Max 
-13.1978  -3.2243  -0.3167   2.4130  12.1485 

Coefficients:
            Estimate Std. Error t value            Pr(>|t|)    
(Intercept) 24.47646    1.88438  12.989 <0.0000000000000002 ***
Temperatura  1.66862    0.07687  21.708 <0.0000000000000002 ***
Altura       0.53687    0.00290 185.140 <0.0000000000000002 ***
UrbanoSí     1.68814    0.77633   2.175              0.0312 *  
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Residual standard error: 4.88 on 157 degrees of freedom
Multiple R-squared:  0.9955,	Adjusted R-squared:  0.9954 
F-statistic: 1.164e+04 on 3 and 157 DF,  p-value: < 0.00000000000000022
```

### AIC del modelo


```
[1] 973.239
```

### Coeficientes del modelo

\changefontsizes{5pt}

<img src="bookdownproj_files/figure-html/unnamed-chunk-21-1.png" width="672" style="display: block; margin: auto;" />

### VIF de las variables seleccionadas


```
Temperatura      Altura    UrbanoSí 
   1.003479    1.008899    1.012153 
```

### MSE del entrenamiento


```
[1] 23.21906
```

### Indicadores predictivos con la base de datos de entrenamiento


```
     RMSE  Rsquared       MAE 
4.8186162 0.9955231 3.7545822 
```

## Stepwise

### Resumen del modelo

\changefontsizes{5pt}


```

Call:
lm(formula = Recuento ~ Altura + Temperatura, data = datos.train)

Residuals:
     Min       1Q   Median       3Q      Max 
-14.1057  -3.1063  -0.3891   2.5381  12.9691 

Coefficients:
             Estimate Std. Error t value            Pr(>|t|)    
(Intercept) 25.740129   1.813561   14.19 <0.0000000000000002 ***
Altura       0.536282   0.002921  183.60 <0.0000000000000002 ***
Temperatura  1.658877   0.077636   21.37 <0.0000000000000002 ***
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Residual standard error: 4.937 on 158 degrees of freedom
Multiple R-squared:  0.9954,	Adjusted R-squared:  0.9953 
F-statistic: 1.705e+04 on 2 and 158 DF,  p-value: < 0.00000000000000022
```

### AIC del modelo


```
[1] 976.0164
```

### Coeficientes del modelo

\changefontsizes{5pt}

<img src="bookdownproj_files/figure-html/unnamed-chunk-27-1.png" width="672" style="display: block; margin: auto;" />

### VIF de las variables seleccionadas


```
     Altura Temperatura 
   1.000067    1.000067 
```

### MSE del entrenamiento


```
[1] 23.91837
```

### Indicadores predictivos con la base de datos de entrenamiento


```
     RMSE  Rsquared       MAE 
4.8906414 0.9953883 3.8580781 
```

## Comparación de modelos

\changefontsizes{7pt}

|            |          |                    |           |           |           |
|------------|----------|--------------------|-----------|-----------|-----------|
| *Método*   | $AIC$    | $R^2$ **ajustado** | $RMSE$    | $R^2$     | $MAE$     |
| *Forward*  | 973.239  | 99.54              | 4.8186162 | 0.9955231 | 3.7545822 |
| *Backward* | 973.239  | 99.54              | 4.8186162 | 0.9955231 | 3.7545822 |
| *Stepwise* | 976.0164 | 99.53              | 4.8906414 | 0.9953883 | 3.8580781 |

Se selecciona al modelo Stepwise, por lo que el modelo final considerará a las variables Altura y Temperatura. La variable Macho, no tiene gran aporte predictivo, por ello, fue descartado.

# Modelo de regresión lineal final

## Resumen del modelo

A continuación presentamos el modelo final:

$$Recuento=\beta_0+\beta_1*Temperatura+\beta_2*Altura+\epsilon_i$$

\changefontsizes{5pt}


```

Call:
lm(formula = Recuento ~ Temperatura + Altura, data = datos.train)

Residuals:
     Min       1Q   Median       3Q      Max 
-14.1057  -3.1063  -0.3891   2.5381  12.9691 

Coefficients:
             Estimate Std. Error t value            Pr(>|t|)    
(Intercept) 25.740129   1.813561   14.19 <0.0000000000000002 ***
Temperatura  1.658877   0.077636   21.37 <0.0000000000000002 ***
Altura       0.536282   0.002921  183.60 <0.0000000000000002 ***
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Residual standard error: 4.937 on 158 degrees of freedom
Multiple R-squared:  0.9954,	Adjusted R-squared:  0.9953 
F-statistic: 1.705e+04 on 2 and 158 DF,  p-value: < 0.00000000000000022
```

## Análisis de variancia


```
Analysis of Variance Table

Response: Recuento
             Df Sum Sq Mean Sq  F value                Pr(>F)    
Temperatura   1   9614    9614   394.47 < 0.00000000000000022 ***
Altura        1 821555  821555 33708.24 < 0.00000000000000022 ***
Residuals   158   3851      24                                   
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
```

## Gráfico de dispersión 3D

<img src="bookdownproj_files/figure-html/unnamed-chunk-33-1.png" width="240px" style="display: block; margin: auto;" />

<img src="bookdownproj_files/figure-html/unnamed-chunk-34-1.png" width="240px" style="display: block; margin: auto;" />

## Análisis de supuestos

### Valores predichos vs Residuos

<img src="bookdownproj_files/figure-html/unnamed-chunk-35-1.png" width="672" style="display: block; margin: auto;" />

### Gráfico de probabilidad normal de residuos

<img src="bookdownproj_files/figure-html/unnamed-chunk-36-1.png" width="672" style="display: block; margin: auto;" />

### Valores predichos vs Raíz de los residuos estandarizados absolutos

<img src="bookdownproj_files/figure-html/unnamed-chunk-37-1.png" width="672" style="display: block; margin: auto;" />

### Leverage vs Residuos estandarizados

<img src="bookdownproj_files/figure-html/unnamed-chunk-38-1.png" width="672" style="display: block; margin: auto;" />

### Distancias de Cook

<img src="bookdownproj_files/figure-html/unnamed-chunk-39-1.png" width="672" style="display: block; margin: auto;" />

### Distancias de Cook vs Leverage

<img src="bookdownproj_files/figure-html/unnamed-chunk-40-1.png" width="672" style="display: block; margin: auto;" />

### Prueba de hipótesis para la normalidad de residuos

#### Simetría de los residuos

\changefontsizes{7pt}


```
[1] 0.2755243
```

#### Curtosis de los residuos

\changefontsizes{7pt}


```
[1] 3.067106
```

### Prueba de hipótesis para la normalidad de residuos

Las pruebas de hipótesis para normalidad de los residuos, con la siguiente hipótesis:

$H_0:$ Los residuos estandarizados del modelo planteado se distribuyen de forma similar a la función normal.

$H_1:$ Los residuos estandarizados del modelo planteado no se distribuyen de forma similar a la función normal.

\changefontsizes{7pt}


```

	Shapiro-Wilk normality test

data:  .
W = 0.98743, p-value = 0.158
```

```

	Anderson-Darling normality test

data:  .
A = 0.75224, p-value = 0.04926
```

```

	One-sample Kolmogorov-Smirnov test

data:  .
D = 0.059144, p-value = 0.6264
alternative hypothesis: two-sided
```

### Prueba de hipótesis para la homocedasticidad

Por otro lado, al evaluar el supuesto de homocedasticidad y constrastar con la siguiente hipótesis:

$H_0:$ La variancia de los errores del modelo planteado es homocedástica.

$H_1:$ La variancia de los errores del modelo planteado es heterocedástica.

\changefontsizes{4pt}


```
Non-constant Variance Score Test 
Variance formula: ~ fitted.values 
Chisquare = 0.1365724, Df = 1, p = 0.71171
```

```

 Breusch Pagan Test for Heteroskedasticity
 -----------------------------------------
 Ho: the variance is constant            
 Ha: the variance is not constant        

                Data                 
 ------------------------------------
 Response : Recuento 
 Variables: fitted values of Recuento 

        Test Summary         
 ----------------------------
 DF            =    1 
 Chi2          =    0.1365724 
 Prob > Chi2   =    0.7117125 
```

```

	studentized Breusch-Pagan test

data:  .
BP = 5.4705, df = 2, p-value = 0.06488
```

### Prueba de hipótesis para la autocorrelación de residuos

Al evaluar el supuesto de autocorrelación y constrastar la siguiente hipótesis:

$H_0:$ Los errores del modelo planteado no están autocorrelacionados.

$H_1:$ Los errores del modelo planteado están autocorrelacionados.

<img src="bookdownproj_files/figure-html/unnamed-chunk-45-1.png" width="672" style="display: block; margin: auto;" />

<img src="bookdownproj_files/figure-html/unnamed-chunk-46-1.png" width="672" style="display: block; margin: auto;" />


```

	Durbin-Watson test

data:  .
DW = 1.8907, p-value = 0.4845
alternative hypothesis: true autocorrelation is not 0
```

\changefontsizes{7pt}


```
 lag Autocorrelation D-W Statistic p-value
   1     0.052208685      1.890666   0.530
   2    -0.054686922      2.102824   0.446
   3     0.024665124      1.908407   0.702
   4     0.003746447      1.942041   0.854
   5    -0.030826966      2.004505   0.750
   6    -0.195071642      2.322778   0.008
   7    -0.015591045      1.960868   0.798
   8     0.050528001      1.806361   0.532
   9     0.107564167      1.686918   0.186
  10     0.033825256      1.824361   0.698
 Alternative hypothesis: rho[lag] != 0
```

### Leverages

\changefontsizes{4pt}


```
     1      2      3      4      5      6      7      8      9     10     11     12     13     14     15     16     17     18 
0.0065 0.0233 0.0130 0.0236 0.0285 0.0086 0.0212 0.0083 0.0299 0.0228 0.0198 0.0121 0.0142 0.0101 0.0083 0.0115 0.0253 0.0098 
    19     20     21     22     23     24     25     26     27     28     29     30     31     32     33     34     35     36 
0.0078 0.0200 0.0213 0.0119 0.0080 0.0250 0.0147 0.0361 0.0208 0.0181 0.0264 0.0215 0.0143 0.0242 0.0198 0.0207 0.0229 0.0247 
    37     38     39     40     41     42     43     44     45     46     47     48     49     50     51     52     53     54 
0.0180 0.0272 0.0308 0.0417 0.0301 0.0109 0.0265 0.0239 0.0160 0.0099 0.0164 0.0217 0.0251 0.0114 0.0154 0.0090 0.0101 0.0160 
    55     56     57     58     59     60     61     62     63     64     65     66     67     68     69     70     71     72 
0.0102 0.0214 0.0382 0.0165 0.0112 0.0173 0.0177 0.0372 0.0253 0.0098 0.0080 0.0076 0.0338 0.0063 0.0288 0.0173 0.0236 0.0123 
    73     74     75     76     77     78     79     80     81     82     83     84     85     86     87     88     89     90 
0.0339 0.0155 0.0258 0.0210 0.0143 0.0137 0.0088 0.0114 0.0157 0.0095 0.0252 0.0077 0.0191 0.0218 0.0286 0.0162 0.0097 0.0236 
    91     92     93     94     95     96     97     98     99    100    101    102    103    104    105    106    107    108 
0.0153 0.0216 0.0336 0.0189 0.0115 0.0237 0.0261 0.0167 0.0209 0.0110 0.0144 0.0124 0.0282 0.0204 0.0262 0.0125 0.0280 0.0256 
   109    110    111    112    113    114    115    116    117    118    119    120    121    122    123    124    125    126 
0.0152 0.0299 0.0246 0.0211 0.0111 0.0069 0.0179 0.0166 0.0231 0.0201 0.0165 0.0255 0.0184 0.0150 0.0092 0.0146 0.0281 0.0072 
   127    128    129    130    131    132    133    134    135    136    137    138    139    140    141    142    143    144 
0.0171 0.0190 0.0077 0.0248 0.0087 0.0167 0.0249 0.0117 0.0076 0.0094 0.0336 0.0171 0.0140 0.0087 0.0180 0.0111 0.0225 0.0212 
   145    146    147    148    149    150    151    152    153    154    155    156    157    158    159    160    161 
0.0162 0.0164 0.0134 0.0149 0.0094 0.0120 0.0124 0.0446 0.0182 0.0258 0.0288 0.0163 0.0221 0.0252 0.0145 0.0186 0.0300 
```

```
[1] 0.03726708
```

```
 [1] "17"  "32"  "60"  "79"  "83"  "100" "102" "120" "123" "143"
```

Entonces, una observación podrá ser considerada como un leverage si $h_ii>2\frac{k}{n}$, donde $k$ es el número de coeficinetes de regresión y $n$ es el tamaño de la muetra, siempre y cuando $2\frac{k}{n}<1$

Para nuestro caso, tenemos que $k=3$ y nuestro $n=161$ observaciones entonces $2\frac{k}{n}<1$ = $2*(3/161)$ = $0.0373 < 1$

En nuestro caso vemos que se cumple para nuestro conjunto de datos donde tenemos que $2k<n$ -\> $n>2k$ -\> $n>2(p+1)$donde $p$ es el número de variables predictoras para nosotros $p=2$ por tanto vemos que se cumple la condición $161>2(2+1)>2$

Por otro lado, sabemos que no todo **leverage** es un punto influenciable.

Cuando se extrajo la matriz Hat para nuestras 161 obervaciones vemos que todos los valores son menores a uno.

Para nuestro caso son considerados valores leverage los siguientes: 26, 44, 77, 101, 125, 127 y 151. Sabemos que estas observaciones no son necesariamente influenciales pero se apartar de la distribución o el patron de los datos.

### Distancia de Cook

\changefontsizes{4pt}


```
     1      2      3      4      5      6      7      8      9     10     11     12     13     14     15     16     17     18 
0.0001 0.0002 0.0112 0.0062 0.0095 0.0044 0.0017 0.0001 0.0001 0.0048 0.0000 0.0011 0.0002 0.0026 0.0000 0.0005 0.0587 0.0099 
    19     20     21     22     23     24     25     26     27     28     29     30     31     32     33     34     35     36 
0.0011 0.0086 0.0000 0.0000 0.0002 0.0154 0.0013 0.0003 0.0005 0.0013 0.0014 0.0040 0.0027 0.0369 0.0062 0.0005 0.0052 0.0022 
    37     38     39     40     41     42     43     44     45     46     47     48     49     50     51     52     53     54 
0.0051 0.0029 0.0397 0.0090 0.0165 0.0003 0.0010 0.0169 0.0008 0.0005 0.0011 0.0004 0.0025 0.0010 0.0097 0.0058 0.0034 0.0000 
    55     56     57     58     59     60     61     62     63     64     65     66     67     68     69     70     71     72 
0.0035 0.0022 0.0017 0.0003 0.0026 0.0241 0.0015 0.0154 0.0002 0.0008 0.0007 0.0052 0.0034 0.0003 0.0000 0.0000 0.0010 0.0004 
    73     74     75     76     77     78     79     80     81     82     83     84     85     86     87     88     89     90 
0.0016 0.0016 0.0027 0.0110 0.0068 0.0012 0.0117 0.0071 0.0001 0.0018 0.0421 0.0016 0.0002 0.0079 0.0019 0.0046 0.0073 0.0002 
    91     92     93     94     95     96     97     98     99    100    101    102    103    104    105    106    107    108 
0.0049 0.0132 0.0004 0.0010 0.0014 0.0204 0.0093 0.0023 0.0144 0.0171 0.0003 0.0346 0.0006 0.0005 0.0133 0.0139 0.0149 0.0248 
   109    110    111    112    113    114    115    116    117    118    119    120    121    122    123    124    125    126 
0.0000 0.0006 0.0308 0.0008 0.0000 0.0002 0.0030 0.0135 0.0119 0.0005 0.0005 0.0368 0.0056 0.0045 0.0215 0.0012 0.0031 0.0015 
   127    128    129    130    131    132    133    134    135    136    137    138    139    140    141    142    143    144 
0.0005 0.0084 0.0007 0.0003 0.0029 0.0085 0.0001 0.0043 0.0001 0.0001 0.0017 0.0029 0.0002 0.0043 0.0110 0.0016 0.0328 0.0008 
   145    146    147    148    149    150    151    152    153    154    155    156    157    158    159    160    161 
0.0160 0.0003 0.0003 0.0128 0.0001 0.0010 0.0010 0.0161 0.0053 0.0315 0.0024 0.0006 0.0008 0.0048 0.0155 0.0015 0.0076 
```

```
character(0)
```

Por otro lado, se ha detectdo que ninguna de las observaciones poseen una distancia de cook estadísticamente significativa. Entones, no existen observaciones que influyen en el cálculo de los betas en el modelo de regresión.

### COVRATIO

\changefontsizes{3pt}


```
        1         2         3         4         5         6         7         8         9        10        11        12 
1.0246461 1.0431601 0.9831590 1.0287298 1.0297765 0.9987384 1.0365463 1.0267326 1.0504323 1.0309733 1.0398088 1.0266196 
       13        14        15        16        17        18        19        20        21        22        23        24 
1.0332680 1.0150475 1.0275330 1.0287605 0.9165026 0.9720765 1.0188842 1.0153079 1.0412715 1.0314311 1.0259932 1.0101339 
       25        26        27        28        29        30        31        32        33        34        35        36 
1.0291826 1.0568724 1.0394527 1.0339127 1.0438523 1.0310277 1.0229310 0.9585235 1.0218441 1.0393447 1.0300923 1.0400187 
       37        38        39        40        41        42        43        44        45        46        47        48 
1.0217138 1.0414705 0.9786504 1.0511861 1.0192849 1.0289358 1.0447348 1.0035653 1.0328976 1.0262228 1.0323557 1.0407284 
       49        50        51        52        53        54        55        56        57        58        59        60 
1.0396838 1.0256936 0.9991319 0.9919179 1.0101643 1.0357709 1.0097214 1.0356007 1.0570894 1.0352375 1.0172387 0.9584740 
       61        62        63        64        65        66        67        68        69        70        71        72 
1.0326235 1.0346069 1.0451530 1.0247135 1.0226577 0.9879805 1.0490487 1.0227691 1.0494264 1.0371655 1.0414559 1.0300405 
       73        74        75        76        77        78        79        80        81        82        83        84 
1.0522292 1.0292717 1.0400763 1.0111171 1.0067756 1.0281380 0.9532081 0.9953646 1.0349635 1.0181800 0.9517715 1.0154089 
       85        86        87        88        89        90        91        92        93        94        95        96 
1.0385375 1.0209780 1.0454665 1.0194781 0.9859151 1.0434582 1.0168091 1.0064841 1.0540221 1.0358166 1.0240535 0.9947749 
       97        98        99       100       101       102       103       104       105       106       107       108 
1.0259357 1.0286304 1.0016137 0.9432092 1.0329486 0.8783661 1.0475342 1.0390431 1.0174389 0.9689674 1.0180006 0.9907930 
      109       110       111       112       113       114       115       116       117       118       119       120 
1.0349759 1.0493812 0.9740104 1.0389050 1.0306605 1.0243460 1.0281497 0.9900953 1.0136662 1.0388087 1.0344560 0.9641211 
      121       122       123       124       125       126       127       128       129       130       131       132 
1.0208798 1.0174862 0.8985450 1.0294251 1.0422284 1.0144117 1.0353234 1.0135188 1.0217410 1.0443345 1.0092636 1.0072077 
      133       134       135       136       137       138       139       140       141       142       143       144 
1.0450831 1.0101432 1.0260878 1.0279854 1.0516792 1.0271125 1.0327607 1.0001283 1.0026927 1.0222574 0.9603639 1.0389789 
      145       146       147       148       149       150       151       152       153       154       155       156 
0.9798408 1.0350031 1.0317032 0.9855949 1.0283664 1.0266370 1.0275286 1.0460211 1.0213784 0.9771124 1.0447675 1.0338941 
      157       158       159       160       161 
1.0400448 1.0344887 0.9734600 1.0337766 1.0361520 
```

```
[1] TRUE
```

```
[1]  17  26  57 100 102 123
```

Las observaciones con un alto COVRATIO fueron: 17, 26, 57, 100, 102 y 123. Estas observaciones influyen en el calculo de los estimadores del error estándar.

## Poder predictivo del modelo final

### MSE del modelo final sobre los datos de prueba


```
[1] 23.91837
```

### Indicadores predictivos con la base de datos de prueba


```
     RMSE  Rsquared       MAE 
5.3664468 0.9944946 4.3281594 
```

<!--chapter:end:index.Rmd-->

