---
title: SQLGetTypeInfo (Driver do Paradox) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 20b5776b5b0e1490ef31ff07d1876afef326db9b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47711478"
---
# <a name="sqlgettypeinfo-paradox-driver"></a>SQLGetTypeInfo (Driver do Paradox)
> [!NOTE]  
>  Este tópico fornece informações específicas de Driver do Paradox. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 O nome do tipo (TYPE_NAME) retornado na tabela produzida pelo **SQLGetTypeInfo** será o nome mais comumente usado pela fonte de dados.  
  
 SQL_ALL_EXCEPT_LIKE será retornado na coluna PESQUISÁVEL por Byte, contador, Double, tipos de dados único, longa e curta. (A capacidade de LIKE pode ser obtida ao converter o valor em um caractere usando as funções de conversão canônico do ODBC e, em seguida, executar a comparação.)
