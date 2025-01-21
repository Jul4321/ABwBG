# Analiza Variant Annotation

## Wprowadzenie

Pakiet **VariantAnnotation**, został zaprojektowany do analizy danych w formacie VCF (Variant Call Format), który jest standardem w bioinformatyce do przechowywania informacji o wariantach genomowych, takich jak SNP (Single Nucleotide Polymorphisms) czy indeli (insercje i delecje).

W tym zadaniu wykorzystano VariantAnnotation do analizy danych wariantowych zawartych w przykładowym `pliku chr22.vcf.gz` (chromosom 22) dostarczonym z pakietem. 
Analiza obejmuje zarówno podstawowe operacje, takie jak wczytywanie i eksploracja danych, jak i bardziej zaawansowane, takie jak adnotacja i filtrowanie wariantów oraz wyodrębnianie regionów o specyficznych cechach biologicznych (np. regiony międzygenowe i UTR).

## Etapy analizy

### 1. Instalaca i ładowanie pakietów

Analiza wymaga zainstalowania i załadowania następujących pakietów:

- `VariantAnnotation` – analiza danych w formacie VCF.
- `GenomicRanges` – manipulacja i analiza danych genomowych.
- `AnnotationHub` – dostęp do danych adnotacyjnych.
  
### 2.  Wczytanie i eksploracja danych

Warianty zostały załadowane z przykładowego `pliku chr22.vcf.gz` dostarczonego z pakietem `VariantAnnotation`. 
Dane zapisano w *obiekcie VCF*, który umożliwia odczyt podstawowych informacji, takich jak liczba wariantów i struktura metadanych.

### 3. Analiza jakości i filtracja

***3.1 Analiza jakości***

Analiza jakości za pomocą funkcji 
```{r}
summary(qual(vcf))
```
umożliwiła wizualizacjie takich danych jak:
- minimum
- mediana
- średnia
- 1 i 3 kwartyl
- maximum
- ilość pustych obserwacji

***3.2 Filtracja***

Za pomocą funkcji `vcf_filtered` dokonano filtracji, gdzie zachowywane są tylko te warianty o wysokiej jakości, które mają wartość jakości większą niż 99 (`qual(vcf) > 99`) i nie mają brakujących wartości (`vcf[!is.na(qual(vcf))`). 
- Liczba wariantów przed filtracją: 10376.
- Liczba wariantów po filtracji: 10308.

### 4. Anotacja wariantów

Adnotacja wariantów genomowych, czyli ich mapowanie na określone regiony funkcjonalne genomu. 
Celem jest określenie, w których regionach genowych (np. eksony, introny, regiony UTR, międzygenowe) znajdują się zidentyfikowane warianty.

Pakiet `TxDb.Hsapiens.UCSC.hg19.knownGene` zawiera adnotacje genowe dla *genomu hg19*, a jego obiekt `txdb` umożliwia mapowanie wariantów do regionów genowych, takich jak eksony i UTR-y. Z obiektu `vcf_filtered` wyodrębniamy zakresy genomowe za pomocą funkcji `rowRanges()`, tworząc obiekt `GRanges`. 
Następnie, używając funkcji `locateVariants()`, przypisujemy warianty do odpowiednich regionów genowych, a wynik przeglądamy za pomocą `head()`.

## Podsumowanie
Analiza wariantów genomowych demonstruje podstawowe techniki przetwarzania danych genotypowych, takie jak wczytanie danych, filtracja jakościowa, adnotacja genowa oraz klasyfikacja wariantów w regionach genomowych. 
Wyniki tej analizy mogą być użyteczne w kontekście badań asocjacyjnych, analizy mutacji lub badania zmienności genetycznej w populacjach.







