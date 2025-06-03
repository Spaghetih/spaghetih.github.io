
# 🎮 Challenge CTF : Tetris – Hackfinity Battle 2025

> 🔍 Catégorie : Hacking de jeu  
> 💻 Plateforme : Windows  
> 🛠️ Moteur : Godot  
> 🎯 Difficulté : Facile  

---

## 🗂️ Arborescence du projet (après extraction)

```
Tetris/
├── .import/
├── assets/
│   ├── block.png
│   └── background.jpg
├── gui.gd         👈 Fichier ciblé !
├── main.tscn
├── project.godot
├── score.gd
└── ...
```

---

## 🧰 Outils utilisés

| Outil                                       | Description                                  |
|---------------------------------------------|----------------------------------------------|
| [Godot Engine](https://godotengine.org/download/windows/) | Pour ouvrir et modifier le projet             |
| [GDRE Decompiler](https://github.com/GDRETools/gdsdecomp/releases/tag/v1.00-beta.3) | Pour extraire les fichiers `.pck`             |
| Windows 10                                  | Système recommandé pour compatibilité         |

---

## 🧩 Étapes de résolution

### 1. 🧨 Extraire le jeu

- Utiliser **GDRE Decompiler** pour décompresser le fichier `.pck`
- On obtient alors le **projet Godot complet** avec tous les scripts `.gd`

---

### 2. 🔎 Modifier la condition de score

- Ouvrir le projet avec **Godot Engine**
- Aller dans le fichier `gui.gd`
- Repérer la fonction suivante :

```gdscript
func _on_Board_update_score(score, lines):
    $ContainerScore / ScoreBackground / ScoreValue.text = str(score)
    $ContainerLines / LinesBackground / LinesCount.text = str(lines)
    if score >= 999999:
        $ButtonContainer / T.show()
```

- Modifier la condition comme ceci :

```gdscript
    if score >= 0:
        $ButtonContainer / T.show()
```

✔️ Cela permet de **désactiver la limite de score** et d'afficher directement le bouton contenant le flag.

---

### 3. ▶️ Lancer le jeu

- Cliquer sur **Play** dans Godot
- Le bouton avec le flag apparaît dès le lancement
- Cliquer dessus pour révéler le flag

---

## 🏁 Flag final

```
THM{I_CAN_READ_IT_ALL}
```

---

## 📁 Remarques

Ce challenge était une excellente initiation au **reverse engineering de jeux créés avec Godot**, à la manipulation de scripts `.gd`, et à la modification de logique de jeu pour contourner les conditions de victoire.

---
