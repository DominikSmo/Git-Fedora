### Konfiguracja Git w Fedorze

Jeśli chcemy dodawać repozytoria do serwisu Github z poziomu wirtualnego Linuxa(w tym przypadku Fedory) to musimy mieć skonfigurowany Git w maszynie wirtualnej.
Co należy zrobić?

**1.** Instalacja systemu Git w Fedorze: 
w terminalu maszyny wirtualnej piszemy: **sudo dnf install git -y**

**2.** Można sprawdzić wersję Git-a: **git --version**
Powinno wyświetlić "git version numer wersji"

**3.** Konfiguracja użytkownika z Github:
**git config --global user.name Twój login do serwisu Github(nie adres email)**
**git config --global user.email Twój adres email połączony z Twoim kontem w serwisie Github**

**4.** Konfigurację użytkownika można sprawdzić poleceniem : 
**git config --list** Wówczas powinno się wyświetlić:
user.name=nasz login do serwisu Github
user.email=nasz adres email połaczony z kontem w serwisie Github
itd.
Jeśli wszystko się zgadza to znaczy, że dobrze skonfigurowaliśmy uzytkownika w maszynie wirtualnej z użytkownikiem w serwsie Github.

**5.** Połączenie Git z Github

**a.** Połączenie za pomocą protokołu **HTTPS(HyperText Transfer Protocol Secure)** 
Jest to szyfrowany protokół do przesyłania danych w sieci. Dla odróżnienia **HTTP** jest protokołem do przesyłania danych w sieci ale nieszyfrowanym.
Jak HTTPS działa w Git.
Jeśli w Git uzyjemy URL repozytorium w formacie: 
**https://github.com/user.name/repo.name.git** to Git łączy się z Github przez szyfrowany kanał HTTPS. Każda wymiana pull, push, fetch jest szyfrowana
i bezpieczna. Należy wspomnieć, że Github nie używa już haseł do HTTPS. Dlatego przy połączeniu Git z Github przez HTTPS potrzebny jest **Personal Access Token**
**(PAT)** zamiast zwykłego hasła użytkownika.

**b.** Połączenie za pomocą klucza **SSH**
Jest to bezpieczna metoda, która nie wymaga wpisywania loginu i tokena przy każdej próbie połączenia Git z Github. Np. niepotrzebne jest podawanie loginu ani
tokena przy każdym przesłaniu na Github nowego repozytorium lub przy edytowaniu go.
Klucz **SSH** to para powiązanych ze sobą kluczy kryptograficznych używanych do bezpiecznej, szyfrowanej komunikacji pomiędzy komputerami, najczęściej w celu
logowania do serwerów lub uwierzytelniania w systemach takich jak Github.

## Wygenerowanie klucza SSH
Należy użyć polecenia:
**ssh-keygen -t abxxxxx -C user.email(z Github)**

Klikamy Enter by zatwierdzić ścieżkę ~/.ssh/id_abxxxxx
Następnie należy wpisać hasło do klucza ale można pozostawić także puste pole.
Klucz id_abxxxxx to klucz prywatny.
Potrzebujemy pary kluczy: jeden to klucz prywatny, drugi to klucz publiczny **(id_abxxxxx.pub)**
Znajdziemy go w naszym katalogu domowym **~/.ssh/id_abxxxxx.pub**
Wówczas należy go skopiować do serwisu Github:
**Settings**
**SSH and GPG keys**
**New SSH key**
Sprawdzenie połączenia Git z Github poleceniem:
**ssh -T git@github.com**
Jeśli wszystko jest w porządku to wyświetli się powitalny komunikat z Github.
Klucza prywatnego nie udostępnia się publicznie. Służy on do podpisywania się i potwierdzania tożsamości użytkownika.
Klucz publiczny udostępnia się serwerowi bądź platformie(np. Github). Pozwala to serwerowi sprawdzić, że loguje się właściciel odpowiedniego klucza prywatnego.
Czyli przy próbie połączenia Git z poziomu Fedory z serwisem Github, serwis ten rozpoznaje maszynę wirtualną użytkownika za pomocą klucza prywatnego wygenerowanego 
w terminalu maszyny wirtualnej.
Można też dodać, że istnieją różne typy kluczy. Zależy to od algorytmu kryptograficznego użytego do stworzenia danego klucza.

