---
title: Agregações do neto | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- grandchild aggregates [ADO]
- data shaping [ADO], grandchild aggregates
ms.assetid: 4162d35f-2ce1-4218-80a5-b6933348837e
author: rothja
ms.author: jroth
ms.openlocfilehash: 148a2798d04bc7ec41832e5103d8ec097ffa9a0c
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764817"
---
# <a name="grandchild-aggregates"></a>Agregações neto
A coluna de capítulo criada em uma cláusula de um comando de forma pode receber um *nome de alias de capítulo* (normalmente com a palavra-chave as). Você pode identificar qualquer coluna em qualquer capítulo do conjunto de **registros** moldado com um nome totalmente qualificado que identifica o filho que contém a coluna. Por exemplo, se o capítulo pai, chap1, contiver um capítulo filho, CHAP2, que tem uma coluna amount, AMT, o nome qualificado será chap1. CHAP2. AMT. O nome qualificado pode ser usado como um argumento para uma das funções de agregação (SUM, AVG, MAX, MIN, COUNT, Desv ou ANY).  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de data shaping](../../../ado/guide/data/data-shaping-example.md)
