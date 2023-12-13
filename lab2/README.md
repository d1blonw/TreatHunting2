# lab2
# by d1blo

# Основы обработки данных с помощью R (часть 1)

## Цель работы

1.  Развить практические навыки использования языка программирования R
    для обработки данных
2.  Закрепить знания базовых типов данных языка R
3.  Развить пркатические навыки использования функций обработки данных
    пакета dplyr – функции select(), filter(), mutate(), arrange(),
    group_by()

## Задание (Ход работы)

1.  Сколько строк в датафрейме?

``` r
install.packages("dplyr")
library(dplyr)
```

    Присоединяем пакет: 'dplyr'


``` r
starwars %>% nrow()
```

    [1] 87

2.  Сколько столбцов в датафрейме?

``` r
starwars %>% ncol()
```

    [1] 14

3.  Как просмотреть примерный вид датафрейма?

``` r
starwars %>% glimpse()
```

    Rows: 87
    Columns: 14
    $ name       <chr> "Luke Skywalker", "C-3PO", "R2-D2", "Darth Vader", "Leia Or…
    $ height     <int> 172, 167, 96, 202, 150, 178, 165, 97, 183, 182, 188, 180, 2…
    $ mass       <dbl> 77.0, 75.0, 32.0, 136.0, 49.0, 120.0, 75.0, 32.0, 84.0, 77.…
    $ hair_color <chr> "blond", NA, NA, "none", "brown", "brown, grey", "brown", N…
    $ skin_color <chr> "fair", "gold", "white, blue", "white", "light", "light", "…
    $ eye_color  <chr> "blue", "yellow", "red", "yellow", "brown", "blue", "blue",…
    $ birth_year <dbl> 19.0, 112.0, 33.0, 41.9, 19.0, 52.0, 47.0, NA, 24.0, 57.0, …
    $ sex        <chr> "male", "none", "none", "male", "female", "male", "female",…
    $ gender     <chr> "masculine", "masculine", "masculine", "masculine", "femini…
    $ homeworld  <chr> "Tatooine", "Tatooine", "Naboo", "Tatooine", "Alderaan", "T…
    $ species    <chr> "Human", "Droid", "Droid", "Human", "Human", "Human", "Huma…
    $ films      <list> <"The Empire Strikes Back", "Revenge of the Sith", "Return…
    $ vehicles   <list> <"Snowspeeder", "Imperial Speeder Bike">, <>, <>, <>, "Imp…
    $ starships  <list> <"X-wing", "Imperial shuttle">, <>, <>, "TIE Advanced x1",…

4.  Сколько уникальных рас персонажей (species) представлено в данных?

``` r
starwars %>% distinct(species) %>% nrow()
```

    [1] 38

5.  Найти самого высокого персонажа.

``` r
starwars %>% select(height,name) %>% filter(!is.na(height)) %>% arrange(height) %>% tail(1) 
```
         height      name
    81    264 Yarael Poof

6.  Найти всех персонажей ниже 170

``` r
starwars %>% select(height,name) %>% filter(height < 170) %>% arrange(height)
```

       height                  name
    1      66                  Yoda
    2      79         Ratts Tyerell
    3      88 Wicket Systri Warrick
    4      94              Dud Bolt
    5      96                 R2-D2
    6      96                R4-P17
    7      97                 R5-D4
    8     112               Sebulba
    9     122               Gasgano
    10    137                 Watto
    11    150           Leia Organa
    12    150            Mon Mothma
    13    157                 Cordé
    14    160             Nien Nunb
    15    163        Shmi Skywalker
    16    163        Ben Quadinaros
    17    165    Beru Whitesun lars
    18    165                 Dormé
    19    165         Padmé Amidala
    20    166         Barriss Offee
    21    167                 C-3PO
    22    167            Jocasta Nu
    23    168            Zam Wesell

7.  Подсчитать ИМТ (индекс массы тела) для всех персонажей. ИМТ
    подсчитать по формуле 𝐼 = 𝑚 ℎ2 , где 𝑚 – масса (weight), а ℎ – рост
    (height).

``` r
starwars %>% mutate(IMP = mass/(height^2)) %>% select(name,IMP) %>% filter(!is.na(IMP)) %>% View()
```

  	
      name IMP
    1 Luke Skywalker 0.002602758
    2 C-3PO 0.002689232
    3 R2-D2 0.003472222
    4 Darth Vader 0.003333007
    5 Leia Organa 0.002177778
    6 Owen Lars 0.003787401
    7 Beru Whitesun lars 0.002754821
    8 R5-D4 0.003400999
    9 Biggs Darklighter 0.002508286
    10 Obi-Wan Kenobi 0.002324598
    11 Anakin Skywalker 0.002376641
    12 Chewbacca 0.002154509
    13 Han Solo 0.002469136
    14 Greedo 0.002472518
    15 Jabba Desilijic Tiure 0.044342857
    16 Wedge Antilles 0.002664360
    17 Jek Tono Porkins 0.003395062
    18 Yoda 0.003902663
    19 Palpatine 0.002595156
    20 Boba Fett 0.002335095
    21 IG-88 0.003500000
    22 Bossk 0.003130194
    23 Lando Calrissian 0.002521625
    24 Lobot 0.002579592
    25 Ackbar 0.002561728
    26 Wicket Systri Warrick 0.002582645
    27 Nien Nunb 0.002656250
    28 Qui-Gon Jinn 0.002389326
    29 Nute Gunray 0.002467038
    30 Jar Jar Binks 0.001718034
    31 Roos Tarpals 0.001634247
    32 Sebulba 0.003188776
    33 Darth Maul 0.002612245
    34 Ayla Secura 0.001735892
    35 Dud Bolt 0.005092802
    36 Ben Quadinaros 0.002446460
    37 Mace Windu 0.002376641
    38 Ki-Adi-Mundi 0.002091623
    39 Kit Fisto 0.002264681
    40 Adi Gallia 0.001476843
    41 Plo Koon 0.002263468
    42 Gregar Typho 0.002483565
    43 Poggle the Lesser 0.002388844
    44 Luminara Unduli 0.001944637
    45 Barriss Offee 0.001814487
    46 Dooku 0.002147709
    47 Jango Fett 0.002358984
    48 Zam Wesell 0.001948696
    49 Dexter Jettster 0.002601775
    50 Lama Su 0.001678076
    51 Ratts Tyerell 0.002403461
    52 Wat Tambor 0.001288625
    53 Shaak Ti 0.001799015
    54 Grievous 0.003407922
    55 Tarfful 0.002483746
    56 Raymus Antilles 0.002235174
    57 Sly Moore 0.001514960
    58 Tion Medon 0.001885192
    59 Padmé Amidala 0.001652893

8.  Найти 10 самых “вытянутых” персонажей. “Вытянутость” оценить по
    отношению массы (mass) к росту (height) персонажей.

``` r
starwars %>% mutate(VIT = mass/height) %>% select(name,VIT,height,mass) %>% filter(!is.na(VIT)) %>% arrange(VIT) %>% head(10) 
```

                 name       VIT height mass
    1          Ratts Tyerell 0.1898734     79   15
    2  Wicket Systri Warrick 0.2272727     88   20
    3             Wat Tambor 0.2487047    193   48
    4                   Yoda 0.2575758     66   17
    5              Sly Moore 0.2696629    178   48
    6             Adi Gallia 0.2717391    184   50
    7          Padmé Amidala 0.2727273    165   45
    8          Barriss Offee 0.3012048    166   50
    9            Ayla Secura 0.3089888    178   55
    10              Shaak Ti 0.3202247    178   57

9.  Найти средний возраст персонажей каждой расы вселенной Звездных
    войн.

``` r
starwars %>% filter(birth_year > 0,species != "NA") %>% group_by(species) %>% summarise('SV' = median(birth_year))
```

       species           SV
        <chr>          <dbl>
     1 Cerean            92
     2 Droid             33
     3 Ewok               8
     4 Gungan            52
     5 Human             48
     6 Hutt             600
     7 Kel Dor           22
     8 Mirialan          49
     9 Mon Calamari      41
    10 Rodian            44
    11 Trandoshan        53
    12 Twi'lek           48
    13 Wookiee          200
    14 Yoda's species   896
    15 Zabrak            54

10.  Найти самый распространенный цвет глаз персонажей вселенной Звездных
    войн.

``` r
starwars %>% filter(!is.na(eye_color)) %>% group_by(eye_color) %>% summarise(VSEGOglaz = n()) %>% arrange(VSEGOglaz) %>% tail(1)
```

    1 brown            21

11.  Подсчитать среднюю длину имени в каждой расе вселенной Звездных
    войн.

``` r
starwars %>% filter(species != "NA") %>% group_by(species) %>% summarise('SV' = median(nchar(name)))
```

       species      SV
       <chr>     <dbl>
     1 Aleena       13
     2 Besalisk     15
     3 Cerean       12
     4 Chagrian     10
     5 Clawdite     10
     6 Droid         5
     7 Dug           7
     8 Ewok         21
     9 Geonosian    17
    10 Gungan       12
    # ℹ 27 more rows

------------------------------------------------------------------------

## 
