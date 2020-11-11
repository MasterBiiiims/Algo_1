# Algo_1

## Calcul de valeurs
### max
\begin{algo}{Max}{T,n}
\IN{$T$ tableau de $n$ entré }
\OUT{$max$ la plus grande valeur de T}
\SET{max}{max=T[0]}
\DOFORI{k}{1}{n-1} % on commence à 1 et pas 0 car le max = T[0] au début
\IF{T[k]>max}
\SET{max}{max=T[k]}
\FI
\OD
\RETURN{max}
\end{algo}
### sum
\begin{algo}{Sum}{T,n}
\IN{$T$ tableau de $n$ entré }
\OUT{$sum$ la sommes des valeurs de T}
\SET{sum}{sum=0}
\DOFORI{k}{0}{n-1} % on commence à 1 et pas 0 car le max = T[0] au début
\SET{sum}{sum+T[k]}
\OD
\RETURN{sum}
\end{algo}
### mean
\begin{algo}{Mean}{T,n}
\IN{$T$ tableau de $n$ entré }
\OUT{$mean$ la moyenne des éléments T}
\SET{sum}{\CALL{Sum}{T,n}}
\IF{n>0}
\RETURN{sum/n}
\ELSE
\RETURN{0}
\FI
\end{algo}
### var
\begin{algo}{Var}{T,n}
\IN{$T$ tableau de $n$ entré, n>0 }
\OUT{$var$ variance de T}
\SET{som}{0}
\SET{mean}{\CALL{Mean}{T,n}}
\DOFORI{k}{0}{n-1}
\SET{som}{(som+T[k]-mean)^2} % attention le carré augmente la compléxité !
\OD
\RETURN{som/n}
\end{algo}

### écart type
\begin{algo}{Ecartype}{T,n}
\IN{$T$ tableau de $n$ entré, n > 0 }
\OUT{$ecart$ ecart type de T}
\SET{var}{\CALL{Var}{T,n}}
\RETURN{\sqrt(var)}
\end{algo}


## Tri tableau
### tri par bulles
\begin{algo}{echange}{liste L}
\IN{$l$ une liste}
\OUT{$tete$ tete de la liste après échange}
\AUX{$tete$ une liste tete}
\SET{tete}{L}{suivant} % 1 ere etape
\SET{L}{suivant}{tete}{suivant} %2 eme etape
\SET{tete}{suivant}{L}%3eme etape
\RETURN{tete}
### tri par max
\begin{algo}{TriTableauParMax}{t,n}
\IN{$t$ tableau contenant n entiers, n>0}
\OUT{$t$ tableau trié}

\SET{pos_droite}{n-1}
\DOWHILE{pos_droite>0}

\SET{m}{\CALL{MaxTableauIndice}{t,pos_droite+1}}
\CALL{Echanger}{t,m,pos_droite}
\SET{pos_droite}{pos_droite-1}

\FI
\OD

\RETURN{$t$}

\end{algo}


### tri par comptage
\begin{algo}{TriTableauParComptage}{t,n}
\IN{$t$ tableau contenant n entiers, n>0}
\OUT{$ttri$ tableau trié}

\DOFORI{k}{0}{n-1}

\SET{c}{0}
\DOFORI{j}{0}{k-1}
\IF{t[j]<=t[k]}
\SET{c}{c+1}
\FI
\OD

\COM{La séparation avant et après l'indice k permet de bien gérer}
\COM{les doublons d'une même valeur dans le tableau. Si le doublon a déjà }
\COM{été croisé et mis dans ttri, il sera à avec k et considéré dans le plus}
\COM{petit ou égal. Sinon il sera dans la deuxième boucle et non compté dans le plus}
\COM{petit strict.}

\DOFORI{j}{k+1}{n-1}
\IF{t[j]<t[k]}
\SET{c}{c+1}
\FI
\OD

\SET{ttri[c]}{t[k]}
\OD

\RETURN{ttri}

\end{algo}

## séquences
### taux gc
\begin{algo}{taux gc}{seq,n}
\IN{séquence ADN $seq$ de longueur $n$}
\OUT{taux GC $gc$}
\SET{compteur}{0}
\DOFORI{k}{0}{n-1}
\IF{seq[k]=='G' or seq[k]=='C'}
\SET{compteur}{compteur++}
\FI
\OD
\SET{gc}{compteur/n}
\RETURN{gc}

\end{algo}
### reverse
\begin{algo}{reverse}{seq,n}
\IN{séquence ADN $seq$ de longueur $n$}
\OUT{renverse $reverse$}
\AUX{$reverse$ chaine de caractère de longueur $n$}
\SET{reverse}{t[n]}
\DOFORI{k}{0}{n-1}
\SET{reverse}{reverse[n-1-k]==seq[k]}
\RETURN{reverse}
\OD
\end{algo}
### complement 
\begin{algo}{seqcomplem}{seq,n}
\IN{séquence ADN $seq$ de longueur $n$}
\OUT{compl $compl$}
\AUX{$compl$ chaine de caractère de longueur $n$}
\SET{compl}{0}
\DOFORI{k}{0}{n-1}
\SET{compl[k]}{basecompl(seq[k])}
\RETURN{compl}
\end{algo}
### nettoyage
\begin{algo}{nettoyage}{seq,n}
\IN{$seq$ une chaine de longueur $n$ fasta}
\OUT{$seq$ contient que la chaine de la séquence}
\AUX{$lecture$ et $ecriture$ 2 indices indiquant le caratere lu et sa position de  recopie éventuelle si c'est une base}
\SET{ecriture}{0}
\SET{lecture}{0}
\DOWHILE{seq[lecture]!= '\backslash n'}
\SET{lecture}{lecture+1}
\OD
\DOWHILE{lecture<n}
\IF{estBase(seq[lecture])}
\SET{seq[ecriture]}{seq[lecture]}
\SET{ecriture}{ecriture+1}
\FI
\SET{lecture}{lecture+1}
\OD
\SET{seq[ecriture]}{'\backslash 0'}
\end{algo}
