# 04-01-03-inheritence-simcard
## Öröklődés (beadandó feladat)
### SIM kártya
A feladat két részből áll. Először egy SimCard osztályt kell kifejleszteni. Az osztály a mobil telefonokban lévő SIM kártyát modellezi. Létre lehet hozni egy SIM kártyát megadott PIN kódal (pinCode) és létrehozáskor a SIM kártya nincs aktiválva. A felhasználó az Activation metódussal aktiválhatja a kártyát egy PIN kód megadásával. Ha a PIN kódot eltalálja, akkor a kártya aktiválódik.  
Az IsActive tulajdonság megadja, hogy a kártya aktív (true) vagy nem (false).  
A ToString() metódus két kimenetet adhat:  
- **A SIM kártya nem aktív.**  
- **A SIM kártya aktív.**  

![image](https://user-images.githubusercontent.com/6060514/116883287-bd063480-ac25-11eb-9c29-63c1edb7ecee.png)

### ExtendedSimCard
Az ExtendedSimCard osztály a SimCard osztály kiterjesztése.  
A kiterjesztett SIM kártya három rosszul beírt PIN kód esetén zárolódik (locked=false).  
Zárolt kártya csak helyesen megadott PUK kód esetén lesz feloldva. PUK kód bármennyiszer megadható büntetlenül. Ha a PUK kóddal feloldottuk a kártyát, még mindig kevesebb, mint három hibátlanunk megadott PIN kóddal lehet újra aktiválni.  
Kiterjesztett kártya PIN és PUK kód megadásával lehet létrehozni. Létrehozás után a kártya nincs zárolva és még egy kísérlet sem történ a PIN kód megadására.
Az IsLock tulajdonság megadja, hogy a kártya zárolva van-e vagy nem!  
Pink kód megadásával csak nem zárolt kártyát lehet aktiválni. Ha az egymás utáni háromszor hibás PIN kódot adunk meg, akkor a kártya zárolva lesz. Ha a PIN kódot jól adjuk meg, akkor a kártya aktív lesz.  
A TurningOff metódussal a telefont kikapcsoljuk, azaz a nem lesz aktív, de nem is lesz zárolva (a próbálkozások számát is ilyenkor nullára kell állítani). Ez után megint próbálkozhatunk a kártya bekapcsolásával (ez a tesztkódba nincs már).  
Zárolt kártyát az UnLock metódussal lehet feloldani, helyes PUK kód megadásával. A próbálkozások számára nincs korlát.  
A ToString a következő kimeneteket adhatja:  
- **A kiterjesztett SIM kártya nem zárolt, és nem aktivált.**
- **A kiterjesztett SIM kártya nem zárolt, és aktivált.**
- **A kiterjesztett SIM kártya zárolt, és nem aktivált.**

[haladó fejlesztési lehetőségek]  
a)   
A PUK kóddal csak egyszer lehet feloldani a kártyát! Ha nem sikerül örökre zárva marad, még el nem visszük a kártyát a szolgáltató céghez (ezt nyilván nem kell leprogramozni, hogy elvisszük!).  
b)  
Ha a PUK kóddal sem sikerült feloldani a kártyát, akkor egy MasterUnLock() metódussal a szolgáltató cég felhasználója új PIN és PUK kódot adhasson meg, és a kártya legyen feloldott, de nem aktív.  


### Tesztkód
```
            SimCard card = new SimCard(1111);
            Console.WriteLine("A SIM kártya aktiválásra vár!");
            do
            {
                Console.WriteLine("Adja meg a SIM kártya PIN kódját:");
                int enteredPinCode = Convert.ToInt32(Console.ReadLine());
                card.Activation(enteredPinCode);
                Console.WriteLine(card);
            }
            while (!card.IsActive);

            ExtentedSimCard extCard = new ExtentedSimCard(1111, 9999);
            extCard.Activation(1234);
            Console.WriteLine(extCard);
            extCard.Activation(1234);
            Console.WriteLine(extCard);
            extCard.Activation(1234);
            Console.WriteLine(extCard);
            do
            {
                if (extCard.IsLocked)
                {
                    do
                    {
                        Console.WriteLine("Adja meg a SIM kártya PUK kódját:");
                        int enteredPukCode = Convert.ToInt32(Console.ReadLine());
                        extCard.UnLock(enteredPukCode);
                        Console.WriteLine(extCard);
                    } while (extCard.IsLocked);
                }
                Console.WriteLine("Adja meg a SIM kártya PIN kódját:");
                int enteredPinCode = Convert.ToInt32(Console.ReadLine());
                extCard.Activation(enteredPinCode);
                Console.WriteLine(extCard);
            }
            while (!extCard.IsActive);
            extCard.TurningOff();
            Console.WriteLine(extCard);
```


### Kimenet
```
A SIM kártya aktiválásra vár!
Adja meg a SIM kártya PIN kódját:
1234
A sim kártya nem aktív.
Adja meg a SIM kártya PIN kódját:
4321
A sim kártya nem aktív.
Adja meg a SIM kártya PIN kódját:
1111
A sim kártya aktív.

A kiterjesztett sim kártya nem zárolt, és nem aktivált.
A kiterjesztett sim kártya nem zárolt, és nem aktivált.
A kiterjesztett sim kártya zárolt, és nem aktivált.
Adja meg a SIM kártya PUK kódját:
1234
A kiterjesztett sim kártya nem zárolt, és nem aktivált.
Adja meg a SIM kártya PIN kódját:
4321
A kiterjesztett sim kártya nem zárolt, és nem aktivált.
Adja meg a SIM kártya PIN kódját:
9999
A kiterjesztett sim kártya nem zárolt, és nem aktivált.
Adja meg a SIM kártya PIN kódját:
1234
A kiterjesztett sim kártya nem zárolt, és nem aktivált.
Adja meg a SIM kártya PIN kódját:
1111
A kiterjesztett sim kártya nem zárolt, és aktivált.
A kiterjesztett sim kártya nem zárolt, és nem aktivált.
```
