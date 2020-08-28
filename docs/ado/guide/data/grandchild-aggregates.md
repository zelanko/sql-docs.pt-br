---
description: Agregações neto
title: Agregações do neto | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 02d481e55fa8fc41e022d41b88c9dcd6c4777dfe
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980707"
---
# <a name="grandchild-aggregates"></a>Agregações neto
A coluna de capítulo criada em uma cláusula de um comando de forma pode receber um *nome de alias de capítulo* (normalmente com a palavra-chave as). Você pode identificar qualquer coluna em qualquer capítulo do conjunto de **registros** moldado com um nome totalmente qualificado que identifica o filho que contém a coluna. Por exemplo, se o capítulo pai, chap1, contiver um capítulo filho, CHAP2, que tem uma coluna amount, AMT, o nome qualificado será chap1. CHAP2. AMT. O nome qualificado pode ser usado como um argumento para uma das funções de agregação (SUM, AVG, MAX, MIN, COUNT, Desv ou ANY).  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de data shaping](./data-shaping-example.md)