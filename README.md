# Pine-script-crash1000-index

Stratégie Pine Script v5 d'estimation de gains et de trading haute probabilité pour l'indice **Crash 1000 Index** sur l'unité de temps **M5** (5 minutes).

## 📌 Présentation
Cette stratégie a été spécialement conçue pour trader en position longue (BUY) sur l'indice synthétique Crash 1000 (Deriv / TradingView).
Afin d'éviter les chutes brutales (*spikes*) caractéristiques de cet indice tout en profitant de la hausse lente continue, l'algorithme combine plusieurs indicateurs clés, des filtres de pente et de forme de bougie, ainsi qu'un système strict anti-trades simultanés/en chaîne.

### 🎯 Objectifs de la stratégie
- **Positions isolées & sélection ultra-stricte** : `pyramiding=0` et temps de pause (*cooldown*) obligatoire entre chaque trade pour éliminer les prises de position consécutives ou simultanées.
- **Filtrage des entrées risquées** : Exigence d'une pente haussière nette de l'EMA, d'un accroissement de l'histogramme MACD et d'un corps de bougie haussier solide (pas de doji ni de faible hésitation).
- **Backtest complet dans le Testeur de Stratégies TradingView** : Visualisation automatique du taux de réussite (Win Rate), du gain net, du profit factor et du drawdown.
- **Gestion du risque sur-mesure** :
  - **Take Profit temporel** : Fermeture automatique de la position 5 minutes (1 bougie M5) après l'entrée.
  - **Stop Loss de protection** : Fixé à 20% de marge/capital par trade pour limiter tout impact en cas de spike inattendu.

---

## 📊 Indicateurs & Logique de Prise de Décision
La stratégie utilise une combinaison d'indicateurs très populaires et de filtres stricts :

1. **Filtre de Tendance Majeure** :
   - EMA 50 > EMA 200
   - Pente de l'EMA 50 strictement positive (`EMA 50 > EMA 50 précédente`)
2. **Filtre de Momentum Accéléré** :
   - **RSI (14)** : Compris entre 50 et 68 + RSI croissant.
   - **MACD (12, 26, 9)** : Ligne MACD > Signal + Histogramme positif **et en hausse** par rapport à la bougie précédente.
3. **Filtre de Corps de Bougie (Solide)** :
   - Exige une bougie haussière franche (le corps représente au moins 35% du range total de la bougie) pour éviter d'entrer sur des bougies d'hésitation (Doji).
4. **Filtre Anti-Spike & Stabilisation** :
   - Détection automatique des bougies de spike grâce à l'ATR.
   - Pause obligatoire de 6 bougies (30 min) après un spike avant toute nouvelle évaluation.
5. **Cooldown Anti-Répétition** :
   - Pause obligatoire (ex: 6 bougies M5 = 30 min) après la clôture d'un trade avant de pouvoir rouvrir une position.

---

## 🚀 Comment Utiliser dans TradingView

1. Ouvrez **TradingView** (ou Deriv TradingView) et sélectionnez le graphique **Crash 1000 Index** sur l'unité de temps **5m (M5)**.
2. Ouvrez l'onglet **Pine Editor** en bas de l'écran.
3. Copiez le contenu du fichier `crash1000_m5_strategy.pine` et collez-le dans le Pine Editor.
4. Cliquez sur **Sauvegarder** (Save), puis sur **Ajouter au graphique** (Add to chart).
5. Ouvrez l'onglet **Testeur de stratégie** (Strategy Tester) pour analyser les performances historiques, le rapport détaillé et le graphique de capital (Equity curve).

---

## ⚙️ Paramètres Ajustables

Dans les paramètres du script (icône d'engrenage sur le graphique) :
- **Indicateurs de Tendance** : Périodes des EMA Fast/Slow (défaut: 50/200).
- **Momentum RSI & MACD** : Seuils et filtres d'accélération.
- **Filtre Anti-Spike** : Multiplicateur ATR et nombre de bougies de temporisation après un spike (défaut: 6 bougies).
- **Gestion du Risk & Pause** :
  - `Durée de détention (Bougies M5)` : Nombre de bougies en position (1 bougie = 5 min).
  - `Cooldown / Pause minimale entre 2 trades` : Nombre de bougies d'attente minimale entre 2 trades (défaut: 6 bougies M5 = 30 min).
  - `Stop Loss (% de la marge)` : Seuil de sécurité fixe (par défaut 20%).
