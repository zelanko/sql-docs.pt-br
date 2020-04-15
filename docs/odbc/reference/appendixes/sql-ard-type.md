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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d7e28d6babb7db8364697ae62092256396b44914
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305027"
---
# <a name="sql_ard_type"></a>SQL_ARD_TYPE
O identificador de tipo SQL_ARD_TYPE é usado para indicar que os dados em um buffer serão do tipo especificado no campo SQL_DESC_CONCISE_TYPE do ARD. SQL_ARD_TYPE é inserida no argumento *TargetType* de uma chamada para **SQLGetData** em vez de um tipo de dados específico e permite que um aplicativo altere o tipo de dados do buffer alterando o campo descritor. Esse valor vincula o tipo de dados do * \*buffer TargetValuePtr* ao campo descritor. (SQL_ARD_TYPE não é inserida em uma chamada para **SQLBindCol** ou **SQLBindParameter** porque o tipo do buffer bound já está vinculado aos campos SQL_DESC_TYPE e SQL_DESC_CONCISE_TYPE e pode ser alterado a qualquer momento alterando qualquer um desses campos.)  
  
 O identificador de SQL_ARD_TYPE tipo pode ser usado para especificar valores não padrão para precisão líder e precisão de segundos de tipos de dados de intervalo, e valores de precisão e escala para o SQL_C_NUMERIC tipo de dados. Para obter mais informações, consulte [Sobreposição de padrões de liderança e precisão de segundos para tipos de dados de intervalo](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md) e [sobreposição de precisão e escala padrão para tipos de dados numéricos,](../../../odbc/reference/appendixes/overriding-default-precision-and-scale-for-numeric-data-types.md)mais tarde neste apêndice.
