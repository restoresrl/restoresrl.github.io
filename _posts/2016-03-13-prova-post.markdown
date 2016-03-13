---
published: true
title: Naming convention
layout: post
tags: [PowerBuilder]
categories: [PowerBuilder]
---
Regole generali
------

- Evitare il `CamelCase`, anche se PB lo usa nella sua documentazione, ma essendo case insensitive l'autoscript poi ti fa impazzire. Preferire `snake_case`
- Evitare di mettere i vari prefissi alle variabili di istanza se sono pubbliche
- Usare solo codice scritto in minuscolo, anche per i metodi nativi senza underscore

Regole naming delle variabili
------

### Variabili di istanza pubbliche
Ridurne l'uso al minimo indispensabile, ma se proprio ci devono essere usare minuscole con snake_case e non usare prefissi.  
Dare semplicemente un nome sensato che non abbia bisogno di prefissi come `is_` e `il_` per far capire che è una stringa o un long.
Ad esempio `customer.name` è più che evidente che sia una stringa!

	pubblic:
	long id
	string full_name
	
### Variabili di istanza protected e private
Pe le variabili di istanza protette e private usare le solite regole di naming di Powerbuilder. Usare snake_case

	protected:
	string internal_name

	private:
	string is_internal_name
	long il_internal_id

### Variabili locali
Usare snake_case e prefissi standard PowerBuilder

	string ls_name
	long ll_count, ll_index

	for ll_index = 1 to ll_count
		...
	next



#### Variable naming conventions
The prefix for variables typically combines a letter that represents the scope of the variable and a letter or letters that represent its datatype. Table 5-3 lists the prefixes used to indicate a variable’s scope. Table 5-4 lists the prefixes for standard datatypes, such as integer or string.

The variable might also be a PowerBuilder object or control. Table 5-5 lists prefixes for some common PowerBuilder system objects. For controls, you can use the standard prefix that PowerBuilder uses when you add a control to a window or visual user object. To see these prefixes, open the Window painter, select Design>Options, and look at the Prefixes 1 and Prefixes 2 pages.

#### Table 5-3: Prefixes that indicate the scope of variables

Prefix | Description
---- | ----
**a** 	| Argument to an event or function
**g** 	| Global variable
**i** 	| Instance variable
**l** 	| Local variable
**s** 	| Shared variable

#### Table 5-4: Prefixes for standard datatypes

Prefix | Description
---- | ----
**a** 		| Any
**blb**		| Blob
**b** 		| Boolean
**ch** 		| Character
**d** 		| Date
**dtm** 	| DateTime
**dc** 		| Decimal
**db** 		| Double
**e** 		| Enumerated
**i** 		| Integer
**l** 		| Long
**r** 		| Real
**s** 		| String
**tm** 		| Time
**ui** 		| UnsignedInteger
**ul** 		| UnsignedLong

#### Table 5-5: Prefixes for selected PowerBuilder system objects

Prefix | Description
---- | ----
**ds**		| DataStore
**dw** 		| DataWindow
**dwc**		| DataWindowChild
**dwo**		| DWobject
**n** 		| NonVisualObject
**tr**		| Transaction
**env**		| Environment
**err**		| Error
**gr**		| Graph
**inet**	| Inet
**ir**		| InternetResult
**lvi**		| ListViewItem
**mfd**		| MailFileDescription
**mm**		| MailMessage
**mr**		| MailRecipient
**ms**		| MailSession
**msg**		| Message
**tvi**		| TreeViewItem


Regole di naming funzioni
-------

Evitare prefissi `of_`, `f_`, ecc per le funzioni pubbliche e protected.
Usare un `_` per quelle private.
Usare identificatori snake_case e non CamelCase

	customer.get_name()
	item.get_code()

Usare `f_` solo per le funzioni globali

Regole di naming eventi
-------

Precedere l'evento con `e_` in snake_case

	triggerevent("e_new")
	customer.event post e_new(id)

## Naming oggetti

### Table 5-2: Common prefixes for objects

Prefix | Description
---- | ----
**w_**				| Window
**m_**				| Menu
**d_**				| DataWindow
**pipe_**			| Data Pipeline
**q_**				| Query
**n_ or n_standardobject_**	| Standard class user object, where standardobject represents the type of object; for example, n_trans
**n_ or n_cst**		| Custom class user object
**u_ or u_standardobject_**	| Standard visual user object, where standardobject represents the type of object; for example, u_cb
**u_**				| Custom visual user object
**f_**				| Global function
**of_**				| Object-level function
**s_**				| Global structure
**str_**			| Object-level structure
**ue_**				| User event