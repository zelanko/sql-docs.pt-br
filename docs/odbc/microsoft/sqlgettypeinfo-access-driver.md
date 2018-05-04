---
title: SQLGetTypeInfo (Driver de acesso) | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLGetTypeInfo
- SQLGetTypeInfo function [ODBC], Access Driver
ms.assetid: a28b16eb-ca36-4297-9297-ecd7c107a84e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5b15ab4faf590850a79317ad5c4cd83342b2b707
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgettypeinfo-access-driver"></a>SQLGetTypeInfo (Driver de acesso)
> [!NOTE]  
>  Este tópico fornece informações específicas de Driver de acesso. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 O nome do tipo (TYPE_NAME) retornado na tabela produzida pela **SQLGetTypeInfo** será o nome mais comumente usado pela fonte de dados.  
  
 SQL_ALL_EXCEPT_LIKE será retornado na coluna PESQUISÁVEL por Byte, contador, Double, tipos de dados único, longa e curta. (O recurso LIKE pode ser obtido ao converter o valor para um caractere usando as funções de conversão canônica ODBC, em seguida, executar a comparação.)
