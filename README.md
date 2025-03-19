```markdown
# **Budget Model App**  

[![Codacy Badge](https://api.codacy.com/project/badge/Grade/0d5d8c2bd2964861ac67dcf2a5e62f22)](https://www.codacy.com/manual/SharonChoong/budget-model?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=sharonchoong/budget-model&amp;utm_campaign=Badge_Grade)

## **Présentation**  
**Budget Model App** est une application de bureau pour Windows, développée en **WPF**. Elle permet de **suivre un budget mensuel**, d’analyser la **valeur nette** et de gérer les **investissements financiers** sur différents comptes bancaires et de courtage.  
📌 **Toutes les données sont stockées localement**, garantissant sécurité et confidentialité.

### **Pourquoi utiliser Budget Model App ?**
✅ Plus **puissant et évolutif** qu’un simple fichier Excel.  
✅ Permet de **lire et analyser n’importe quel relevé bancaire**.  
✅ **Aucun mot de passe bancaire n’est enregistré** (contrairement à Mint, Quicken ou QuickBooks).  

L’application ne **synchronise pas automatiquement les comptes bancaires**, ce qui **évite tout risque lié au stockage des identifiants bancaires**.

---

## **Fonctionnalités**
1. 📊 **Vue mensuelle** des revenus et dépenses classés par catégorie.  
2. 🏷 **Possibilité de modifier les catégories** des transactions.  
3. 📈 **Historique des dépenses, revenus et économies sous forme de graphiques**.  
4. 📊 **Suivi de la valeur nette et de son évolution dans le temps**.  
5. 💹 **Analyse des investissements** (gains/pertes, catégories d’actifs, titres spécifiques).  
6. 🏦 **Gestion des transactions boursières**, avec comparaison des prix d’achat/vente (nécessite **Alpha Vantage API**).  

---

## **🎬 Démarrage rapide : Tester l'application avec des données d'exemple**
1. **Exécutez** `Budget Model.exe` dans le dossier `Budget Model\bin\Debug\`.  
2. L’écran **Budget Statement** s'affichera avec des données **déjà catégorisées**.  
3. Naviguez entre les différentes sections :  
   - 📊 **Historical Budget and Net Worth Analysis** *(Analyse budgétaire historique et valeur nette)*  
   - 💹 **Investments** *(Investissements)*  

📁 **Les données d’exemple sont disponibles dans le dossier** `\test_data`.  

![Investment Analysis screen](/images/demo.gif)

---

## **🔧 Personnalisation**
Avant la première utilisation, certaines configurations doivent être **définies dans le code** :

### **1️⃣ Déclaration des institutions financières**
📌 **Fichier** : `FinancialInstitutions_Sample.cs` (dossier `Models`)  
🔹 La méthode `GetFinancialInstitutions` liste les **banques et comptes analysés** par l’application.  
🔹 **Par défaut**, la liste d’exemple comprend `BankSample` et `BrokerageSample`.

### **2️⃣ Définition des titulaires de comptes**
📌 **Fichier** : `Holders_Sample.cs` (dossier `Models`)  
🔹 La méthode `HolderCollection` doit être **modifiée pour lister les titulaires de comptes**.  
🔹 Un foyer peut avoir plusieurs titulaires (ex. un couple) et l’application permet **une analyse détaillée par personne ou pour l’ensemble du foyer**.

### **3️⃣ Importation de relevés bancaires**
📌 **Fichier** : `ExcelImport_Sample.cs` (dossier `Helpers`)  
🔹 Permet de **lire les fichiers CSV** des relevés bancaires.  
🔹 Doit être **configuré selon le format des fichiers** fournis par la banque.  

---

## **📂 Gestion des données et particularités**
### **📝 Salaire brut**
💡 Les relevés bancaires **indiquent généralement uniquement le salaire net**.  
📌 Une option permet **d’indiquer manuellement le salaire brut** dans **Data & Definitions**.

### **💰 Solde initial des comptes**
📌 Pour éviter toute incohérence, il faut **ajouter manuellement le solde initial** si l’historique des transactions est incomplet.

---

## **📁 Autres fichiers à configurer**
1. **🔧 Fichiers de configuration**  
   - 📌 `Connections.config` : gère la connexion à la base de données SQLite.  
   - 🔑 `CustomAppSettings.config` : contient les **clés API** pour **récupérer les prix des actions via Alpha Vantage**.

2. **📊 Base de données (SQLite)**  
   - L’application utilise une base de données **SQLite** (`BudgetData_Sample.db`).  
   - 📌 Les catégories de dépenses et d’investissement sont stockées dans `Categories` et `InvestmentCategories`.

---

## **📊 Analyse et calculs financiers**
### **💹 Calcul des gains/pertes en pourcentage dans l’onglet Investments**
📌 **Formule utilisée** :
\[
\text{Performance mensuelle} = \frac{\text{Variation de la valeur de l’investissement}}{\text{Valeur des actifs du mois précédent}}
\]
💡 **Les liquidités bancaires sont prises en compte**, mais pas la distinction entre fonds d’investissement et épargne de précaution.

---

## **📜 Licence**
Ce projet est sous **licence GNU AGPLv3**.  
Toute modification ou réutilisation du code **doit être publiée en open-source sous la même licence**.

---

## **🛠 Améliorations possibles**
- [ ] 🔄 **Plus de flexibilité dans la gestion des catégories.**  
- [ ] 🎛 **Interface pour configurer les banques et les comptes (actuellement en code).**  
- [ ] 📂 **Ajout d’une interface pour définir les formats de relevés bancaires.**  
- [ ] 📊 **Intégration des comptes de retraite dans l’analyse financière.**  

---

## **📞 Contact**
🔗 [Mon site GitHub Pages](https://sharonchoong.github.io/)  

---

## **📸 Interface : Écran Data & Definitions**
Cet écran permet de :  
- 📂 **Charger des relevés bancaires**  
- 🏷 **Définir des catégories** pour classifier les transactions **par mots-clés**  

![Data & Definitions screen](/images/Categorizing%20transaction%20items%20in%20accounts.png)
```
