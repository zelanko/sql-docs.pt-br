---
title: SQLDriverConnect | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLDriverConnect function
ms.assetid: a1e38e2c-3a97-42d1-9c45-a0ca3282ffd1
caps.latest.revision: 60
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 117c8afa4b8dc406067105013b1c45282f905e23
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2018
ms.locfileid: "35696597"
---
# <a name="sqldriverconnect"></a>SQLDriverConnect
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  O driver ODBC para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client define atributos de conexão que substituem ou aprimoram palavras-chave de cadeia de conexão. Várias palavras-chave de cadeia de conexão têm valores padrão especificados pelo driver ODBC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 Para obter uma lista de palavras-chave disponíveis no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o driver ODBC Native Client, consulte [usando Conexão String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Para obter mais informações sobre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atributos de conexão e comportamentos padrão do driver, consulte [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md).  
  
 Para obter uma discussão de conexão cadeia palavras-chave que são válidos para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, consulte [usando Conexão String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Quando o **SQLDriverConnect * DriverCompletion* valor do parâmetro é SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE ou SQL_DRIVER_COMPLETE_REQUIRED, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client recupera valores de palavra-chave das caixa de diálogo exibida. Se o valor de palavra-chave for transmitido na cadeia de caracteres da conexão e o usuário não alterar o valor para a palavra-chave na caixa de diálogo, o driver ODBC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client usará o valor da cadeia de caracteres da conexão. Se o valor não for definido na cadeia de caracteres da conexão e o usuário não fizer nenhuma atribuição na caixa de diálogo, o driver usará o padrão.  
  
 **SQLDriverConnect** deve ser fornecido um válido *WindowHandle* quando qualquer *DriverCompletion* valor exige (ou pode exigir) a exibição da caixa de diálogo de conexão do driver. Um identificador inválido retorna SQL_ERROR.  
  
 Especifique as palavras-chave DRIVER ou DSN. O ODBC declara que um driver usa a que está mais à esquerda dessas duas palavras-chave e ignora a outra se ambas estão especificadas. Se o DRIVER for especificado ou estiver mais à esquerda dos dois e o **SQLDriverConnect * DriverCompletion* o valor do parâmetro for SQL_DRIVER_NOPROMPT, a palavra-chave do servidor e um valor apropriado são necessários.  
  
 Quando SQL_DRIVER_NOPROMPT é especificado, as palavras-chave de autenticação de usuário devem estar presentes com valores. O driver assegura que a cadeia de caracteres "Trusted_Connection=yes" ou as palavras-chave UID e PWD estão presentes.  
  
 Se o *DriverCompletion* o valor do parâmetro for SQL_DRIVER_NOPROMPT ou SQL_DRIVER_COMPLETE_REQUIRED e o idioma ou o banco de dados proveniente da cadeia de conexão e uma for inválido, **SQLDriverConnect**retornará SQL_ERROR.  
  
 Se o *DriverCompletion* o valor do parâmetro for SQL_DRIVER_NOPROMPT ou SQL_DRIVER_COMPLETE_REQUIRED e o idioma ou o banco de dados provenientes de definições de fonte de dados ODBC e uma for inválido, **SQLDriverConnect**  usa o idioma padrão ou o banco de dados para a ID de usuário especificada e retorna SQL_SUCCESS_WITH_INFO.  
  
 Se o *DriverCompletion* o valor do parâmetro é SQL_DRIVER_COMPLETE ou SQL_DRIVER_PROMPT e se o idioma ou o banco de dados é inválido, **SQLDriverConnect** exibe novamente a caixa de diálogo.  
  
## <a name="sqldriverconnect-support-for-high-availability-disaster-recovery"></a>Suporte de SQLDriverConnect à alta disponibilidade e recuperação de desastre  
 Para obter mais informações sobre como usar **SQLDriverConnect** para se conectar a um [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] de cluster, consulte [SQL Server Native Client Support for High Availability, Disaster Recovery](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).  
  
## <a name="sqldriverconnect-support-for-service-principal-names-spns"></a>Suporte de SQLDriverConnect a SPNs (nomes de entidade de serviço)  
 SQLDDriverConnect usará o logon do ODBC diálogo quando for solicitado. Isto permite que os SPNs sejam inseridos no servidor principal e no seu parceiro de failover.  
  
 SQLDriverConnect aceitará as palavras-chave cadeia de caracteres de conexão nova **ServerSPN** e **FailoverPartnerSPN**e reconhecerá os novos atributos de conexão SQL_COPT_SS_SERVER_SPN e SQL_COPT_SS_ FAILOVER_PARTNER_SPN.  
  
 Quando um valor de atributo de conexão é especificado mais de uma vez, um valor definido programaticamente tem precedência sobre o valor em um DSN e um valor em uma cadeia de caracteres de conexão. Um valor em um DSN tem precedência sobre um valor em uma cadeia de caracteres de conexão.  
  
 Quando uma conexão é aberta, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client define SQL_COPT_SS_MUTUALLY_AUTHENTICATED e SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD como o método de autenticação usado para abrir a conexão.  
  
 Para obter mais informações sobre os SPNs, consulte [nomes da entidade de serviço &#40;SPNs&#41; em conexões de cliente &#40;ODBC&#41;](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md).  
  
## <a name="examples"></a>Exemplos  
 A chamada a seguir ilustra a menor quantidade de dados necessários para **SQLDriverConnect**:  
  
```  
SQLDriverConnect(hdbc, hwnd,  
    (SQLTCHAR*) TEXT("DRIVER={SQL Server Native Client 10};"), SQL_NTS, szOutConn,  
    MAX_CONN_OUT, &cbOutConn, SQL_DRIVER_COMPLETE);  
```  
  
 As cadeias de conexão a seguir ilustram o mínimo necessário de dados quando o *DriverCompletion* o valor do parâmetro é SQL_DRIVER_NOPROMPT:  
  
```  
"DSN=Human Resources;Trusted_Connection=yes"  
  
"FILEDSN=HR_FDSN;Trusted_Connection=yes"  
  
"DRIVER={SQL Server Native Client 10};SERVER=(local);Trusted_Connection=yes"  
```  
  
## <a name="see-also"></a>Consulte também  
 [Função SQLDriverConnect](http://go.microsoft.com/fwlink/?LinkId=59340)   
 [Detalhes de implementação de API de ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)  
  
  
