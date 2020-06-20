---
title: SPNs (nomes da entidade de serviço) no cliente ODBC
description: Saiba mais sobre atributos e funções ODBC que dão suporte a SPNs (nomes de entidade de serviço) em aplicativos cliente.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 1d60cb30-4c46-49b2-89ab-701e77a330a2
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 77db02433bfc67f348a5fbac6c195e76bbd1d69a
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84950259"
---
# <a name="service-principal-names-spns-in-client-connections-odbc"></a>SPNs (Nomes da Entidade de Serviço) em conexões de cliente (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Este tópico descreve atributos e funções ODBC que dão suporte a SPNs (nomes de entidades de serviço) em aplicativos cliente. Para obter mais informações sobre SPNs em aplicativos cliente, consulte [nome da entidade de serviço &#40;SPN&#41; suporte em conexões de cliente](../../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md) e [obter autenticação Kerberos mútua](../../../relational-databases/native-client-odbc-how-to/get-mutual-kerberos-authentication.md).  
  
## <a name="connection-string-keywords"></a>Palavras-chave de cadeia de conexão  
 As palavras-chave de cadeia de conexão a seguir permitem que aplicativos cliente especifiquem um SPN.  
  
|Palavra-chave|Valor|  
|-------------|-----------|  
|**ServerSPN**|O SPN do servidor. O valor padrão é uma cadeia de caracteres vazia, que faz com que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client use o SPN padrão gerado pelo driver.|  
|**FailoverPartnerSPN**|O SPN do parceiro de failover. O valor padrão é uma cadeia de caracteres vazia, que faz com que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client use o SPN padrão gerado pelo driver.|  
  
## <a name="connection-attributes"></a>Atributos de conexão  
 Os atributos de conexão a seguir permitem que aplicativos cliente especifiquem um SPN e consultem o método de autenticação.  
  
|Nome|Type|Uso|  
|----------|----------|-----------|  
|SQL_COPT_SS_SERVER_SPN<br /><br /> SQL_COPT_SS_FAILOVER_PARTNER_SPN|SQLTCHAR, leitura/gravação|Especifica o SPN do servidor. O valor padrão é uma cadeia de caracteres vazia, que faz com que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client use o SPN padrão gerado pelo driver.<br /><br /> Esse atributo só poderá ser consultado depois que for definido por meio de programação ou depois que uma conexão for aberta. Se for feita uma tentativa de consultar esse atributo em uma conexão que não esteja aberta e o atributo não tiver sido definido por meio de programação, SQL_ERROR será retornado e um registro de diagnóstico será registrado com SQLState 08003 e uma mensagem informando que a conexão não está aberta.<br /><br /> Se for feita uma tentativa de definir esse atributo quando uma conexão estiver aberta, SQL_ERROR será retornado e um registro de diagnóstico será registrado com SQLState HY011 e uma mensagem informando que a operação não é válida no momento.|  
|SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD|SQLTCHAR, somente leitura|Retorna o método de autenticação usado para a conexão. O valor retornado ao aplicativo é o valor que o Windows retorna ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Os valores possíveis são:<br /><br /> "NTLM", que é retornado quando uma conexão é aberta usando a autenticação NTLM.<br /><br /> "Kerberos", que é retornado quando uma conexão é aberta usando a autenticação Kerberos.<br /><br /> <br /><br /> Esse atributo só pode ser lido para uma conexão aberta que usou a Autenticação do Windows. Se for feita uma tentativa de lê-lo antes da abertura de uma conexão, SQL_ERROR será retornado e um erro será registrado com SQLState 08003 e uma mensagem que informa que a conexão não está aberta.<br /><br /> Se esse atributo for consultado em uma conexão que não usou a Autenticação do Windows, será retornado SQL_ERROR e um erro será registrado com SQLState HY092 e a mensagem de identificador de atributo/opção inválido (SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD só está disponível para conexões confiáveis).<br /><br /> Se o método de autenticação não puder ser determinado, SQL_ERROR será retornado e um erro será registrado com SQLState HY000 e uma mensagem de erro geral.|  
|SQL_COPT_SS_MUTUALLY_AUTHENTICATED|SQLSMALLINT, somente leitura|Retornará SQL_TRUE se o servidor na conexão tiver sido autenticado mutuamente; caso contrário, retornará SQL_FALSE.<br /><br /> Esse atributo só pode ser lido para uma conexão aberta. Se for feita uma tentativa de lê-lo antes da abertura de uma conexão, SQL_ERROR será retornado e um erro será registrado com SQLState 08003 e uma mensagem que informa que a conexão não está aberta.<br /><br /> Se esse atributo for consultado para uma conexão que não usou a Autenticação do Windows, será retornado SQL_FALSE.|  
  
## <a name="odbc-function-support-for-specifying-spns"></a>Suporte de funções ODBC para especificação de SPNs  
 As seguintes funções ODBC oferecem suporte a aplicativos cliente e SPNs:  
  
-   [SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)  
  
-   [SQLConnect](../../../relational-databases/native-client-odbc-api/sqlconnect.md)  
  
-   [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md)  
  
-   [SQLGetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md)  
  
-   [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Native Client &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
