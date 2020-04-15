---
title: ONDE Limitações de Cláusulas | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307557"
---
# <a name="where-clause-limitations"></a>Limitações da cláusula WHERE
O número máximo de cláusulas em uma cláusula WHERE é 40.  
  
 As colunas LONGVARBINARY e LONGVARCHAR podem ser comparadas a literais de até 255 caracteres de comprimento, mas não podem ser comparadas usando parâmetros.
