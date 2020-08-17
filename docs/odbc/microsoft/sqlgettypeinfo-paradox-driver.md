---
description: SQLGetTypeInfo (Driver do Paradox)
title: SQLGetTypeInfo (driver do Paradox) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLGetTypeInfo
ms.assetid: e65063c7-ba9e-4cf0-ac13-4bb5bd2937db
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bedb9170ba18b04e47f9e56bdc47098b9182f8b2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339942"
---
# <a name="sqlgettypeinfo-paradox-driver"></a>SQLGetTypeInfo (Driver do Paradox)
> [!NOTE]  
>  Este tópico fornece informações específicas do driver do Paradox. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 O nome do tipo (TYPE_NAME) retornado na tabela produzida por **SQLGetTypeInfo** será o nome mais comumente usado pela fonte de dados.  
  
 SQL_ALL_EXCEPT_LIKE será retornado na coluna PESQUISÁvel para os tipos de dados byte, contador, duplo, único, longo e curto. (O recurso LIKE pode ser obtido convertendo o valor em um caractere usando as funções de conversão canônica ODBC e, em seguida, executando a comparação.)
