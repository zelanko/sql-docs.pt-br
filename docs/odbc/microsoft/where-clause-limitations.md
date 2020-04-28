---
title: Limitações da cláusula WHERE | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1699397db81d6fe702f60f6953fe7a0ae3726fe3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307557"
---
# <a name="where-clause-limitations"></a>Limitações da cláusula WHERE
O número máximo de cláusulas em uma cláusula WHERE é 40.  
  
 As colunas LONGVARBINARY e LONGVARCHAR podem ser comparadas com literais de até 255 caracteres de comprimento, mas não podem ser comparadas usando parâmetros.
