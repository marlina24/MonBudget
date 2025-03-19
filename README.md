# Application Budget Model

Une simple application de bureau Windows en WPF qui suit le budget mensuel des dépenses et des revenus, le patrimoine net et les investissements financiers sur l’ensemble des comptes bancaires et de courtage. Toutes les données sont locales.

- Plus puissant et évolutif que de créer et maintenir une feuille de calcul  
- Possibilité de programmer l’application pour lire n’importe quel format de relevé ou rapport bancaire et afficher toutes les analyses souhaitées  
- Les mots de passe bancaires ne sont pas enregistrés et restent privés  

Contrairement aux solutions de finance personnelle comme Mint, Quicken et Quickbooks, il n’y a aucun lien ou synchronisation automatique avec les comptes, donc les mots de passe et identifiants bancaires ne sont jamais confiés à des entreprises ni sauvegardés dans une base de données.

## Fonctionnalités
1. Vue mensuelle des revenus et dépenses catégorisés  
2. Possibilité de modifier les éléments automatiquement catégorisés (par exemple, une dépense d’essence classée dans « Déplacements » peut être reclassée dans « Voyage » pour refléter un voyage ponctuel)  
3. Historique des dépenses, revenus et économies mensuels dans des graphiques récapitulatifs  
4. Évolution du patrimoine net dans le temps  
5. Gains/pertes d’investissement mois par mois et de manière cumulative  
6. Analyse des investissements dans le temps, par titre ou par classe d’actifs  
7. Historique des achats et ventes d’actions/fonds (comparaison du prix exécuté par rapport au prix de marché nécessitant un compte Alpha Vantage)  

## Démarrage rapide : Prévisualiser les fonctionnalités avec des données d’exemple
Exécutez l’application **Budget Model.exe** dans le dossier **Budget Model\bin\Debug\**. L’application affichera d’abord l’écran **Budget Statement**, avec des données d’exemple déjà catégorisées. Utilisez les boutons en haut à droite pour naviguer vers les autres écrans, y compris l’écran **Analyse historique du budget et du patrimoine net** et l’écran **Investissements**.

![Écran d’analyse des investissements](/images/demo.gif)

Les données d’exemple chargées dans l’application se trouvent dans le dossier **\test_data**. L’écran **Données & Définitions** est l’endroit où les relevés bancaires et rapports de courtage peuvent être téléchargés, et où les catégories peuvent être définies pour les achats ou revenus apparaissant dans les relevés. La catégorisation repose sur la correspondance de mots-clés, qui attribue automatiquement la même catégorie à tous les éléments de relevé ayant la même série de mots dans leur description.

**Écran Données & Définitions**  
![Écran Données & Définitions](/images/Categorizing%20transaction%20items%20in%20accounts.png)

## Démarrage rapide : Personnaliser

Plusieurs éléments doivent être configurés pour une première utilisation.

1. **FinancialInstitutions_Sample.cs dans le dossier Models**  
   - La méthode *GetFinancialInstitutions* dans la classe *FinancialInstitution* retourne la liste des comptes bancaires et comptes de courtage que l’application analyse. Avant la première utilisation, cette liste doit être définie dans le code. Si la méthode n’est pas implémentée, la liste d’exemple trouvée dans la classe abstraite *BaseFinancialInstitution* dans le fichier *IFinancialInstitution.cs* sera utilisée, comprenant *BankSample* et *BrokerageSample*.  

2. **Holders_Sample.cs dans le dossier Models**  
   - La méthode *HolderCollection* dans la classe *Holder* doit être écrite pour lister les titulaires de comptes. Les foyers peuvent avoir plusieurs titulaires, et l’application permet d’afficher des analyses pour chaque titulaire, ainsi qu’au niveau agrégé du foyer nommé *"Home"*. Si la méthode n’est pas implémentée, la liste d’exemple trouvée dans la classe abstraite *BaseHolder* dans le fichier *IHolder.cs* sera utilisée, comprenant *Person1* et *Person2*.  

3. **ExcelImport_Sample.cs dans le dossier Helpers**  
   - La classe *ExcelImport* implémente la méthode qui lit les fichiers CSV des relevés d’activité bancaire et des relevés de courtage. Pour extraire les transactions quotidiennes et les valeurs des actifs à partir des fichiers CSV, la classe doit être écrite pour lire les colonnes appropriées selon les différents formats de relevés. Elle utilise la librairie CsvHelper.

   **Particularités des données :**  
   - **Salaire brut** :  
     - Le salaire brut n’apparaît généralement pas sur les relevés bancaires — seul le salaire net apparaît comme un flux entrant. Cependant, le salaire brut peut être spécifié manuellement dans la fenêtre **Données & Définitions**. Une fois défini, le montant sera automatiquement reporté au mois suivant, mais peut être modifié manuellement (par exemple en cas d’augmentation de salaire).
   - **Solde initial** :  
     - L’application calcule le solde de vos comptes bancaires en effectuant une somme cumulative de toutes les transactions. Pour afficher des soldes précis, l’historique complet des transactions doit être disponible. Si seul un historique limité est chargé, le solde initial juste avant la première transaction doit être indiqué comme une « transaction » initiale séparée.

### Autres fichiers à modifier

Les fichiers suivants peuvent être personnalisés.

1. **Fichiers de configuration**  
   - **Connections.config**  
     - Ce fichier contient la chaîne de connexion vers la base de données où toutes les données seront enregistrées. Par défaut, il pointe vers la base de données SQLite *BudgetData_Sample.db* dans le dossier *App_Data*.  
   - **CustomAppSettings.config**  
     - Ce fichier contient les clés API ou mots de passe utilisés pour intégrer les API de prix des actions et des rendements obligataires afin de suivre la performance des investissements. L’API gratuite [Alpha Vantage](https://www.alphavantage.co/) est utilisée ici pour afficher les prix des actions/ETF dans l’écran **Investissements**. Une clé API est fournie lors de l’inscription sur le site et doit être spécifiée dans *CustomAppSettings.config* comme suit :  
     `<appSettings><add key="alphav_key" value="[clé API]"/></appSettings>`  
     Lorsque vous ajoutez des fichiers de configuration, veillez à ce qu’ils soient copiés dans le répertoire de sortie lors de la compilation.  

2. **La base de données - SQLite**  
   - À titre d’exemple, l’application utilise actuellement la base de données *BudgetData_Sample.db*. Dans cette base, les tables *Categories* et *InvestmentCategories* stockent la liste des catégories utilisées. Toutes les autres tables sont alimentées par les données saisies par l’utilisateur. SQLite est utilisé car il est léger et adapté au stockage local.

## Autres points notables
- Une remarque sur le calcul des pourcentages de gain/perte dans *Investissements* :  
   - Le pourcentage mensuel de gain/perte sur les investissements est calculé par la variation de la valeur de l’investissement divisée par la valeur totale des actifs à la fin du mois précédent, y compris les dépôts bancaires. Cette méthode prend en compte le coût d’opportunité de la détention de liquidités, même si elle ne considère pas l’argent qui n’est jamais destiné à être investi (comme un fonds d’urgence).
