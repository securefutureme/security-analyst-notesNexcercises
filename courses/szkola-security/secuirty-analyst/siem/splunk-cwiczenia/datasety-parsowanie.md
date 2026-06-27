Zadanie - dodanie logów do Splunka krok po kroku.

**Mamy dwa logi - sqlmap.log i LFI_webshell.log**. Zajmijmy się dodaniem najpierw pierwszych logów.

1. Wchodzimy do Splunk -> Add Data

![alt](/courses/szkola-security/secuirty-analyst/siem/splunk-cwiczenia/Attachments/1-image.png)

lub

![alt](/courses/szkola-security/secuirty-analyst/siem/splunk-cwiczenia/Attachments/2-image.png)

2. Klikamy **Upload**
   
![alt](/courses/szkola-security/secuirty-analyst/siem/splunk-cwiczenia/Attachments/3-image.png)

2. Następnie Select File -> po wybraniu klikamy -> Next.

![alt](/courses/szkola-security/secuirty-analyst/siem/splunk-cwiczenia/Attachments/4-image.png)

3. Powinny nam się pokazać sparsowane dane z logów:

![alt](/courses/szkola-security/secuirty-analyst/siem/splunk-cwiczenia/Attachments/5-image.png)

4. Source type ustawiamy na **"access_combined"** -> Klikamy **Next**.
5. Następnie ustawiamy nazwę hosta.

![alt](/courses/szkola-security/secuirty-analyst/siem/splunk-cwiczenia/Attachments/6-image.png)

6. Wybieramy index, albo tworzymy nowy.

![alt](/courses/szkola-security/secuirty-analyst/siem/splunk-cwiczenia/Attachments/8-image.png)

Tutaj oprócz nazwy nic nie zmieniamy, klikamy Save i wybieramy go po utworzeniu.

![alt](/courses/szkola-security/secuirty-analyst/siem/splunk-cwiczenia/Attachments/9-image.png)

7. Klikamy Review

![alt](/courses/szkola-security/secuirty-analyst/siem/splunk-cwiczenia/Attachments/10-image.png)

8. Następnie Submit i przechodzimy do wyszukiwania.

![alt](/courses/szkola-security/secuirty-analyst/siem/splunk-cwiczenia/Attachments/11-image.png)

![alt](/courses/szkola-security/secuirty-analyst/siem/splunk-cwiczenia/Attachments/12-image.png)

9. Na początku sprawdzamy czy Splunk wyparsował nam pola prawidłowo. Będzie to widoczne po ilości widocznych pól z eventu **(index="zadanieindex"  sourcetype="access_combined" host="zadanie-sqlmap")**:

![alt](/courses/szkola-security/secuirty-analyst/siem/splunk-cwiczenia/Attachments/13-image.png)

10. Jeżeli Splunk nie zrobił tego prawidłowo, mamy modyfikowanie źródłowego pliku logów albo napisanie parsera. Wybieramy pierwszą opcję. **Wchodzimy do niej, poprzez rozwinięcie "Event Actions" -> "Extract Fields"** (albo **Settings → Fields → Field extractions → Open field extractor**.)

![alt](/courses/szkola-security/secuirty-analyst/siem/splunk-cwiczenia/Attachments/15-image.png)

11. Jednak ta opcja, opisana w kursie, jest nieidealna, ponieważ format logów się miesza w tych plikach i musimy przeprowadzić pewną operację, by te logi zostały prawidłowo sparsowane.

12. Wchodzimy do terminala. Tutaj użyjemy komendy do "wycięcia" pierwszego pola i stworzenie kopii pliku logów. 

`cat sqlmap.log | cut -d " " -f2- > copysqlmap.log`

Tak to powinno wyglądać:

![alt](/courses/szkola-security/secuirty-analyst/siem/splunk-cwiczenia/Attachments/17-image.png)

13. Pozostaje nam dodać jeszcze raz kopię pliku do Splunka.

![alt](/courses/szkola-security/secuirty-analyst/siem/splunk-cwiczenia/Attachments/18-image.png)

**Jak widać, plik został dodany, i wszystkie pola wyświetlają się prawidłowo :)**

Poniżej dowód na dodany plik LFI_webshell.log

![alt](/courses/szkola-security/secuirty-analyst/siem/splunk-cwiczenia/Attachments/19-image.png)
