---
title: "COMO as limitações de predicado | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
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
ms.openlocfilehash: 3ccf71ebc5bedb1f778af8992aae71cea8320603
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="like-predicate-limitations"></a>COMO as limitações de predicado
Se os dados em uma coluna são maiores que 255 caracteres, a comparação LIKE se baseará apenas os primeiros 255 caracteres.  
  
 Um tipo usado em um procedimento tem suporte apenas com padrões constantes. Os Drivers de banco de dados de área de trabalho oferecem suporte a SQL-92 como correspondência de padrões.  
  
 Não há suporte para o uso de uma cláusula de escape em um predicado LIKE.  
  
 Uma comparação LIKE não deve ser executada em uma coluna que contém dados de um tipo de dados numérico ou float. Os resultados podem ser imprevisíveis. Para obter mais informações, consulte o *guia do programador do Microsoft Jet Database Engine*.
