---
title: React and Meta
pubDate: 10/10/2024
author: "Julien de Rubinat"
tags:
  - React
  - Meta
imgUrl: '../../assets/meta.jpg'
description: A brief description of your blog post.
layout: '../../layouts/BlogPost.astro'
---

## React and Meta

Lors de Meta Connect 2024, Mark Zuckerberg a annoncé qu'Instagram et Facebook avaient été reconstruits pour la réalité mixte (MR) sur Meta Quest. Au lieu de simplement adapter les versions mobiles, Meta a choisi React Native pour son efficacité et sa capacité à créer rapidement des animations fluides. Instagram intègre des interactions uniques, comme le passage fluide des vidéos au plein écran et des animations contextuelles. Pour Facebook, les équipes ont réutilisé du code existant, notamment grâce à des technologies comme StyleX et React Strict DOM, afin d'offrir une expérience optimisée pour MR.
Cette année, Meta a lancé une nouvelle version de l'application mobile Meta Horizon, facilitant la personnalisation des avatars et l'interaction avec Horizon Worlds via des quêtes exclusives. Les équipes ont amélioré les performances en optimisant le démarrage de l'application, notamment en initiant les requêtes réseau plus tôt grâce à la librairie GraphQL Relay. Comparé à Facebook, Meta Horizon utilise React Native dès le lancement, offrant des performances équivalentes aux autres applications sociales de Meta. L'application profite aussi des outils de profilage comme Android Systrace et React DevTools.
Meta a ouvert le Meta Horizon Store à tous les développeurs, y compris pour des applications 2D. Des améliorations importantes ont été apportées à la navigation, au classement des applications, et une section "Accès anticipé" a été ajoutée. La boutique est maintenue sur plusieurs plateformes (Android, iOS, Horizon OS, Web) grâce à l'utilisation de React et React Native, ce qui permet une plus grande efficacité de développement. La boutique utilise des technologies comme StyleX et React Strict DOM pour améliorer l'internationalisation, les modes clair/sombre et les futures mises à jour.
Meta a lancé le Meta Spatial SDK et le Meta Spatial Editor pour permettre aux développeurs mobiles de créer des expériences immersives pour Horizon OS avec des outils Android et des capacités spécifiques comme la MR et la 3D. L'éditeur de scènes 3D, construit avec React Native pour Desktop, intègre un moteur de rendu personnalisé en C++ pour des performances élevées. Initialement sceptiques, les ingénieurs C++ ont adopté React Native grâce à sa rapidité de développement.
