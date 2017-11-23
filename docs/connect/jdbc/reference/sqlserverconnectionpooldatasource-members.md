---
title: Membros SQLServerConnectionPoolDataSource | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: dac0337e-8088-488c-a25a-801a2190f6ca
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: da18ece75049aa2681379f265e9812159017d722
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverconnectionpooldatasource-members"></a>Membros SQLServerConnectionPoolDataSource
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  As tabelas a seguir listam os membros expostos pelo [SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md) classe.  
  
## <a name="constructors"></a>Construtores  
  
|Nome|Description|  
|----------|-----------------|  
|[(SQLServerConnectionPoolDataSource)](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-constructor.md)|Inicializa uma nova instância do [SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md) classe.|  
  
## <a name="fields"></a>Campos  
 Nenhum.  
  
## <a name="inherited-fields"></a>Campos herdados  
 Nenhum.  
  
## <a name="methods"></a>Métodos  
  
|Nome|Description|  
|----------|-----------------|  
|[getApplicationIntent](../../../connect/jdbc/reference/getapplicationintent-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) retorna o valor da **applicationIntent** propriedade de conexão.|  
|[getApplicationName](../../../connect/jdbc/reference/getapplicationname-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) retorna o nome do aplicativo.|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) tenta estabelecer uma conexão com a fonte de dados que representa esse objeto de fonte de dados.|  
|[getDatabaseName](../../../connect/jdbc/reference/getdatabasename-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) retorna o nome do banco de dados.|  
|[getDescription](../../../connect/jdbc/reference/getdescription-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) retorna uma descrição da fonte de dados.|  
|[getFailoverPartner](../../../connect/jdbc/reference/getfailoverpartner-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) retorna o nome do servidor de failover que é usado em um configuração de espelhamento de banco de dados.|  
|[getInstanceName](../../../connect/jdbc/reference/getinstancename-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) retorna o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] nome da instância.|  
|[getLastUpdateCount](../../../connect/jdbc/reference/getlastupdatecount-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) retorna um **booliano** valor que indica se a propriedade lastUpdateCount está habilitada.|  
|[getLockTimeout](../../../connect/jdbc/reference/getlocktimeout-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) retorna um **int** valor que indica o número de milissegundos que o banco de dados aguardará antes de relatar um tempo limite de bloqueio.|  
|[getLoginTimeout](../../../connect/jdbc/reference/getlogintimeout-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) retorna o número de segundos que o objeto de fonte de dados aguardará enquanto tenta estabelecer uma conexão.|  
|[getLogWriter](../../../connect/jdbc/reference/getlogwriter-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) retorna um fluxo de saída de caracteres a ser usado para todas as mensagens de rastreamento e registro em log.|  
|[getMultiSubnetFailover](../../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) retorna o valor da **multiSubnetFailover** propriedade de conexão.|  
|[getPooledConnection](../../../connect/jdbc/reference/getpooledconnection-method-sqlserverconnectionpooldatasource.md)|Tenta estabelecer uma conexão de banco de dados física que possa ser usada como uma conexão em pool.|  
|[getPortNumber](../../../connect/jdbc/reference/getportnumber-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) retorna o número da porta atual que é usado para se comunicar com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].|  
|[getReference](../../../connect/jdbc/reference/getreference-method-sqlserverconnectionpooldatasource.md)|Retorna uma referência a esse objeto de fonte de dados.|  
|[getSelectMethod](../../../connect/jdbc/reference/getselectmethod-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) retorna o tipo de cursor padrão que é usado para todos os conjuntos de resultados que são criados com o objeto de fonte de dados.|  
|[getSendStringParametersAsUnicode](../../../connect/jdbc/reference/getsendstringparametersasunicode-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) retorna um **booliano** valor que indica se o envio de parâmetros de cadeia de caracteres para o servidor no formato UNICODE está habilitado.|  
|[getServerName](../../../connect/jdbc/reference/getservername-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) retorna o nome do computador que está executando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].|  
|[getURL](../../../connect/jdbc/reference/geturl-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) retorna a URL que é usada para se conectar à fonte de dados.|  
|[getUser](../../../connect/jdbc/reference/getuser-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) retorna o nome de usuário que é usado para se conectar à fonte de dados.|  
|[getWorkstationID](../../../connect/jdbc/reference/getworkstationid-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) retorna o nome do cliente do computador que é usado para se conectar à fonte de dados.|  
|[getXopenStates](../../../connect/jdbc/reference/getxopenstates-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) retorna um **booliano** valor que indica se a conversão de estados SQL em estados compatíveis com XOPEN está habilitada.|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverconnectionpooldatasource.md)|Indica se o objeto em questão é um wrapper para a interface especificada.|  
|[setApplicationIntent](../../../connect/jdbc/reference/setapplicationintent-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) define o valor da **applicationIntent** propriedade de conexão.|  
|[setApplicationName](../../../connect/jdbc/reference/setapplicationname-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) define o nome do aplicativo.|  
|[setAuthenticationSceme](../../../connect/jdbc/reference/setauthenticationscheme-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) indica o tipo de segurança integrada você deseja que seu aplicativo para usar.|  
|[setDatabaseName](../../../connect/jdbc/reference/setdatabasename-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) define o nome do banco de dados para se conectar ao.|  
|[setDescription](../../../connect/jdbc/reference/setdescription-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) define a descrição da fonte de dados.|  
|[setFailoverPartner](../../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) define o nome do servidor de failover que é usado em um configuração de espelhamento de banco de dados.|  
|[setInstanceName](../../../connect/jdbc/reference/setinstancename-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) define o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] nome da instância.|  
|[setIntegratedSecurity](../../../connect/jdbc/reference/setintegratedsecurity-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) define um **booliano** valor que indica se a propriedade integratedSecurity está habilitada.|  
|[setLastUpdateCount](../../../connect/jdbc/reference/setlastupdatecount-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) define um **booliano** valor que indica se a propriedade lastUpdateCount está habilitada.|  
|[setLockTimeout](../../../connect/jdbc/reference/setlocktimeout-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) define um **int** valor que indica o número de milissegundos de espera antes que o banco de dados relate um tempo limite de bloqueio.|  
|[setLoginTimeout](../../../connect/jdbc/reference/setlogintimeout-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) define o número de segundos que o objeto de fonte de dados aguardará enquanto tenta estabelecer uma conexão.|  
|[setLogWriter](../../../connect/jdbc/reference/setlogwriter-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) define um fluxo de saída de caracteres a ser usado para todas as mensagens de rastreamento e registro em log.|  
|[setMultiSubnetFailover](../../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) define o valor da **multiSubnetFailover** propriedade de conexão.|  
|[setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) define a senha que será usada para se conectar ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].|  
|[setPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) define o número da porta a ser usado para se comunicar com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].|  
|[setSelectMethod](../../../connect/jdbc/reference/setselectmethod-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) define o tipo de cursor padrão que é usado para todos os conjuntos de resultados que são criados com o objeto de fonte de dados.|  
|[setSendStringParametersAsUnicode](../../../connect/jdbc/reference/setsendstringparametersasunicode-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) define um **booliano** valor que indica se o envio de parâmetros de cadeia de caracteres para o servidor no formato UNICODE está habilitado.|  
|[setServerName](../../../connect/jdbc/reference/setservername-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) define o nome do computador que está executando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].|  
|[setURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) define a URL que é usada para se conectar à fonte de dados.|  
|[setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) define o nome de usuário que é usado para se conectar à fonte de dados.|  
|[setWorkstationID](../../../connect/jdbc/reference/setworkstationid-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) define o cliente do nome do computador que é usado para se conectar à fonte de dados.|  
|[setXopenStates](../../../connect/jdbc/reference/setxopenstates-method-sqlserverdatasource.md)|(Herdado de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) define um **booliano** valor que indica se a conversão de estados SQL em estados compatíveis com XOPEN está habilitada.|  
|[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md)|Retorna um objeto que implementa a interface especificada para permitir acesso a [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-métodos específicos.|  
  
## <a name="inherited-methods"></a>Métodos herdados  
  
|Classe herdada de:|Métodos|  
|---------------------------|-------------|  
|com.microsoft.sqlserver.jdbc.SQLServerDataSource|getApplicationName, getConnection, getDatabaseName, getDescription, getFailoverPartner, getInstanceName, getLastUpdateCount, getLockTimeout, getLoginTimeout, getLogWriter, getPortNumber, getSelectMethod, getSendStringParametersAsUnicode, getServerName, getURL, getUser, getWorkstationID, getXopenStates, setApplicationName, setDatabaseName, setDescription, setFailoverPartner, setInstanceName, setIntegratedSecurity, setLastUpdateCount, setLockTimeout, setLoginTimeout, setLogWriter, setPassword, setPortNumber, setSelectMethod, setSendStringParametersAsUnicode, setServerName, setURL, setUser, setWorkstationID, setXopenStates|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
|javax.sql.ConnectionPoolDataSource|getLoginTimeout, getLogWriter, setLoginTimeout, setLogWriter, getPooledConnection|  
  
## <a name="see-also"></a>Consulte também  
 [Classe SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
  

