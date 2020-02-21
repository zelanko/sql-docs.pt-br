---
title: Pooling de conexão com reconhecimento do ODBC Driver for SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 455ab165-8e4d-4df9-a1d7-2b532bfd55d6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 97ddd5aa4abf926ecd4e68e89bef63b8f25ce323
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "68009975"
---
# <a name="driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server"></a>Pooling de conexão com reconhecimento de driver no driver ODBC para SQL Server
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

  O Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dá suporte para [Pool de Conexões com Reconhecimento de Driver](https://msdn.microsoft.com/library/hh405031(VS.85).aspx). Este tópico descreve os aprimoramentos feitos no pool de conexões com reconhecimento de driver no Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Windows:  
  
-   Independentemente das propriedades de conexão, as conexões que usam `SQLDriverConnect` entram em um pool separado das conexões que usam `SQLConnect`.
- Ao usar a Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e o pool de conexões com reconhecimento de driver, o driver não usa o contexto de segurança do usuário do Windows do thread atual para separar as conexões no pool. Ou seja, se as conexões forem equivalentes em seus parâmetros para cenários de representação do Windows com Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e se estiverem usando as mesmas credenciais de Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para se conectar ao back-end, diferentes usuários do Windows poderão potencialmente usar o mesmo pool de conexões. Ao usar a Autenticação do Windows e o pool de conexões com reconhecimento de driver, o driver usa o contexto de segurança do usuário do Windows para separar as conexões no pool. Ou seja, para cenários de representação do Windows, diferentes usuários do Windows não compartilharão conexões mesmo se elas usarem os mesmos parâmetros.
- Quando usar o Azure Active Directory e o pool de conexões com reconhecimento de driver, o driver também usará o valor de Autenticação para determinar a associação no pool de conexões.
  
-   O pool de conexões com reconhecimento de driver impede que uma conexão inválida seja retornada do pool.  
  
-   O pool de conexões com reconhecimento de driver reconhece os atributos de conexão específicos do driver. Portanto, se uma conexão usar `SQL_COPT_SS_APPLICATION_INTENT` definido como somente leitura, essa conexão obterá seu próprio pool de conexões.
-   Definir o atributo `SQL_COPT_SS_ACCESS_TOKEN` faz com que uma conexão seja agrupada separadamente 
  
Se uma das IDs de atributo de conexão ou palavras-chave de cadeia de conexão a seguir for diferente entre a cadeia de conexão e a cadeia de conexão em pool, o driver usará uma conexão em pool. No entanto, o desempenho será melhor se todas as IDs de atributo de conexão ou palavras-chave de cadeia de conexão corresponderem. Para corresponder a uma conexão no pool, o driver redefine o atributo. O desempenho é prejudicado porque, para redefinir os parâmetros a seguir, é necessária uma chamada de rede extra.  
  
-    Se dois ou mais dos atributos de conexão ou palavras-chave de conexão a seguir forem diferentes, uma conexão em pool não será usada.  
  
  - `Language`  
  - `QuoteId`  
  - `SQL_ATTR_TXN_ISOLATION` 
  - `SQL_COPT_SS_QUOTED_IDENT`  
  
-   Se houver uma diferença em qualquer uma das palavras-chave de conexão a seguir entre a cadeia de conexão e uma cadeia de conexão em pool, uma conexão em pool não será usada.  
  
    |Palavra-chave|ODBC Driver 13|ODBC Driver 11|
    |-|-|-|
    |`Address`|Sim|Sim|
    |`AnsiNPW`|Sim|Sim|
    |`App`|Sim|Sim|
    |`ApplicationIntent`|Sim|Sim|  
    |`Authentication`|Sim|Não|
    |`ColumnEncryption`|Sim|Não|
    |`Database`|Sim|Sim|
    |`Encrypt`|Sim|Sim|  
    |`Failover_Partner`|Sim|Sim|
    |`FailoverPartnerSPN`|Sim|Sim|
    |`MARS_Connection`|Sim|Sim|
    |`Network`|Sim|Sim|
    |`PWD`|Sim|Sim|
    |`Server`|Sim|Sim|
    |`ServerSPN`|Sim|Sim|
    |`TransparentNetworkIPResolution`|Sim|Sim|
    |`Trusted_Connection`|Sim|Sim|
    |`TrustServerCertificate`|Sim|Sim|
    |`UID`|Sim|Sim|
    |`WSID`|Sim|Sim|
    
- Se houver uma diferença em qualquer um dos atributos de conexão a seguir entre a cadeia de conexão e uma cadeia de conexão em pool, uma conexão em pool não será usada.  
  
    |Atributo|ODBC Driver 13|ODBC Driver 11|  
    |-|-|-|  
    |`SQL_ATTR_CURRENT_CATALOG`|Sim|Sim|
    |`SQL_ATTR_PACKET_SIZE`|Sim|Sim|
    |`SQL_COPT_SS_ANSI_NPW`|Sim|Sim|
    |`SQL_COPT_SS_ACCESS_TOKEN`|Sim|Não|
    |`SQL_COPT_SS_AUTHENTICATION`|Sim|Não|
    |`SQL_COPT_SS_ATTACHDBFILENAME`|Sim|Sim|
    |`SQL_COPT_SS_BCP`|Sim|Sim|
    |`SQL_COPT_SS_COLUMN_ENCRYPTION`|Sim|Não|
    |`SQL_COPT_SS_CONCAT_NULL`|Sim|Sim|
    |`SQL_COPT_SS_ENCRYPT`|Sim|Sim|
    |`SQL_COPT_SS_FAILOVER_PARTNER`|Sim|Sim|
    |`SQL_COPT_SS_FAILOVER_PARTNER_SPN`|Sim|Sim|
    |`SQL_COPT_SS_INTEGRATED_SECURITY`|Sim|Sim|
    |`SQL_COPT_SS_MARS_ENABLED`|Sim|Sim|
    |`SQL_COPT_SS_OLDPWD`|Sim|Sim|
    |`SQL_COPT_SS_SERVER_SPN`|Sim|Sim|
    |`SQL_COPT_SS_TRUST_SERVER_CERTIFICATE`|Sim|Sim|
    |`SSPROP_AUTH_REPL_SERVER_NAME`|Sim|Sim|
    |`SQL_COPT_SS_TNIR`|Sim|Não|
 
-   O driver pode redefinir e ajustar as palavras-chave e os atributos de conexão a seguir sem fazer uma chamada de rede extra. O driver redefine esses parâmetros para garantir que a conexão não contenha informações incorretas.  
  
     Essas palavras-chave de conexão não são consideradas quando o Gerenciador de Driver tenta corresponder a conexão a uma conexão no pool. (Mesmo se você alterar um desses parâmetros, uma conexão existente poderá ser reutilizada. O driver redefinirá as opções conforme a necessidade.) Esses atributos podem ser redefinidos no lado do cliente sem fazer uma chamada de rede extra.  
  
    |Palavra-chave|ODBC Driver 13|ODBC Driver 11|  
    |-|-|-|  
    |`AutoTranslate`|Sim|Sim|
    |`Description`|Sim|Sim|
    |`MultisubnetFailover`|Sim|Sim|  
    |`QueryLog_On`|Sim|Sim|
    |`QueryLogFile`|Sim|Sim|
    |`QueryLogTime`|Sim|Sim|
    |`Regional`|Sim|Sim|
    |`StatsLog_On`|Sim|Sim|
    |`StatsLogFile`|  Sim|Sim|
  
     Se você alterar um dos atributos de conexão a seguir, uma conexão existente poderá ser reutilizada.  O driver redefinirá o valor conforme a necessidade. O driver pode redefinir esses atributos no lado do cliente sem fazer uma chamada de rede extra.  
  
    |Atributo|ODBC Driver 13|ODBC Driver 11|  
    |-|-|-|  
    |Todos os atributos de instrução|Sim|Sim|
    |`SQL_ATTR_AUTOCOMMIT`|Sim|Sim|
    |`SQL_ATTR_CONNECTION_TIMEOUT`|  Sim|Sim|
    |`SQL_ATTR_DISCONNECT_BEHAVIOR SQL_ATTR_CONNECTION_TIMEOUT`|Sim|Sim|
    |`SQL_ATTR_LOGIN_TIMEOUT`|Sim|Sim|
    |`SQL_ATTR_ODBC_CURSORS`|  Sim|Sim|
    |`SQL_COPT_SS_PERF_DATA`|Sim|Sim|
    |`SQL_COPT_SS_PERF_DATA_LOG`|Sim|Sim|
    |`SQL_COPT_SS_PERF_DATA_LOG_NOW`| Sim|Sim| 
    |`SQL_COPT_SS_PERF_QUERY`|Sim|Sim|
    |`SQL_COPT_SS_PERF_QUERY_INTERVAL`|Sim|Sim|
    |`SQL_COPT_SS_PERF_QUERY_LOG`|  Sim|Sim|
    |`SQL_COPT_SS_PRESERVE_CURSORS`|Sim|Sim|
    |`SQL_COPT_SS_TRANSLATE`|Sim|Sim|
    |`SQL_COPT_SS_USER_DATA`|  Sim|Sim|
    |`SQL_COPT_SS_WARN_ON_CP_ERROR`|Sim|Sim|  
  
## <a name="see-also"></a>Consulte Também  
 [Microsoft ODBC Driver for SQL Server no Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
  
  
