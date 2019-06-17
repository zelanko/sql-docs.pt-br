---
title: ONDE limitações da cláusula | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, WHERE clause limitations
- WHERE clause limitations [ODBC]
ms.assetid: 46b54f74-e4a3-4318-87cf-8a97c38a2718
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e883d585db0fe11e92b188b2cfc26db9fff415fe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63057767"
---
# <a name="where-clause-limitations"></a>Limitações da cláusula WHERE
O número máximo de cláusulas em uma cláusula WHERE é 40.  
  
 Colunas LONGVARBINARY e LONGVARCHAR podem ser comparadas a literais de até 255 caracteres de comprimento, mas não podem ser comparadas usando parâmetros.
