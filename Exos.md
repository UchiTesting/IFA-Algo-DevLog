Algo II : Cycle developpement logiciel IFA - Metz
=================================================

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
## 19/12/2019
