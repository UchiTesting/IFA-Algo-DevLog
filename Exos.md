---
marp: false
_class: invert
---

Algo II : Cycle developpement logiciel IFA - Metz
=================================================

> La syntaxe admise en cours d'algo est susceptible de différer avec celle présentée ici.\
> Parmi les changements possibles:\
> Les fonctions `Fonction nomFonction():sortie` au lieu de `nomFonction:Fonction():sortie`

## 17/12/2019

---
## Afficher les nombres de 0 à 100

```
Debut Nb100
	Pour i allant de 0 à 100 par pas de 1 Faire
		afficherEntier(i)
	FinPour
Fin
```

---
## Même chose en demandant la valeur max à l'utilisateur

```
Debut Nb100Utilisateur
	var n: entier
Debut
	n = saisirEntier()
	Pour i allant de 0 à 100 par pas de 1 Faire
		afficherEntier(i)
	FinPour
Fin
```

---
## Soit un tableau de 100 entiers. Demander à l'utilisateur de remplir le tableau. Ajouter 5 à 10 entrées au choix. En faire la somme du tableau.

```
Debut Exotab
	var n: entier
	var cpt: entier
	var tab: tableau[100]: entier
Debut
	Pour i allant de 0 à 99 par pas de 1 Faire
		tab[i] = saisirEntier()
	FinPour
	
	cpt = 0
	
	Faire
		n = saisirEntier()
		Si n >= 0 && n < 100 Alors
			cpt = cpt + 1
			tab[n] = tab[n] + 5
		FinSi
	TantQue (cpt < 10)
	FinFaire
	// On réutilise la variable n pour le calcul de la somme (pas forcément une bonne pratique)
	n = 0
	Pour i allant de 0 à 99 par pas de 1 Faire
		n = n + tab[i]
	FinPour
	
	afficherEntier(n)
Fin
```

---

## Écrire un algorithme qui affiche un mot illimité. Le caractère '.' termine la saisie.

```
Debut Mot
	var tab: tableau[]: char
	var taille: entier
	var c: char
Debut
	taille = 0
	TantQue (c = saisirChar() != '.') Faire
		Redim(tab, taille + 1)
		tab[taille] = c
		taille = taille + 1
	FinTantQue
	
	Pour i allant de 0 à taille - 1 par pas de 1 Faire
		afficherChar(tab[i])
	FinPour
Fin
```

---
## Demander 2 nombres. Stocker leur division pour chacune des 10 cases d'un tableau.

```
Debut Tab10Entiers
	var tab: tableau[10]: entier
	
	Fonction div2Nb(): entier
		var x: entier
		var y: entier
	Debut
		x = saisirEntier()
		Faire
			y = saisirEntier()
		TantQue (y == 0)
		FinFaire
		
		Retourne x/y
		
	FinFonction
Debut
	tab[0] = div2Nb()
	tab[1] = div2Nb()
	tab[2] = div2Nb()
	tab[3] = div2Nb()
	tab[4] = div2Nb()
	tab[5] = div2Nb()
	tab[6] = div2Nb()
	tab[7] = div2Nb()
	tab[8] = div2Nb()
	tab[9] = div2Nb()
Fin
```

---
## Écrire un algorithme qui demande n. Afficher ensuite la somme des n premiers entiers.
- U(0) = 0
- U(n) = n + U(n-1) pour n > 0


```
Debut SommeDesN
	Fonction sommeN(n: entier): entier
		Si n == 0 Alors
			Retourne 0
		Sinon
			Retourne n + sommeN(n-1)
		FinSi
	FinFonction
	var unN: entier	
Debut
	unN = saisirEntier()
	afficherEntier(sommeN(unN))
Fin
```

---
## Écrire la factorielle n!
- n > 1
- 0! → 1
     - U(n) = n * U(n-1)
     - Factorielle de 0 renvoi 1
- n * (n-1) 

```
Debut Factorielle
	Fonction factorielle(n:entier): entier
		Si n <= 1 Alors
			Retourne 1
		Sinon
			Retourne n * factorielle(n-1)
		FinSi
	FinFonction
	var n: entier
Debut
	n = saisirEntier()
	afficherEntier(factorielle(n))
Fin
```

---
## Écrire un algorithme qui rempli de façon récursive un tableau de 10 entiers

```
Debut
	Fonction remplirTabRecursif(ref tab: tableau[]: entier, n: entier): NULL
		var x: entier
		var y: entier
	Debut
		x = saisirEntier()
		Faire
			y = saisirEntier()
		TantQue (y == 0)
		FinFaire
		
		tab[n] = x/y
		
		Si n > 0 Alors
			remplirTabRecursif(tab, n-1)
		FinSi
	FinFonction
	var tab: tableau[10]: entier
Debut
	remplirTabRecursif(tab, 9)
	Pour i allant de 0 à 9 par pas de 1 Faire
		afficherEntier(tab[i])
	FinPour
Fin
```
---
## 18/12/2019
---
## Soit un tableau d'entiers. L'utilisateur le rempli. Trouver le minimum par récursivité.

### Ma version
```
Debut Min Recur
	Fonction remplirTabRecursif(ref tab: tableau[]: entier, n:entier): NULL
		var x: entier
	Debut
		x = saisirEntier()
		tab[n] = x
		Si n > 0 Alors
			remplirTabRecursif(tab, n-1)
		FinSi
	FinFonction
	
	Fonction minRecursif(ref tat: tableau[]: entier, n: entier): entier
		Si n = 0 Alors
			Retourne tab[n]
		Sinon Si ( minRecursif(tab, n-1) < tab[n]) Alors
			Retourne tab[n-1]
		Sinon
			Retourne tab[n]
		FinSi
	FinFonction
	
	var tab: tableau[10]: entier
Debut
	remplirTabRecursif(tab, 9)
	afficherEntier(minRecursif(tab, 9))
Fin
```

### Correction 1
```
Debut Exo
	Fonction remplirTab(ref tab: tableau[] d'entiers, taille: entier, ref min: entier): NULL
	Debut
		tab[taille-1] = saisirEntier()
		Si tab[taille-1] < min Alors
			min = tab[taille-1]
		FinSi
		Si taille > 1 Alors
			remplirTab(tab, taille-1, min)
		FinSi
	FinFonction
	
	var min: entier
	var tab:tableau[10] d'entiers
Debut
	min = 10^9
	remplirTab(tab, 10, min)
	afficherEntier(min)
Fin
```

### Correction 2
```
Debut Exo
	Fonction rechercheMini(ref tab: tableau[] d'entiers, taille: entier, idx: entier, ref min: entier): NULL
	Debut
		Si (idx < taille) Alors
			Si tab[idx] < min Alors
				min = tab[idx]
			FinSi
			rechercheMini(tab, taille, idx+1, min)
		FinSi
	FinFonction
	
	var min: entier
	var tab:tableau[10] d'entiers
Debut
	Pour i allant de 0 à 9 par pas de 1 Faire
		tab[i] = saisirEntier()
	FinPour
	
	min = tab[0]
	rechercheMini(tab,10,0,min)
	afficherEntier(min)
Fin
```

---
## Écrire un programme qui gère un tableau de 10^999 éléments. Écrire une fonction qui remplit le tableau

### Ma version
```
Debut grotablo
	var tab: tableau [10^999]
	var taille: entier
	Fonction remplirTabRecursif(ref tab: tableau[]: entier, idx: entier, taille: entier): NULL
		// Degressif
		Si idx >= 0 Alors
			tab[idx] = saisirEntier()
		FinSi
		Si idx > 0 Alors
			remplirTabRecursif(tab, idx - 1, taille)
		FinSi
		
		// Progressif
		Si idx <= taille-1 Alors
			tab[idx] = saisirEntier()
		FinSi
		Si idx < taille-1 Alors
			remplirTabRecursif(tab, idx + 1, taille)
		FinSi
	FinFonction
Debut
	// Dégressif
	remplirTabRecursif(tab, 10^999, 10^999)
	// Progressif
	remplirTabRecursif(tab, 0, 10^999)
Fin
```

### Correction 1
```
Debut Achètes des RAM
	Fonction recu(ref tab: tableau[]: entier, ref taille: entier): NULL
		Si taille < 10^999 // Capacité mémoire max
			taille = taille + 1
			redim(tab, taille)
			tab[taille-1] = saisirEntier()
			recu(tab, taille)
		FinSi
	FinFonction
	var taille: entier
	var tab: tableau[]: entier
Debut
	taille = 0
	recu(tab, taille)
Fin
```

### Correction 2 de Vincent
```
Debut Recu
	Fonction recu(ref tab: tableau[]: entier, ref index: entier): NULL
		Si index < 10^999 Alors
			tab[index] = saisirEntier()
			index = index + 1
			recu(tab, index)
		FinSi
	FinFonction

	var tab: tableau[10^999]: entier
	var index: entier
Debut
	index = 0
	recu(tab, index)
Fin
```

---
## Ecrire un programme qui rempli un tableau de taille fixe. Demander à l'utilisateur une lettre à rechercher dans le tableau. Écrire une fonction qui retourne l'index de la première occurence de la lettre ou -1

### Ma version
```
Debut Recherche Lettre
	var tab: tableau[]: char
	Fonction remplirTabRecursif(ref tab: tableau[]: char, ref index: entier) NULL
		Si index < 10^999 Alors
			tab[index] = saisirChar()
			index = index + 1
			remplirTabRecursif(tab, index)
		FinSi
	FinFonction
	
	Fonction trouveIndexLettre(ref tab: tableau[]: char, lettre, char, idx: entier, taille: entier): entier
		Si (idx >= 0 et idx < taille) Alors
			Si tab[idx] == lettre Alors
				Retourne tab[idx]
			Sinon Si (idx <= taille-2) Alors
				Retourne trouveIndexLettre(tab, lettre, idx+1, taille)
			Sinon
				Retourne -1
			FinSi
		FinSi
	FinFonction
Debut
	remplirTabRecursif(tab, 9)
	afficherEntier(trouveIndexLettre(tab, lettre, 0, 10))
Fin
```

### Correction
```
Debut Recherche Lettre
	var lettre: char
	var tab: tableau[10]: char
	
	Fonction recherche(lettre: char, tab: tableau[]: char): entier
		var index: entier
	Debut
		index = 0
		TantQue (index < 10 && tab[index] != lettre) Faire
			index = index + 1
		FinTantQue
		
		Si index == 10 Alors
			Retourne -1
		Sinon
			Retourne index
		FinSi
	FinFonction
Debut
	Pour i allant de 0 à 9 par pas de 1
		tab[i] = saisirChar()
	FinPour
	
	lettre = saisirChar()
	afficherEntier(recherche(lettre, tab))
Fin
```

---
## 19/12/2019
---
## Écrire une calculatrice qui affiche un menu.
- Addition
- Soustraction
- Division
- Multiplication
- Afficher le résultat
### Ma version
```
Debut Calculatrice
	Fonction add(a: reel, b: reel): reel
		Retourne a + b
	FinFonction
	Fonction sub(a: reel, b: reel): reel
		Retourne a - b
	FinFonction
	Fonction mult(a: reel, b: reel): reel
		Retourne a * b
	FinFonction
	Fonction div(a: reel, b: reel): reel
		Si b == 0 Alors
			Faire
				b = saisirReel()
			TantQue (b == 0)
			FinFaire
		FinSi
		Retourne a / b
	FinFonction
	
	var continue: Booleen
	var oper: char
	var resultat: entier
	var operande: entier
Debut
	Faire
		resultat = saisirReel()
		oper = saisirChar()
		
		Si oper == 'q' Alors
			continue = FAUX			
		Sinon
			continue = VRAI
			
			Si oper != 'p' Alors
				operande = saisirReel()
			FinSi
		FinSi
		
		SelonQue oper:
			Cas 'a': // Addition
				resultat = add(resultat, operande)
			FinCas
			Cas 'm': // Multiplication
				resultat = mult(resultat, operande)
			FinCas
			Cas 's': // Soustraction
				resultat = sub(resultat, operande)
			FinCas
			Cas 'd': // Division
				resultat = div(resultat, operande)
			FinCas
			Cas 'p': // print
				afficherReel(resultat)
			FinCas
			autrement: // inclus oper = 'q'
				continue = FAUX
			FinCas
		FinSelonQue
	TantQue (continue)
	FinFaire
Fin
```

### Correction
```
Debut Calculatrice
	Fonction addition(a: reel, b: reel): reel
		var resultat: reel
	Debut
		resultat = a + b
		Retourne resultat
	FinFonction
	
	Fonction soustraction(a: reel, b: reel): reel
		var resultat: reel
	Debut
		resultat = a - b
		Retourne resultat
	FinFonction
	
	Fonction multiplication(a: reel, b: reel): reel
		var resultat: reel
	Debut
		resultat = a * b
		Retourne resultat
	FinFonction
	
	Fonction division(a: reel, b: reel): reel
		var resultat: reel
	Debut
		resultat = a / b
		Retourne resultat
	FinFonction
	
	var n1: reel
	var n2: reel
	var operateur: char
Debut
	n1 = saisirReel()
	Faire
		operateur = saisirChar()
		// Note: Perso j'aurais saisie n2 ici pour ne pas le répéter
		SelonQue
			Cas '+'
				n2 = saisirReel()
				n1 = addition(n1,n2)
			FinCas
			// Même principe pour multiplication et soustraction
			Cas '/'
				Faire
					n2 = saisirReel()
				TantQue (n2 == 0)
				FinFaire
				n1 = division(n1, n2)
			FinCas
			Cas '='
				afficherReel(n1)
			FinCas
		FinSelonQue
	TantQue (operateur != 'q')
	FinFaire
Fin
```

## Suite de Fibonacci

- F(0) = 0
- F(1) = 1
- F(n) = F(n-1) + F(n-2)
- n >= 0

### Ma version
```
Debut Fibonacci
	Fonction fibonacciRecursif(n: entier):entier
		Si (n == 0) Alors
			Retourne 0
		Sinon Si (n == 1) Alors
			Retourne 1
		Sinon Si (n > 1) Alors
			Retourne fibonacci(n-1) + fibonacci(n-2)
		Sinon
			Retourne -1
		FinSi
	FinFonction
	var n: entier
Debut
	n = saisirEntier()
	afficherEntier(fibonacci(7))
Fin

Debut Fibonacci Itératif

	Fonction fibonacciIteratif(n: entier):entier
		var tmp: entier
		var vald:entier
		var valf: entier
	Debut
		vald = 0
		valf = 1
		Si n > 1
			Pour i allant de 2 à n par pas de 1 Faire
				tmp = vald + valf
				vald = valf
				valf = tmp
			FinPour
			Retourne tmp
		Sinon Si n == 1 ou n == 0 Alors
			Retourne n
		FinSi
	FinFonction
	var n: entier
Debut
	Faire
		1n = saisirEntier()
	TantQue (n < 0)
	FinFaire
	afficherEntier(fibonacciRecursif(7))
	afficherEntier(fibonacciIteratif(7))
Fin
```