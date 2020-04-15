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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b2f7e459cc7b89106bf1b7ebcd49c699d43da9f6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298893"
---
# <a name="odbc-service-provider-interface-summary"></a>Resumo da Interface do provedor de serviços do ODBC
A tabela a seguir descreve as funções de interface do Provedor de Serviços ODBC. Para obter mais informações sobre a sintaxe e semântica para cada função, consulte [A Referência do Provedor de Serviços ODBC (SPI).](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)  
  
|Nome da função|Finalidade|  
|-------------------|-------------|  
|[SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|O mesmo que [SQLSetConnectAttr,](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)mas ele define o atributo no token de informações de conexão em vez de no cabo de conexão.|  
|[SqlSetDriverConnectInfo](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|Define a seqüência de conexões no token de informações de conexão para a chamada [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) de um aplicativo.|  
|[SQLSetConnectInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Define a fonte de dados, o ID do usuário e a senha no token de informações de conexão para a chamada [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) de um aplicativo.|  
|[Sqlgetpoolid](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Recupera a id da piscina.|  
|[Conexão SQLRate](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Determina se um driver pode reutilizar uma conexão existente no pool de conexão.|  
|[SQLpoolConnect](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Crie uma nova conexão se nenhuma conexão no pool puder ser reutilizada.|  
|[SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Informa um motorista que uma ida de bilhar foi cronometrada.|
