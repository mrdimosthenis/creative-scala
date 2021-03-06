## Αλγεβρικοί Τύποι Δεδομένων

```tut:invisible
import doodle.core._
import doodle.core.Image._
import doodle.syntax._
import doodle.jvm.Java2DFrame._
import doodle.backend.StandardInterpreter._
```

Στην Creative Scala έχουμε χρησιμοποιήσει πολλές φορές αλγεβρικούς τύπους δεδομένων
αλλά δεν τους έχουμε περιγράψει ποτέ επίσημα.
Σ' αυτό το σημείο όμως είναι χρήσιμη λίγη αυστηρότητα.

Ένας αλγεβρικός τύπος, χτίζεται από δύο συστατικά:
- τα *λογικά ή* και
- τα *λογικά και*.

Ο τύπος δεδομένων `List` είναι ένα πολύ καλό παράδειγμα αλγεβρικού τύπου, αφού χρησιμοποιεί και τα δύο παραπάνω στοιχεία.
Μία λίστα είναι `Nil` *ή* είναι ένα ζεύγος (λογικό ή). Ένα ζεύγος αποτελείται από μία κεφαλή *και* μία ουρά (λογικό και).
Ένα σημείο `Point` είναι ένα ακόμη παράδειγμα. Είναι είτε καρτεσιανό είτε πολικό.
Ένα καρτεσιανό σημείο έχει μία συντεταγμένη x και μία y, ενώ ένα πολικό έχει μία ακτίνα και μία γωνία.
Σημειώστε ότι δεν είναι απαραίτητη η χρήση και των δύο μορφών ώστε ο τύπος δεδομένων να είναι αλγεβρικός.

Αφού είμαστε συναρτησιακοί προγραμματιστές, διαθέτουμε όπως ήταν αναμενόμενο μερικές πιο επίστημονικές λέξεις για τους τύπους του λογικού "ή" και του λογικού "και".

Μπορείτε να τους δείτε παρακάτω:
- έναν *τύπο αθροίσματος* για το λογικό "ή"
- έναν *τύπο γινομένου* για το λογικό "και".

Η έννοια του αλγεβρικού τύπου δεδομένων δεν είναι πολύ συγκεκριμένη στην Scala.
Ας εξασκηθούμε λίγο.

#### Ασκήσεις {-}

##### Στοιχεία Μονοπατιών {-}

Ο τύπος `PathElement` χρησιμοποιείται για την κατασκευή μονοπατιών και είναι ένας απλός αλγεβρικός τύπος δεδομένων.
Έχουμε ήδη χρησιμοποιήσει τον `PathElement` αρκετά.
Πώς πιστεύετε ότι ορίζεται ο `PathElement` χρησιμοποιώντας τους τύπους του αθροίσματος και του γινομένου;

<div class="solution">
Ο `PathElement` είναι από μόνος του τύπος αθροίσματος:
- μία `MoveTo`, ή
- μία `LineTo` ή
- μία `CurveTo`.

Μία `MoveTo` είναι τύπος γινομένου που κρατάει αποθηκευμένο ένα σημείο (εκεί που θα μετακινηθεί).

Μία `LineTo` είναι τύπος γινομένου που κρατάει αποθηκευμένο ένα σημείο (το τελευταίο σημείο της γραμμής).

Μία `CurveTo` είναι τύπος γινομένου που κρατάει αποθηκευμένα τρία σημεία: δύο σημεία ελέγχου και το τελευταίο σημείο της γραμμής.
</div>

##### Εντελώς Turtles {-}

Ο τύπος `Instruction` που χρησιμοποιήσαμε για τον έλεγχο του turtle είναι επίσης ένας αλγεβρικός τύπος δεδομένων.
Πώς πιστεύετε ότι ορίζεται ο `Instruction`;

<div class="solution">
Ένας τύπος `Instruction` είναι:
- μία `Forward`, ή
- μία `Turn`, ή
- μία `Branch`, ή
- μία `NoOp`

Άρα ο `Instruction` είναι τύπος αθροίσματος. Οι `Forward`, `Turn` και `Branch` έχουν όλες τύπο γινομένου.

Η `Forward` έχει αποθηκευμένη μία απόσταση, τύπου `Double`.

Η `Turn` έχει αποθηκευμένη μία γωνία, τύπου `Angle`.

Η `Branch` έχει αποθηκευμένη μία `List[Instruction]`---άρα ο τύπος `Instruction` ορίζεται σε σχέση με τον εαυτό του, ακριβώς όπως κάνει και μία λίστα.

Η `NoOp` δεν έχει τίποτα αποθηκευμένο.
</div>


### Ορίζοντας Αλγεβρικούς Τύπους Δεδομένων

Τώρα που καταλάβαμε πώς μπορούμε να μοντελοποιήσουμε δεδομένα με αλγεβρικούς τύπους δεδομένων, ας δούμε και πώς μπορούμε να ορίσουμε τους δικούς μας.

Η μορφή είναι η παρακάτω:

- Αν ο `A` είναι `B` ή `C` τότε γράψτε το παρακάτω

```tut:book
sealed abstract class A extends Product with Serializable
final case class B() extends A
final case class C() extends A
```

Παραπάνω υπάρχουν πολλοί όροι που δεν έχουμε δει αλλά μπορούμε να τους αγνοήσουμε και να αποδεχτούμε ότι πρέπει να τους γράφουμε μαζί με τον υπόλοιπο κώδικα. Όμως αν ενδιαφέρεστε για το τι σημαίνουν (και πολύ πιθανόν να έχετε προηγούμενη εμπειρία με τον αντικειμενοστραφή προγραμματισμό), τότε εξερευνήστε τους.

Για να ορίσουμε τον τύπο `PathElement` θα μπορούσαμε να ξεκινήσουμε με το παρακάτω

```tut:book
sealed abstract class PathElement extends Product with Serializable
final case class MoveTo() extends PathElement
final case class LineTo() extends PathElement
final case class CurveTo() extends PathElement
```

Το άλλο μισό της μορφής είναι το ακόλουθο

- Αν ο `A` έχει έναν `B` και έναν `C`, τότε γράψτε

```scala
final case class A(b: B, c: C)
```

<div class="info-warning">
Περιγράψτε τις παραμέτρους του constructor εδώ.
</div>

Επιστρέφοντας στις `PathElement`, `MoveTo` και `LineTo`, όλες τους έχουν ένα σημείο (τον προορισμό) και η `CurveTo` έχει ένα σημείο προορισμού και δύο σημεία ελέγχου. Οπότε μπορούμε να γράψουμε το παρακάτω.

```scala
sealed abstract class PathElement extends Product with Serializable
final case class MoveTo(to: Point) extends PathElement
final case class LineTo(to: Point) extends PathElement
final case class CurveTo(cp1: Point, cp2: Point, to: Point) extends PathElement
```

Αυτός είναι ο τρόπος ορισμού του `PathElement` στο Doodle.

#### Άσκηση {-}

Ορίστε τον δικό σας αλγεβρικό τύπο δεδομένων για αναπαράσταση του `Instruction`.

<div class="solution">
Μπορούμε να μετατρέψουμε απευθείας την περιγραφή σε κώδικα, χρησιμοποιώντας τα παρακάτω.

```tut:book
sealed abstract class Instruction extends Product with Serializable
final case class Forward(distance: Double) extends Instruction
final case class Turn(angle: Angle) extends Instruction
final case class Branch(instructions: List[Instruction]) extends Instruction
final case class NoOp() extends Instruction
```
</div>
