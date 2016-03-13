---
published: true
title: Associazioni PowerBuilder
layout: post
---
# RAF associations
Le associazioni di RAF peremettono di modellare le
relazioni che esistono tra i PDO e gestire in maniera semplice le sottostanti tabelle e campi sul 
database secondo alcune convenzioni.


Le possibili associazioni sono:

- `belongs_to`
- `belongs_to_poly`
- `has_many`
- `has_one`

## Associazione belongs\_to
Questa associazione permette di definire una relazione uno a uno tra due classi
di PDO, in cui le istanze di uno dipendendo dall'istanza di un altro.
Ad esempio un cliente ed i suoi ordini potrebbero essere così modellati:

![](http://i.imgur.com/HbiTJdy.png)

    // order.constructor
    belongs_to(customer)

Grazie a questa definizione avendo un'istanza di `order` si potrà recuparare la
corrispondente istanza di `customer` con

    lu_customer = lu_order.get_related("customer")

Inoltre si potrà settare in una istanza di `order` il corrispondente `customer` 
con il metodo `set_related`

    lu_order.new()
    lu_order.set_related("customer", lu_customer)

Il metodo `belongs_to` inferisce il nome della classe da cui dipende e la relativa
foreign key sulla tabella dal nome dell'associazione passata in argomento.  
Es: per `belongs_to(customer)` la classe da cui dipende dovrà essere `customer` e la chiave sulla
tabella `order.id_order`

### Opzioni di belongs\_to
	belongs_to(as_association_name{, as_class_name{, as_foreign_key}})

Nel caso i nomi di classe o delle colonne utilizzate non fossero deducibili dal
nome dell'associazione, è possibile utilizzare le seguenti opzioni per modificare
i default utilizzati.

- `class_name`
- `foreign_ky`

#### Opzione class\_name
Nel caso il nome del PDO da cui dipendere non sia lo stesso del nome che si
vuol dare all'associazione si può usare l'opzione
`belongs_to(association, class_name)`
Ad esempio se il nome della classe PDO per il customer fosse `user` allora
si potrà scrivere

    belongs_to("customer", "user")
In questo caso RAF presume che la foreign key nella tabella `user` sia sempre
`id_order`

### Opzione foreign\_key
Nel caso invece in cui la foreign key non possa essere inferita dal nome
dell'associazione si può usare la forma
`belongs_to(association, class_name, foreign_key)`

Per esempio se nella tabella `order` la foreign key verso `customer`
fosse `id_user` allora

    belongs_to("customer", "user", "id_user")


## Associazione belongs\_to\_poly
Questa associazione permette di creare una associazione uno ad uno di tipo polimorfico, 
cioè in cui il PDO dipendente può essere associato a PDO di classi diverse, non conosciute a
priori dall'oggetto stesso.
Ad esempio un PDO `image` potrebbe essere associato sia al PDO `user` che a quello `product`.

![](http://i.imgur.com/LsvULUj.png)

Per fare questo la definizione di `image` sarà

    belongs_to_poly("imageable")

Nella tabella `picture` dovranno essere definite due colonne: `id_imageable` che manterrà l'id del PDO associato e `class_imageable` (di tipo `raf_class`) che mantiene la classe del PDO associato.

### Opzioni per belongs\_to\_poly
	belongs_to_poly(as_association_name{, as_class_name})

L'unica opzione per una associazione `belongs_to_poly` è `class_name` che permette di indicare il nome degli attributi polimorfici nel caso questi non possano essere inferiti dal nome dell'associazione.
Ad esempio se nella tabella `picture` le colonne sono `id_reference` e `class_reference` la definizione 
dovrà essere

    belongs_to_poly("imageable", "reference")

## Associazione has\_many
Permette di definire una relazione uno a molti con un altro PDO.  
Questa associazione si trova spesso "dall'altro lato" di una associazione belongs_to ed indica che ogni 
istanza del PDO puà avere zero o più istanze dell'altro PDO collegate.

![](http://i.imgur.com/HbiTJdy.png)

    // customer.constructor
    has_many("orders", "order")

Grazie a questa definizione avendo un'istanza di `customer` si potranno recuparare tutte
le istanze di `order` tarmite una collection

    lu_order_collection = lu_customer.get_related("orders")

Inoltre si potrà creare in una nuova istanza di `order` di un `customer` 
con il metodo `new_related`

    lu_order = customer.new_related("orders")

### Opzioni per has\_many
	has_many(as_association_name, as_belongs_to_class{, as_belongs_to_assoc{, ab_delete_dependent}})
	has_many(as_association_name, as_belongs_to_class{, ab_delete_dependent}})

#### Opzione as\_belongs\_to\_assoc
RAF inferisce il nome dell'associazione opposta `belongs_to` usando il nome della classe in cui è dichiarato `has_many`. Questa associazione `belongs_to` viene usata per inizializzare la collection con la corretta foreign key e per poter creare un nuovo PDO tramite `new_related()`.
Ad esempio se in `customer` viene dichiarato `has_many("orders", "order")` allora RAF suppone che esista una associazione `belongs_to("customer)` nella classe `order`. Se l'associazione `belongs_to` ha un nome diverso, deve essere fornita a RAF tramite il terzo parametro `as_belongs_to_assoc`. Ad esempio se nel `order` l'associazine verso `customer` è `belong_to("user", "customer")` allora la `has_many` deve essere definita così:

    has_many("orders", "order", "user")


#### Opzione ab\_delete\_dependent
Questa opzione indica che RAF deve cancellare tutti gli oggetti dipendenti
quando viene cancellato quello da cui dipendono. Il default è `false`

Quindi se è stato definito

	has_many("orders", "order", true)
	has_many("orders", "order", "user", true)

quando sarà cancellato un customer saranno cancellati automaticamente tutti i
suoi `order` collegati. L'operazione viene eseguita da RAF e non da un eventuale
constraint delete cascade del database. Quindi se sul db c'è un vincolo di non
cancellazione, l'operazione fallirà.

## Associazione has\_one
Questa associazione permette di definire una relazione uno a uno con un altro PDO.  
Questa ssociazione si trova spesso "dall'altro lato" di una associazione belongs\_to ed indica che ogni istanza del PDO può avere zero o una istanze dell'altro PDO collegato.

![](http://i.imgur.com/bxiScG2.png)

    // customer.constructor
    has_one("account")

Grazie a questa definizione avendo un'istanza di `customer` si potrà recuparare l'istanza di 
`account`

    lu_account = lu_customer.get_related("account")

Inoltre si potrà creare in una nuova istanza di `account` di un `customer` 
con il metodo `new_related`

    lu_order = customer.new_related("account")

> Attenzione: il metodo new_related al momento non verifica se esiste già un un'istanza collegata 
> e quindi potrebbe generare altre istanze collegate. 
> Dovrebbe invece fallire se esiste già istanza oppure tornare quella collegata????


### Opzioni per has\_one
	has_one(as_association_name{, as_belongs_to_class{, as_belongs_to_assoc{, ab_delete_dependent}}})
	has_one(as_association_name{, as_belongs_to_class{, ab_delete_dependent}}})
	has_one(as_association_name{, ab_delete_dependent}})

#### Opzione as\_belongs\_to\_class
RAF inferisce il nome della classe associata usando il nome dell'associazione in cui è dichiarato `has_one`.
Se questa è diversa si può indicare esplicitamente con l'opzione as\_belongs\_to\_class

    // customer.constructor
    has_one("account", "balance")

#### Opzione as\_belongs\_to\_assoc
RAF inferisce il nome dell'associazione opposta `belongs_to` usando il nome della classe in cui è dichiarato `has_one`. Questa associazione `belongs_to` viene usata per inizializzare la collection con la corretta foreign key e per poter creare un nuovo PDO tramite `new_related()`.
Ad esempio se in `customer` viene dichiarato `has_one("account", "balance")` allora RAF suppone che esista una associazione `belongs_to("customer)` nella classe `balance`. Se l'associazione `belongs_to` ha un nome diverso, deve essere fornita a RAF tramite il terzo parametro `as_belongs_to_assoc`. Ad esempio se in `balance` l'associazione verso `customer` è `belong_to("user", "customer")` allora la `has_one` deve essere definita così:

    has_one("account", "balance", "user")


#### Opzione ab\_delete\_dependent
Questa opzione indica che RAF deve cancellare tutti gli oggetti dipendenti
quando viene cancellato quello da cui dipendono. Il default è `false`

Quindi se è stato definito

	has_one("account", true)

quando sarà cancellato un customer saranno cancellati automaticamente il suo
`account` collegato. L'operazione viene eseguita da RAF e non da un eventuale
constraint delete cascade del database. Quindi se sul db c'è un vincolo di non
cancellazione, l'operazione fallirà.






## Associazioni child\_of e parent\_of
RAF prevede un particolare tipo di associazione che modella relazioni di tipo
uno a molti padre/figlio. Si tratta di un shortcut per definire da un lato una relazione di nome
`childs` di tipo has\_many con cancellazione automatica e dall'altra una belongs\_to di nome `parent`.  


Le relazioni parent e child vanno definite nei constructor come le altre
associazioni

    // invoice.constructor
    parent_of("invoice_row")
    ...
    //invoice_row.constructor
    child_of("invoice")

Un padre ed i suoi figli possono essere rispettivamente recuparati mediante i
metodi `get_parent()` sul figlio che torna
il PDO padre e `get_childs()` sul padre che torna una collection dei figli.

	// get a collection of childs
	n_raf_collection lu_my_invoice_rows

	lu_invoice.sync(123)
	lu_my_invoice_rows = lu_invoice.get_childs()


    // get the parent of a child
    invoice iu_my_invoice

    iu_my_invoice = lu_my_invoice_rows.get_parent()

Il metodo del padre `new_child()` crea una PDO figlio già agganciato al padre

	lu_invoice.sync(123)
    lu_new_row = lu_invoice.new_child()

Nella tabella child la foreign key viene inferita a partire dal nome della
classe padre con il prefisso `id_`
Nell'esempio precedente quind la tabella per invoice_row dovrà contenere il
campo `id_invoice` in relazione al campo `invoice.id`

### Parent e child quando la foreing key è diversa
Se la foreign key utilizzata nel child non è il default `id_`*classe_del_padre*
allora devono essere specificate nelle opzioni i nomi della fk e della relazione
in modod da parmettere a RAF di ricostruire le relazioni corrette

Es.
Se la foreign key nella tabella `invoice_row` è `id_my_invoice` invece di `id_invoice`

    // Nel padre
    parent_of("invoice_row", "my_invoice")

    // Nel figlio
    child_of("invoice", "id_my_invoice")
