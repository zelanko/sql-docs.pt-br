---
title: Resumo da interface do provedor de serviços ODBC | Microsoft Docs
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
ms.openlocfilehash: 0a97bed3bb921b9c881a98d8d9a9031ef7630f26
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68111901"
---
# <a name="odbc-service-provider-interface-summary"></a>Resumo da Interface do provedor de serviços do ODBC
A tabela a seguir descreve as funções de interface do provedor de serviços ODBC. Para obter mais informações sobre a sintaxe e a semântica para cada função, consulte [referência de SPI (interface do provedor de serviço) ODBC](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md).  
  
|Nome da função|Finalidade|  
|-------------------|-------------|  
|[SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|O mesmo que [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), mas define o atributo no token de informações de conexão em vez de no identificador de conexão.|  
|[SQLSetDriverConnectInfo](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|Define a cadeia de conexão no token de informações de conexão para a chamada [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) de um aplicativo.|  
|[SQLSetConnectInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Define a fonte de dados, a ID de usuário e a senha no token de informações de conexão para uma chamada de [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) de um aplicativo.|  
|[SQLGetPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Recupera a ID do pool.|  
|[SQLRateConnection](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Determina se um driver pode reutilizar uma conexão existente no pool de conexões.|  
|[SQLPoolConnect](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Crie uma nova conexão se nenhuma conexão no pool puder ser reutilizada.|  
|[SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Informa um driver que atingiu o tempo limite de uma ID de pool.|
