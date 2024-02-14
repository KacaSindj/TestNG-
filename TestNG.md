# TestNG (Testing framework for next generations )

## Uvod u TestNG

TestNG je open-source testing framework, koji je namijenjen **Java** programskom jeziku, a razvio ga je Cédric Beust. Omogućava pisanje specifičnih testova, koji provjeravaju ispravnost, efikasnost i očekivano ponašanje djelova aplikacije. Inspirisan je JUnit-om i prevazilazi njegove nedostatke, jer je dizajniran da olakša testiranje do kraja.

#### Neke prednosti TestNG-a u odnosu na JUnit

- Anotacije su lakše za razumijevanje
- Test slučajevi (cases) mogu lakše da se grupišu
- Moguće je paralelno testiranje
- Proizvodi HTML izvještaje za implementaciju
- Generiše logove
- Podržava tri dodatna nivoa, kao što su **@Before/After suite**, **@Before/AfterTest** i **Before/AfterGroup**
- Koristi više Java i OO funkcija

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

## TestNG okruženje

- Sistemski zahtijevi : JDK 1.7 ili više

**Korak 1 - Instalacija Java programa**
- Instalirati Java programa, ako već nije instaliran. Link za instalaciju Java Software Development Kit (SDK): https://www.oracle.com/technetwork/java/javase/downloads/index.h

**Korak 2 - Podešavanje Java okruženja**
- Podesiti promjenljivu JAVA_HOME da ukazuje na lokaciju osnovnog direktorijuma, gdje je Java instalirana. Npr. za *Windows* podesiti varijablu JAVA_HOME na *C:\Program Files\Java\jdk15.0.2.* Zatim, dodati lokaciju Java kompajlera u sistemsku putanju. Dodati string *C:\Program Files\Java\jdk1.7.0_25\bin* na kraju System Variable, Path-a. Provjeriti instalaciju koristeći komandu *java -version*.

**Koark 3 - Preuzeti TestNG Archive**
- Preuzeti najnoviju verziju TestNG jar datoteke sa http://www.testng.org ili [odavde](https://mvnrepository.com/artifact/org.testng/testng).

**Korak 4 - Podešavanje TestNG okruženja**
- Podesiti promjenljivu TESTNG_HOME da ukazuje na lokaciju osnovnog direktorijuma, gdje je TestNG smješten na računaru. Npr. za *Windows*, pod pretpostavkom da je testng.jar smješten na lokaciji /work/testng, setujemo varijablu TESTNG_HOME na *C:\testng*.

**Korak 5 - Podešavanje CLASSPATH varijable**
- Za **Windows** postavljamo CLASSPATH varijablu da ukazuje na TestNG jar lokaciju, *%CLASSPATH%;%TESTNG_HOME%\testng-7.4.jar.*

**Korak 6 - Testiranje TestNG setup-a**
- Napraviti java klasu pod nazivom *TestNGSimpleTest* na /work/testng/src.

```java
import org.testng.annotations.Test;
import static org.testng.Assert.assertEquals;

public class TestNGSimpleTest {
   @Test
   public void testAdd() {
      String str = "TestNG is working fine";
      AssertEquals("TestNG is working fine", str);
   }
}
```
TestNG se može pozvati na nekoliko različitih načina :

- Sa testng.xml fajlom
- Sa ANT
- Sa komandne linije

U ovom primjeru se poziva putem datoteke testng.xml. Kreiramo xml datoteku testng.xml u /work.testng/src da bi se izvršili test slučajevi.

```html
<?xml version = "1.0" encoding = "UTF-8"?>
<!DOCTYPE suite SYSTEM "http://testng.org/testng-1.0.dtd" >

<suite name = "Suite1">
   <test name = "test1">
      <classes>
         <class name = "TestNGSimpleTest"/>
      </classes>
   </test>
</suite>
```

**Korak 7 - Verifikacija rezultata**
- Kompajliramo klasu koristeći javac compiler */work/testng/src$ javac TestNGSimpleTest.java*
- Pozivamo testng.xml da vidimo rezultat */work/testng/src$ java org.testng.TestNG testng.xml*
- Verifikacija output-a

```html
 ===============================================
  Suite
  Total tests run: 1, Passes: 1, Failures: 0, Skips: 0
  ===============================================

```
