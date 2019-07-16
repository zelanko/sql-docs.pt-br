---
title: SQL_ARD_TYPE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], pseudo-type identifiers
- pseudo-type identifiers [ODBC], SQL_ARD_TYPE
- SQL_ARD_TYPE [ODBC]
ms.assetid: 8d87ca10-f955-4284-8689-e9f4cc31e7ae
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 802040851259a8537fabcd3cc0da1afdf9b8dbe0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68057047"
---
# <a name="sqlardtype"></a>SQL_ARD_TYPE
O identificador de tipo SQL_ARD_TYPE é usado para indicar que os dados em um buffer será do tipo especificado no campo SQL_DESC_CONCISE_TYPE da descartar. SQL_ARD_TYPE é inserido na *TargetType* argumento de uma chamada para **SQLGetData** em vez de um tipo de dados específico e permite que um aplicativo para alterar os dados de tipo de buffer, alterando o descritor de campo. Esse valor vincula o tipo de dados do  *\*TargetValuePtr* buffer para o campo do descritor. (SQL_ARD_TYPE não é inserido em uma chamada para **SQLBindCol** ou **SQLBindParameter** porque o tipo de buffer associado já está vinculado aos campos SQL_DESC_TYPE e SQL_DESC_CONCISE_TYPE e pode ser alterado a qualquer momento alterando qualquer um desses campos.)  
  
 O identificador de tipo SQL_ARD_TYPE pode ser usado para especificar valores não padrão para precisão à esquerda e a precisão de segundos de intervalo de tipos de dados e digite valores de precisão e escala para os dados SQL_C_NUMERIC. Para obter mais informações, consulte [substituindo padrão à esquerda e a precisão de segundos para tipos de dados de intervalo](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md) e [substituindo padrão precisão e escala para tipos de dados numéricos](../../../odbc/reference/appendixes/overriding-default-precision-and-scale-for-numeric-data-types.md), mais adiante neste apêndice.
