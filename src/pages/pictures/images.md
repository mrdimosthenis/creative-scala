## Εικόνες

```tut:invisible
import doodle.core._
import doodle.core.Image._
import doodle.syntax._
import doodle.jvm.Java2DFrame._
import doodle.backend.StandardInterpreter._
```

Ας ξεκινήσουμε με μερικά απλά σχήματα, προγραμματίζοντας στην κονσόλα όπως και πριν.

```tut:book
Image.circle(10)
```

Τι συμβαίνει εδώ; Το `Image` είναι ένα αντικείμενο και το `circle` μία μέθοδος αυτού του αντικειμένου. Περνάμε μία παράμετρο στο `circle`, την `10`, η οποία αντιστοιχεί στην ακτίνα του κύκλου που κατασκευάζουμε. Παρατηρήστε τον τύπο του αποτελέσματος ---είναι `Image`.

Μπορούμε επίσης απλώς να γράψουμε `circle(10)`, αφού εκτελώντας την κονσόλα μέσα στο Doodle είναι σαν να δίνεται αυτόματα η ικανότητα σε αυτή την μέθοδο αλλά και σε άλλες, να κατασκευάζουν εικόνες.

```tut:book
circle(10)
```

Σχεδιάζουμε τον κύκλο, δηλαδή τον εμφανίζουμε στην οθόνη, καλώντας την μέθοδο `draw`.

```scala
circle(10).draw
```

Μετά την εκτέλεση της παραπάνω εντολής θα πρέπει να εμφανιστεί ένα παράθυρο όπως φαίνεται στην εικόνα [@fig:pictures:circle].

![Ένας κύκλος](src/pages/pictures/circle.pdf+svg){#fig:pictures:circle}

Το Doodle υποστηρίζει πολλές "βασικές" εικόνες: κύκλους, ορθογώνια και τρίγωνα. Ας προσπαθήσουμε να ζωγραφίσουμε ένα ορθογώνιο.

```scala
rectangle(100, 50).draw
```

Το αποτέλεσμα φαίνεται στην εικόνα [@fig:pictures:rectangle].

![Ένα ορθογώνιο](src/pages/pictures/rectangle.pdf+svg){#fig:pictures:rectangle}

Τέλος, ας προσπαθήσουμε να δημιουργήσουμε το τρίγωνο που φαίνεται στην εικόνα [@fig:pictures:triangle].


```scala
triangle(60, 40).draw
```

![Ένα τρίγωνο](src/pages/pictures/triangle.pdf+svg){#fig:pictures:triangle}

### Ασκήσεις {-}

#### Κάνοντας Κύκλους {-}

Δημιουργήστε κύκλους με πλάτος 1, 10, και 100. Σχεδιάστε τους!

<div class="solution">
Σε αυτή την άσκηση ελέγχουμε αν η εγκατάσταση του Doodle δουλεύει σωστά και εξοικειωνόμαστε με την βιβλιοθήκη. Ένα από τα σημαντικά στοιχεία του Doodle είναι ότι διαχωρίζουμε τον *ορισμό μίας εικόνας* από τον *σχεδιασμό της*. Θα μιλήσουμε περισσότερο γι' αυτό αργότερα στο βιβλίο.

Μπορούμε να δημιουργήσουμε τους κύκλους με τον παρακάτω κώδικα.

```tut:silent:book
circle(1)
circle(10)
circle(100)
```

Μπορούμε να σχεδιάσουμε τους κύκλους αυτούς καλώντας την μέθοδο `draw` για κάθε έναν ξεχωριστά.

```scala
circle(1).draw
circle(10).draw
circle(100).draw
```
</div>


#### Τύποι Σχημάτων {-}

Ποιός είναι ο τύπος ενός κύκλου; Ενός ορθογωνίου; Ενός τριγώνου;

<div class="solution">
Όλα έχουν τον τύπο `Image` όπως μπορούμε να διαπιστώσουμε και από την κονσόλα.

```scala
:type circle(10)
// doodle.core.Image
:type rectangle(10, 10)
// doodle.core.Image
:type triangle(10, 10)
// doodle.core.Image
```
</div>

#### Τύποι Σχεδίων {-}

Ποιός είναι ο τύπος του *σχεδίου* μίας εικόνας; Τι σημαίνει αυτό;

<div class="solution">
Για άλλη μία φορά, μπορούμε να κάνουμε αυτή την ερώτηση στην κονσόλα.

```scala
:type circle(10).draw
// Unit
```

Βλέπουμε ότι ο τύπος του σχεδίου μίας εικόνας είναι ο `Unit`. Ο `Unit` είναι ένας τύπος που χρησιμοποιείται για εκφράσεις που δεν επιστρέφουν κάποια ενδιαφέρουσα τιμή. Αυτό συμβαίνει και στην περίπτωση της `draw`. Την καλούμε επειδή θέλουμε να εμφανιστεί κάτι στην οθόνη και όχι επειδή έχουμε μία χρήση για την τιμή που επιστρέφει. Υπάρχει μόνο μία τιμή με τύπο `Unit`. Αυτή η τιμή ονομάζεται επίσης unit και αν γραφεί ως κυριολεκτική έκφραση τότε θα είναι η `()`

Θα παρατηρήσετε ότι η κονσόλα δεν εκτυπώνει την unit από μόνη της.

```scala
()
```

Μπορούμε να ζητήσουμε τον τύπο από την κονσόλα ώστε να δείξουμε ότι όντως υπάρχει η unit.

```scala
:type ()
// Unit
```
</div>
