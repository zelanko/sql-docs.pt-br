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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8d1455f0b91313ea137ec9c13a2d318fba0807b3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302535"
---
# <a name="sqldriverconnect"></a>SQLDriverConnect
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O driver ODBC para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client define atributos de conexão que substituem ou aprimoram palavras-chave de cadeia de conexão. Várias palavras-chave de cadeia de conexão têm valores padrão especificados pelo driver ODBC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 Para obter uma lista das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] palavras-chave disponíveis no driver ODBC do cliente nativo, consulte [Usando palavras-chave de string de conexão com o Cliente Nativo do Servidor SQL](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Para obter [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mais informações sobre atributos de conexão e comportamentos padrão do driver, consulte [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md).  
  
 Para uma discussão sobre palavras-chave [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de seqüência de conexão válidas para o Cliente Nativo, consulte [Usando palavras-chave de seqüência de conexão com o Cliente Nativo do Servidor SQL](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Quando o valor do parâmetro **SQLDriverConnect**_DriverConclusão_ é [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE ou SQL_DRIVER_COMPLETE_REQUIRED, o driver ODBC do Cliente Nativo recupera valores de palavras-chave da caixa de diálogo exibida. Se o valor de palavra-chave for transmitido na cadeia de caracteres da conexão e o usuário não alterar o valor para a palavra-chave na caixa de diálogo, o driver ODBC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client usará o valor da cadeia de caracteres da conexão. Se o valor não for definido na cadeia de caracteres da conexão e o usuário não fizer nenhuma atribuição na caixa de diálogo, o driver usará o padrão.  
  
 **O SQLDriverConnect** deve receber uma *janela válida* quando qualquer valor de Conclusão *de Driver* exigir (ou pode exigir) a exibição da caixa de diálogo de conexão do driver. Um identificador inválido retorna SQL_ERROR.  
  
 Especifique as palavras-chave DRIVER ou DSN. O ODBC declara que um driver usa a que está mais à esquerda dessas duas palavras-chave e ignora a outra se ambas estão especificadas. Se driver for especificado ou for o mais à esquerda dos dois, e o valor do parâmetro **SQLDriverConnect**_DriverConclusão_ for SQL_DRIVER_NOPROMPT, a palavra-chave SERVER e um valor apropriado são necessários.  
  
 Quando SQL_DRIVER_NOPROMPT é especificado, as palavras-chave de autenticação de usuário devem estar presentes com valores. O driver assegura que a cadeia de caracteres "Trusted_Connection=yes" ou as palavras-chave UID e PWD estão presentes.  
  
 Se o valor do parâmetro *DriverComplet* for SQL_DRIVER_NOPROMPT ou SQL_DRIVER_COMPLETE_REQUIRED e o idioma ou banco de dados vier da seqüência de conexões e for inválido, **o SQLDriverConnect** retorna SQL_ERROR.  
  
 Se o valor do parâmetro *DriverComplet* for SQL_DRIVER_NOPROMPT ou SQL_DRIVER_COMPLETE_REQUIRED e o idioma ou banco de dados vier das definições de origem de dados do ODBC e for inválido, o **SQLDriverConnect** usará o idioma ou banco de dados padrão para o ID do usuário especificado e retorna SQL_SUCCESS_WITH_INFO.  
  
 Se o valor do parâmetro *DriverComplet* for SQL_DRIVER_COMPLETE ou SQL_DRIVER_PROMPT e se o idioma ou o banco de dados for inválido, o **SQLDriverConnect** reexibirá a caixa de diálogo.  
  
## <a name="sqldriverconnect-support-for-high-availability-disaster-recovery"></a>Suporte de SQLDriverConnect à alta disponibilidade e recuperação de desastre  
 Para obter mais informações sobre como usar [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] **o SQLDriverConnect** para se conectar a um cluster, consulte o suporte ao cliente nativo do [SQL Server para alta disponibilidade, recuperação de desastres](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).  
  
## <a name="sqldriverconnect-support-for-service-principal-names-spns"></a>Suporte de SQLDriverConnect a SPNs (nomes de entidade de serviço)  
 O SQLDDriverConnect usará a caixa de diálogo de login ODBC quando o prompting estiver ativado. Isto permite que os SPNs sejam inseridos no servidor principal e no seu parceiro de failover.  
  
 O SQLDriverConnect aceitará as novas palavras-chave **serverSPN** e **FailoverPartnerSPN**e reconhecerá os novos atributos de conexão SQL_COPT_SS_SERVER_SPN e SQL_COPT_SS_FAILOVER_PARTNER_SPN.  
  
 Quando um valor de atributo de conexão é especificado mais de uma vez, um valor definido programaticamente tem precedência sobre o valor em um DSN e um valor em uma cadeia de caracteres de conexão. Um valor em um DSN tem precedência sobre um valor em uma cadeia de caracteres de conexão.  
  
 Quando uma conexão é aberta, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client define SQL_COPT_SS_MUTUALLY_AUTHENTICATED e SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD como o método de autenticação usado para abrir a conexão.  
  
 Para obter mais informações sobre SPNs, consulte [Os principais nomes do serviço &#40;SPNs&#41; em conexões ao cliente &#40;&#41;ODBC ](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md).  
  
## <a name="examples"></a>Exemplos  
 A chamada a seguir ilustra a menor quantidade de dados necessários para **o SQLDriverConnect**:  
  
```  
SQLDriverConnect(hdbc, hwnd,  
    (SQLTCHAR*) TEXT("DRIVER={SQL Server Native Client 10};"), SQL_NTS, szOutConn,  
    MAX_CONN_OUT, &cbOutConn, SQL_DRIVER_COMPLETE);  
```  
  
 As seguintes seqüências de conexão ilustram os dados mínimos necessários quando o valor do parâmetro *DriverComplet* é SQL_DRIVER_NOPROMPT:  
  
```  
"DSN=Human Resources;Trusted_Connection=yes"  
  
"FILEDSN=HR_FDSN;Trusted_Connection=yes"  
  
"DRIVER={SQL Server Native Client 10};SERVER=(local);Trusted_Connection=yes"  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLDriverConnect](https://go.microsoft.com/fwlink/?LinkId=59340)   
 [Detalhes da implementação da API da ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [CONJUNTO ANSI_NULLS&#41;&#40;Transact-SQL](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [&#41;de ANSI_PADDING &#40;Transact-SQL](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)  
  
  
