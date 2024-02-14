# TestNG (Testing framework for next generations )

## Uvod u TestNG

TestNG je open-source testing framework, koji je namijenjen **Java** programskom jeziku, a razvio ga je Cédric Beust. Omogućava pisanje specifičnih testova, koji provjeravaju ispravnost, efikasnost i očekivano ponašanje djelova aplikacije. Inspirisan je JUnit-om i prevazilazi njegove nedostatke, jer je dizajniran da olakša testiranje do kraja.

### Neke prednosti TestNG-a u odnosu na JUnit

- Anotacije su lakše za razumijevanje
- Test slučajevi (cases) mogu lakše da se grupišu
- Moguće je paralelno testiranje
- Proizvodi HTML izvještaje za implementaciju
- Geberiše logove
- Podržava tri dodatna nivoa, kao što su **@Before/After suite**, **@Before/AfterTest** i **Before/AfterGroup**

Koristeći TestNG, možemo da generišemo odgovarajući izvještaj i da lako saznamo koliko je test slučajeva prošlo, neuspješno ili prekočeno. Neuspjele test slučajeve možemo da izvršimo zasebno.

**Primjer:** Imamo 5 test slučajeva i jedna metoda je napisana za svaki od njih. (Pretpostavka da je program napisan koristeći glavnu metodu bez upotrebe TestNG.) Kada prvo pokrenemo program, uspješno se izvršavaju tri metode, a četvrta je neuspješna. Zatim, ispravimo greške prisutne u četvrtoj metodi i želimo da pokrenemo samo nju, jer se prve tri svakako izvršavaju uspješno. Sve ovo ne bi bilo moguće bez TestNG-a.

## Ključne karakteristike

- **Anotacije** (za laku identifikaciju metoda testa) - linije koda koje mogu da kontrolišu kako će se izvršiti metoda ispod njih. Uvijek im prethodi simbol **@**. Primjer:

```java
@Test(priority = 0)
public void goToHomepage() {
    driver.get(baseUrl);
    Assert.assertEquals(driver.getTitle(), "Welcome: Simon S");
}

@Test(priority = 1)
public void logout() {
    driver.findElement(By.linkText("SIGN-OFF")).click();
    Assert.assertEquals("Sign-on: Simon S", driver.getTitle());
}
```

Ovaj primjer jednostavno pokazuje, da metoda **goToHomepage()** treba da se izvrši prije **logout()** metode, jer ima niži prioritet.

- **Fleksibilne konfiguracije testova** - omogućava kreiranje fleksibilnih i dinamičkih konfiguracija testova, korišćenjem XML datoteka. To znači da lako možemo definisati kako, kada i koji testovi treba da se pokrenu, što je posebno korisno za složene test scenarije.
- **Podrška za paralelno izvršavanje testova** - značajno smanjuje vrijeme potrebno za izvršavanje velikog broja testova.
- **Snažna izvještavanja** - pruža detaljne izvještaje o izvršenju testova.
- **Zavisnosti** - podržava definisanje zavisnosti između test metoda.