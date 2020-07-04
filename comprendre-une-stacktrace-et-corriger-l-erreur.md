# Comment bien comprendre une stacktrace

## Préambule
Il existe deux types d'exceptions :
- Les _unchecked exceptions_ qui sont des exceptions qui n'ont pas besoins d'être déclarer dans le code
- Les _checked exceptions_ qui sont des exceptions qui doivent être encadrée d'un `try catch`

### Unchecked Exception
#### Error
La classe [Error](https://docs.oracle.com/javase/8/docs/api/java/lang/Error.html) est invoquée lors d'une erreur grave intervenue dans la JVM, elle stop immédiatement le programme

#### Exception
La classe [Exception](https://docs.oracle.com/javase/8/docs/api/java/lang/Exception.html) est invoquée lors d'une erreur moins grave, elles peuvent stopper le programme<br>

### Checked Exception
#### RuntimeException
La classe [RuntimeException](https://docs.oracle.com/javase/8/docs/api/java/lang/RuntimeException.html) hérite de la classe [Exception](https://docs.oracle.com/javase/8/docs/api/java/lang/Exception.html) <br>
Toutes les classes héritant de la classe [RuntimeException](https://docs.oracle.com/javase/8/docs/api/java/lang/RuntimeException.html) dont des exceptions de type _checked_

## Méthode :
Une stacktrace est faite pour comprendre une erreur tout est dedans
```
java.lang.Exception: Template exception
	at ga.enimaloc.Main.main(Main.java:7)
```
Ici vous avez un stacktrace qui ne seras jamais invoqué mais me serviras d'exemple<br>
Composition de la stacktrace,<br>
- `java.lang.Exception` est le chemin de l'exception, elle permet de déterminer le nom de l'exception et de savoir de qu'elle librairie elle provient.
- `Template exception` est le message fourni lors de l'invocation, souvent elle précise pourquoi l'exception a été invoqué
- le reste en dessous `at ga.enimaloc.Main.main(Main.java:7)` est le chemin de l'exception, `ga.enimaloc` est le package de la classe, `Main` est la classe, `main` la méthode, `Main.java` le fichier source, `7` est la ligne de l'invocation

Maintenant si on essaye de transposée ça en français cela donnerait :<br>
`Exception` faisant partie du package `java.lang` a été invoqué a la ligne `7` de la classe `Main` du package `ga.enimaloc` avec en précision `Template exception`<br>
<br>
Pour éviter une exception, soit elle est attendue(_checked exception_) donc faut "attrapée" l'erreur via un `try catch` ou vous pouvez faire `x` action si l'exception est invoqué sinon si c'est une exception non attendu(_unchecked exception_) elle provient surement de votre code maintenant cela seras à vous de savoir la corriger par vous-même, hors si l'utilisateur de votre application peut provoquer cette exception vous pouvez —comme toute les classe héritant de la classe [Throwable](https://docs.oracle.com/javase/8/docs/api/java/lang/Throwable.html)— peut être entourée d'un `try catch` pour faire une autre action lorsqu'elle est "attrapé".
## Quelques exceptions :
### NullPointerException :
Une [NullPointerException](https://docs.oracle.com/javase/8/docs/api/java/lang/NullPointerException.html) (ou sous forme réduite NPE) est une exception héritant de la classe [RuntimeException](https://docs.oracle.com/javase/8/docs/api/java/lang/RuntimeException.html), c'est donc une _checked exception_.<br>
<br>
Elle est invoquée quand le programme essaye d'accéder a une valeur `null`, cela inclut :
- L'invocation de la méthode d'instance d'un objet `null`.
- La récupération/modification d'une variable d'un objet `null`.
- La récupération de la taille d'un tableau définit à `null`.
- La récupération/modification d'un element dans un tableau définit à `null`.
- Invoquer une exception qui est `null`.

### IndexOutOfBoundException :
Une [IndexOutOfBoundException](https://docs.oracle.com/javase/8/docs/api/java/lang/IndexOutOfBoundException.html) (ou sous forme réduite IOOB) est une exception héritant de la classe [RuntimeException](https://docs.oracle.com/javase/8/docs/api/java/lang/RuntimeException.html), c'est donc une _checked exception_.<br>
<br>
Elle est invoquée quand le programme essaye d'accéder a un element avec un index qui est supérieur a la limite de l'objet.

# Quelques erreurs
### StackOverflowError :
Une [StackOverflowError](https://docs.oracle.com/javase/8/docs/api/java/lang/StackOverflowError.html) est une erreur héritant de la classe [Error](https://docs.oracle.com/javase/8/docs/api/java/lang/Error.html), c'est donc une erreur grave.<br>
<br>
Elle est invoquée quand le programme invoque dans une méthode cette même méthode ce qui causerait une boucle infinie.

### NoClassDefFoundError :
Une [NoClassDefFoundError](https://docs.oracle.com/javase/8/docs/api/java/lang/NoClassDefFoundError.html) est une erreur héritant de la classe [Error](https://docs.oracle.com/javase/8/docs/api/java/lang/Error.html), c'est donc une erreur grave.<br>
<br>
Elle est invoquée quand le programme essaye de chargé une classe inexistante.
