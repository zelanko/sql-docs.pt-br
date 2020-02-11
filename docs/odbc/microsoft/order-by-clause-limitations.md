---
title: Limitações da cláusula ORDER BY | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, ORDER BY clause limitations
- ORDER BY clause limitations [ODBC]
ms.assetid: fd4ddc7c-9c7e-4a0c-a781-e5427dfb2e18
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b58afff444c09622027f50a87bd77fcd6ed45640
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68100775"
---
# <a name="order-by-clause-limitations"></a>Limitações da cláusula ORDER BY
Se uma instrução SELECT contiver uma cláusula GROUP BY e uma cláusula ORDER BY, a cláusula ORDER BY poderá conter apenas uma coluna no conjunto de resultados ou uma expressão na cláusula GROUP BY.
