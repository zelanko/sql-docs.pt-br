---
title: "COMO as limitações de predicado | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- LIKE predicate limitations [ODBC]
- ODBC SQL grammar, LIKE predicate limitations
ms.assetid: dbd39099-caf6-4c4c-9ad8-f6c63c1bd5e4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5668f03e785c0d27133965f16af40ce69c2a2567
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="like-predicate-limitations"></a>COMO as limitações de predicado
Se os dados em uma coluna são maiores que 255 caracteres, a comparação LIKE se baseará apenas os primeiros 255 caracteres.  
  
 Um tipo usado em um procedimento tem suporte apenas com padrões constantes. Os Drivers de banco de dados de área de trabalho oferecem suporte a SQL-92 como correspondência de padrões.  
  
 Não há suporte para o uso de uma cláusula de escape em um predicado LIKE.  
  
 Uma comparação LIKE não deve ser executada em uma coluna que contém dados de um tipo de dados numérico ou float. Os resultados podem ser imprevisíveis. Para obter mais informações, consulte o *guia do programador do Microsoft Jet Database Engine*.
