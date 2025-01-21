# Analiza GWAS (Genome-Wide Association Study)

## Wprowadzenie 
**Badanie GWAS** (***Genome-Wide Association Study***, ***Badanie Asocjacji Całogenomowych***) to zaawansowane narzędzie umożliwiające identyfikację związków między wariantami genetycznymi – głównie polimorfizmami pojedynczych nukleotydów (SNP) – a różnorodnymi cechami fenotypowymi, takimi jak podatność na choroby, cechy fizyczne czy reakcje organizmu na leczenie. 
Poprzez analizę markerów genetycznych występujących w całym genomie dużych grup osobników, GWAS pozwala na przewidywanie powiązań genotyp-fenotyp za pomocą zaawansowanych metod statystycznych.

Metoda ta znalazła szerokie zastosowanie w wielu dziedzinach, w tym w medycynie, genomice roślinnej oraz badaniach nad genami odpowiedzialnymi za złożone cechy zwierząt i roślin. 
Dzięki GWAS możliwe jest nie tylko lepsze zrozumienie genetycznych podstaw chorób czy cech fenotypowych, ale także identyfikacja genów powiązanych z określonymi cechami oraz biomarkerów, które mogą być wykorzystywane w diagnostyce lub personalizacji terapii.

## Kroki analizy

### 1. Instalacja i ładowanie pakietów

Do analizy załadowano niezbędne pakiety R, takie jak:

- `rrBLUP`  analiza związku między genotypami a fenotypami,
- `BGLR` zaawansowane analizy genotypów,
- `SNPRelate` analiza danych SNP,
- `qqman` wizualizacja wyników GWAS,
- `poolr` i `dplyr` analizy statystyczne

## 2. Przygotowanie danych genotypowych i fenotypowych

Wczytano dane genotypowych z pliku `.ped`, informacje o subpopulacjach z pliku `.fam` i informacje o mapowaniu markerów z pliku `.map`. Dane zostały przekształcone w odpowiedni format, dostosowany do późniejszych etapów analizy.

Dane genotypowe poddano rekodowaniu, wartości markerów zostały przekodowane w następujący sposób:
- Brakujące wartości danych oznaczone jako 2 zastąpiono wartością NA,
- Wartości 0 zastąpiono na 0 (homozygota dla allelu głównego)
- Wartości 1 zmieniono na 1 (heterozygota)
- Wartości 3 przekonwertowano na 2 (homozygota dla allelu mniejszościowego).

Po przekształceniu dane zapisano w formie macierzy i dokonano ich transpozycji, pozwoliło to na jej odpowiednie uporządkowanie do analizy. Dzięki czemu wiersze odpowiadały osobnikom, a kolumny – markerom SNP.

***Ostateczne wymiary macierzy:*** 
- 413 osobników,
- 36901 markerów SNP.

Przygotowanie danych fenotypowych dotyczyło wyodrębnienia cech i dopasowania danych fenotypowych do danych genotypowych oraz usunięcie brakujących danych z macierzy.

## 3. Kontrola jakości (QC) danych markerów

Brakujące wartości markerów SNP zastąpiono średnią wartością dla każdego markera w celu uzupełnienia braków. Następnie zastosowano filtrację markerów o niskiej frekwencji allelu mniejszościowego (MAF), przyjmując próg 5%.
Wyeliminowanie markerów o niskiej zmienności zapobiegło wprowadzeniu szumu do wyników analizy. Zaktualizowano również dane genotypowe i plik `.map`, uwzględniając jedynie markery spełniające przyjęte kryteria.
W wyniku filtracji zmniejszyła się liczba markerów SNP z 36901 do 36542.

## 4. Analiza PCA

**Analiza głównych składowych** (PCA) umożliwiła wizualizację struktury danych i ocenę różnorodności genetycznej w próbie. 
Utworzono zoptymalizowany **plik GDS** (Genomic Data Structure), który pozwolił na wydajne przetwarzanie danych SNP. 
Na podstawie analizy PCA obliczono pierwsze cztery składowe główne (PC1, PC2, PC3, PC4) oraz utworzono wykresy, przedstawiające różnice między subpopulacjami. Subpopulacje zostały przypisane do wyników PCA na podstawie dodatkowych danych.

## 5. Analiza GWAS

***5.1 Przygotowanie danych do analizy GWAS***

Przygotowano dane genotypowe i fenotypowe w formatach wymaganych do analizy GWAS. Dane genotypowe zapisano w tabelarycznej strukturze, gdzie wiersze odpowiadały próbom, a kolumny – markerom SNP. 
Dane fenotypowe zawierały przypisanie cech do odpowiednich identyfikatorów próbek.

***5.2 Analiza GWAS***

Przeprowadzono analizę GWAS, identyfikując markery SNP, które mogły być powiązane z analizowaną cechą. 

***5.3 Wyodrębnienie istotnych markerów SNP***

Analiza GWAS pozwoliła na identyfikację potencjalnych markerów SNP związanych z cechami fenotypowymi
Po filtracji na podstawie wartości p-value (y < 1e-04) wybrano 6 markerów SNP zlokalizowanych na chromosomie 1.

***5.4 Wizualizacja wyników- wykres Manhattan***

Wyniki zostały zwizualizowane na wykresie Manhattan, przedstawiającym rozkład istotnych markerów SNP wzdłuż chromosomów.





