---
title: Agregações neto | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f1bff3c8a155e1e9378acbb659f00817f478382e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47602374"
---
# <a name="grandchild-aggregates"></a>Agregações neto
A coluna de capítulo criada em uma cláusula de um comando de forma pode receber um *nome do alias do capítulo* (normalmente com a palavra-chave). Você pode identificar qualquer coluna em qualquer capítulo o moldado **Recordset** com um nome totalmente qualificado que identifica o filho que contém a coluna. Por exemplo, se o capítulo pai, Cap1, contém um capítulo de filho, chap2, que tem uma coluna de quantidade amt, e o nome qualificado seria chap1.chap2.amt. O nome qualificado, em seguida, pode ser usado como um argumento para uma das funções de agregação (SUM, AVG, MAX, MIN, COUNT, STDEV ou qualquer).  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de data shaping](../../../ado/guide/data/data-shaping-example.md)
