# 🐢 Système de Minage Automatisé - ComputerCraft

[![ComputerCraft](https://img.shields.io/badge/ComputerCraft-1.12.2-orange.svg)](https://www.computercraft.info/)
[![Minecraft](https://img.shields.io/badge/Minecraft-1.12.2-green.svg)](https://minecraft.net/)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

Un système de minage automatisé complet utilisant des turtles et un serveur central pour Minecraft avec le mod ComputerCraft.

![Interface Serveur](https://via.placeholder.com/800x400.png?text=Interface+Serveur+de+Contrôle)

## ✨ Fonctionnalités

### 🎯 Système de Contrôle
- **Serveur central** avec interface graphique avancée
- **Contrôle en temps réel** de multiples turtles
- **Statistiques détaillées** (blocs minés, carburant, position)
- **Gestion individuelle ou groupée** des turtles

### 🤖 Turtles Intelligentes
- **Minage automatique** en 3D avec paramètres configurables
- **Gestion automatique** des échelles pour la remontée
- **Détection de carburant** et inventaire
- **Communication Rednet** robuste

### 🎨 Interface Avancée
- **Affichage en temps réel** sur moniteur ou terminal
- **Statuts colorés** pour une visibilité optimale
- **Commandes clavier** intuitives
- **Configuration dynamique** sans redémarrage

## 🚀 Installation

### Prérequis
- Minecraft 1.12.2
- Mod ComputerCraft
- Ordinateur ou turtle avancée
- Modem sans fil pour la communication

### Configuration

1. **Serveur Central** ('minerServer.lua')

```
bash
# Placer sur un ordinateur avec modem
pastebin get XXXXXXXXX minerServer.lua
minerServer
```

2. **Turtles de Minage** ('turtleMiner.lua')

```
bash
# Placer sur chaque turtle avec modem
pastebin get YYYYYYYYY turtleMiner.lua
turtleMiner
```

## 📖 Utilisation

### Démarrage Rapide

1. **Démarrer le serveur** sur un ordinateur central
2. **Démarrer les turtles** sur chaque turtle de minage
3. **Configurer les dimensions** de minage via l'interface
4. **Lancer le minage** avec la touche Entrée

### Commandes du Serveur

| Touche | Action |
|--------|--------|
| 'Entrée' | Démarrer le minage |
| 'S' | Arrêter toutes les turtles |
| 'P' | Mettre en pause/reprendre |
| 'C' | Envoyer la configuration |
| 'R' | Rafraîchir l'interface |
| 'Q/A' | Modifier la hauteur |
| 'W/S' | Modifier la longueur |
| '1-5' | Largeurs prédéfinies |
| 'E' | Activer/désactiver les échelles |

### Configuration des Turtles

Chaque turtle peut être configurée individuellement :

```
lua
-- Exemple de configuration
local config = {
    xWidth = 10,      -- Largeur du minage
    yHeight = 3,      -- Hauteur/nombre d'étages
    zLength = 5,      -- Longueur/tunnels
    useLadder = true  -- Utilisation d'échelles
}
```

## 📊 Protocole de Communication

### Messages Rednet

#### Enregistrement

```
lua
{ type = 'register', turtleId = 123 }
```

#### Statut

```
lua
{
    type = 'status',
    turtleId = 123,
    data = {
        currentTask = 'Minage en cours',
        blocksMined = 150,
        fuelLevel = 5000,
        x = 10, y = 64, z = -20
    }
}
```

#### Commandes

```
lua
-- Démarrer
{ type = 'start', xWidth = 10, yHeight = 3, zLength = 5 }

-- Arrêter
{ type = 'stop' }

-- Pause
{ type = 'pause' }

-- Configuration
{ type = 'config', xWidth = 15 }
```

## 🏗️ Architecture

```
┌─────────────────┐    Rednet    ┌─────────────────┐
│   Serveur       │◄─────────────│   Turtle #1     │
│   Central       │              │                 │
│                 │─────────────►│   Minage Zone   │
└─────────────────┘              └─────────────────┘
         │                               │
         │                       ┌─────────────────┐
         └───────────────────────│   Turtle #2     │
                                 │                 │
                                 │   Minage Zone   │
                                 └─────────────────┘
```

## 🔧 Personnalisation

### Modifier les Dimensions par Défaut

Éditez 'miningConfig' dans 'minerServer.lua' :

```
lua
local miningConfig = {
    xWidth = 15,      -- Largeur par défaut
    yHeight = 4,      -- Hauteur par défaut  
    zLength = 8,      -- Longueur par défaut
    useLadder = true  -- Échelles par défaut
}
```

### Ajouter de Nouvelles Commandes

Dans 'turtleMiner.lua' :

```
lua
local function handleCommand(message)
    -- ... commandes existantes ...
    
    if message.type == 'custom' then
        -- Votre logique personnalisée
    end
end
```

## 🐛 Dépannage

### Problèmes Courants

**Turtle non détectée**
- Vérifier que le modem est connecté sur 'left'
- Confirmer que rednet est ouvert

**Communication intermittente**
- Vérifier la distance entre les appareils
- S'assurer qu'aucun bloc n'obstrue la communication

**Carburant insuffisant**
- Les turtles nécessitent du carburant (charbon, etc.)
- Vérifier 'turtle.getFuelLevel()'

### Logs de Débogage

Activez les messages de debug dans le code :

```
lua
local DEBUG = true

local function debugLog(message)
    if DEBUG then
        print('[DEBUG] ' .. message)
    end
end
```

## 📈 Performances

- **Jusqu'à 20 turtles** gérées simultanément
- **Latence < 1s** pour les commandes
- **Mise à jour automatique** toutes les 2 secondes
- **Nettoyage automatique** des turtles inactives

## 🤝 Contribution

Les contributions sont les bienvenues ! 

1. Fork le projet
2. Créez votre branche ('git checkout -b feature/AmazingFeature')
3. Commit vos changements ('git commit -m 'Add some AmazingFeature'')
4. Push sur la branche ('git push origin feature/AmazingFeature')
5. Ouvrez une Pull Request

## 📝 Licence

Distribué sous licence MIT. Voir 'LICENSE' pour plus d'informations.

## 🙏 Remerciements

- [ComputerCraft](https://www.computercraft.info/) - Pour le mod fantastique
- [Minecraft Forge](https://files.minecraftforge.net/) - Pour la plateforme de modding
- La communauté ComputerCraft pour l'inspiration

---

**⭐ N'oubliez pas de mettre une étoile si ce projet vous est utile !**
