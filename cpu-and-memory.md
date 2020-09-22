# CPU & Memory

[https://www.akkadia.org/drepper/cpumemory.pdf](https://www.akkadia.org/drepper/cpumemory.pdf.)

{% embed url="https://stackoverflow.com/questions/8126311/what-every-programmer-should-know-about-memory" %}

Pamięć wirtualna jest podzielona na strony \(przykładowo 4kB\). Za translację pomiędzy adresami wirtualnymi a fizycznymi odpowiada bufor translacji adresów - TLB. Procesor wczytuje dane o wielkości cache line \(64B\). Czytanie danych położonych jednym ciągiem w pamięci jest korzystne.

DMA - direct memory access - dzięki bezpośredniemu dostępowi do pamięci RAM, urządzenia zewnętrzna nie potrzebują CPU do zapisywania / odczytywania z pamięci RAM. 

Northbridge \(historycznie\) - mostek pełniący rolę kontrolera pamięci, służący do komunikacji pomiędzy CPU, pamięcią RAM oraz Southbridge. Obecnie kontroler pamięci jest prawie zawsze częścią CPU. Funkcjonalności Northbridge zostały zintregrowane z CPU. 

Southbridge \(historycznie\) - mostek odpowiedzialny za komunikację z urządzeniami zewnętrznymi

Problemem jest jednak walka o przepustowość Northbridge pomiędzy zewnętrznymi urządzeniami a CPU.

FSB \(historycznie\) - Front Side Bus, szyna służąca przesyłaniu danych pomiędzy CPU a Northbridge. U intela wyparty przez QPI.

NUMA - Not Uniform Memory Access, architektura w której występuje wiele CPU \(multi-socket\), każdy z pamięcią RAM. Koszt dostępu do pamięci jest różny.

SRAM - Static RAM - szybki, potrzebuje dużo energii, 6 tranzystorów. Ze względu na koszty wykorzystywany w małych ilościach - np. CPU Cache

DRAM - Dynamic RAM - mniejszy, wolniejszy, 1 tranzystor, 1 kondensator. Potrzeba odświeżania kondensatora, potrzeba detekcji czy stan to 0 czy 1.

DDR SDRAM - Double Data Rate SDRAM - rodzaj SDRAM w którym odczyty są na zboczach rosnących i opadających przez co zwiększona jest przepustowość.

Pamięć RAM jest wczytywana słowami o wielkości 8B - 64b. Podczas każdego taktu zegara wczytuje się jedno słowo lub więcej \(DDR\). Zazwyczaj wczytuje się od razu cały cache line - 8 słów czyli 64B.

Cache dla instrukcji oraz cache danych są osobne - co tam Von Neuman :\). 

Cache ma strukturę hierarchiczną. Kolejne poziomy \(L1, L2, L3\) są coraz wolniejsze i większe.

Wątki fizyczne mają niektóre rejestry rdzenie wspólne, inne oddzielne. Wątki fizyczne dzielą L1 cache.  Rdzenie dzielą L2 i L3 cache. CPU pomiędzy sobą dzielą tylko RAM.

Pamięć zapisywana jest zawsze do i z cache. Jeden cache entry to cache line - 64B. Gdy procesor potrzebuje danych, cały cache line zapisywany jest do L1d.





