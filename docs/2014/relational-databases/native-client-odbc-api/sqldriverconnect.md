---
title: SQLDriverConnect | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLDriverConnect function
ms.assetid: a1e38e2c-3a97-42d1-9c45-a0ca3282ffd1
author: rothja
ms.author: jroth
ms.openlocfilehash: 40691dfb381883b59155607fb56f4933820e3e44
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85022639"
---
# <a name="sqldriverconnect"></a>SQLDriverConnect
  O driver ODBC para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client define atributos de conexão que substituem ou aprimoram palavras-chave de cadeia de conexão. Várias palavras-chave de cadeia de conexão têm valores padrão especificados pelo driver ODBC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 Para obter uma lista das palavras-chave disponíveis no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client, consulte [usando palavras-chave da cadeia de conexão com o SQL Server Native Client](../native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Para obter mais informações sobre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atributos de conexão e comportamentos padrão de driver, consulte [SQLSetConnectAttr](sqlsetconnectattr.md).  
  
 Para obter uma discussão sobre palavras-chave da cadeia de conexão que são válidas para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, consulte [usando palavras-chave da cadeia de conexão com SQL Server Native Client](../native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Quando o `SQLDriverConnect` valor do parâmetro *DriverCompletion* é SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE ou SQL_DRIVER_COMPLETE_REQUIRED, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client recupera os valores da palavra-chave da caixa de diálogo exibida. Se o valor de palavra-chave for transmitido na cadeia de caracteres da conexão e o usuário não alterar o valor para a palavra-chave na caixa de diálogo, o driver ODBC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client usará o valor da cadeia de caracteres da conexão. Se o valor não for definido na cadeia de caracteres da conexão e o usuário não fizer nenhuma atribuição na caixa de diálogo, o driver usará o padrão.  
  
 `SQLDriverConnect`deve receber um *WindowHandle* válido quando qualquer valor de *DriverCompletion* exigir (ou pode exigir) a exibição da caixa de diálogo de conexão do driver. Um identificador inválido retorna SQL_ERROR.  
  
 Especifique as palavras-chave DRIVER ou DSN. O ODBC declara que um driver usa a que está mais à esquerda dessas duas palavras-chave e ignora a outra se ambas estão especificadas. Se o DRIVER for especificado, ou for o mais à esquerda dos dois, e o `SQLDriverConnect` valor do parâmetro *DriverCompletion* for SQL_DRIVER_NOPROMPT, a palavra-chave do servidor e um valor apropriado serão necessários.  
  
 Quando SQL_DRIVER_NOPROMPT é especificado, as palavras-chave de autenticação de usuário devem estar presentes com valores. O driver assegura que a cadeia de caracteres "Trusted_Connection=yes" ou as palavras-chave UID e PWD estão presentes.  
  
 Se o valor do parâmetro *DriverCompletion* for SQL_DRIVER_NOPROMPT ou SQL_DRIVER_COMPLETE_REQUIRED e o idioma ou o banco de dados vier da cadeia de conexão e for inválido, o `SQLDriverConnect` retornará SQL_ERROR.  
  
 Se o valor do parâmetro *DriverCompletion* for SQL_DRIVER_NOPROMPT ou SQL_DRIVER_COMPLETE_REQUIRED e o idioma ou o banco de dados vierem das definições de fonte de dado ODBC e forem inválidos, o `SQLDriverConnect` usará o idioma padrão ou o Database para a ID de usuário especificada e retornará SQL_SUCCESS_WITH_INFO.  
  
 Se o valor do parâmetro *DriverCompletion* for SQL_DRIVER_COMPLETE ou SQL_DRIVER_PROMPT e se o idioma ou o banco de dados for inválido, `SQLDriverConnect` o exibirá novamente a caixa de diálogo.  
  
## <a name="sqldriverconnect-support-for-high-availability-disaster-recovery"></a>Suporte de SQLDriverConnect à alta disponibilidade e recuperação de desastre  
 Para obter mais informações sobre como usar `SQLDriverConnect` o para se conectar a um [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] cluster, consulte [suporte a SQL Server Native Client para alta disponibilidade e recuperação de desastre](../native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).  
  
## <a name="sqldriverconnect-support-for-service-principal-names-spns"></a>Suporte de SQLDriverConnect a SPNs (nomes de entidade de serviço)  
 O SQLDDriverConnect usará a caixa de diálogo logon do ODBC boxwhen solicitação está habilitada. Isto permite que os SPNs sejam inseridos no servidor principal e no seu parceiro de failover.  
  
 O SQLDriverConnect aceitará as novas palavras-chave da cadeia de conexão `ServerSPN` e `FailoverPartnerSPN` reconhecerá os novos atributos de conexão SQL_COPT_SS_SERVER_SPN e SQL_COPT_SS_FAILOVER_PARTNER_SPN.  
  
 Quando um valor de atributo de conexão é especificado mais de uma vez, um valor definido programaticamente tem precedência sobre o valor em um DSN e um valor em uma cadeia de caracteres de conexão. Um valor em um DSN tem precedência sobre um valor em uma cadeia de caracteres de conexão.  
  
 Quando uma conexão é aberta, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client define SQL_COPT_SS_MUTUALLY_AUTHENTICATED e SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD como o método de autenticação usado para abrir a conexão.  
  
 Para obter mais informações sobre SPNs, consulte [nomes de entidade de serviço &#40;SPNs&#41; em conexões de cliente &#40;&#41;ODBC ](../native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md).  
  
## <a name="examples"></a>Exemplos  
 A chamada a seguir ilustra a quantidade mínima de dados necessários para `SQLDriverConnect` :  
  
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
 [Detalhes de implementação da API ODBC](odbc-api-implementation-details.md)   
 [DEFINIR ANSI_NULLS &#40;&#41;Transact-SQL](/sql/t-sql/statements/set-ansi-nulls-transact-sql)   
 [DEFINIR ANSI_PADDING &#40;&#41;Transact-SQL](/sql/t-sql/statements/set-ansi-padding-transact-sql)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-warnings-transact-sql)  
  
  
