---
title: CSS Anchor Positioning Guide
pubDate: 10/10/2024
author: "Julien de Rubinat"
tags:
  - CSS
imgUrl: '../../assets/anchor-css.png'
description: Explication du fonctionnement de la fonctionnalité CSS "Anchor"
layout: '../../layouts/BlogPost.astro'
---

## CSS Anchor Positioning Guide

Cet article explique l'évolution de la gestion des infobulles ou popovers en CSS, notamment grâce à la nouvelle fonctionnalité de positionnement d'ancrage. Auparavant, positionner une infobulle sur un élément nécessitait l'utilisation des propriétés de position et de transformation, ce qui pouvait entraîner des problèmes de placement lors des défilements, zooms ou animations, souvent résolus avec du JavaScript. Avec le "CSS Anchor Positioning", introduit dans Chrome 125 un an après sa première version en juin 2023, on peut maintenant attacher des éléments à d'autres directement en CSS, tout en définissant des positions de repli pour éviter les débordements. Cela simplifie grandement le processus et améliore la compatibilité.
Le CSS Anchor Positioning est une nouvelle méthode permettant de positionner des éléments relatifs les uns aux autres. Il introduit deux concepts clés :
•	Anchor : l'élément de référence pour positionner d'autres éléments.
•	Target : un élément en position absolue, placé par rapport à l'anchor.
Le positionnement absolu est au cœur de cette fonctionnalité. Il faut aussi comprendre deux notions importantes :
1.	Containing Block : la boîte contenant l'élément absolu, qui peut être le viewport ou le plus proche ancêtre avec une position spécifique.
2.	IMCB (Inset-Modified Containing Block) : une boîte modifiée par les propriétés d'inset (top, right, bottom, left), influençant la taille et le positionnement des éléments.
Ces concepts sont essentiels pour utiliser des propriétés comme position-area et position-try-order en CSS Anchor Positioning.
Les deux propriétés clés du CSS Anchor Positioning : anchor-name et position-anchor.
1.	anchor-name : Cette propriété permet de désigner explicitement un élément comme étant un "anchor" (point d'ancrage) en lui attribuant un nom personnalisé. Ce nom doit être un identifiant précédé de deux tirets (par ex. --my-anchor).
Exemple :
.anchor {
  anchor-name: --my-anchor;
}
2.	position-anchor : Cette propriété attache un élément "target" (cible) à un "anchor" en utilisant le nom défini avec anchor-name. Le target doit être en position absolue et relié à l'anchor.
Exemple :
.target {
  position: absolute;
  position-anchor: --my-anchor;
}
Si l'ancre spécifiée n'est pas trouvée, les autres propriétés d'ancrage sont ignorées. Cela permet de lier efficacement des éléments entre eux pour un positionnement précis.
