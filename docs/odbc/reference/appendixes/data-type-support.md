---
title: Suporte ao tipo de dados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- data types [ODBC], ODBC drivers
- ODBC drivers [ODBC], data types
ms.assetid: 782b4490-372b-4366-aad7-a486fb8a07c8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3abfe85ee32fb9ff4a8499c9949c0685563fec70
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284423"
---
# <a name="data-type-support"></a>Suporte do tipo de dados
Os motoristas da ODBC devem suportar pelo menos um de SQL_CHAR e SQL_VARCHAR. O suporte para outros tipos de dados é determinado pelo nível de conformidade SQL-92 do driver ou da fonte de dados. Um aplicativo deve ligar para **o SQLGetTypeInfo** para determinar os tipos de dados suportados pelo driver.  
  
 Para obter mais informações sobre os tipos de dados, consulte [o apêndice D: Tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).
