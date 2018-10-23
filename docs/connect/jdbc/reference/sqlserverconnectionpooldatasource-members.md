---
title: Membros SQLServerConnectionPoolDataSource | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: dac0337e-8088-488c-a25a-801a2190f6ca
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 103dcc54b470be5db744dc6b5bf7bed6660de787
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47746904"
---
# <a name="sqlserverconnectionpooldatasource-members"></a>Membros SQLServerConnectionPoolDataSource
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  As tabelas a seguir listam os membros expostos pela classe [SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md).  
  
## <a name="constructors"></a>Construtores  
  
|Nome|Descrição|  
|----------|-----------------|  
|[SQLServerConnectionPoolDataSource ()](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-constructor.md)|Inicializa uma nova instância da classe [SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md).|  
  
## <a name="fields"></a>Campos  
 Nenhum.  
  
## <a name="inherited-fields"></a>Campos herdados  
 Nenhum.  
  
## <a name="methods"></a>Métodos  
  
|Nome|Descrição|  
|----------|-----------------|  
|[getApplicationIntent](../../../connect/jdbc/reference/getapplicationintent-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Retorna o valor da propriedade de conexão **applicationIntent**.|  
|[getApplicationName](../../../connect/jdbc/reference/getapplicationname-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Retorna o nome do aplicativo.|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Tenta estabelecer uma conexão com a fonte de dados que o objeto DataSource representa.|  
|[getDatabaseName](../../../connect/jdbc/reference/getdatabasename-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Retorna o nome do banco de dados.|  
|[getDescription](../../../connect/jdbc/reference/getdescription-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Retorna a descrição da fonte de dados.|  
|[getFailoverPartner](../../../connect/jdbc/reference/getfailoverpartner-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Retorna o nome do servidor de failover usado em uma configuração de espelhamento de banco de dados.|  
|[getInstanceName](../../../connect/jdbc/reference/getinstancename-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Retorna o nome da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[getLastUpdateCount](../../../connect/jdbc/reference/getlastupdatecount-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Retorna um valor **booliano** que indica se a propriedade lastUpdateCount está habilitada.|  
|[getLockTimeout](../../../connect/jdbc/reference/getlocktimeout-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Retorna um valor **int** que indica o número de milissegundos que o banco de dados aguardará antes de relatar um tempo limite de bloqueio.|  
|[getLoginTimeout](../../../connect/jdbc/reference/getlogintimeout-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Retorna o número de segundos que o objeto DataSource aguardará ao tentar estabelecer uma conexão.|  
|[getLogWriter](../../../connect/jdbc/reference/getlogwriter-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Retorna um fluxo de saída de caracteres a ser usado em todas as mensagens de log e rastreamento.|  
|[getMultiSubnetFailover](../../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Retorna o valor da propriedade de conexão **multiSubnetFailover**.|  
|[getPooledConnection](../../../connect/jdbc/reference/getpooledconnection-method-sqlserverconnectionpooldatasource.md)|Tenta estabelecer uma conexão de banco de dados física que possa ser usada como uma conexão em pool.|  
|[getPortNumber](../../../connect/jdbc/reference/getportnumber-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Retorna o número da porta atual usado para comunicação com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[getReference](../../../connect/jdbc/reference/getreference-method-sqlserverconnectionpooldatasource.md)|Retorna uma referência a esse objeto de fonte de dados.|  
|[getSelectMethod](../../../connect/jdbc/reference/getselectmethod-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Retorna o tipo de cursor padrão usado para todos os conjuntos de resultados criados com o uso do objeto DataSource em questão.|  
|[getSendStringParametersAsUnicode](../../../connect/jdbc/reference/getsendstringparametersasunicode-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Retorna um valor **booliano** que indica se o envio de parâmetros de cadeia de caracteres ao servidor no formato UNICODE está habilitado.|  
|[getServerName](../../../connect/jdbc/reference/getservername-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Retorna o nome do computador que está executando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[getURL](../../../connect/jdbc/reference/geturl-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Retorna a URL usada para estabelecer conexão com a fonte de dados.|  
|[getUser](../../../connect/jdbc/reference/getuser-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Retorna o nome de usuário usado para estabelecer conexão com a fonte de dados.|  
|[getWorkstationID](../../../connect/jdbc/reference/getworkstationid-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Retorna o nome do computador cliente usado para estabelecer conexão com a fonte de dados.|  
|[getXopenStates](../../../connect/jdbc/reference/getxopenstates-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Retorna um valor **booliano** que indica se a conversão de estados do SQL em estados compatíveis do XOPEN está habilitada.|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverconnectionpooldatasource.md)|Indica se o objeto em questão é um wrapper para a interface especificada.|  
|[setApplicationIntent](../../../connect/jdbc/reference/setapplicationintent-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Define o valor da propriedade de conexão **applicationIntent**.|  
|[setApplicationName](../../../connect/jdbc/reference/setapplicationname-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Define o nome do aplicativo.|  
|[setAuthenticationSceme](../../../connect/jdbc/reference/setauthenticationscheme-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Indica o tipo de segurança integrada que você deseja ver em uso por seu aplicativo.|  
|[setDatabaseName](../../../connect/jdbc/reference/setdatabasename-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Define o nome do banco de dados a ser conectado.|  
|[setDescription](../../../connect/jdbc/reference/setdescription-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Define a descrição da fonte de dados.|  
|[setFailoverPartner](../../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Define o nome do servidor de failover usado em uma configuração de espelhamento de banco de dados.|  
|[setInstanceName](../../../connect/jdbc/reference/setinstancename-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Define o nome da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[setIntegratedSecurity](../../../connect/jdbc/reference/setintegratedsecurity-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Define um valor **booliano** que indica se a propriedade integratedSecurity está habilitada.|  
|[setLastUpdateCount](../../../connect/jdbc/reference/setlastupdatecount-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Define um valor **booliano** que indica se a propriedade lastUpdateCount está habilitada.|  
|[setLockTimeout](../../../connect/jdbc/reference/setlocktimeout-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Define um valor **int** que indica o número de milissegundos de espera antes que o banco de dados relate um tempo limite de bloqueio.|  
|[setLoginTimeout](../../../connect/jdbc/reference/setlogintimeout-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Define o número de segundos que o objeto DataSource aguardará ao tentar estabelecer uma conexão.|  
|[setLogWriter](../../../connect/jdbc/reference/setlogwriter-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Define um fluxo de saída de caracteres a ser usado em todas as mensagens de log e rastreamento.|  
|[setMultiSubnetFailover](../../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Define o valor da propriedade de conexão **multiSubnetFailover**.|  
|[setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Define a senha que será usada para conexão com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[setPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Define o número da porta a ser usado para comunicação com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[setSelectMethod](../../../connect/jdbc/reference/setselectmethod-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Define o tipo de cursor padrão usado para todos os conjuntos de resultados criados com o uso do objeto DataSource em questão.|  
|[setSendStringParametersAsUnicode](../../../connect/jdbc/reference/setsendstringparametersasunicode-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Define um valor **booliano** que indica se o envio de parâmetros de cadeia de caracteres ao servidor no formato UNICODE está habilitado.|  
|[setServerName](../../../connect/jdbc/reference/setservername-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Define o nome do computador que está executando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[setURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Define a URL usada para estabelecer conexão com a fonte de dados.|  
|[setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Define o nome de usuário usado para estabelecer conexão com a fonte de dados.|  
|[setWorkstationID](../../../connect/jdbc/reference/setworkstationid-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Define o nome do computador cliente usado para estabelecer conexão com a fonte de dados.|  
|[setXopenStates](../../../connect/jdbc/reference/setxopenstates-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Define um valor **booliano** que indica se a conversão de estados do SQL em estados compatíveis do XOPEN está habilitada.|  
|[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md)|Retorna um objeto que implementa a interface especificada para permitir o acesso aos métodos específicos do [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)].|  
  
## <a name="inherited-methods"></a>Métodos herdados  
  
|Classe herdada de:|Métodos|  
|---------------------------|-------------|  
|com.microsoft.sqlserver.jdbc.SQLServerDataSource|getApplicationName, getConnection, getDatabaseName, getDescription, getFailoverPartner, getInstanceName, getLastUpdateCount, getLockTimeout, getLoginTimeout, getLogWriter, getPortNumber, getSelectMethod, getSendStringParametersAsUnicode, getServerName, getURL, getUser, getWorkstationID, getXopenStates, setApplicationName, setDatabaseName, setDescription, setFailoverPartner, setInstanceName, setIntegratedSecurity, setLastUpdateCount, setLockTimeout, setLoginTimeout, setLogWriter, setPassword, setPortNumber, setSelectMethod, setSendStringParametersAsUnicode, setServerName, setURL, setUser, setWorkstationID, setXopenStates|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
|javax.sql.ConnectionPoolDataSource|getLoginTimeout, getLogWriter, setLoginTimeout, setLogWriter, getPooledConnection|  
  
## <a name="see-also"></a>Consulte Também  
 [Classe SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
  
