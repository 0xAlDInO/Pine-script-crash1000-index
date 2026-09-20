# Pine-script-crash1000-index

Stratégie Pine Script v5 d'estimation de gains et de trading haute probabilité pour l'indice **Crash 1000 Index** sur l'unité de temps **M5** (5 minutes).

## 📌 Présentation
Cette stratégie a été spécialement conçue pour trader en position longue (BUY) sur l'indice synthétique Crash 1000 (Deriv / TradingView).
Afin d'éviter les chutes brutales (*spikes*) caractéristiques de cet indice tout en profitant de la hausse lente continue, l'algorithme combine des indicateurs clés ajustés pour générer un flux régulier de trades hautement sécurisés dans le Testeur de Stratégie (Strategy Tester).

### 🎯 Timing Précis d'Exécution (Achat & Vente)
- **Ouverture de Position (00s)** : Dès validation de la condition à la clôture de la bougie précédente, l'ordre d'achat est exécuté **exactement à la première seconde de la bougie ciblée** (ex: **10:35:00 pile**).
- **Fermeture de Position (59s)** : La position est automatiquement fermée à la fin de la bougie M5 ciblée (ex: **10:39:59 / 10:40:00**), couvrant précisément les 5 minutes complètes de la bougie haussière.

### 🎯 Objectifs de la stratégie
- **Génération de données de backtest riches** : Paramètres calibrés pour assurer des prises de position régulières sur n'importe quelle période historique (sans être bloqué par des critères sur-filtrés).
- **Positions isolées sans sur-trading** : `pyramiding=0` et temps de pause (*cooldown* de 2 bougies) pour éviter le chevauchement ou les entrées anarchiques.
- **Backtest complet dans le Testeur de Stratégies TradingView** : Visualisation automatique du taux de réussite (Win Rate), du gain net, du profit factor et de la courbe de capital.
- **Gestion du risque sur-mesure** :
  - **Take Profit temporel** : Fermeture automatique de la position après les 5 minutes de la bougie (10:35:00 -> 10:39:59).
  - **Stop Loss de protection** : Fixé à 20% de marge/capital par trade pour limiter tout impact en cas de spike inattendu.

---

## 📊 Indicateurs & Logique de Prise de Décision
La stratégie utilise une combinaison d'indicateurs très populaires :

1. **Filtre de Tendance** :
   - EMA 20 (Rapide) et EMA 50 (Lente)
   - Validation haussière lorsque le prix est supérieur à l'EMA 20 ou que l'EMA 20 est supérieure à l'EMA 50.
2. **Filtre de Momentum** :
   - **RSI (14)** : Plage de validation élargie (45 à 75) pour capturer les poussées haussières régulières.
   - **MACD (12, 26, 9)** : Ligne MACD > Signal ou Histogramme MACD positif.
3. **Filtre Anti-Spike (ATR)** :
   - Détection des bougies anormalement baissières via l'ATR.
   - Pause de 2 bougies M5 post-spike avant d'autoriser de nouvelles entrées.
4. **Cooldown (Pause inter-trades)** :
   - Pause de 2 bougies (10 min) après la clôture d'un trade avant de réévaluer le marché.

---

## 🚀 Comment Utiliser dans TradingView

1. Ouvrez **TradingView** (ou Deriv TradingView) et sélectionnez le graphique **Crash 1000 Index** sur l'unité de temps **5m (M5)**.
2. Ouvrez l'onglet **Pine Editor** en bas de l'écran.
3. Copiez le contenu du fichier `crash1000_m5_strategy.pine` et collez-le dans le Pine Editor.
4. Cliquez sur **Sauvegarder** (Save), puis sur **Ajouter au graphique** (Add to chart).
5. Ouvrez l'onglet **Testeur de stratégie** (Strategy Tester) : vous y verrez l'ensemble des métriques (Trades exécutés, Win Rate, Gain Net, Drawdown).

---

## ⚙️ Paramètres Ajustables

Dans les paramètres du script (icône d'engrenage sur le graphique) :
- **Indicateurs de Tendance** : Périodes des EMA Fast/Slow (défaut: 20/50).
- **Momentum RSI & MACD** : Seuils RSI (min: 45, max: 75) et paramètres MACD.
- **Filtre Anti-Spike** : Multiplicateur ATR (2.0) et bougies de temporisation post-spike (2 bougies).
- **Gestion du Risk & Pause** :
  - `Durée de détention (Bougies M5)` : 1 bougie (entrée à XX:X0:00 et sortie à XX:X4:59).
  - `Cooldown / Pause minimale entre 2 trades` : 2 bougies M5 (10 minutes).
  - `Stop Loss (% de la marge)` : Seuil de sécurité fixe (par défaut 20%).
