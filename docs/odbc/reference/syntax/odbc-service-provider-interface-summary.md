---
title: "Resumo de Interface de provedor de serviço ODBC | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ace6085b-355b-435b-8734-503fc3c12ec2
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 82610a48532970f14800574155db89929e371baf
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-service-provider-interface-summary"></a>Resumo de Interface de provedor de serviço ODBC
A tabela a seguir descreve as funções de interface de provedor de serviços de ODBC. Para obter mais informações sobre a sintaxe e semântica para cada função, consulte [referência de Interface de provedor de serviço do ODBC (IDA)](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md).  
  
|Nome da função|Finalidade|  
|-------------------|-------------|  
|[SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Mesmo que [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), mas ela define o atributo no token de informações de conexão em vez de no identificador da conexão.|  
|[SQLSetDriverConnectInfo](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|Define a cadeia de caracteres de conexão para o token de informações de conexão para um aplicativo [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) chamar.|  
|[SQLSetConnectInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Define a fonte de dados, ID de usuário e senha para o token de informações de conexão para um aplicativo [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) chamar.|  
|[SQLGetPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Recupera a ID do pool.|  
|[SQLRateConnection](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Determina se um driver pode reutilizar uma conexão existente no pool de conexão.|  
|[SQLPoolConnect](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Crie uma nova conexão se nenhuma conexão no pool pode ser reutilizada.|  
|[SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Informa um driver que uma ID do pool foi atingida.|
