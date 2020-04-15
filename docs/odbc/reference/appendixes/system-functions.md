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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca71687887444cafc502c15683f3972cf6308e6b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302827"
---
# <a name="system-functions"></a>Funções de sistema
A tabela a seguir lista as funções do sistema incluídas no conjunto de funções escalares ODBC. Ao ligar para **o SQLGetInfo** com um tipo de *informação* de SQL_SYSTEM_FUNCTIONS, um aplicativo pode determinar quais funções do sistema são suportadas por um driver.  
  
 Argumentos apontados como *exp* podem ser o nome de uma coluna, resultado de outra função escalar, ou literal, onde o tipo de dados subjacente poderia ser representado como SQL_NUMERIC, SQL_DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_FLOAT, SQL_REAL, SQL_DOUBLE, SQL_TYPE_DATE, SQL_TYPE_TIME ou SQL_TYPE_TIMESTAMP.  
  
 Os argumentos apontados como *valor* podem ser uma constante literal, onde o tipo de dados subjacente pode ser representado como SQL_NUMERIC, SQL_DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_FLOAT, SQL_REAL, SQL_DOUBLE, SQL_TYPE_DATE, SQL_TYPE_TIME ou SQL_TYPE_TIMESTAMP.  
  
 Os valores devolvidos são representados como tipos de dados ODBC.  
  
|Função|Descrição|  
|--------------|-----------------|  
|**BANCO DE DADOS** (ODBC 1.0)|Retorna o nome do banco de dados correspondente à alça de conexão. (O nome do banco de dados também está disponível ligando para **SQLGetConnectOption** com a opção de conexão SQL_CURRENT_QUALIFIER.)|  
|**IFNULL** _(exp_,_valor)_**)** (ODBC 1.0)|Se *o exp* for nulo, *o valor* será devolvido. Se *exp* não for nulo, *exp* é devolvido. O possível tipo de dados ou tipos de *valor* deve ser compatível com o tipo de dados *de exp*.|  
|**(ODBC** 1.0)|Retorna o nome de usuário no DBMS. (O nome de usuário também está disponível por meio do **SQLGetInfo** especificando o tipo de informação: SQL_USER_NAME.) Isso pode ser diferente do nome de login.|
