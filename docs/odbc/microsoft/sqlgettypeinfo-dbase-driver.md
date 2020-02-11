---
title: SQLGetTypeInfo (driver do dBASE) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], dBASE Driver
- DBase driver [ODBC], SQLGetTypeInfo
ms.assetid: 6e9ce02b-97c7-4c1a-91e0-829df7459c84
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 43319f7f23741a1533321c9369077d42a2484395
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67898747"
---
# <a name="sqlgettypeinfo-dbase-driver"></a>SQLGetTypeInfo (Driver do dBASE)
> [!NOTE]  
>  Este tópico fornece informações específicas do driver do dBASE. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 O nome do tipo (TYPE_NAME) retornado na tabela produzida por **SQLGetTypeInfo** será o nome mais comumente usado pela fonte de dados.  
  
 SQL_ALL_EXCEPT_LIKE será retornado na coluna PESQUISÁvel para os tipos de dados byte, contador, duplo, único, longo e curto. (O recurso LIKE pode ser obtido convertendo o valor em um caractere usando as funções de conversão canônica ODBC e, em seguida, executando a comparação.)
