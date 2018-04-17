---
title: SQL_ARD_TYPE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data types [ODBC], pseudo-type identifiers
- pseudo-type identifiers [ODBC], SQL_ARD_TYPE
- SQL_ARD_TYPE [ODBC]
ms.assetid: 8d87ca10-f955-4284-8689-e9f4cc31e7ae
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7e021086561f0af45ddab1bd9ab777267ae515dd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sqlardtype"></a>SQL_ARD_TYPE
O identificador de tipo SQL_ARD_TYPE é usado para indicar que os dados em um buffer será do tipo especificado no campo SQL_DESC_CONCISE_TYPE da descartar. SQL_ARD_TYPE é inserido no *TargetType* argumento de uma chamada para **SQLGetData** em vez de um tipo de dados específico e permite que um aplicativo para alterar os dados de tipo de buffer alterando o descritor campo. Esse valor vincula o tipo de dados de  *\*TargetValuePtr* buffer para o campo do descritor. (SQL_ARD_TYPE não é inserido em uma chamada para **SQLBindCol** ou **SQLBindParameter** porque o tipo do buffer associado já está associado aos campos SQL_DESC_TYPE e SQL_DESC_CONCISE_TYPE e pode ser alterado a qualquer momento alterando esses campos.)  
  
 O identificador de tipo SQL_ARD_TYPE pode ser usado para especificar valores não padrão para precisão à esquerda e a precisão de segundos de tipos de dados de intervalo e tipo de precisão e escala de valores para os dados SQL_C_NUMERIC. Para obter mais informações, consulte [substituindo padrão à esquerda e a precisão de segundos para tipos de dados de intervalo](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md) e [substituindo padrão precisão e escala para tipos de dados numéricos](../../../odbc/reference/appendixes/overriding-default-precision-and-scale-for-numeric-data-types.md), mais adiante neste apêndice.
