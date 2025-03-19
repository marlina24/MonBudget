# **Budget Model App**  

[![Codacy Badge](https://api.codacy.com/project/badge/Grade/0d5d8c2bd2964861ac67dcf2a5e62f22)](https://www.codacy.com/manual/SharonChoong/budget-model?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=sharonchoong/budget-model&amp;utm_campaign=Badge_Grade)

## **Présentation**  
Budget Model App est une application de bureau simple pour Windows, développée en WPF. Elle permet de suivre le budget mensuel des revenus et dépenses, la valeur nette et les investissements financiers sur tous les comptes bancaires et de courtage. Toutes les données restent stockées localement sur l'ordinateur de l'utilisateur.

### **Pourquoi utiliser Budget Model App ?**
- Plus puissant et évolutif qu’un simple tableau Excel pour gérer ses finances.
- Permet d’analyser tous types de rapports bancaires ou relevés d’investissement, sans limitation.
- Aucun mot de passe bancaire n'est enregistré, garantissant une sécurité optimale.  

Contrairement aux solutions de gestion financière comme **Mint, Quicken et QuickBooks**, cette application ne synchronise pas automatiquement les comptes bancaires. Ainsi, les informations de connexion bancaires ne sont jamais stockées ni partagées.

---

## **Fonctionnalités**
1. **Vue mensuelle** des revenus et dépenses classés par catégories.  
2. **Recatégorisation manuelle** des transactions (ex. une dépense en carburant peut être déplacée de "Transport" vers "Voyage" pour un déplacement exceptionnel).  
3. **Historique** des dépenses, revenus et économies sous forme de graphiques récapitulatifs.  
4. **Suivi de l’évolution de la valeur nette** au fil du temps.  
5. **Analyse des gains et pertes des investissements**, mois par mois ou de manière cumulative.  
6. **Analyse détaillée des investissements**, soit par titre spécifique, soit par classe d’actifs.  
7. **Historique des transactions boursières** (achats/ventes d’actions et de fonds) avec possibilité de comparer le prix d'exécution avec le prix du marché (nécessite un compte **Alpha Vantage**).  

---

## **Démarrage rapide : Tester l'application avec des données d'exemple**
1. Exécutez **Budget Model.exe** dans le dossier `Budget Model\bin\Debug\`.  
2. L'écran principal **Budget Statement** s'affichera avec des données déjà catégorisées.  
3. Utilisez les boutons en haut à droite pour naviguer vers :  
   - **Historical Budget and Net Worth Analysis** (Analyse budgétaire historique et valeur nette)  
   - **Investments** (Investissements)  

Les données d’exemple utilisées se trouvent dans le dossier `\test_data`.  

### **Écran Data & Definitions**
Cet écran permet :  
- **D’importer des relevés bancaires et rapports d’investissement**,  
- **De définir des catégories** pour classer automatiquement les dépenses et revenus en fonction de mots-clés.  

![Data & Definitions screen](/images/Categorizing%20transaction%20items%20in%20accounts.png)

---

## **Personnalisation**
Avant la première utilisation, certaines configurations doivent être définies dans le code :

1. **Déclaration des institutions financières** (`FinancialInstitutions_Sample.cs` dans `Models`)  
   - La méthode `GetFinancialInstitutions` retourne la liste des comptes bancaires et d’investissement analysés par l’application.  
   - Par défaut, la liste d'exemple `BankSample` et `BrokerageSample` est utilisée.  

2. **Définition des titulaires de comptes** (`Holders_Sample.cs` dans `Models`)  
   - La méthode `HolderCollection` doit être modifiée pour indiquer les titulaires des comptes analysés.  
   - Par défaut, les titulaires `Person1` et `Person2` sont utilisés.  

3. **Importation de relevés bancaires** (`ExcelImport_Sample.cs` dans `Helpers`)  
   - Cette classe est responsable de la lecture des fichiers CSV contenant l’historique des transactions bancaires.  
   - Elle doit être adaptée pour extraire les informations en fonction du format des relevés utilisés par la banque.  

### **Particularités des données**
- **Salaire brut** : les relevés bancaires n’indiquent généralement que le salaire net. Il peut être ajouté manuellement dans **Data & Definitions**, et sera reporté automatiquement chaque mois.  
- **Solde initial des comptes** : l’application calcule le solde bancaire en additionnant toutes les transactions disponibles. Si l’historique est incomplet, il faut indiquer le solde initial avant la première transaction importée.  

---

## **Autres fichiers à configurer**
1. **Fichiers de configuration**  
   - `Connections.config` : contient la chaîne de connexion vers la base de données SQLite (`BudgetData_Sample.db`).  
   - `CustomAppSettings.config` : contient les **clés API** nécessaires pour récupérer les cours des actions et obligations via **Alpha Vantage**.  

2. **Base de données (SQLite)**  
   - La base de données **BudgetData_Sample.db** est utilisée en exemple.  
   - Les catégories de dépenses et d’investissement sont stockées dans les tables `Categories` et `InvestmentCategories`.  

---

## **Autres éléments importants**
- **Calcul des gains/pertes en pourcentage** dans l’onglet **Investments**  
  - Le gain/perte mensuel est calculé comme suit :  
    \[
    \frac{\text{Variation de la valeur de l’investissement}}{\text{Valeur totale des actifs du mois précédent}}
    \]
  - Cette méthode prend en compte les liquidités détenues en banque, mais ne distingue pas l'argent destiné aux investissements de l’épargne de précaution.  

---

## **Licence**
Ce projet est sous **licence GNU AGPLv3**. Toute modification ou réutilisation du code doit être publiée en open-source sous la même licence.

---

## **Améliorations possibles**
- [ ] Plus de flexibilité dans l’ajout et le tri des catégories.  
- [ ] Interface graphique pour la configuration des comptes bancaires et des titulaires (actuellement modifiable uniquement dans le code).  
- [ ] Interface pour définir les formats de relevés bancaires (actuellement configurable uniquement dans le code).  
- [ ] Intégration des comptes de retraite.  

---

## **Contact**
[Mon site GitHub Pages](https://sharonchoong.github.io/)
