---
title: "COMO as limitações de predicado | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- LIKE predicate limitations [ODBC]
- ODBC SQL grammar, LIKE predicate limitations
ms.assetid: dbd39099-caf6-4c4c-9ad8-f6c63c1bd5e4
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4cb55109261fee419af8bd0773ed8e85956e8ca9
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="like-predicate-limitations"></a>COMO as limitações de predicado
Se os dados em uma coluna são maiores que 255 caracteres, a comparação LIKE se baseará apenas os primeiros 255 caracteres.  
  
 Um tipo usado em um procedimento tem suporte apenas com padrões constantes. Os Drivers de banco de dados de área de trabalho oferecem suporte a SQL-92 como correspondência de padrões.  
  
 Não há suporte para o uso de uma cláusula de escape em um predicado LIKE.  
  
 Uma comparação LIKE não deve ser executada em uma coluna que contém dados de um tipo de dados numérico ou float. Os resultados podem ser imprevisíveis. Para obter mais informações, consulte o *guia do programador do Microsoft Jet Database Engine*.
