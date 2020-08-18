---
description: SQL_ARD_TYPE
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
ms.openlocfilehash: 826b5aa2ff103a2c2868a6bc1dc09fb8cad40382
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483159"
---
# <a name="sql_ard_type"></a>SQL_ARD_TYPE
O identificador de tipo de SQL_ARD_TYPE é usado para indicar que os dados em um buffer serão do tipo especificado no campo SQL_DESC_CONCISE_TYPE do ARD. SQL_ARD_TYPE é inserido no argumento *TargetType* de uma chamada para **SQLGetData** em vez de um tipo de dados específico e permite que um aplicativo altere o tipo de dados do buffer alterando o campo do descritor. Esse valor vincula o tipo de dados do buffer * \* TargetValuePtr* ao campo de descritor. (SQL_ARD_TYPE não é inserido em uma chamada para **SQLBindCol** ou **SQLBindParameter** porque o tipo do buffer associado já está vinculado aos campos SQL_DESC_TYPE e SQL_DESC_CONCISE_TYPE e pode ser alterado a qualquer momento, alterando qualquer um desses campos.)  
  
 O identificador de tipo de SQL_ARD_TYPE pode ser usado para especificar valores não padrão para a precisão de precisão e de segundos dos tipos de dados de intervalo e os valores de precisão e escala para o tipo de dados SQL_C_NUMERIC. Para obter mais informações, consulte [substituindo a precisão padrão inicial e de segundos para tipos de dados de intervalo](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md) e [substituindo a precisão e a escala padrão para tipos de dados numéricos](../../../odbc/reference/appendixes/overriding-default-precision-and-scale-for-numeric-data-types.md), posteriormente neste apêndice.
