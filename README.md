# 🐢 Système de Minage Automatisé - ComputerCraft

[![ComputerCraft](https://img.shields.io/badge/ComputerCraft-1.12.2-orange.svg)](https://www.computercraft.info/)
[![Minecraft](https://img.shields.io/badge/Minecraft-1.12.2-green.svg)](https://minecraft.net/)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

Un système de minage automatisé complet utilisant des turtles et un serveur central pour Minecraft avec le mod ComputerCraft.

![Interface Serveur](https://via.placeholder.com/800x400.png?text=Interface+Serveur+de+Contrôle)

## ✨ Fonctionnalités

### 🎯 Système de Contrôle Avancé
- **Serveur central** avec interface graphique avancée
- **Contrôle en temps réel** de multiples turtles
- **Sélection individuelle ou groupée** des turtles
- **10 configurations sauvegardées** avec accès rapide
- **Mode édition** pour configuration fine

### 🤖 Turtles Intelligentes
- **Minage automatique** en 3D avec paramètres configurables
- **Gestion automatique** des échelles pour la remontée
- **Détection de carburant** et inventaire
- **Communication Rednet** robuste
- **Retour automatique** à la base

### 🎨 Interface Avancée
- **Affichage en temps réel** sur moniteur ou terminal
- **Statuts colorés** pour une visibilité optimale
- **Commandes clavier** intuitives et contextuelles
- **Curseur visuel** pour l'édition des coordonnées
- **Indicateurs de sélection** des turtles

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
pastebin get 8iz2scyW minerServer.lua
minerServer
```

2. **Turtles de Minage** ('turtleMiner.lua')

```
bash
# Placer sur chaque turtle avec modem
pastebin get wyFw9uA2 turtleMiner.lua
turtleMiner
```

## 📖 Utilisation

### Démarrage Rapide

1. **Démarrer le serveur** sur un ordinateur central
2. **Démarrer les turtles** sur chaque turtle de minage
3. **Sélectionner les turtles** à contrôler (T, A, N)
4. **Configurer les dimensions** de minage via l'interface
5. **Lancer le minage** avec la touche Entrée

### Commandes du Serveur

#### Mode Normal
| Touche | Action |
|--------|--------|
| 'Entrée' | Démarrer le minage avec config actuelle |
| 'S' | Arrêter les turtles sélectionnées |
| 'P' | Mettre en pause/reprendre |
| 'C' | Activer le mode configuration |
| 'R' | Rafraîchir l'interface |
| '1-0' | Envoyer la configuration 1-10 |
| 'T' | Sélectionner/désélectionner une turtle |
| 'A' | Sélectionner toutes les turtles |
| 'N' | Désélectionner toutes les turtles |

#### Mode Configuration
| Touche | Action |
|--------|--------|
| '1-0' | Changer de configuration (1-10) |
| 'W' | +1 sur la coordonnée sélectionnée |
| 'S' | -1 sur la coordonnée sélectionnée |
| 'Q' | Déplacer le curseur vers la gauche (X→Y→Z) |
| 'E' | Déplacer le curseur vers la droite (X←Y←Z) |
| 'ESPACE' | Activer/désactiver les échelles |
| 'Entrée' | Envoyer la configuration |
| 'C' | Quitter le mode configuration |

### Configuration des Turtles

Chaque turtle peut être configurée individuellement avec 10 profils sauvegardés :

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
-- Démarrer avec configuration
{ type = 'start', xWidth = 10, yHeight = 3, zLength = 5, useLadder = true }

-- Arrêter
{ type = 'stop' }

-- Pause/Reprise
{ type = 'pause' }

-- Configuration sans démarrer
{ type = 'config', xWidth = 15 }

-- Confirmation d'enregistrement
{ type = 'registered' }
```

## 🏗️ Architecture

```
┌─────────────────┐    Rednet    ┌─────────────────┐
│   Serveur       │◄─────────────│   Turtle #1     │
│   Central       │              │                 │
│                 │─────────────►│   Minage Zone   │
│ 10 Configs      │              └─────────────────┘
│ Sélection       │                     
│ Mode Édition    │    Rednet    ┌─────────────────┐
└─────────────────┘─────────────►│   Turtle #2     │
                                 │                 │
                                 │   Minage Zone   │
                                 └─────────────────┘
```

## 🔧 Personnalisation

### Modifier les Configurations par Défaut

Éditez 'configs' dans 'minerServer.lua' :

```
lua
local configs = {}
for i = 1, 10 do
    configs[i] = {
        xWidth = 10 + i,      -- Largeur progressive
        yHeight = 3,          -- Hauteur fixe
        zLength = 5,          -- Longueur fixe
        useLadder = true,     -- Échelles activées
        name = "Config " .. i -- Nom de la configuration
    }
end
```

### Ajouter de Nouvelles Commandes

Dans 'turtleMiner.lua' :

```
lua
local function handleCommand(message)
    -- Commandes existantes...
    
    if message.type == 'custom' then
        -- Votre logique personnalisée
        if message.action == 'return_base' then
            returnToBase()
        end
    end
end
```

### Personnaliser l'Interface

Modifiez les fonctions d'affichage dans 'minerServer.lua' :

```
lua
local function drawHeader()
    -- Personnaliser l'en-tête
    centerText("=== MON SYSTÈME DE MINAGE ===", 1, width)
end
```

## 🐛 Dépannage

### Problèmes Courants

**Turtle non détectée**
- Vérifier que le modem est connecté sur 'left'
- Confirmer que rednet est ouvert des deux côtés
- Vérifier la distance (max 64 blocs)

**Communication intermittente**
- Vérifier la distance entre les appareils
- S'assurer qu'aucun bloc n'obstrue la communication
- Redémarrer les modems si nécessaire

**Carburant insuffisant**
- Les turtles nécessitent du carburant (charbon, lave, etc.)
- Vérifier 'turtle.getFuelLevel()'
- Ajouter du carburant dans l'inventaire

**Turtle non sélectionnée**
- Appuyer sur 'A' pour sélectionner toutes les turtles
- Ou 'T' pour sélectionner individuellement

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

-- Utilisation
debugLog('Turtle ' .. id .. ' enregistrée')
```

## 📈 Performances

- **Jusqu'à 20 turtles** gérées simultanément
- **Latence < 1s** pour les commandes
- **10 configurations** sauvegardées
- **Mise à jour automatique** toutes les 2 secondes
- **Nettoyage automatique** des turtles inactives
- **Sélection granulaire** des turtles

## 🎮 Guide des Commandes Rapides

### Contrôle Immédiat
- **1-0** : Envoyer directement les configs 1-10
- **T+A+N** : Gestion rapide des sélections
- **C** : Basculer mode configuration

### Édition Efficace
- **Q/E** : Navigation fluide entre coordonnées
- **W/S** : Ajustement rapide des valeurs
- **ESPACE** : Basculer les échelles instantanément

## 🤝 Contribution

Les contributions sont les bienvenues ! 

1. Fork le projet
2. Créez votre branche ('git checkout -b feature/AmazingFeature')
3. Commit vos changements ('git commit -m 'Add some AmazingFeature'')
4. Push sur la branche ('git push origin feature/AmazingFeature')
5. Ouvrez une Pull Request

### Améliorations Planifiées
- [ ] Interface web externe
- [ ] Système de sauvegarde des configurations
- [ ] Historique des activités
- [ ] Alertes automatiques (carburant faible, inventaire plein)

## 📝 Licence

Distribué sous licence MIT. Voir 'LICENSE' pour plus d'informations.

## 🙏 Remerciements

- [ComputerCraft](https://www.computercraft.info/) - Pour le mod fantastique
- [Minecraft Forge](https://files.minecraftforge.net/) - Pour la plateforme de modding
- La communauté ComputerCraft pour l'inspiration et le support

---

**⭐ N'oubliez pas de mettre une étoile si ce projet vous est utile !**

**🐛 Signaler un bug** : [Ouvrir une Issue](https://github.com/votre-repo/issues)

**💡 Suggestions** : Les idées d'amélioration sont les bienvenues !
