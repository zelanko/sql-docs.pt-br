---
title: Funções do sistema | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- system functions [ODBC]
- functions [ODBC], system functions
ms.assetid: 36614b4c-e037-43ef-8692-67f4861b144d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5870cb445d7afd098aba32ffd9be7a88c048bae5
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/18/2018
ms.locfileid: "53591510"
---
# <a name="system-functions"></a>Funções de sistema
A tabela a seguir lista as funções do sistema que estão incluídas no conjunto de função escalar ODBC. Chamando **SQLGetInfo** com um *tipo de informação* de SQL_SYSTEM_FUNCTIONS, um aplicativo pode determinar quais funções de sistema são suportadas por um driver.  
  
 Argumentos denotado como *exp* pode ser o nome de uma coluna, o resultado de outra função escalar ou um literal, onde o tipo de dados poderia ser representado como SQL_NUMERIC, SQL_DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL _BIGINT, SQL_FLOAT, SQL_REAL, SQL_DOUBLE, SQL_TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP.  
  
 Argumentos denotado como *valor* pode ser uma constante literal, onde o tipo de dados subjacente pode ser representado como SQL_NUMERIC, SQL_DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_FLOAT, SQL_REAL, SQL_DOUBLE, SQL _ TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP.  
  
 Valores retornados são representados como tipos de dados ODBC.  
  
|Função|Descrição|  
|--------------|-----------------|  
|**() DO BANCO DE DADOS** (ODBC 1.0)|Retorna o nome do banco de dados correspondente ao identificador de conexão. (O nome do banco de dados também está disponível por meio da chamada **SQLGetConnectOption** com a opção de conexão SQL_CURRENT_QUALIFIER.)|  
|**IFNULL (** _exp_,_valor_**)** (ODBC 1.0)|Se *exp* for nulo, *valor* é retornado. Se *exp* não for nulo, *exp* é retornado. O tipo de dados possíveis ou tipos de *valor* deve ser compatível com o tipo de dados *exp*.|  
|**(USUÁRIO)** (ODBC 1.0)|Retorna o nome de usuário no DBMS. (O nome de usuário também está disponível por meio de **SQLGetInfo** , especificando o tipo de informações: SQL_USER_NAME.) Isso pode ser diferente do nome de logon.|
