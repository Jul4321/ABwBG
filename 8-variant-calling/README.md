# VARIANT- CALLING

## Wprowadzenie
Proces variant- calling (wykrywanie wariantów) polega na identyfikacji wariantów genomowych, takich jak pojedyncze zmiany nukleotydów (SNPs), insercje oraz delecje, poprzez analizę danych sekwencyjnych. Jest to kluczowy krok w bioinformatyce, który pozwala na zrozumienie różnorodności genetycznej, badanie mutacji odpowiedzialnych za choroby oraz analizę populacyjną.

Warianty genomowe są identyfikowane poprzez porównanie sekwencji DNA próbek do genomu referencyjnego. Podczas tego procesu uwzględnia się takie aspekty jak jakość sekwencjonowania, głębokość pokrycia genomu oraz dokładność dopasowania odczytów do referencji.

**Zastosowanie variant calling:**

- Badania medyczne: Identyfikacja mutacji związanych z chorobami genetycznymi i nowotworowymi.

- Genetyka populacyjna: Analiza różnorodności genetycznej w populacjach.

- Rolnictwo: Wykrywanie mutacji odpowiedzialnych za cechy użytkowe w roślinach i zwierzętach hodowlanych.

## 1. Instalacja i ładowanie wymaganych pakietów

Instalowanie i ładowanie niezbędnych pakietów do analizy danych genomowych 

BiocManager służy do instalacji i zarządzania pakietami specjalnie zaprojektowanymi do zadań bioinformatycznych.

```{r}
BiocManager::install(c("VariantTools", "Rsamtools", "GenomicRanges", "GenomicFeatures", "VariantAnnotation", "BiocParallel"))
```

- `VariantTools` - Narzędzia do wykrywania wariantów genetycznych
- `Rsamtools` - Funkcje do pracy z plikami BAM/SAM
- `GenomicRanges` - Operacje na zakresach genomowych
- `GenomicFeatures` - Tworzenie obiektów opisujących cechy genomu
- `VariantAnnotation` - Funkcje do anotacji i manipulacji wariantami
- `BiocParallel` - Wykorzystanie obliczeń równoległych

## Zadanie 2: Konfiguracja środowiska pracy

Definiowanie katalogu roboczego przy pomocy funkcji `setwd()` zapewnia, że wszystkie pliki wejściowe i wyjściowe są zarządzane w jednym miejscu. Dodatkowo zastosowanie funkcji `list.files()` umożliwia sprawdzenie dostępnych plików w aktualnym katalogu, potwierdza obecność wymaganych plików wejściowych.

## Zadanie 3: Wczytanie danych

Za pomocą funkcji `BamFile()` dokonuje się wczytania pliku BAM (`aligned_sample.BAM`). Natomiast za pomocą funkcji `FaFile()` wczytywany jest plik referencyjny (`ecoli_reference.fasta`)

Sortowanie zapewnia, że odczyty są uporządkowane według współrzędnych genomowych, co jest kluczowe dla dalszej analizy, wykonanie tego umożliwia funkcja `sortBAM`.

Indeksowanie pomaga w odnalezieniu się w strukturze pliku, które umożliwiaja szybki dostęp do określonych regionów genomu referencyjnego i pliku BAM.
```{r}
indexFa(ref_genome)
indexBam(sorted_bam)
```

## Zadanie 4: Kontrola jakości danych sekwencyjnych
Kontrola jakości pozwala na identyfikację potencjalnych problemów z danymi przed variant- calling. Zapewnienie, że analiza wariantów będzie opierała się na wiarygodnych danych, jest niezbędne do uzyskania dokładnych i rzetelnych wyników. 

***4.1 Nagłówek pliku BAM***

Jednym z pierwszych kroków w ocenie jakości danych jest weryfikacja nagłówka pliku BAM, który zawiera metadane istotne dla analizy. Funkcja `scanBamHeader()` umożliwia odczyt tych metadanych, dzięki czemu możliwe jest sprawdzenie struktury pliku i upewnienie się, że plik jest poprawny oraz zawiera wszystkie niezbędne informacje.

***4.2 podstawowych statystyk pliku BAM***

Funkcja `idxstatsBam()` jest wykorzystywana do generowania podstawowych statystyk na temat pliku BAM, w tym liczby odczytów przypisanych do sekwencji w genomie. Uzyskuje się informacje o liczbie odczytów, które zostały zmapowane, a także o odczytach niezmapowanych. Wysoka liczba odczytów niezmapowanych może sugerować problemy z jakością danych sekwencyjnych lub błędy w mapowaniu, które wymagają dalszej analizy.
   
Zmapowane odczyty: 713927
   
Niezmapowane odczyty: 506059

***4.3 Obliczenie i zwizualizowanie pokrycia genomu***

Ocena pokrycia genomu jest kolejnym ważnym krokiem w analizie jakości danych. Funkcja `coverage()` pozwala na obliczenie pokrycia genomu, czyli liczby odczytów przypadających na każdą pozycję w genomie. Pokrycie jest istotnym wskaźnikiem jakości danych, ponieważ w wysokiej jakości danych sekwencyjnych każda pozycja genomu powinna być pokryta odpowiednią liczbą odczytów.

Analiza rozkładu pokrycia za pomocą wizualizacji, np. wykresu wygenerowanego przez `plot(coverage_data)`, umożliwia ocenę jakości procesu sekwencjonowania. Regiony genomu o wysokim pokryciu mogą wskazywać na obecność artefaktów lub sekwencji powtarzalnych, które mogą wymagać dalszego zbadania. Z kolei niskie pokrycie może sugerować problemy z jakością danych lub z technologią sekwencjonowania, co może prowadzić do utraty istotnych informacji w analizie.

## Zadanie 5: Wykrywanie wariantów

***5.1 Definiowanie parametrów skanowania za pomocą `pileup()`***

Pierwszym krokiem w wykrywaniu wariantów jest skonfigurowanie parametrów dla funkcji `pileup()`, która służy do generowania danych o odczytach sekwencji w okolicach określonych pozycji genomu. Funkcja `pileup()` jest stosowana do przesortowanego pliku BAM, generując dane o pokryciu dla każdej pozycji w genomie, co stanowi punkt wyjścia do dalszej analizy wariantów.

***5.2 Konwercja wyników do ramki danych***

Dane wygenerowane przez `pileup()` są następnie konwertowane do ramki danych (data frame), co umożliwia ich dalszą obróbkę i analizę. Użycie funkcji `as.data.frame()` pozwala na przekształcenie danych z formatu listy w formę tabelaryczną.

***5.3 Pogrupowanie danych według pozycji***

Grupowanie danych na podstawie pozycji w genomie. Funkcja `group_by()` pozwala na pogrupowanie danych według sekwencji (seqnames) oraz pozycji (pos)

Aby zidentyfikować potencjalne warianty, dane są filtrowane według minimalnej liczby odczytów dla allelu alternatywnego. Stosując filtry minimalnej liczby odczytów (≥ 5) oraz proporcji odczytów alternatywnych (≥ 20%), identyfikowane są prawdopodobne warianty, eliminując szumy techniczne.

Po zastosowaniu powyższych filtrów, lista wariantów jest gotowa do dalszej analizy. Warianty mogą zostać wyświetlone za pomocą funkcji `head()`, co pozwala na wstępną ocenę wyników analizy.

## Zadanie 6: Filtracja i eksportowanie wyników do pliku

Filtracja wariantów genetycznych ma na celu usunięcie potencjalnych fałszywych pozytywów oraz selekcję najbardziej istotnych wariantów na podstawie jakości danych oraz głębokości pokrycia.

Za pomocą funkcji `filter()` z pakietu `dplyr`, warianty są filtrowane na podstawie niżej wymienionych kryteriów. Filtracja pozwala na usunięcie wariantów o niskiej jakości lub takich, które mogą być efektem szumów lub artefaktów sekwencjonowania.

*Kryteria filtracji*
- Liczba odczytów dla danej pozycji (≥ 10)
- Proporcja odczytów alternatywnych (≥ 20%)

***6.1 Eksport do pliku CSV***

Ostatecznym krokiem jest eksportowanie przefiltrowanych wyników do **pliku CSV**. Funkcja `write.csv()` pozwala na zapisanie danych w formacie tekstowym, który może być łatwo odczytany przez inne narzędzia do analizy danych.

## Podsumowanie

Wykrywanie wariantów genetycznych to proces, który wymaga precyzyjnej analizy danych sekwencyjnych i odpowiedniego przetwarzania bioinformatycznego.

Kluczowymi czynnikami wpływającymi na dokładność tej analizy są jakość danych sekwencyjnych, głębokość pokrycia genomu, parametry ustawione podczas analizy oraz poprawność mapowania odczytów na genom referencyjny. Filtrowanie wykrytych wariantów jest istotnym etapem, ponieważ pozwala wyeliminować fałszywie pozytywne warianty, poprawia wiarygodność wyników i skupia analize na najbardziej istotnych biologicznie wariantach. Natomiast potencjalne źródła błędów jakie mogą wystąpić w procesie variant calling dotyczą błędów sekwencjonowania, niewłaściwie zmapowanych odczytów, artefaktów PCR oraz zanieczyszczenia próbek. 

Po wykryciu wariantów kolejnym krokiem jest ich anotacja, analiza funkcjonalna oraz interpretacja kliniczna. Dzięki temu można lepiej zrozumieć potencjalne znaczenie biologiczne i medyczne wykrytych wariantów, co stanowi fundament dalszych badań lub zastosowań klinicznych.


