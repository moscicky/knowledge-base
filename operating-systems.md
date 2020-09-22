# Operating Systems

## Books

**Operating systems concepts** - [https://www.os-book.com/](https://www.os-book.com/) best OS introduction 

### Tutorials

**Writing OS in Rust** - [https://github.com/phil-opp/blog\_os](https://github.com/phil-opp/blog_os)

**OS tutorial** - [https://github.com/cfenollosa/os-tutorial](https://github.com/cfenollosa/os-tutorial) \(C and Assembly\)



## Articles

**Epoll** [https://medium.com/@copyconstruct/the-method-to-epolls-madness-d9d2d6378642](https://medium.com/@copyconstruct/the-method-to-epolls-madness-d9d2d6378642)

**More Epoll** - [https://thenewstack.io/how-io\_uring-and-ebpf-will-revolutionize-programming-in-linux/](https://thenewstack.io/how-io_uring-and-ebpf-will-revolutionize-programming-in-linux/)

## Videos

**Is It Time to Rewrite the Operating System in Rust?**, Bryan Cantrill - [https://youtu.be/HgtRAbE1nBM](https://youtu.be/HgtRAbE1nBM)

### Chapter 1

#### Przerwania i system 

System składa się z CPU oraz kontrolerów urządzeń zewnętrznych. Kontroler zawiera zbiór rejestrów oraz mały bufor pamięci, jest odpowiedzialny za przenoszenie danych pomiędzy urządzeniem a buforem. Urządzenia są połączone między sobą i pamięcią za pomocą szyny. System operacyjny posiada sterowniki dla kontrolerów urządzeń zewnętrznych, dzięki czemu inne fragmenty OS mogą z nich korzystać. Kontrolery urządzeń zewnętrznych mogą funkcjonować równolegle z CPU, walcząc o dostęp do pamięci. Za synchronizacje dostępu do pamięci odpowiada kontroler pamięci. 

By wykonać operację I/O system operacyjny za pomocą sterownika zapisuje dane do rejestrów w kontrolerze urządzenia zewnętrznego. Kontroler odczytuje polecenie z rejestru i wczytuje dane z urządzenia do bufora. Kontroler informuje sterownik o zakończeniu pracy poprzez **przerwanie**. Przerwanie jest sygnalizowane do CPU, które uruchamia procedurę obsługi przerwania. Procedury obsługi przerwania są zapisane nisko w pamięci. Przed obsługą przerwania należy zapisać stan rejestrów oraz miejsce \(adres\) w którym przerwano program. Przerwanie obsługiwane jest przez kontroler przerwań.

CPU sprawdza czy wystąpiło przerwanie na lini żądania przerwania. CPU posiada 2 linie żądania przerwania: maskowalną i niemaskowalną - czyli takie, które można i nie można zignorować. Maskowalna linia jest wyłącza przy wykonywaniu krytycznego kodu, używają jej urządzenia I/O. Niemaskowalna jest wykorzystywana podczas np. krytycznego błędu pamięci. Przerwania mają hierarchie i priorytety.

### I/O 

Dzięki DMA kontroler urządzenia zewnętrznego może komunikować się bezpośrednio z pamięcią, z pominięciem CPU.

#### Architektura

Rdzenie na jednym CPU mają osobne cache L1. Współdzielą cache L2. W multi - CPU jeden RAM jest współdzielony. W NUMA wiele CPU współdzieli wiele RAM z jedną fizyczną przestrzenią adresową. Czas dostępu do pamięci jest różny do lokalnego i oddalonego RAM.



