# 04-01-03-inheritence-simcard
## Öröklődés (beadandó feladat)
![image](https://user-images.githubusercontent.com/6060514/116874919-5fb8b600-ac1a-11eb-9a00-635db62479e5.png)
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
