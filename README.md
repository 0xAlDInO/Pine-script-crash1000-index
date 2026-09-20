# Pine-script-crash1000-index

Stratégie Pine Script v5 d'estimation de gains et de trading haute probabilité pour l'indice **Crash 1000 Index** sur l'unité de temps **M5** (5 minutes).

## 📌 Présentation
Cette stratégie a été spécialement conçue pour trader en position longue (BUY) sur l'indice synthétique Crash 1000 (Deriv / TradingView).
Afin d'éviter les chutes brutales (*spikes*) caractéristiques de cet indice tout en profitant de la hausse lente continue, l'algorithme combine plusieurs indicateurs clés et filtres stricts.

### 🎯 Objectifs de la stratégie
- **Ciblage de bougies haussières sûres en M5** : Prise de position après confirmation d'une dynamique haussière forte pour assurer 1 à 2 bougies haussières successives.
- **Backtest complet dans le Testeur de Stratégies TradingView** : Visualisation automatique du taux de réussite (Win Rate), du gain net, du profit factor et du drawdown.
- **Gestion du risque sur-mesure** :
  - **Take Profit temporel** : Fermeture automatique de la position 5 minutes (ou 1 à 2 bougies M5) après l'entrée.
  - **Stop Loss de protection** : Fixé à 20% de marge/capital par trade pour limiter tout impact en cas de spike inattendu.

---

## 📊 Indicateurs & Logique de Prise de Décision
La stratégie utilise une combinaison d'indicateurs très populaires pour filtrer le bruit du marché :

1. **Filtre de Tendance Majeure** :
   - EMA 50 (Moyenne Mobile Exponentielle Rapide) > EMA 200 (Moyenne Mobile Exponentielle Lente)
   - Prix de clôture au-dessus de l'EMA 50
2. **Filtre de Momentum** :
   - **RSI (14)** : Compris entre 45 et 70 (Zone de momentum haussier sain sans être en surachat extrême).
   - **MACD (12, 26, 9)** : Ligne MACD supérieure à la ligne Signal et histogramme positif.
3. **Filtre Anti-Spike (Volatilité ATR)** :
   - Détection automatique des bougies de spike récentes grâce à l'ATR (Average True Range).
   - Pause obligatoire de $N$ bougies post-spike pour laisser le marché se stabiliser.

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
- **Momentum RSI & MACD** : Seuils de validation du momentum.
- **Filtre Anti-Spike** : Multiplicateur ATR et nombre de bougies de temporisation après un spike.
- **Gestion du Risk** :
  - `Durée de détention (Bougies M5)` : Nombre de bougies en position (1 bougie = 5 min).
  - `Stop Loss (% de la marge)` : Seuil de sécurité fixe (par défaut 20%).
