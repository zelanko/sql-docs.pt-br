---
title: COMO as limitações de predicado | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- LIKE predicate limitations [ODBC]
- ODBC SQL grammar, LIKE predicate limitations
ms.assetid: dbd39099-caf6-4c4c-9ad8-f6c63c1bd5e4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 891c6499f54c56635d74289517e8cf33f66ba4ee
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="like-predicate-limitations"></a>COMO as limitações de predicado
Se os dados em uma coluna são maiores que 255 caracteres, a comparação LIKE se baseará apenas os primeiros 255 caracteres.  
  
 Um tipo usado em um procedimento tem suporte apenas com padrões constantes. Os Drivers de banco de dados de área de trabalho oferecem suporte a SQL-92 como correspondência de padrões.  
  
 Não há suporte para o uso de uma cláusula de escape em um predicado LIKE.  
  
 Uma comparação LIKE não deve ser executada em uma coluna que contém dados de um tipo de dados numérico ou float. Os resultados podem ser imprevisíveis. Para obter mais informações, consulte o *guia do programador do Microsoft Jet Database Engine*.
