---
title: SQLDriverConnect | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLDriverConnect function
ms.assetid: a1e38e2c-3a97-42d1-9c45-a0ca3282ffd1
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9a76a653277b7f99ecf88c3b0277617eb053a41c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73787100"
---
# <a name="sqldriverconnect"></a>SQLDriverConnect
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O driver ODBC para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client define atributos de conexão que substituem ou aprimoram palavras-chave de cadeia de conexão. Várias palavras-chave de cadeia de conexão têm valores padrão especificados pelo driver ODBC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 Para obter uma lista das palavras-chave disponíveis no driver [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC do Native Client, consulte [usando palavras-chave da cadeia de conexão com o SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Para obter mais informações [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sobre atributos de conexão e comportamentos padrão de driver, consulte [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md).  
  
 Para obter uma discussão sobre palavras-chave da cadeia de conexão que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são válidas para o Native Client, consulte [usando palavras-chave da cadeia de conexão com SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Quando o valor do parâmetro **SQLDriverConnect**_DriverCompletion_ é SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE ou SQL_DRIVER_COMPLETE_REQUIRED, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client recupera os valores da palavra-chave da caixa de diálogo exibida. Se o valor de palavra-chave for transmitido na cadeia de caracteres da conexão e o usuário não alterar o valor para a palavra-chave na caixa de diálogo, o driver ODBC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client usará o valor da cadeia de caracteres da conexão. Se o valor não for definido na cadeia de caracteres da conexão e o usuário não fizer nenhuma atribuição na caixa de diálogo, o driver usará o padrão.  
  
 **SQLDriverConnect** deve receber um *WindowHandle* válido quando qualquer valor de *DriverCompletion* exigir (ou pode exigir) a exibição da caixa de diálogo de conexão do driver. Um identificador inválido retorna SQL_ERROR.  
  
 Especifique as palavras-chave DRIVER ou DSN. O ODBC declara que um driver usa a que está mais à esquerda dessas duas palavras-chave e ignora a outra se ambas estão especificadas. Se o DRIVER for especificado, ou for o mais à esquerda dos dois, e o valor do parâmetro **SQLDriverConnect**_DriverCompletion_ for SQL_DRIVER_NOPROMPT, a palavra-chave do servidor e um valor apropriado serão necessários.  
  
 Quando SQL_DRIVER_NOPROMPT é especificado, as palavras-chave de autenticação de usuário devem estar presentes com valores. O driver assegura que a cadeia de caracteres "Trusted_Connection=yes" ou as palavras-chave UID e PWD estão presentes.  
  
 Se o valor do parâmetro *DriverCompletion* for SQL_DRIVER_NOPROMPT ou SQL_DRIVER_COMPLETE_REQUIRED e o idioma ou o banco de dados vier da cadeia de conexão e for inválido, o **SQLDriverConnect** retornará SQL_ERROR.  
  
 Se o valor do parâmetro *DriverCompletion* for SQL_DRIVER_NOPROMPT ou SQL_DRIVER_COMPLETE_REQUIRED e o idioma ou o banco de dados vierem das definições de fonte de dado ODBC e forem inválidos, **SQLDriverConnect** usará o idioma ou o banco padrão para a ID de usuário especificada e retornará SQL_SUCCESS_WITH_INFO.  
  
 Se o valor do parâmetro *DriverCompletion* for SQL_DRIVER_COMPLETE ou SQL_DRIVER_PROMPT e se o idioma ou o banco de dados for inválido, o **SQLDriverConnect** reexibirá a caixa de diálogo.  
  
## <a name="sqldriverconnect-support-for-high-availability-disaster-recovery"></a>Suporte de SQLDriverConnect à alta disponibilidade e recuperação de desastre  
 Para obter mais informações sobre como usar o **SQLDriverConnect** para [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] se conectar a um cluster, consulte [suporte a SQL Server Native Client para alta disponibilidade e recuperação de desastre](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).  
  
## <a name="sqldriverconnect-support-for-service-principal-names-spns"></a>Suporte de SQLDriverConnect a SPNs (nomes de entidade de serviço)  
 O SQLDDriverConnect usará a caixa de diálogo logon do ODBC boxwhen solicitação está habilitada. Isto permite que os SPNs sejam inseridos no servidor principal e no seu parceiro de failover.  
  
 O SQLDriverConnect aceitará as novas palavras-chave de cadeia de conexão **ServerSPN** e **FailoverPartnerSPN**e reconhecerá os novos atributos de conexão SQL_COPT_SS_SERVER_SPN e SQL_COPT_SS_FAILOVER_PARTNER_SPN.  
  
 Quando um valor de atributo de conexão é especificado mais de uma vez, um valor definido programaticamente tem precedência sobre o valor em um DSN e um valor em uma cadeia de caracteres de conexão. Um valor em um DSN tem precedência sobre um valor em uma cadeia de caracteres de conexão.  
  
 Quando uma conexão é aberta, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client define SQL_COPT_SS_MUTUALLY_AUTHENTICATED e SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD como o método de autenticação usado para abrir a conexão.  
  
 Para obter mais informações sobre SPNs, consulte [nomes de entidade de serviço &#40;SPNs&#41; em conexões de cliente &#40;&#41;ODBC ](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md).  
  
## <a name="examples"></a>Exemplos  
 A chamada a seguir ilustra a quantidade mínima de dados necessária para **SQLDriverConnect**:  
  
```  
SQLDriverConnect(hdbc, hwnd,  
    (SQLTCHAR*) TEXT("DRIVER={SQL Server Native Client 10};"), SQL_NTS, szOutConn,  
    MAX_CONN_OUT, &cbOutConn, SQL_DRIVER_COMPLETE);  
```  
  
 As seguintes cadeias de conexão ilustram os dados mínimos necessários quando o valor do parâmetro *DriverCompletion* é SQL_DRIVER_NOPROMPT:  
  
```  
"DSN=Human Resources;Trusted_Connection=yes"  
  
"FILEDSN=HR_FDSN;Trusted_Connection=yes"  
  
"DRIVER={SQL Server Native Client 10};SERVER=(local);Trusted_Connection=yes"  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLDriverConnect](https://go.microsoft.com/fwlink/?LinkId=59340)   
 [Detalhes de implementação da API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)  
  
  
