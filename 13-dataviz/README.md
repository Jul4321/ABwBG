# Data visualization - techniki wizualizacji danych

## Wprowadzenie
Wizualizacja danych jest kluczowym etapem analizy danych, umożliwiającym odkrywanie wzorców, zależności i rozkładów w zbiorach danych. 
W tym opracowaniu omówione zostaną różne typy wykresów, które są powszechnie stosowane w badaniach naukowych i analizie danych.

### 1. Podstawowe Wykresy Eksploracyjne

***1.1 Boxplot (wykres pudełkowy)***

Wykres pudełkowy jest używany do przedstawienia rozkładu danych, w tym mediany, kwartali oraz potencjalnych wartości odstających. 
Pozwala na szybkie zrozumienie rozkładu zmiennej w różnych grupach.W genomice wykorzystywany jest do porównania ekspresji genów między różnymi warunkami eksperymentalnymi lub grupami prób.

![boxplot](https://github.com/user-attachments/assets/89c83593-48d6-4e2e-92e4-8a5fae40a49c)


***1.2 Histogram***

Histogram pokazuje rozkład danych, co jest użyteczne w analizie rozkładu intensywności ekspresji genów w różnych próbach.
W genomice histogramy mogą być stosowane do analizy częstości występowania mutacji lub ekspresji genów w populacji.

![histogram](https://github.com/user-attachments/assets/72bc5a42-365a-42c5-af90-cde7c46d5836)


***1.3 Scatter plot (wykres punktowy)***

Scatter plot ilustruje zależności między dwiema zmiennymi ciągłymi, co jest użyteczne w genomice do analizy korelacji między różnymi genami lub między genotypem a fenotypem. 
Na przykład, może być używany do wizualizacji zależności między ekspresją dwóch genów.

![Scatter plot](https://github.com/user-attachments/assets/06a8be66-47c3-45f3-9623-4ddc32c2fd40)


***1.4 Violin + Boxplot (hybryda)***

połączenie wykresu skrzyniowego i violin plot daje pełniejszy obraz rozkładu danych, a w genomice pozwala na lepsze zrozumienie rozkładu poziomów ekspresji genów w różnych warunkach eksperymentalnych.

![Violin + Boxplot](https://github.com/user-attachments/assets/114e0997-2d7e-468a-8c2d-a6080df9dfc9)


### 2.Wykres Stacked Bar Plot (skumulowane słupki)

Wykres Stacked Bar Plot jest używany do porównania składników różnych grup, co jest pomocne w genomice do analizy proporcji różnych wariantów genotypów lub porównania ekspresji genów w różnych grupach prób.

![Stacked Bar Plot](https://github.com/user-attachments/assets/0ed789c5-2cd1-40eb-82ca-1963eaa2be2f)


### 3. Waffle Plot

Wykres waffle pozwala na przedstawienie proporcji, co może być użyteczne w genomice do wizualizacji częstotliwości występowania różnych wariantów genetycznych lub obecności mutacji w różnych populacjach.

![Waffle Plot](https://github.com/user-attachments/assets/6e838231-7daf-43fd-ac41-61b4b3963cb5)

### 4. Time Series Plot (analiza czasowa)

Wykresy czasowe pomagają analizować zmiany w danych w kontekście upływu czasu, co jest stosowane w genomice do monitorowania zmian w ekspresji genów w czasie w odpowiedzi na różne bodźce lub traktowanie komórek.

![Time Series Plot](https://github.com/user-attachments/assets/48703772-7a87-4cb6-961f-c123e5430e7d)

### 5. Waterfall Plot

Wykres wodospadowy jest wykorzystywany w genomice do przedstawiania zmian w ekspresji genów w różnych próbach, takich jak różnice w poziomach ekspresji między nowotworami a tkankami zdrowymi.

***5.1 Klasyczny Waterfall Plot***
![klasyczny_Waterfall Plot](https://github.com/user-attachments/assets/d1cc9ef5-492a-4b22-a765-9cff3e2c9dff)

***5.2 Waterfall w analizach mutacji***
![Waterfall w analizach mutacji](https://github.com/user-attachments/assets/cc262534-6d2a-438e-8567-ff2aadd1c7e0)

### 6. Volcano Plot

Wykres wulkanowy jest szczególnie popularny w genomice, zwłaszcza w analizach RNA-Seq, do przedstawiania wyników analizy różnicowej ekspresji genów. Umożliwia wizualizację istotnych różnic w ekspresji genów przy jednoczesnym uwzględnieniu ich poziomów statystycznej istotności.

***6.1 Metoda 1: base R***
![Volcano Plot_baseR](https://github.com/user-attachments/assets/18df4548-1e90-44e2-9575-75f1a3dce474)


***6.2 Metoda 2: pakiet EnhancedVolcano***
![VolcanoPlot_pakiet EnhancedVolcano](https://github.com/user-attachments/assets/967f75a3-6b55-4559-9311-66bd544ae109)


### 7. Heatmap
Heatmap jest stosowana w genomice do przedstawiania danych z eksperymentów typu RNA-Seq, gdzie wartości ekspresji genów w różnych próbach są przedstawiane za pomocą kolorów, co umożliwia łatwe dostrzeganie wzorców ekspresji.

![heatmap](https://github.com/user-attachments/assets/d527e085-7a7a-4be6-b72f-43369931b877)

### 8. Wykresy redukcji wymiarów (PCA, t-SNE)
Redukcja wymiarów za pomocą PCA lub t-SNE pozwala na wizualizację dużych zbiorów danych genomowych w przestrzeni o mniejszych wymiarach. W genomice te techniki są stosowane do klasyfikacji próbek na podstawie ekspresji genów lub mutacji, co pomaga w wykrywaniu ukrytych struktur w danych.

![PCA](https://github.com/user-attachments/assets/cd1ad4ea-86ab-407b-af32-87b05ae6179e)

![t-SNE](https://github.com/user-attachments/assets/99266310-b7a7-4700-ba77-66cce95f8c55)

### 9. Manhattan Plot
Wykres Manhattan jest szeroko stosowany w genomice do przedstawiania wyników badań skojarzeń genotypów z fenotypami, zwłaszcza w badaniach GWAS (Genome-Wide Association Studies), gdzie pokazuje istotność statystyczną wariantów genetycznych w kontekście ich lokalizacji na chromosomach.

![Manhattan Plot](https://github.com/user-attachments/assets/f0d62215-0124-4419-90ac-9ac6b22a095f)

### 10. Venn Diagrams i UpSet Plots


