
# Minishell fonksiyonları

Bu proje, 42 okullarındaki Minishell projesinde kullanılabilir olarak belirlenen fonksiyonlar için Türkçe kaynak oluşturma amacıyla hazırlanmıştır.

## readline(3)
#### Açıklama :
readline(3) fonksiyonu, bir karakter dizisi okuyan ve bu diziyi geri döndüren özel bir girdi işlevi (input function) olarak kullanılır. Fonksiyon, klavyeden okunan metnin sonunda yer alan satır sonu karakterini (\n) otomatik olarak kaldırır ve karakter dizisi içinde saklar.
#### Return :
readline(3) fonksiyonu, başarılı olursa, bir char türü işaretçisi (pointer) döndürür ve hafızada dinamik olarak ayrılmış bir bellek bloğu içinde okunan karakter dizisini tutar. Eğer okuma işlemi başarısız olursa NULL döner.
### Kullanım/Örnekler

```javascript
#include <stdio.h>
#include <stdlib.h>
#include <readline/readline.h>

int main() {
   char *str;

   printf("Metin giriniz: ");
   str = readline(NULL);

   printf("Girilen metin: %s\n", str);

   free(str);
   return (0);
}
```
Bu örnekte, kullanıcıdan klavyeden girilen bir metin, readline(3) fonksiyonu ile bir karakter dizisine (char *) okunuyor ve daha sonra ekrana yazdırılıyor. Okunan karakter dizisi, hafızada dinamik olarak ayrılmış bir bellek bloğunda tutulduğu için, işlem sonunda free() fonksiyonu ile serbest bırakılması gerekmektedir.

## rl_clear_history()
#### Açıklama :
rl_clear_history() fonksiyonu, readline kütüphanesi tarafından tutulan komut satırı geçmişini temizlemek için kullanılır. Bu fonksiyon çağrıldığında, geçmişte kaydedilmiş tüm komutlar ve girdiler silinir
#### Return :
rl_clear_history() fonksiyonu, herhangi bir değer döndürmez (void).
### Kullanım/Örnekler
```javascript
#include <readline/readline.h>
#include <readline/history.h>

int main() {
    // önce bazı komutlar ekleyelim
    add_history("komut1");
    add_history("komut2");
    add_history("komut3");

    // komut geçmişini temizle
    rl_clear_history();

    return (0);
}
```
Bu örnekte, add_history() fonksiyonu ile bazı komutlar komut geçmişine eklenir. Daha sonra, rl_clear_history() fonksiyonu çağrılarak komut geçmişi temizlenir. Artık geçmişte kaydedilmiş hiçbir komut yoktur.

## rl_on_new_line()
#### Açıklama :
rl_on_new_line() fonksiyonu, klavyeden girilen verilerin okunması işlemi sırasında kullanılır. readline kütüphanesi, klavyeden girilen verileri okumak için çeşitli işlevleri kullandığından, bu işlevlerin arasında verilerin doğru bir şekilde işlenmesini sağlamak için bazı yardımcı işlevler kullanılır. rl_on_new_line() fonksiyonu, klavyeden girilen verilerin okunması işleminin tamamlandığını belirtir ve bir alt satıra geçer.
#### Return :
rl_on_new_line() fonksiyonu, herhangi bir değer döndürmez (void).
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <readline/readline.h>
#include <readline/history.h>

int main() {
    char *input;

    while ((input = readline("> "))) {
        // klavyeden girilen verileri işle
        // ...

        // okuma işlemi tamamlandı, bir alt satıra geç
        rl_on_new_line();

        // komut geçmişine ekle
        add_history(input);

        // bellekten klavye girdisi için ayrılan alanı serbest bırak
        free(input);
    }

    return 0;
}
```
Bu örnekte, readline() fonksiyonu kullanılarak klavyeden veri okunur ve işlenir. Daha sonra, rl_on_new_line() fonksiyonu çağrılarak okuma işlemi tamamlandığı belirtilir ve bir alt satıra geçilir. Son olarak, add_history() fonksiyonu kullanılarak girilen komut geçmişine eklenir.

## rl_replace_line()
#### Açıklama :
rl_replace_line() fonksiyonu, bir satırın içeriğini değiştirmek için kullanılır. Bu fonksiyon, klavyeden girilen verilerin okunması işlemi sırasında kullanılabilir. 
#### Return :
rl_replace_line() fonksiyonu, herhangi bir değer döndürmez (void).
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <readline/readline.h>
#include <readline/history.h>

int main() {
    char *input;

    while ((input = readline("> "))) {
        // klavyeden girilen verileri işle
        // ...

        // satırın içeriğini değiştir
        rl_replace_line(input, "Yeni metin");

        // satırın içeriğini ekrana yazdır
        rl_redisplay();

        // komut geçmişine ekle
        add_history(input);

        // bellekten klavye girdisi için ayrılan alanı serbest bırak
        free(input);
    }

    return (0);
}
```
Bu örnekte, readline() fonksiyonu kullanılarak klavyeden veri okunur ve işlenir. Daha sonra, rl_replace_line() fonksiyonu kullanılarak satırın içeriği "Yeni metin" ile değiştirilir. Ardından, rl_redisplay() fonksiyonu kullanılarak yeni satır içeriği ekrana yazdırılır. Son olarak, add_history() fonksiyonu kullanılarak girilen komut geçmişine eklenir.

## rl_redisplay()
#### Açıklama :
rl_redisplay() fonksiyonu, klavyeden girilen verileri okur ve ekrana yazdırır.
#### Return :
rl_redisplay() fonksiyonu, herhangi bir değer döndürmez (void).
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <readline/readline.h>
#include <readline/history.h>

int main() {
    char *input;

    while ((input = readline("> "))) {
        // klavyeden girilen verileri işle
        // ...

        // ekrana yazdır
        rl_redisplay();

        // komut geçmişine ekle
        add_history(input);

        // bellekten klavye girdisi için ayrılan alanı serbest bırak
        free(input);
    }

    return (0);
}
```
Bu örnekte, readline() fonksiyonu kullanılarak klavyeden veri okunur ve işlenir. Daha sonra, rl_redisplay() fonksiyonu kullanılarak yeni satır içeriği ekrana yazdırılır. Son olarak, add_history() fonksiyonu kullanılarak girilen komut geçmişine eklenir.

## add_history()
#### Açıklama :
add_history() fonksiyonu, klavyeden girilen verilerin geçmişe eklenmesini sağlar. Bu fonksiyon, readline kütüphanesi tarafından kullanılan bir veri yapısı olan "history" yapısını günceller.
#### Return :
add_history() fonksiyonu, herhangi bir değer döndürmez (void).
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <readline/readline.h>
#include <readline/history.h>

int main() {
    char *input;

    while ((input = readline("> "))) {
        // klavyeden girilen verileri işle
        // ...

        // komut geçmişine ekle
        add_history(input);

        // bellekten klavye girdisi için ayrılan alanı serbest bırak
        free(input);
    }

    return 0;
}
```
Bu örnekte, readline() fonksiyonu kullanılarak klavyeden veri okunur ve işlenir. Daha sonra, add_history() fonksiyonu kullanılarak girilen verilerin geçmişine eklenir. Son olarak, free() fonksiyonu kullanılarak bellekten klavye girdisi için ayrılan alan serbest bırakılır.

## access()
#### Açıklama :
access() fonksiyonu, belirtilen dosya veya dizin için erişim izni kontrolü yapmak için kullanılır. Bu işlev, istenen erişim türüne göre dosya veya dizinin var olup olmadığını kontrol eder ve erişim izinleri açısından kontrol eder. İstenen erişim türü, R_OK, W_OK, X_OK veya F_OK sembolleri kullanılarak belirtilir. R_OK, okuma izni; W_OK, yazma izni; X_OK, yürütme izni; F_OK, dosyanın varlığını kontrol etmek için kullanılır.
#### Return :
access() fonksiyonu, istenen dosya veya dizin için erişim izni verilirse 0 değerini döndürür. Eğer erişim izni verilmezse, −1 değerini döndürür ve hata kodunu errno değişkeninde ayarlar.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <unistd.h>

int main() {
    if (access("/path/to/file.txt", R_OK) == 0) {
        printf("Dosyaya okuma izni var.\n");
    } else {
        printf("Dosyaya okuma izni yok.\n");
    }

    return 0;
}
```
Bu örnekte, access() fonksiyonu kullanılarak /path/to/file.txt dosyası için okuma izni kontrol edilir. Eğer erişim izni verilirse, "Dosyaya okuma izni var" mesajı yazdırılır. Aksi takdirde, "Dosyaya okuma izni yok" mesajı yazdırılır.

## fork()
#### Açıklama :
fork() fonksiyonu, çağıran işlemi ebeveyn olarak kullanarak yeni bir çocuk işlemi oluşturur. Oluşturulan çocuk işlemi, ebeveyn işlemle aynı kodu ve verileri paylaşır, ancak ayrı bir adrese, yığın ve işlem kaynaklarına sahiptir. Çocuk işlem, fork() fonksiyonunun çağrıldığı noktadan devam eder.
#### Return :
fork() fonksiyonu, ebeveyn işlemde geri dönerken, oluşturulan çocuk işlemde 0 değerini döndürür. Ebeveyn işlemde fork() fonksiyonu, çocuk işlemin PID'sini döndürürken, çocuk işlemin fork() fonksiyonu 0 değerini döndürür.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <unistd.h>

int main() {
    pid_t pid;

    pid = fork();

    if (pid == -1) {
        printf("Çocuk işlem oluşturulamadı.\n");
        return 1;
    } else if (pid == 0) {
        printf("Ben çocuk işlemim (%d).\n", getpid());
    } else {
        printf("Ben ebeveyn işlemim (%d). Çocuk işlemin PID'si %d.\n", getpid(), pid);
    }

    return 0;
}
```
Bu örnekte, fork() fonksiyonu kullanılarak yeni bir çocuk işlemi oluşturulur. Ebeveyn işlem, fork() fonksiyonunun geri dönüş değeri olarak çocuk işlemin PID'sini alırken, çocuk işlem, fork() fonksiyonunun geri dönüş değeri olarak 0 değerini alır. Ebeveyn işlem ve çocuk işlem, printf() fonksiyonunu kullanarak kendilerini ve PID'lerini ekrana yazdırırlar.

Eğer fork() fonksiyonu başarılı olursa, kodun çıktısı şu şekilde olur:
```javascript
Ben ebeveyn işlemim (ebeveyn_PID). Çocuk işlemin PID'si (çocuk_PID).
Ben çocuk işlemim (çocuk_PID).
```
Burada, ebeveyn_PID ve çocuk_PID, her çalıştırıldığında değişen işlem PID'leri olacaktır.

## wait()
#### Açıklama :
wait() fonksiyonu, çağıran işlemi bekletir ve o işleme bağlı bir çocuk işlemi tamamlanana kadar işlemi askıya alır. Çocuk işlem tamamlandığında, ebeveyn işlem wait() fonksiyonundan devam eder.
#### Return :
wait() fonksiyonu, çocuk işlem PID'sini döndürür. Çocuk işlem tarafından kullanılan kaynaklar serbest bırakılır ve çocuk işlem sonlandırılır.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>

int main() {
    pid_t pid;

    pid = fork();

    if (pid == -1) {
        printf("Çocuk işlem oluşturulamadı.\n");
        return 1;
    } else if (pid == 0) {
        printf("Ben çocuk işlemim (%d).\n", getpid());
        exit(0);
    } else {
        printf("Ben ebeveyn işlemim (%d). Çocuk işlemin PID'si %d.\n", getpid(), pid);
        wait(NULL);
        printf("Çocuk işlem tamamlandı.\n");
    }

    return 0;
}
```
Bu örnekte, fork() fonksiyonu kullanılarak yeni bir çocuk işlemi oluşturulur. Çocuk işlem, printf() fonksiyonu kullanarak kendisini ve PID'sini ekrana yazdırır ve ardından exit() fonksiyonu kullanarak işlemi sonlandırır. Ebeveyn işlem, printf() fonksiyonu kullanarak kendisini ve çocuk işlemin PID'sini ekrana yazdırır ve wait() fonksiyonunu kullanarak çocuk işlemin tamamlanmasını bekler. Çocuk işlem tamamlandığında, ebeveyn işlem, wait() fonksiyonundan devam eder ve printf() fonksiyonu kullanarak çocuk işlemin tamamlandığını ekrana yazdırır.

Bu programın çıktısı, her çalıştırıldığında değişebilir. Ancak, örnek bir çıktı aşağıdaki gibidir:
```javascript
Ben ebeveyn işlemim (5678). Çocuk işlemin PID'si 1234.
Ben çocuk işlemim (1234).
Çocuk işlem tamamlandı.
```
Bu çıktı, ebeveyn işleminin önce kendisini ve oluşturulan çocuk işleminin PID'sini, ardından çocuk işleminin kendisini ve son olarak çocuk işleminin tamamlandığını belirtmek için "Çocuk işlem tamamlandı." mesajını yazdırdığını gösterir.

## waitpid()
#### Açıklama :
waitpid() fonksiyonu, wait() fonksiyonuna benzer şekilde, çağıran işlemi bekletir ve belirli bir PID'ye sahip bir çocuk işleminin tamamlanmasını bekler. Ancak, waitpid() fonksiyonu, hangi çocuk işleminin beklenmesi gerektiğini belirlemek için PID parametresi alır. Bu sayede, birden fazla çocuk işleminin tamamlanmasını beklemek için kullanılabilir.
#### Return :
waitpid() fonksiyonu, tamamlanan çocuk işlemin PID'sini döndürür. Çocuk işlem tarafından kullanılan kaynaklar serbest bırakılır ve çocuk işlem sonlandırılır.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>

int main() {
    pid_t pid1, pid2, child_pid;
    int status;

    pid1 = fork();

    if (pid1 == -1) {
        printf("Çocuk işlem oluşturulamadı.\n");
        return 1;
    } else if (pid1 == 0) {
        printf("Ben birinci çocuk işlemim (%d).\n", getpid());
        exit(0);
    }

    pid2 = fork();

    if (pid2 == -1) {
        printf("Çocuk işlem oluşturulamadı.\n");
        return 1;
    } else if (pid2 == 0) {
        printf("Ben ikinci çocuk işlemim (%d).\n", getpid());
        exit(0);
    }

    printf("Ben ebeveyn işlemim (%d).\n", getpid());

    child_pid = waitpid(pid1, &status, 0);
    printf("PID'si %d olan çocuk işlem tamamlandı.\n", child_pid);

    child_pid = waitpid(pid2, &status, 0);
    printf("PID'si %d olan çocuk işlem tamamlandı.\n", child_pid);

    return 0;
}
```
Bu örnekte, fork() fonksiyonu kullanılarak iki çocuk işlemi oluşturulur. Her bir çocuk işlem, printf() fonksiyonu kullanarak kendisini ve PID'sini ekrana yazdırır ve ardından exit() fonksiyonu kullanarak işlemi sonlandırır. Ebeveyn işlem, printf() fonksiyonu kullanarak kendisini ve çocuk işlemlerinin PID'lerini ekrana yazdırır ve waitpid() fonksiyonu kullanılarak her bir çocuk işleminin tamamlanması beklenir. waitpid(), beklenen çocuk işleminin PID'sini ve işlemin durumunu (başarılı veya başarısız tamamlandı mı) döndürür. Bu bilgiler printf() fonksiyonu kullanılarak ekrana yazdırılır. Son olarak, ebeveyn işlemi de sonlandırılır.

Bu programın çıktısı, her çalıştırıldığında değişebilir. Ancak, örnek bir çıktı aşağıdaki gibidir:

```javascript
Ben birinci çocuk işlemim (1234).
Ben ikinci çocuk işlemim (1235).
Ben ebeveyn işlemim (1233).
PID'si 1234 olan çocuk işlem tamamlandı.
PID'si 1235 olan çocuk işlem tamamlandı.
```
Bu çıktı, önce iki çocuk işlemi oluşturulduğunu ve her birinin PID'sinin yazdırıldığını gösterir. Daha sonra, ebeveyn işlemi "Ben ebeveyn işlemim" mesajını yazdırır ve ardından her bir çocuk işleminin tamamlanmasını bekler. İlk waitpid çağrısı pid1'in tamamlanmasını beklerken, ikinci waitpid çağrısı pid2'nin tamamlanmasını bekler. Her bir çocuk işlemi tamamlandığında, ebeveyn işlemi ilgili mesajı yazdırır ve program sonlanır.

## wait3()
#### Açıklama :
wait3() fonksiyonu, waitpid() fonksiyonuna benzer şekilde, bir çocuk işlemin tamamlanmasını bekler. Ancak, wait3() fonksiyonu, waitpid() fonksiyonuna kıyasla daha fazla bilgi toplamak için kullanılabilir. Bu fonksiyon çağrısı, waitpid() fonksiyonuna göre daha eski bir sistem çağrısıdır ve POSIX standartlarında önerilmez.
#### Return :
wait3() fonksiyonu, tamamlanan çocuk işlemin PID'sini döndürür. Çocuk işlem tarafından kullanılan kaynaklar serbest bırakılır ve çocuk işlem sonlandırılır.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>

int main() {
    pid_t pid1, pid2, child_pid;
    int status;

    pid1 = fork();

    if (pid1 == -1) {
        printf("Çocuk işlem oluşturulamadı.\n");
        return 1;
    } else if (pid1 == 0) {
        printf("Ben birinci çocuk işlemim (%d).\n", getpid());
        exit(0);
    }

    pid2 = fork();

    if (pid2 == -1) {
        printf("Çocuk işlem oluşturulamadı.\n");
        return 1;
    } else if (pid2 == 0) {
        printf("Ben ikinci çocuk işlemim (%d).\n", getpid());
        exit(0);
    }

    printf("Ben ebeveyn işlemim (%d).\n", getpid());

    child_pid = wait3(&status, 0, NULL);
    printf("PID'si %d olan çocuk işlem tamamlandı.\n", child_pid);

    child_pid = wait3(&status, 0, NULL);
    printf("PID'si %d olan çocuk işlem tamamlandı.\n", child_pid);

    return 0;
}
```
Bu örnekte, fork() fonksiyonu kullanılarak iki çocuk işlemi oluşturulur. Her bir çocuk işlem, printf() fonksiyonu kullanarak kendisini ve PID'sini ekrana yazdırır ve ardından exit() fonksiyonu kullanarak işlemi sonlandırır. Ebeveyn işlem, printf() fonksiyonu kullanarak kendisini ve çocuk işlemlerinin PID'lerini ekrana yazdırır ve ardından waitpid() fonksiyonu kullanarak çocuk işlemlerinin bitmesini bekler.

Bu programın çıktısı, her çalıştırıldığında değişebilir. Ancak, örnek bir çıktı aşağıdaki gibidir:

```javascript
Ben birinci çocuk işlemim (1234).
Ben ikinci çocuk işlemim (1235).
Ben ebeveyn işlemim (1233).
PID'si 1234 olan çocuk işlem tamamlandı.
PID'si 1235 olan çocuk işlem tamamlandı.
```
Bu çıktıda, birinci çocuk işlemi pid1'e, ikinci çocuk işlemi pid2'ye atanır. Ebeveyn işlemi, önce "Ben ebeveyn işlemim" mesajını yazdırır, ardından wait3 fonksiyonunu kullanarak iki çocuk işleminin tamamlanmasını bekler. İlk wait3 çağrısı pid1'in tamamlanmasını beklerken, ikinci wait3 çağrısı pid2'nin tamamlanmasını bekler. Her bir çocuk işlemi tamamlandığında, ebeveyn işlemi ilgili mesajı yazdırır ve program sonlanır.

## wait4()
#### Açıklama :
wait4() fonksiyonu, belirtilen bir süreç için bekler ve sürecin çıkış durumunu rapor eder. Fonksiyon, çocuk sürecin bitmesini ve çıkış durumunu bekleyen bir ana süreç tarafından çağrılır.
#### Return :
wait4() fonksiyonu, beklenen çocuk sürecin kimlik numarası ve çıkış durumunu içeren bir int değerini döndürür. Fonksiyonun başarısız olması durumunda -1 döndürür ve errno değişkeni ayarlanır.
### Kullanım/Örnekler
```javascript
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>
#include <stdlib.h>
#include <stdio.h>

int main() {
  pid_t pid = fork();

  if (pid == 0) {
    // Çocuk süreç
    printf("Çocuk süreç başladı.\n");
    exit(0);
  } else if (pid > 0) {
    // Ebeveyn süreç
    int status;
    pid_t child_pid = wait4(pid, &status, 0, NULL);
    if (child_pid == -1) {
      perror("wait4");
      exit(1);
    }
    if (WIFEXITED(status)) {
      printf("Çocuk süreç başarıyla sonlandı. Çıkış durumu: %d\n", WEXITSTATUS(status));
    }
  } else {
    perror("fork");
    exit(1);
  }

  return 0;
}
```
Bu örnek, bir çocuk süreç oluşturur ve çocuk sürecin işlemini tamamlamasını bekler. Çocuk süreç, exit(0) çağrısı ile sonlandırılır ve çıkış durumu 0 olarak ayarlanır. Ebeveyn süreç, wait4() fonksiyonunu kullanarak çocuk sürecin bitmesini bekler ve çıkış durumunu rapor eder.

Örnek çıktı şu şekildedir :
```javascript
Çocuk süreç başladı.
Çocuk süreç başarıyla sonlandı. Çıkış durumu: 0
```
Örnek kodda, çocuk süreç önce "Çocuk süreç başladı." mesajını yazdırır ve sonra exit(0) çağrısı ile sonlandırılır. Ebeveyn süreç, wait4() fonksiyonu ile çocuk sürecin bitmesini bekler ve sonra çocuk sürecin çıkış durumunu WEXITSTATUS() fonksiyonu ile rapor eder. Çocuk sürecin çıkış durumu 0 olduğundan, ebeveyn süreç "Çocuk süreç başarıyla sonlandı. Çıkış durumu: 0" mesajını yazdırır.

## signal()
#### Açıklama :
signal() fonksiyonu, belirtilen bir sinyal için bir işlevi işaret eder. İşaretçi, bir sinyal alındığında çağrılır ve sinyal işleme işlevi olarak hareket eder.
#### Return :
signal() fonksiyonu, işaret edilen sinyal için önceki işlevin işaretçisini döndürür. Fonksiyonun başarısız olması durumunda SIG_ERR döndürür.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <signal.h>
#include <unistd.h>

void sig_handler(int signo) {
  if (signo == SIGINT) {
    printf("SIGINT sinyali alındı.\n");
    exit();
  }
}

int main() {
  if (signal(SIGINT, sig_handler) == SIG_ERR) {
    printf("Sinyal işleyicisi atanamadı.\n");
  }

  while(1) {
    printf("Bir sinyal bekleniyor...\n");
    sleep(1);
  }

  return 0;
}
```
Bu örnek, SIGINT sinyalini işleyen bir işlevi atanır. signal() fonksiyonu, SIGINT sinyali için sig_handler() işlevini işaret eder. Program, sonsuz bir döngüde döner ve her bir döngüde "Bir sinyal bekleniyor..." mesajını yazdırır. Sinyal alındığında, sig_handler() işlevi çağrılır ve "SIGINT sinyali alındı." mesajını yazdırır ve sonrasında program biter.

## sigaction()
#### Açıklama :
sigaction() fonksiyonu, bir sinyal için işlem davranışını ayarlamak için kullanılır. Bu fonksiyon, signal() fonksiyonundan daha esnek bir yapıya sahiptir. signal() fonksiyonu sinyal işleyicisinin işlev işaretçisini değiştirirken, sigaction() fonksiyonu daha ayrıntılı bir sinyal işlemesi yapılmasını sağlar.
#### Return :
sigaction() fonksiyonu başarılıysa 0 döndürür, aksi takdirde -1 döndürür.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <signal.h>
#include <unistd.h>

void sig_handler(int signo) {
  if (signo == SIGINT) {
    printf("SIGINT sinyali alındı.\n");
    exit();
  }
}

int main() {
  struct sigaction sa;

  sa.sa_handler = sig_handler;
  sigemptyset(&sa.sa_mask);
  sa.sa_flags = 0;

  if (sigaction(SIGINT, &sa, NULL) == -1) {
    printf("Sinyal işleyicisi atanamadı.\n");
  }

  while(1) {
    printf("Bir sinyal bekleniyor...\n");
    sleep(1);
  }

  return 0;
}
```
Bu örnekte, sigaction() fonksiyonu SIGINT sinyalini işlemek için sig_handler() işlevi ile ilişkilendirir. sigemptyset() fonksiyonu, sa_mask yapısını sıfırlar ve sinyal işleyicisi işlevi çalışırken engellenecek sinyalleri belirtir. sa_flags yapısı, ek sinyal işleme özelliklerini belirtir. NULL parametresi, önceki sinyal işleyici bilgisinin alınmadığını belirtir.
Program, sonsuz bir döngüde döner ve her bir döngüde "Bir sinyal bekleniyor..." mesajını yazdırır. Sinyal alındığında, sig_handler() işlevi çağrılır ve "SIGINT sinyali alındı." mesajını yazdırır ve program biter.

## sigemptyset()
#### Açıklama :
sigemptyset() fonksiyonu, bir sinyal kümesi için bir boş küme oluşturmak için kullanılır. Boş bir küme, sinyal kümesindeki tüm sinyalleri engeller.
#### Return :
sigemptyset() fonksiyonu her zaman 0 döndürür.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <signal.h>

int main() {
  sigset_t set;

  sigemptyset(&set);

  return 0;
}
```
Bu örnekte, sigemptyset() fonksiyonu, set adlı bir sinyal kümesini sıfırlar. sigset_t türü, signal.h başlık dosyasında tanımlanmıştır.
Program, sigemptyset() fonksiyonunu çağırır ve herhangi bir çıktı vermeden sonlanır.

## sigaddset()
#### Açıklama :
sigaddset() fonksiyonu, belirtilen sinyali bir sinyal kümesine eklemek için kullanılır. Fonksiyon, sinyal kümesindeki ilgili sinyalin 1 olmasını sağlar.
#### Return :
sigaddset() fonksiyonu her zaman 0 döndürür.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <signal.h>

int main() {
  sigset_t set;

  sigemptyset(&set);
  sigaddset(&set, SIGINT);

  return 0;
}
```
Bu örnekte, sigaddset() fonksiyonu, set adlı bir sinyal kümesine SIGINT sinyalini ekler. SIGINT sinyali, Ctrl+C tuş kombinasyonuna karşılık gelir ve genellikle programı sonlandırmak için kullanılır.
Program, sigaddset() fonksiyonunu çağırır ve herhangi bir çıktı vermeden sonlanır.

## kill()
#### Açıklama :
kill() fonksiyonu, belirtilen bir işlem veya işlem grubuna bir sinyal göndermek için kullanılır.
#### Return :
kill() fonksiyonu, sinyal gönderme işlemi başarılı bir şekilde tamamlandığında 0 değerini döndürür. Hata durumunda ise -1 döndürür ve errno değişkenine uygun bir hata kodu atanır.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <signal.h>
#include <unistd.h>

int main() {
  pid_t pid = getpid();

  // Sinyal gönderme işlemi
  int result = kill(pid, SIGTERM);

  // Hata durumunda işlem
  if (result == -1) {
    perror("kill");
    return 1;
  }

  return 0;
}
```
Bu örnekte, kill() fonksiyonu, getpid() fonksiyonu ile alınan mevcut işlem kimliğine (pid) SIGTERM sinyalini gönderir. SIGTERM sinyali, bir programı düzgün bir şekilde sonlandırmak için kullanılır. Eğer işlem başarıyla sonlandırılamazsa, SIGKILL sinyali kullanılabilir.
Program, kill() fonksiyonu çağırır ve herhangi bir çıktı vermeden sonlanır.

## exit()
#### Açıklama :
exit() fonksiyonu, programın anında sonlandırılmasını sağlar ve işletim sistemine çıkış durumunu bildirir.
#### Return :
exit() fonksiyonu herhangi bir değer döndürmez.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <stdlib.h>

int main() {
  printf("Program sonlandı.\n");

  exit(0);
}
```
Bu örnekte, exit() fonksiyonu, 0 çıkış durum kodu ile birlikte programı sonlandırır. 0 çıkış durum kodu, işlemin normal bir şekilde sonlandığını belirtir. exit() fonksiyonu çağrıldığında, önce stdio.h başlık dosyasında tanımlanan printf() fonksiyonu çağrılır ve "Program sonlandı." metni ekrana yazdırılır.
Program, exit() fonksiyonu çağrılarak sonlandırılır ve herhangi bir çıktı vermeden sonlanır.

## getcwd()
#### Açıklama :
getcwd() fonksiyonu, çalışma dizinini belirten bir dizeye işaret eden bir işaretçi döndürür.
#### Return :
getcwd() fonksiyonu, çalışma dizinini belirten bir dizeye işaret eden bir işaretçi döndürür. Başarısız olursa NULL döndürür ve errno değişkenine uygun bir hata kodu atanır.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <unistd.h>

int main() {
  char cwd[1024];

  if (getcwd(cwd, sizeof(cwd)) != NULL) {
    printf("Mevcut çalışma dizini: %s\n", cwd);
  } else {
    perror("getcwd() hata");
    return 1;
  }

  return 0;
}
```
Bu örnekte, getcwd() fonksiyonu, char türünden bir diziye (cwd) mevcut çalışma dizinini belirten bir dize kopyalar. Fonksiyon başarılı olursa, printf() fonksiyonu çağrılarak mevcut çalışma dizini ekrana yazdırılır. Aksi takdirde, perror() fonksiyonu, hata mesajını yazdırır ve program 1 ile sonlandırılır.
Program, mevcut çalışma dizinini belirten bir dizeyi ekrana yazdırır ve 0 ile başarılı bir şekilde sonlanır.

## chdir()
#### Açıklama :
chdir() fonksiyonu, programın çalışma dizinini değiştirir.
#### Return :
chdir() fonksiyonu, başarı durumunda 0 değerini, başarısızlık durumunda -1 değerini döndürür ve errno değişkenine uygun bir hata kodu atanır.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <unistd.h>

int main() {
  if (chdir("/") == 0) {
    printf("Mevcut çalışma dizini: / (kök dizin)\n");
  } else {
    perror("chdir() hata");
    return 1;
  }

  return 0;
}
```
Bu örnekte, chdir() fonksiyonu, programın çalışma dizinini / dizinine (kök dizin) değiştirir. Fonksiyon başarılı olursa, printf() fonksiyonu çağrılarak mevcut çalışma dizini ekrana yazdırılır. Aksi takdirde, perror() fonksiyonu, hata mesajını yazdırır ve program 1 ile sonlandırılır.

Program, mevcut çalışma dizinini / dizini olarak değiştirir ve ekrana yazdırır. Sonrasında, 0 ile başarılı bir şekilde sonlanır.

## stat()
#### Açıklama :
stat() fonksiyonu, bir dosyanın özniteliklerini (dosya türü, boyutu, değiştirilme tarihi, erişim hakları vb.) elde etmek için kullanılır.
#### Return :
stat() fonksiyonu, başarı durumunda 0 değerini, başarısızlık durumunda -1 değerini döndürür ve errno değişkenine uygun bir hata kodu atanır.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <sys/stat.h>

int main() {
  struct stat sb;

  if (stat("ornek.txt", &sb) == 0) {
    printf("Dosya boyutu: %ld bytes\n", sb.st_size);
    printf("Dosya son değiştirilme tarihi: %ld\n", sb.st_mtime);
  } else {
    perror("stat() hata");
    return 1;
  }

  return 0;
}
```
Bu örnekte, stat() fonksiyonu, "ornek.txt" dosyasının özniteliklerini (st_size ve st_mtime) elde etmek için kullanılır. Fonksiyon başarılı olursa, printf() fonksiyonu çağrılarak dosya boyutu ve son değiştirilme tarihi ekrana yazdırılır. Aksi takdirde, perror() fonksiyonu, hata mesajını yazdırır ve program 1 ile sonlandırılır.

Program, "ornek.txt" dosyasının boyutunu ve son değiştirilme tarihini ekrana yazdırır ve 0 ile başarılı bir şekilde sonlanır.

## lstat()
#### Açıklama :
lstat() fonksiyonu, bir dosyanın özniteliklerini (dosya türü, boyutu, değiştirilme tarihi, erişim hakları vb.) elde etmek için kullanılır. stat() fonksiyonuna benzer ancak sembolik bağlantıları takip etmez.
#### Return :
lstat() fonksiyonu, başarı durumunda 0 değerini, başarısızlık durumunda -1 değerini döndürür ve errno değişkenine uygun bir hata kodu atanır.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <sys/stat.h>

int main() {
  struct stat sb;

  if (lstat("ornek", &sb) == 0) {
    printf("Dosya boyutu: %ld bytes\n", sb.st_size);
    printf("Dosya son değiştirilme tarihi: %ld\n", sb.st_mtime);
  } else {
    perror("lstat() hata");
    return 1;
  }

  return 0;
}
```
Bu örnekte, lstat() fonksiyonu, "ornek" sembolik bağlantısının özniteliklerini (st_size ve st_mtime) elde etmek için kullanılır. Fonksiyon başarılı olursa, printf() fonksiyonu çağrılarak dosya boyutu ve son değiştirilme tarihi ekrana yazdırılır. Aksi takdirde, perror() fonksiyonu, hata mesajını yazdırır ve program 1 ile sonlandırılır.

Program, "ornek" sembolik bağlantısının boyutunu ve son değiştirilme tarihini ekrana yazdırır ve 0 ile başarılı bir şekilde sonlanır.

## fstat()
#### Açıklama :
fstat() fonksiyonu, bir dosya tanımlayıcısına (file descriptor) göre bir dosyanın özniteliklerini (dosya türü, boyutu, değiştirilme tarihi, erişim hakları vb.) elde etmek için kullanılır. stat() fonksiyonuna benzer ancak fstat() fonksiyonu dosya tanımlayıcısını kullanarak dosyanın özniteliklerini elde ederken, stat() fonksiyonu ise dosya adını kullanır.
#### Return :
fstat() fonksiyonu, başarı durumunda 0 değerini, başarısızlık durumunda -1 değerini döndürür ve errno değişkenine uygun bir hata kodu atanır.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <fcntl.h>
#include <sys/stat.h>

int main() {
  int fd;
  struct stat sb;

  fd = open("ornek", O_RDONLY);
  if (fd == -1) {
    perror("open() hata");
    return 1;
  }

  if (fstat(fd, &sb) == -1) {
    perror("fstat() hata");
    return 1;
  }

  printf("Dosya boyutu: %ld bytes\n", sb.st_size);
  printf("Dosya son değiştirilme tarihi: %ld\n", sb.st_mtime);

  close(fd);

  return 0;
}
```
Bu örnekte, open() fonksiyonu, "ornek" dosyasının okuma modunda açılması için kullanılır. fstat() fonksiyonu, dosya tanımlayıcısı fd'ye sahip olan dosyanın özniteliklerini (st_size ve st_mtime) elde etmek için kullanılır. Fonksiyon başarılı olursa, printf() fonksiyonu çağrılarak dosya boyutu ve son değiştirilme tarihi ekrana yazdırılır. Aksi takdirde, perror() fonksiyonu, hata mesajını yazdırır ve program 1 ile sonlandırılır.

Program, "ornek" dosyasının boyutunu ve son değiştirilme tarihini ekrana yazdırır ve 0 ile başarılı bir şekilde sonlanır.

## unlink()
#### Açıklama :
unlink() fonksiyonu, silinecek dosyanın adını alır ve bu dosyayı siler. Eğer dosya sembolik bir bağlantı ise, sembolik bağlantı dosyası silinir. Ancak, sembolik bağlantı dosyasının hedefi silinmez. Dosyanın kilitli olması durumunda bile, unlink() fonksiyonu dosyayı siler ve bu dosyayı açmaya çalışan diğer işlemler, dosyanın artık mevcut olmadığından bir hata kodu alırlar.
#### Return :
unlink() fonksiyonu, başarı durumunda 0 değerini, başarısızlık durumunda -1 değerini döndürür ve errno değişkenine uygun bir hata kodu atanır.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <unistd.h>

int main() {
  if (unlink("ornek.txt") == -1) {
    perror("unlink() hata");
    return 1;
  }

  printf("Dosya başarıyla silindi.\n");

  return 0;
}
```
Bu örnekte, "ornek.txt" dosyası unlink() fonksiyonu ile silinir. Fonksiyon başarılı olursa, "Dosya başarıyla silindi." mesajı ekrana yazdırılır. Aksi takdirde, perror() fonksiyonu, hata mesajını yazdırır ve program 1 ile sonlandırılır.

Program, "ornek.txt" dosyasını başarıyla siler ve 0 ile başarılı bir şekilde sonlanır.

## execve()
#### Açıklama :
execve() fonksiyonu, mevcut işlemin yerine başka bir programı yükler ve çalıştırır. Yeni program, mevcut işlemi tamamen değiştirir ve aynı işlem kimliğine (PID) sahip olur. Bu işlem, işletim sistemi tarafından sağlanan bir özelliktir ve sıklıkla bir shell betiği içinde kullanılır.

execve() fonksiyonu, üç argüman alır: char *path (yeni programın tam yolu), char **argv (yeni programın komut satırı argümanları) ve char **envp (yeni programın ortam değişkenleri). path argümanı, yüklemek istediğimiz programın tam yolunu içeren bir karakter dizisidir. argv argümanı, yüklenen programın komut satırı argümanlarıdır ve son argümanın değeri NULL olmalıdır. envp argümanı ise, yeni programın ortam değişkenleri için bir dizi karakter dizisi içerir.
#### Return :
execve() fonksiyonu başarılı bir şekilde çalışırsa, asla geri dönmez. Ancak, başarısızlık durumunda -1 değeri döndürür ve errno değişkenine uygun bir hata kodu atanır.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <unistd.h>

int main() {
  char *path = "/bin/ls";
  char *argv[] = { "ls", "-l", NULL };
  char *envp[] = { "PATH=/bin", NULL };

  execve(path, argv, envp);

  perror("execve() hata");
  return 1;
}
```
Bu örnekte, /bin/ls programı execve() fonksiyonu ile yüklenir ve çalıştırılır. Program başarılı bir şekilde yüklenirse, mevcut işlem tamamen değiştirilir ve ls -l komutunun çıktısı ekrana yazdırılır. perror() fonksiyonu, hata mesajını yazdırır ve program 1 ile sonlandırılır.

Program, /bin/ls programını başarıyla yükler ve çalıştırır. Program, mevcut işlemi tamamen değiştirir ve ls -l komutunun çıktısını ekrana yazdırır. Program, 0 ile başarılı bir şekilde sonlanır.

## dup()
#### Açıklama :
dup() fonksiyonu, dosya tanımlayıcısının kopyasını oluşturarak aynı dosyayı işaret eder. Yeni dosya tanımlayıcısı, orijinal dosya tanımlayıcısı ile aynı dosyayı işaret eder. Bu işlem, dosya okuma ve yazma işlemlerini koordine etmek için kullanışlı bir tekniktir.

dup() fonksiyonu, tek bir argüman alır: int oldfd (kopyalanacak dosya tanımlayıcısı). Bu, mevcut bir dosya tanımlayıcısının kopyasını oluşturarak aynı dosyayı işaret etmek için kullanılır. dup() fonksiyonu, yeni dosya tanımlayıcısı olarak kullanılacak en düşük boş tanımlayıcıyı döndürür.
#### Return :
dup() fonksiyonu, başarılı bir şekilde çalışırsa, yeni dosya tanımlayıcısını döndürür. Ancak, başarısızlık durumunda -1 değeri döndürür ve errno değişkenine uygun bir hata kodu atanır.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <fcntl.h>
#include <unistd.h>

int main() {
  int fd, newfd;

  fd = open("file.txt", O_RDONLY);
  if (fd == -1) {
    perror("Dosya açılamadı");
    return 1;
  }

  newfd = dup(fd);
  if (newfd == -1) {
    perror("Dosya tanımlayıcısı kopyalanamadı");
    return 1;
  }

  printf("Mevcut dosya tanımlayıcısı: %d\n", fd);
  printf("Yeni dosya tanımlayıcısı: %d\n", newfd);

  close(fd);
  close(newfd);

  return 0;
}
```
Bu örnekte, file.txt dosyası open() fonksiyonu ile açılır ve fd değişkenine atanır. Daha sonra, dup() fonksiyonu kullanılarak newfd değişkeni oluşturulur ve fd dosya tanımlayıcısının kopyası olarak ayarlanır. Program, mevcut dosya tanımlayıcısı (fd) ve yeni dosya tanımlayıcısı (newfd) değerlerini ekrana yazdırır. Son olarak, close() fonksiyonları kullanılarak dosya tanımlayıcıları kapatılır.

## dup2()
#### Açıklama :
dup2() fonksiyonu, iki dosya tanımlayıcısı arasında kopyalama işlemi yaparak aynı dosyayı işaret etmek için kullanılır. Eğer hedef tanımlayıcı zaten açık bir dosyaya işaret ediyorsa, bu dosya kapandıktan sonra tekrar açılır. Eğer kaynak dosya tanımlayıcısı mevcut değilse, hedef dosya tanımlayıcısıyla birlikte açılır.

dup2() fonksiyonu, iki argüman alır: int oldfd (kaynak dosya tanımlayıcısı) ve int newfd (hedef dosya tanımlayıcısı). Bu fonksiyon, kaynak dosya tanımlayıcısını hedef dosya tanımlayıcısı ile değiştirir. Eğer kaynak dosya tanımlayıcısı mevcut değilse, hedef dosya tanımlayıcısıyla birlikte açılır. dup2() fonksiyonu, hedef dosya tanımlayıcısının değerini döndürür.
#### Return :
dup2() fonksiyonu, başarılı bir şekilde çalışırsa, hedef dosya tanımlayıcısının değerini döndürür. Ancak, başarısızlık durumunda -1 değeri döndürür ve errno değişkenine uygun bir hata kodu atanır.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <fcntl.h>
#include <unistd.h>

int main() {
  int fd1, fd2;

  fd1 = open("file.txt", O_RDONLY);
  if (fd1 == -1) {
    perror("Dosya açılamadı");
    return 1;
  }

  fd2 = open("file2.txt", O_WRONLY | O_CREAT, 0644);
  if (fd2 == -1) {
    perror("Dosya açılamadı");
    return 1;
  }

  printf("Mevcut dosya tanımlayıcısı 1: %d\n", fd1);
  printf("Mevcut dosya tanımlayıcısı 2: %d\n", fd2);

  if (dup2(fd1, fd2) == -1) {
    perror("Dosya tanımlayıcısı kopyalanamadı");
    return 1;
  }

  printf("Yeni dosya tanımlayıcısı 1: %d\n", fd1);
  printf("Yeni dosya tanımlayıcısı 2: %d\n", fd2);

  close(fd1);
  close(fd2);

  return 0;
}
```
Bu kod parçası, öncelikle file.txt adlı bir dosyayı okumak için fd1 dosya tanımlayıcısını açar ve file2.txt adlı bir dosyayı yazmak için fd2 dosya tanımlayıcısını açar. dup2() fonksiyonu, fd1 dosya tanımlayıcısını fd2 dosya tanımlayıcısına kopyalar ve fd2 dosya tanımlayıcısının değerini döndürür. Bu işlem başarılıysa, fd1 dosya tanımlayıcısı artık fd2 dosya tanımlayıcısı ile aynı dosyayı işaret eder.

Sonrasında, mevcut ve yeni dosya tanımlayıcılarının değerleri ekrana yazdırılır ve açılan dosya tanımlayıcıları kapatılır. Program sonlandırılır ve 0 değeri döndürülür.

Eğer file.txt ve file2.txt adlı dosyalar mevcut değilse, program Dosya açılamadı hatası verecektir. Eğer dosyalar başarılı bir şekilde açılırsa ve dup2() fonksiyonu başarılı bir şekilde çalışırsa, fd1 ve fd2 dosya tanımlayıcıları farklı olacak ancak fd1 dosya tanımlayıcısı, fd2 dosya tanımlayıcısının ilk değerini alacaktır.

## pipe()
#### Açıklama :
pipe() fonksiyonu, iki yönlü bir veri akışı oluşturmak için kullanılan bir sistem çağrısıdır. Bu fonksiyon, bir dizi dosya tanımlayıcısı döndürür ve bu dosya tanımlayıcılarından biri, veri akışının okuma ucu için, diğeri ise yazma ucu için kullanılır. Bu fonksiyon çağrıldığında, yeni bir çocuk işlem oluşturulur ve çocuk işlem, veri akışının okuma ucunu miras alırken, ebeveyn işlem ise veri akışının yazma ucunu kullanır. Bu sayede, ebeveyn işlem ve çocuk işlem arasında veri alışverişi yapılabilir.
#### Return :
pipe() fonksiyonu, başarılı bir şekilde çalıştığında 0 değerini döndürür. Hata durumlarında ise -1 değeri döndürür ve errno değişkenine hata kodunu kaydeder.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <unistd.h>

int main() {
   int fd[2];
   char buf[20];
   
   if (pipe(fd) < 0) {
      perror("pipe");
      exit(1);
   }

   if (fork() == 0) {
      close(fd[1]); // Yazma ucu kapatılıyor
      read(fd[0], buf, sizeof(buf));
      printf("Çocuk işlem: %s\n", buf);
      close(fd[0]); // Okuma ucu kapatılıyor
   }
   else {
      close(fd[0]); // Okuma ucu kapatılıyor
      write(fd[1], "Merhaba dünya", 14);
      close(fd[1]); // Yazma ucu kapatılıyor
   }
   return 0;
}
```
Bu örnekte, pipe() fonksiyonu çağrılarak bir veri akışı oluşturuluyor. Daha sonra fork() fonksiyonu kullanılarak bir çocuk işlem oluşturuluyor. Çocuk işlem, veri akışının okuma ucunu miras alıyor ve ebeveyn işlem, veri akışının yazma ucunu kullanıyor. Ebeveyn işlem, "Merhaba dünya" yazısını yazma ucu üzerinden yazıyor ve çocuk işlem, okuma ucu üzerinden bu yazıyı okuyarak ekrana yazdırıyor. Son olarak, her iki işlem de dosya tanımlayıcılarını kapatıyor ve program sonlanıyor.

## opendir()
#### Açıklama :
opendir() fonksiyonu, bir dizindeki dosyaları okumak için kullanılan bir sistem çağrısıdır. Bu fonksiyon, dizin adı olarak verilen bir dizinin yolunu alır ve bu dizindeki dosyaların okunabilmesi için gerekli bir işaretçi döndürür. Döndürülen işaretçi, dizindeki dosyaları okumak için kullanılacak bir araçtır. Bu araç, readdir() fonksiyonu kullanılarak kullanılabilir.
#### Return :
opendir() fonksiyonu, başarılı bir şekilde çalıştığında dizin işaretçisi (directory pointer) döndürür. Hata durumlarında ise NULL değeri döndürür ve errno değişkenine hata kodunu kaydeder.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <stdlib.h>
#include <dirent.h>

int main() {
   DIR *d;
   struct dirent *dir;
   d = opendir(".");
   
   if (d) {
      while ((dir = readdir(d)) != NULL) {
         printf("%s\n", dir->d_name);
      }
      closedir(d);
   }
   else {
      perror("opendir");
      exit(1);
   }
   return 0;
}
```
Bu örnekte, opendir() fonksiyonu çağrılarak, mevcut dizindeki dosyaları okumak için bir dizin işaretçisi elde ediliyor. Daha sonra, readdir() fonksiyonu kullanılarak dizindeki dosyaların adları okunuyor ve ekrana yazdırılıyor. En son olarak, dizin işaretçisi kapatılıyor ve program sonlanıyor.

## readdir()
#### Açıklama :
readdir() fonksiyonu, opendir() fonksiyonu tarafından açılan bir dizin işaretçisi (directory pointer) kullanarak bir dizindeki dosyaları okumak için kullanılan bir sistem çağrısıdır. Bu fonksiyon, her çağrıldığında, bir sonraki dosya ismini döndürür.
#### Return :
readdir() fonksiyonu, başarılı bir şekilde çalıştığında, bir dirent yapısı ile ilgili bilgileri içeren bir işaretçi döndürür. dirent yapısı, bir dizindeki dosya hakkındaki bilgileri içerir.

readdir() fonksiyonu, dizindeki tüm dosyalar okunduktan sonra NULL değeri döndürür ve errno değişkenine hata kodunu kaydeder.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <stdlib.h>
#include <dirent.h>

int main() {
   DIR *d;
   struct dirent *dir;
   d = opendir(".");
   
   if (d) {
      while ((dir = readdir(d)) != NULL) {
         printf("%s\n", dir->d_name);
      }
      closedir(d);
   }
   else {
      perror("opendir");
      exit(1);
   }
   return 0;
}
```
Bu örnekte, opendir() fonksiyonu çağrılarak, mevcut dizindeki dosyaları okumak için bir dizin işaretçisi elde ediliyor. Daha sonra, readdir() fonksiyonu kullanılarak dizindeki dosyaların adları okunuyor ve ekrana yazdırılıyor. En son olarak, dizin işaretçisi kapatılıyor ve program sonlanıyor.

## rl_on_new_line()
#### Açıklama :
closedir() fonksiyonu, opendir() fonksiyonu tarafından açılan bir dizin işaretçisini kapatmak için kullanılan bir sistem çağrısıdır. Bu fonksiyon, açılan dizindeki kaynakların serbest bırakılmasını ve işaretçinin geçersiz hale getirilmesini sağlar.
#### Return :
closedir() fonksiyonu herhangi bir değer döndürmez (void).
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <stdlib.h>
#include <dirent.h>

int main() {
   DIR *d;
   struct dirent *dir;
   d = opendir(".");
   
   if (d) {
      while ((dir = readdir(d)) != NULL) {
         printf("%s\n", dir->d_name);
      }
      closedir(d);
   }
   else {
      perror("opendir");
      exit(1);
   }
   return 0;
}
```
Bu örnekte, opendir() fonksiyonu çağrılarak, mevcut dizindeki dosyaları okumak için bir dizin işaretçisi elde ediliyor. Daha sonra, readdir() fonksiyonu kullanılarak dizindeki dosyaların adları okunuyor ve ekrana yazdırılıyor. En son olarak, dizin işaretçisi closedir() fonksiyonu kullanılarak kapatılıyor. Bu işlem, açılan dizindeki kaynakların serbest bırakılmasını ve işaretçinin geçersiz hale getirilmesini sağlar. Program, son olarak, sonlandırılıyor.

## strerror()
#### Açıklama :
strerror() fonksiyonu, bir hata kodu (error code) için karşılık gelen açıklama (description) metnini verir. Hata kodu, bir önceki sistem çağrısının geri dönüş değeri olan errno değişkeninde tutulur.
#### Return :
strerror() fonksiyonu, bir hata kodu için karşılık gelen açıklama metnini (string) döndürür.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <string.h>
#include <errno.h>

int main() {
   FILE *f;
   f = fopen("nonexistent_file.txt", "r");
   
   if (f == NULL) {
      printf("Hata kodu: %d\n", errno);
      printf("Açıklama: %s\n", strerror(errno));
   }
   else {
      fclose(f);
   }
   return 0;
}
```
Bu örnekte, fopen() fonksiyonu kullanılarak açılamayan bir dosya açılmaya çalışılıyor. Fonksiyon başarısız olursa, errno değişkenine bir hata kodu atanıyor. Daha sonra, strerror() fonksiyonu kullanılarak hata koduna karşılık gelen açıklama metni elde ediliyor ve ekrana yazdırılıyor. Bu işlem, hatanın nedenini anlamak için kullanışlıdır. En son olarak, program sonlandırılıyor.

## perror()
#### Açıklama :
perror() fonksiyonu, bir sistem çağrısının geri dönüş değerinin hata kodu olduğu durumlarda, hatanın açıklamasını ekrana yazdırır. Bu işlev, hatayı tanımlamaya yardımcı olur ve programcıların hatayı nasıl çözebileceklerine dair bir fikir edinmelerine yardımcı olur.
#### Return :
perror() fonksiyonu bir değer döndürmez (void).
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <stdlib.h>
#include <errno.h>

int main() {
   FILE *f;
   f = fopen("nonexistent_file.txt", "r");
   
   if (f == NULL) {
      perror("Hata");
      exit(1);
   }
   else {
      fclose(f);
   }
   return 0;
}
```
Bu örnekte, fopen() fonksiyonu kullanılarak açılamayan bir dosya açılmaya çalışılıyor. Fonksiyon başarısız olursa, perror() fonksiyonu kullanılarak hatanın açıklaması ekrana yazdırılır. Bu işlem, hatayı tanımlamaya yardımcı olur ve programcıların hatayı nasıl çözebileceklerine dair bir fikir edinmelerine yardımcı olur. En son olarak, program sonlandırılıyor.

## isatty()
#### Açıklama :
isatty() fonksiyonu, bir dosya tanıtıcısının (file descriptor) terminal cihazına (tty) bağlı olup olmadığını kontrol eder.
#### Return :
isatty() fonksiyonu, dosya tanıtıcısının terminal cihazına bağlı olması durumunda 1 değerini döndürür. Aksi takdirde 0 değerini döndürür.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <unistd.h>

int main() {
   if (isatty(0)) {
      printf("Standart girdi terminal cihazına bağlıdır.\n");
   }
   else {
      printf("Standart girdi terminal cihazına bağlı değildir.\n");
   }
   return 0;
}
```
Bu örnekte, isatty() fonksiyonu kullanılarak standart girdinin (stdin) terminal cihazına bağlı olup olmadığı kontrol ediliyor. Eğer bağlı ise, ekrana bir mesaj yazdırılıyor. Eğer bağlı değilse, başka bir mesaj yazdırılıyor. En son olarak, program sonlandırılıyor.

## ttyname()
#### Açıklama :
ttyname() fonksiyonu, bir dosya tanıtıcısının (file descriptor) bağlı olduğu terminal cihazının adını döndürür. Eğer dosya tanıtıcısı terminal cihazına bağlı değilse, NULL değerini döndürür.
#### Return :
ttyname() fonksiyonu, başarılı bir şekilde çağrıldığı takdirde, bağlı olduğu terminal cihazının adını (char *) döndürür. Eğer dosya tanıtıcısı terminal cihazına bağlı değilse, NULL değerini döndürür.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main() {
   char *terminal_cihazi;
   int dosya_tanitacisi = 0; /* standart girdi */
   terminal_cihazi = ttyname(dosya_tanitacisi);
   
   if (terminal_cihazi == NULL) {
      printf("Bağlı terminal cihazı bulunamadı.\n");
   }
   else {
      printf("Bağlı terminal cihazı: %s\n", terminal_cihazi);
   }
   return 0;
}
```
Bu örnekte, ttyname() fonksiyonu kullanılarak standart girdinin (stdin) bağlı olduğu terminal cihazının adı alınıyor. Eğer bir hata oluşursa, NULL değeri döndürülüyor. Eğer bir hata yoksa, terminal cihazının adı ekrana yazdırılıyor. En son olarak, program sonlandırılıyor.

## ttyslot()
#### Açıklama :
ttyslot() fonksiyonu, terminal oturumunun utmp veritabanındaki girişinin sırasını döndürür. utmp veritabanı, kullanıcıların giriş ve çıkış işlemlerini izleyen bir veritabanıdır.
#### Return :
ttyslot() fonksiyonu, başarılı bir şekilde çağrıldığı takdirde, terminal oturumunun utmp veritabanındaki girişinin sırasını (int) döndürür. Eğer hata oluşursa, -1 değeri döndürülür.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <stdlib.h>
#include <utmp.h>

int main() {
   int slot;
   struct utmp *utmp_girdi;

   /* utmp veritabanındaki girişi oku */
   setutent();
   utmp_girdi = getutent();

   while (utmp_girdi != NULL) {
      if (utmp_girdi->ut_type == USER_PROCESS) {
         /* kullanıcı oturumu bulundu */
         slot = ttyslot();
         printf("Terminal oturumunun utmp sırası: %d\n", slot);
         break;
      }
      utmp_girdi = getutent();
   }

   endutent();
   return 0;
}
```
Bu örnekte, ttyslot() fonksiyonu kullanılarak kullanıcının oturumunun utmp veritabanındaki sırası bulunuyor. İlk önce, setutent() fonksiyonu kullanılarak utmp veritabanı açılıyor. Daha sonra, getutent() fonksiyonu kullanılarak utmp veritabanındaki her bir giriş okunuyor ve kullanıcı oturumu bulunana kadar döngü devam ediyor. Eğer kullanıcı oturumu bulunursa, ttyslot() fonksiyonu çağrılarak oturumun utmp veritabanındaki sırası alınıyor ve ekrana yazdırılıyor. En son olarak, endutent() fonksiyonu kullanılarak utmp veritabanı kapatılıyor ve program sonlandırılıyor.

## ioctl()
#### Açıklama :
ioctl() fonksiyonu, sistem çağrıları arasında yer alan bir fonksiyondur. Bu fonksiyon, çeşitli giriş/çıkış (I/O) cihazlarına veya sistem kaynaklarına ilişkin kontrol işlemlerini yapmak için kullanılır.
#### Return :
ioctl() fonksiyonu, çağrıldığı sistem kaynağına ve işleme bağlı olarak farklı bir değer döndürebilir. Genellikle, başarılı bir işlem sonucunda 0 değeri döndürülürken, hata durumlarında -1 değeri döndürülür.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <stdlib.h>
#include <sys/ioctl.h>
#include <fcntl.h>

int main() {
   int dosya_ac = open("/dev/tty", O_RDONLY);
   int satir_sayisi;

   /* satır sayısını öğren */
   if (ioctl(dosya_ac, TIOCGWINSZ, &satir_sayisi) == -1) {
      perror("ioctl hatası");
      exit(1);
   }

   printf("Satır sayısı: %d\n", satir_sayisi);
   close(dosya_ac);
   return 0;
}
```
Bu örnekte, ioctl() fonksiyonu kullanılarak /dev/tty dosyasının boyutu öğreniliyor. İlk olarak, open() fonksiyonu kullanılarak /dev/tty dosyası açılıyor ve bir dosya tanımlayıcısı (file descriptor) alınıyor. Daha sonra, ioctl() fonksiyonu çağrılarak TIOCGWINSZ belirteci kullanılarak dosya boyutu öğreniliyor. Eğer bir hata oluşursa, perror() fonksiyonu kullanılarak hatanın ayrıntıları ekrana yazdırılıyor. Son olarak, dosya kapatılıyor ve program sonlandırılıyor.

## getenv()
#### Açıklama :
getenv() fonksiyonu, verilen bir çevre değişkeninin değerini döndürmek için kullanılır. Çevre değişkenleri, bir programın çalıştığı ortamın değişkenleridir ve sıklıkla programların farklı ayarlarını belirlemek için kullanılır.
#### Return :
getenv() fonksiyonu, verilen çevre değişkeninin değerini döndürür. Eğer verilen çevre değişkeni mevcut değilse NULL değeri döndürür.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <stdlib.h>

int main() {
   char *home_dir = getenv("HOME");
   if (home_dir == NULL) {
      printf("HOME çevre değişkeni mevcut değil.\n");
   } else {
      printf("Home dizini: %s\n", home_dir);
   }
   return 0;
}
```
Bu örnekte, getenv() fonksiyonu kullanılarak HOME çevre değişkeninin değeri öğreniliyor. Eğer HOME çevre değişkeni mevcut değilse, ekrana "HOME çevre değişkeni mevcut değil." yazısı yazdırılıyor. Eğer çevre değişkeni mevcutsa, değeri printf() fonksiyonu kullanılarak ekrana yazdırılıyor.

## tcsetattr()
#### Açıklama :
tcsetattr() fonksiyonu, terminal ayarlarını değiştirmek için kullanılır. Bu fonksiyon, terminalin özelliklerini kontrol etmek ve değiştirmek için kullanılan termios yapısını kullanır.
#### Return :
tcsetattr() fonksiyonu, başarılıysa 0 değerini, başarısız olursa -1 değerini döndürür.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <stdlib.h>
#include <termios.h>

int main() {
    struct termios term;
    if (tcgetattr(STDIN_FILENO, &term) == -1) {
        perror("tcgetattr");
        return 1;
    }
    term.c_lflag &= ~(ICANON | ECHO);
    if (tcsetattr(STDIN_FILENO, TCSAFLUSH, &term) == -1) {
        perror("tcsetattr");
        return 1;
    }
    // Terminalde girdi alınabilir
    // Ayarlar orijinal hale getirilir
    if (tcsetattr(STDIN_FILENO, TCSAFLUSH, &term) == -1) {
        perror("tcsetattr");
        return 1;
    }
    return 0;
}
```
Bu örnekte, tcgetattr() fonksiyonu kullanılarak standart girdinin terminal ayarları elde edilir. term.c_lflag değişkeni kullanılarak, girdinin satır modu (ICANON) ve geri yansıtma (ECHO) ayarları devre dışı bırakılır. Daha sonra, değiştirilmiş ayarlar tcsetattr() fonksiyonu kullanılarak uygulanır. TCSAFLUSH bayrağı, çıktı tamamen boşaltılıp ayarların uygulanmasına kadar beklemek için kullanılır. Son olarak, orijinal ayarlara geri dönülür. perror() fonksiyonu, tcgetattr() veya tcsetattr() fonksiyonlarından herhangi biri hata döndürürse hatayı ekrana yazdırır.

## tcgetattr()
#### Açıklama :
tcgetattr() fonksiyonu, terminal ayarlarını elde etmek için kullanılır. Bu fonksiyon, terminalin özelliklerini kontrol etmek ve değiştirmek için kullanılan termios yapısını kullanır.
#### Return :
tcgetattr() fonksiyonu, başarılıysa 0 değerini, başarısız olursa -1 değerini döndürür.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <stdlib.h>
#include <termios.h>

int main() {
    struct termios term;
    if (tcgetattr(STDIN_FILENO, &term) == -1) {
        perror("tcgetattr");
        return 1;
    }
    printf("Baud rate: %d\n", cfgetispeed(&term));
    printf("Data bits: %d\n", (term.c_cflag & CSIZE) + 5);
    printf("Stop bits: %d\n", (term.c_cflag & CSTOPB) ? 2 : 1);
    printf("Parity: %d\n", (term.c_cflag & PARENB) ? ((term.c_cflag & PARODD) ? 1 : 2) : 0);
    return 0;
}
```
Bu örnekte, tcgetattr() fonksiyonu kullanılarak standart girdinin terminal ayarları elde edilir. cfgetispeed() fonksiyonu kullanılarak, girdinin baud hızı elde edilir. CSIZE, CSTOPB ve PARENB bayrakları kullanılarak, veri bitleri, durdurma bitleri ve çiftlik denetimi ayarları elde edilir. Elde edilen ayarlar, printf() fonksiyonu kullanılarak ekrana yazdırılır. perror() fonksiyonu, tcgetattr() fonksiyonu hata döndürürse hatayı ekrana yazdırır.

## tgetent()
#### Açıklama :
tgetent() fonksiyonu, termcap veritabanındaki bir terminal tanım dosyasını yüklemek için kullanılır. Bu fonksiyon, termcap veritabanındaki bir terminale ilişkin tüm bilgileri yükler ve bir yerel bellek alanına kaydeder.
#### Return :
tgetent() fonksiyonu, başarılıysa 1 değerini, belirtilen terminale ilişkin bir tanım bulunamazsa veya tanım dosyası açılamazsa 0 değerini, bir hata oluşursa ise -1 değerini döndürür.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <term.h>

int main() {
    char buf[1024];
    if (tgetent(buf, "xterm") == 1) {
        char *termtype = getenv("TERM");
        if (termtype == NULL) {
            printf("TERM is not set.\n");
        } else {
            printf("Terminal type: %s\n", termtype);
        }
    } else {
        printf("Cannot load terminal definition.\n");
    }
    return 0;
}
```
Bu örnekte, tgetent() fonksiyonu kullanılarak xterm terminal tanım dosyası yüklenir. getenv() fonksiyonu kullanılarak, TERM değişkeninin değeri alınır. Eğer TERM değişkeni tanımlı ise, terminal tipi ekrana yazdırılır. Eğer TERM değişkeni tanımlı değilse, TERM is not set. mesajı ekrana yazdırılır. tgetent() fonksiyonu hata döndürürse, Cannot load terminal definition. mesajı ekrana yazdırılır.

## tgetflag()
#### Açıklama :
tgetflag() fonksiyonu, termcap veritabanındaki bir terminale ilişkin bayrak değerlerini döndürür. tgetflag() fonksiyonu, terminale özgü bir bayrak değeri varsa 1 değerini döndürür, aksi takdirde 0 değerini döndürür.
#### Return :
tgetflag() fonksiyonu, terminale özgü bir bayrak değeri varsa 1 değerini, aksi takdirde 0 değerini döndürür.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <term.h>

int main() {
    char buf[1024];
    if (tgetent(buf, "xterm") == 1) {
        if (tgetflag("am") == 1) {
            printf("Automatic margins are supported.\n");
        } else {
            printf("Automatic margins are not supported.\n");
        }
    } else {
        printf("Cannot load terminal definition.\n");
    }
    return 0;
}
```
Bu örnekte, tgetent() fonksiyonu kullanılarak xterm terminal tanım dosyası yüklenir. tgetflag() fonksiyonu kullanılarak, am bayrağı kontrol edilir. Eğer bayrak varsa, Automatic margins are supported. mesajı ekrana yazdırılır. Eğer bayrak yoksa, Automatic margins are not supported. mesajı ekrana yazdırılır. tgetent() fonksiyonu hata döndürürse, Cannot load terminal definition. mesajı ekrana yazdırılır.

## tgetnum()
#### Açıklama :
tgetnum() fonksiyonu, termcap veritabanındaki bir terminale ilişkin sayısal değerleri döndürür. tgetnum() fonksiyonu, belirtilen değerin adı ile eşleşen sayısal değeri döndürür. Örneğin, tgetnum("cols") fonksiyonu, terminale ilişkin sütun sayısını döndürür.
#### Return :
tgetnum() fonksiyonu, belirtilen değerin adı ile eşleşen sayısal değeri döndürür. Eğer bu değer mevcut değilse, -1 değeri döndürülür.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <term.h>

int main() {
    char buf[1024];
    if (tgetent(buf, "xterm") == 1) {
        int cols = tgetnum("cols");
        int rows = tgetnum("rows");
        if (cols > 0 && rows > 0) {
            printf("Terminal size is %dx%d.\n", cols, rows);
        } else {
            printf("Cannot get terminal size.\n");
        }
    } else {
        printf("Cannot load terminal definition.\n");
    }
    return 0;
}
```
Bu örnekte, tgetent() fonksiyonu kullanılarak xterm terminal tanım dosyası yüklenir. tgetnum() fonksiyonu kullanılarak, cols ve rows değerleri elde edilir. Eğer her iki değer de mevcutsa, Terminal size is <cols>x<rows>. mesajı ekrana yazdırılır. Eğer herhangi bir değer mevcut değilse, Cannot get terminal size. mesajı ekrana yazdırılır. tgetent() fonksiyonu hata döndürürse, Cannot load terminal definition. mesajı ekrana yazdırılır.

## tgetstr()
#### Açıklama :
tgetstr() fonksiyonu, termcap veritabanındaki bir terminale ilişkin karakter dizisi değerini döndürür. tgetstr() fonksiyonu, belirtilen değerin adı ile eşleşen karakter dizisi değerini döndürür. Örneğin, tgetstr("cm") fonksiyonu, terminale ilişkin imleç hareketi karakter dizisini döndürür.
#### Return :
tgetstr() fonksiyonu, belirtilen değerin adı ile eşleşen karakter dizisi değerini döndürür. Eğer bu değer mevcut değilse, NULL değeri döndürülür.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <term.h>

int main() {
    char buf[1024];
    if (tgetent(buf, "xterm") == 1) {
        char *cm = tgetstr("cm", NULL);
        if (cm != NULL) {
            printf("Cursor movement string is %s.\n", cm);
        } else {
            printf("Cannot get cursor movement string.\n");
        }
    } else {
        printf("Cannot load terminal definition.\n");
    }
    return 0;
}
```
Bu örnekte, tgetent() fonksiyonu kullanılarak xterm terminal tanım dosyası yüklenir. tgetstr() fonksiyonu kullanılarak, cm değeri elde edilir. Eğer cm değeri mevcutsa, Cursor movement string is <cm>. mesajı ekrana yazdırılır. Eğer cm değeri mevcut değilse, Cannot get cursor movement string. mesajı ekrana yazdırılır. tgetent() fonksiyonu hata döndürürse, Cannot load terminal definition. mesajı ekrana yazdırılır.

## tgoto()
#### Açıklama :
tgoto() fonksiyonu, terminal ekranında, belirli bir yere gitmek için kullanılan hareket dizgisi karakter dizisini oluşturur. Bu karakter dizisi, terminal kontrol karakterlerini (özellikle imleç hareketleri) içerir. Fonksiyon, hareket dizgisini oluşturmak için terminal tanım dosyasından gerekli bilgileri alır.
#### Return :
tgoto() fonksiyonu, belirtilen koordinatlara hareket etmek için gereken karakter dizisi değerini döndürür.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <curses.h>

int main() {
    char *move_str = tgoto(tgetstr("cm", NULL), 10, 20);
    printf("Move cursor to (10, 20): %s\n", move_str);
    return 0;
}
```
Bu örnekte, tgetstr() fonksiyonu kullanılarak cm karakter dizisi elde edilir. tgoto() fonksiyonu kullanılarak, cm karakter dizisi ve 10, 20 koordinatları kullanılarak hareket dizgisi oluşturulur. Son olarak, oluşturulan hareket dizgisi printf() fonksiyonu kullanılarak ekrana yazdırılır.

## tputs()
#### Açıklama :
tputs() fonksiyonu, terminal ekranında belirli bir etkiyi (örneğin, renk değiştirme veya imleç hareketi) oluşturmak için kullanılan kontrol karakterlerini yazdırır. Fonksiyon, terminal tanım dosyasından gerekli bilgileri alarak kontrol karakterlerini oluşturur.
#### Return :
tputs() fonksiyonu, başarılı bir şekilde yazdırılan karakter sayısını döndürür. Başarısızlık durumunda ise ERR (-1) değerini döndürür.
### Kullanım/Örnekler
```javascript
#include <stdio.h>
#include <curses.h>

int main() {
    char *setaf_str = tparm(tgetstr("setaf", NULL), COLOR_GREEN);
    tputs(setaf_str, 1, putchar);
    printf("This text is green.\n");
    return 0;
}
```
Bu örnekte, tgetstr() fonksiyonu kullanılarak setaf karakter dizisi elde edilir. tparm() fonksiyonu kullanılarak, setaf karakter dizisi ve COLOR_GREEN (yeşil renk kodu) kullanılarak renk değiştirme kontrol karakteri oluşturulur. tputs() fonksiyonu kullanılarak, oluşturulan kontrol karakteri putchar() fonksiyonu aracılığıyla yazdırılır. Son olarak, printf() fonksiyonu kullanılarak yeşil renkli metin ekrana yazdırılır.
## Katkı/Kapanış

Sevgili dostlar,

Bu kaynak, C programlama dilinde sıkça kullanılan fonksiyonların Türkçe açıklamalarını içeren bir rehberdir. Bu kaynak, Minishell projesinde çalışanlar için önemli bir kaynak olmayı hedeflemektedir.

Kaynağın geliştirilmesi ve genişletilmesine katkı sağlamak isteyen herkesi de açık bir şekilde davet ediyorum.

Umarım bu kaynak, C programlama dilinde çalışanlara yardımcı olur ve bu alanda çalışanların işlerini kolaylaştırır.

Saygılarımla,

[Bilal Nurtaş](https://github.com/bilalnrts)
  
## Destek

Destek için [bana](https://www.linkedin.com/in/bilal-salih-nurtaş-047bb7212/) adresinden mesaj atabilirsiniz.

  