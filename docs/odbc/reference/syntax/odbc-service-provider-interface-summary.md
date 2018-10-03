---
title: Resumo de Interface do provedor de serviço ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ace6085b-355b-435b-8734-503fc3c12ec2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e351f08a5e72966c92a7452872532b90e4127964
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47837464"
---
# <a name="odbc-service-provider-interface-summary"></a>Resumo da Interface do provedor de serviços do ODBC
A tabela a seguir descreve as funções de interface de provedor de serviços do ODBC. Para obter mais informações sobre a sintaxe e semântica para cada função, consulte [referência de Interface de provedor de serviço de ODBC (SPI)](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md).  
  
|Nome da função|Finalidade|  
|-------------------|-------------|  
|[SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Mesmo que [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), mas ele define o atributo no token de informações de conexão em vez de no identificador de conexão.|  
|[SQLSetDriverConnectInfo](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|Define a cadeia de caracteres de conexão para o token de informações de conexão para um aplicativo [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) chamar.|  
|[SQLSetConnectInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Define a fonte de dados, ID de usuário e senha para o token de informações de conexão para um aplicativo [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) chamar.|  
|[SQLGetPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Recupera a ID do pool.|  
|[SQLRateConnection](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Determina se um driver pode reutilizar uma conexão existente no pool de conexão.|  
|[SQLPoolConnect](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Crie uma nova conexão se nenhuma conexão no pool pode ser reutilizada.|  
|[SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Informa um driver que uma ID do pool foi atingida.|
