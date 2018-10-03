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
ms.openlocfilehash: 048db455419d2b74658b758f3a3c525b02bf37f3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47811404"
---
# <a name="system-functions"></a>Funções de sistema
A tabela a seguir lista as funções do sistema que estão incluídas no conjunto de função escalar ODBC. Chamando **SQLGetInfo** com um *tipo de informação* de SQL_SYSTEM_FUNCTIONS, um aplicativo pode determinar quais funções de sistema são suportadas por um driver.  
  
 Argumentos denotado como *exp* pode ser o nome de uma coluna, o resultado de outra função escalar ou um literal, onde o tipo de dados poderia ser representado como SQL_NUMERIC, SQL_DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL _BIGINT, SQL_FLOAT, SQL_REAL, SQL_DOUBLE, SQL_TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP.  
  
 Argumentos denotado como *valor* pode ser uma constante literal, onde o tipo de dados subjacente pode ser representado como SQL_NUMERIC, SQL_DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_FLOAT, SQL_REAL, SQL_DOUBLE, SQL _ TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP.  
  
 Valores retornados são representados como tipos de dados ODBC.  
  
|Função|Description|  
|--------------|-----------------|  
|**() DO BANCO DE DADOS** (ODBC 1.0)|Retorna o nome do banco de dados correspondente ao identificador de conexão. (O nome do banco de dados também está disponível por meio da chamada **SQLGetConnectOption** com a opção de conexão SQL_CURRENT_QUALIFIER.)|  
|**IFNULL (** *exp*,*valor * * *)** (ODBC 1.0)|Se *exp* for nulo, *valor* é retornado. Se *exp* não for nulo, *exp* é retornado. O tipo de dados possíveis ou tipos de *valor* deve ser compatível com o tipo de dados *exp*.|  
|**(USUÁRIO)** (ODBC 1.0)|Retorna o nome de usuário no DBMS. (O nome de usuário também está disponível por meio de **SQLGetInfo** especificando o tipo de informação: SQL_USER_NAME.) Isso pode ser diferente do nome de logon.|
