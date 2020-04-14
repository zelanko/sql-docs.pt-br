---
title: Membros de SQLServerDataSource | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7e749bc5-d765-4864-be2b-7822d4c20c09
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 26d778c5d75686a3de61064037fd0ade492f998b
ms.sourcegitcommit: 54cfeb36c9caa51ec68fa8f4a1918e305db5e00a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/11/2020
ms.locfileid: "81219275"
---
# <a name="sqlserverdatasource-members"></a>Membros de SQLServerDataSource
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  As tabelas a seguir listam os membros expostos pela classe [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md).  
  
## <a name="constructors"></a>Construtores  
  
|Nome|Descrição|  
|----------|-----------------|  
|[SQLServerDataSource ()](../../../connect/jdbc/reference/sqlserverdatasource-constructor.md)|Inicializa uma nova instância da classe [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md).|  
  
## <a name="fields"></a>Campos  
 Nenhum.  
  
## <a name="inherited-fields"></a>Campos herdados  
 Nenhum.  
  
## <a name="methods"></a>Métodos  
  
|Nome|Descrição|  
|----------|-----------------|  
|[getApplicationIntent](../../../connect/jdbc/reference/getapplicationintent-method-sqlserverdatasource.md)|Retorna o valor da propriedade de conexão **applicationIntent**.|  
|[getApplicationName](../../../connect/jdbc/reference/getapplicationname-method-sqlserverdatasource.md)|Retorna o nome do aplicativo.|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)|Tenta estabelecer uma conexão com a fonte de dados que o objeto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) representa.|  
|[getDatabaseName](../../../connect/jdbc/reference/getdatabasename-method-sqlserverdatasource.md)|Retorna o nome do banco de dados.|  
|[getDisableStatementPooling](../../../connect/jdbc/reference/getdisablestatementpooling-method-sqlserverdatasource.md)|Retorna o valor da propriedade de conexão **disableStatementPooling**. Essa configuração controla se o pool de instruções está ou não habilitado para essa conexão.|  
|[getEnablePrepareOnFirstPreparedStatementCall](../../../connect/jdbc/reference/getenableprepareonfirstpreparedstatementcall-method-sqlserverdatasource.md)|Retorna o valor da propriedade de conexão **enablePrepareOnFirstPreparedStatementCall**.|  
|[getEncrypt](../../../connect/jdbc/reference/getencrypt-method-sqlserverdatasource.md)|Retorna um valor **booliano** que indica se a propriedade encrypt está habilitada.|  
|[getDescription](../../../connect/jdbc/reference/getdescription-method-sqlserverdatasource.md)|Retorna uma descrição da fonte de dados.|  
|[getFailoverPartner](../../../connect/jdbc/reference/getfailoverpartner-method-sqlserverdatasource.md)|Retorna o nome do servidor de reserva usado em uma configuração de espelhamento de banco de dados.|  
|[getHostNameInCertificate](../../../connect/jdbc/reference/gethostnameincertificate-method-sqlserverdatasource.md)|Retorna o nome do host usado na validação do certificado TLS, anteriormente conhecido como SSL, do SQL Server.|  
|[getInstanceName](../../../connect/jdbc/reference/getinstancename-method-sqlserverdatasource.md)|Retorna o nome da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[getLastUpdateCount](../../../connect/jdbc/reference/getlastupdatecount-method-sqlserverdatasource.md)|Retorna um valor **booliano** que indica se a propriedade lastUpdateCount está habilitada.|  
|[getLockTimeout](../../../connect/jdbc/reference/getlocktimeout-method-sqlserverdatasource.md)|Retorna um valor **int** que indica o número de milissegundos que o banco de dados aguarda antes de informar um tempo limite de bloqueio.|  
|[getLoginTimeout](../../../connect/jdbc/reference/getlogintimeout-method-sqlserverdatasource.md)|Retorna o número de segundos que o objeto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) aguarda enquanto tenta estabelecer uma conexão.|  
|[getLogWriter](../../../connect/jdbc/reference/getlogwriter-method-sqlserverdatasource.md)|Retorna um fluxo de saída de caracteres a ser usado em todas as mensagens de registro em log e de rastreamento.|  
|[getMultiSubnetFailover](../../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md)|Retorna o valor da propriedade de conexão **multiSubnetFailover**.|  
|[getPacketSize](../../../connect/jdbc/reference/getpacketsize-method-sqlserverdatasource.md)|Retorna o tamanho do pacote de rede atual usado para se comunicar com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], especificado em bytes.|  
|[getPortNumber](../../../connect/jdbc/reference/getportnumber-method-sqlserverdatasource.md)|Retorna o número da porta atual usado para se comunicar com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[getReference](../../../connect/jdbc/reference/getreference-method-sqlserverdatasource.md)|Retorna uma referência ao objeto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md).|  
|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverdatasource.md)|Retorna o modo de buffer de resposta do objeto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md).|  
|[getSelectMethod](../../../connect/jdbc/reference/getselectmethod-method-sqlserverdatasource.md)|Retorna o tipo de cursor padrão usado em todos os conjuntos de resultados criados com o objeto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md).|  
|[getSendStringParametersAsUnicode](../../../connect/jdbc/reference/getsendstringparametersasunicode-method-sqlserverdatasource.md)|Retorna um valor **booliano** que indica se o envio de parâmetros de cadeia de caracteres ao servidor no formato UNICODE está habilitado.|  
|[getSendTimeAsDatetime](../../../connect/jdbc/reference/getsendtimeasdatetime-method-sqlserverdatasource.md)|Retorna a configuração da propriedade de conexão **SendTimeAsDatetime**.|  
|[getServerName](../../../connect/jdbc/reference/getservername-method-sqlserverdatasource.md)|Retorna o nome do computador que executa o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[getServerPreparedStatementDiscardThreshold](../../../connect/jdbc/reference/getserverpreparedstatementdiscardthreshold-method-sqlserverdatasource.md)|Retorna o valor da propriedade de conexão **serverPreparedStatementDiscardThreshold**.|  
|[getStatementPoolingCacheSize](../../../connect/jdbc/reference/getstatementpoolingcachesize-method-sqlserverdatasource.md)|Retorna o tamanho do cache de instruções preparado para esta conexão.|  
|[getTrustManagerClass](../../../connect/jdbc/reference/gettrustmanagerclass-method-sqlserverdatasource.md)|Retorna o valor String da propriedade de conexão TrustManagerClass.|  
|[getTrustManagerConstructorArg](../../../connect/jdbc/reference/gettrustmanagerconstructorarg-method-sqlserverdatasource.md)|Retorna o valor String da propriedade de conexão TrustManagerConstructorArg.|  
|[getTrustServerCertificate](../../../connect/jdbc/reference/gettrustservercertificate-method-sqlserverdatasource.md)|Retorna um valor **booliano** que indica se a propriedade trustServerCertificate está habilitada.|  
|[getTrustStore](../../../connect/jdbc/reference/gettruststore-method-sqlserverdatasource.md)|Retorna o caminho (inclusive o nome do arquivo) para o arquivo trustStore do certificado.|  
|[getURL](../../../connect/jdbc/reference/geturl-method-sqlserverdatasource.md)|Retorna a URL usada para se conectar à fonte de dados.|  
|[getUser](../../../connect/jdbc/reference/getuser-method-sqlserverdatasource.md)|Retorna o nome do usuário usado para se conectar à fonte de dados.|  
|[getUseSQLServerBaseDate](../../../connect/jdbc/reference/getsendtimeasdatetime-method-sqlserverdatasource.md)|Retorna a configuração da propriedade de conexão useSQLServerBaseDate.|  
|[getWorkstationID](../../../connect/jdbc/reference/getworkstationid-method-sqlserverdatasource.md)|Retorna o nome do computador cliente usado para se conectar à fonte de dados.|  
|[getXopenStates](../../../connect/jdbc/reference/getxopenstates-method-sqlserverdatasource.md)|Retorna um valor **booliano** que indica se a conversão de estados SQL em estados compatíveis com XOPEN está habilitada.|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md)|Indica se o objeto da fonte de dados é um wrapper da interface especificada.|  
|[setApplicationIntent](../../../connect/jdbc/reference/setapplicationintent-method-sqlserverdatasource.md)|Define o valor da propriedade de conexão **applicationIntent**.|  
|[setApplicationName](../../../connect/jdbc/reference/setapplicationname-method-sqlserverdatasource.md)|Define o nome do aplicativo.|  
|[setAuthenticationScheme](../../../connect/jdbc/reference/setauthenticationscheme-sqlserverdatasource.md)|Indica o tipo de segurança integrada que o aplicativo deve usar.|  
|[setDatabaseName](../../../connect/jdbc/reference/setdatabasename-method-sqlserverdatasource.md)|Define o nome do banco de dados ao qual se conectar.|  
|[setDescription](../../../connect/jdbc/reference/setdescription-method-sqlserverdatasource.md)|Define a descrição da fonte de dados.|  
|[setDisableStatementPooling](../../../connect/jdbc/reference/setdisablestatementpooling-method-sqlserverdatasource.md)|Define o pool de instruções como true ou false.|  
|[setEnablePrepareOnFirstPreparedStatementCall](../../../connect/jdbc/reference/setenableprepareonfirstpreparedstatementcall-method-sqlserverdatasource.md)|Especifica o novo valor da propriedade de conexão **enablePrepareOnFirstPreparedStatementCall**.|  
|[setEncrypt](../../../connect/jdbc/reference/setencrypt-method-sqlserverdatasource.md)|Define um valor **booliano** que indica se a propriedade encrypt está habilitada.|  
|[setFailoverPartner](../../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md)|Define o nome do servidor de reserva usado em uma configuração de espelhamento de banco de dados.|  
|[setHostNameInCertificate](../../../connect/jdbc/reference/sethostnameincertificate-method-sqlserverdatasource.md)|Define o nome do host a ser usado na validação do certificado TLS, anteriormente conhecido como SSL, do SQL Server.|  
|[setInstanceName](../../../connect/jdbc/reference/setinstancename-method-sqlserverdatasource.md)|Define o nome da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[setIntegratedSecurity](../../../connect/jdbc/reference/setintegratedsecurity-method-sqlserverdatasource.md)|Define um valor **Booliano** que indica se a propriedade integratedSecurity está habilitada.|  
|[setLastUpdateCount](../../../connect/jdbc/reference/setlastupdatecount-method-sqlserverdatasource.md)|Define um valor **booliano** que indica se a propriedade lastUpdateCount está habilitada.|  
|[setLockTimeout](../../../connect/jdbc/reference/setlocktimeout-method-sqlserverdatasource.md)|Define um valor **int** que indica o número de milissegundos que o banco de dados deve aguardar antes de informar um tempo limite de bloqueio.|  
|[setLoginTimeout](../../../connect/jdbc/reference/setlogintimeout-method-sqlserverdatasource.md)|Define o número de segundos que o objeto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) aguarda enquanto tenta estabelecer uma conexão.|  
|[setLogWriter](../../../connect/jdbc/reference/setlogwriter-method-sqlserverdatasource.md)|Define um fluxo de saída de caracteres a ser usado em todas as mensagens de registro em log e de rastreamento.|  
|[setMultiSubnetFailover](../../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md)|Define o valor da propriedade de conexão **multiSubnetFailover**.|  
|[setPacketSize](../../../connect/jdbc/reference/setpacketsize-method-sqlserverdatasource.md)|Define o tamanho do pacote de rede atual usado para se comunicar com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], especificado em bytes.|  
|[setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md)|Define a senha usada para se conectar ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[setPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md)|Define o número da porta usado para se comunicar com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverdatasource.md)|Define o modo de buffer de resposta para conexões criadas usando o objeto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md).|  
|[setSelectMethod](../../../connect/jdbc/reference/setselectmethod-method-sqlserverdatasource.md)|Define o tipo de cursor padrão usado em todos os conjuntos de resultados criados com o objeto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md).|  
|[setSendStringParametersAsUnicode](../../../connect/jdbc/reference/setsendstringparametersasunicode-method-sqlserverdatasource.md)|Define um valor **booliano** que indica se o envio de parâmetros de cadeia de caracteres ao servidor no formato UNICODE está habilitado.|  
|[setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)|Especifica como enviar valores java.sql.Time ao servidor.|  
|[setServerName](../../../connect/jdbc/reference/setservername-method-sqlserverdatasource.md)|Define o nome do computador que executa o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[setServerPreparedStatementDiscardThreshold](../../../connect/jdbc/reference/setserverpreparedstatementdiscardthreshold-method-sqlserverdatasource.md)|Define o novo valor da propriedade de conexão **serverPreparedStatementDiscardThreshold**.|  
|[setStatementPoolingCacheSize](../../../connect/jdbc/reference/setstatementpoolingcachesize-method-sqlserverdatasource.md)|Define o tamanho do cache de instruções preparado para esta conexão.|  
|[setTrustManagerClass](../../../connect/jdbc/reference/settrustmanagerclass-method-sqlserverdatasource.md)|Define o valor String da propriedade de conexão TrustManagerClass.|  
|[setTrustManagerConstructorArg](../../../connect/jdbc/reference/settrustmanagerconstructorarg-method-sqlserverdatasource.md)|Define o valor String da propriedade de conexão TrustManagerConstructorArg.|  
|[setTrustServerCertificate](../../../connect/jdbc/reference/settrustservercertificate-method-sqlserverdatasource.md)|Define um valor **booliano** que indica se a propriedade trustServerCertificate está habilitada.|  
|[setTrustStore](../../../connect/jdbc/reference/settruststore-method-sqlserverdatasource.md)|Define o caminho (inclusive o nome de arquivo) para o arquivo trustStore do certificado.|  
|[setTrustStorePassword](../../../connect/jdbc/reference/settruststorepassword-method-sqlserverdatasource.md)|Define a senha usada para verificar a integridade dos dados de trustStore.|  
|[setURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md)|Define a URL usada para se conectar à fonte de dados.|  
|[setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md)|Define o nome do usuário usado para se conectar à fonte de dados.|  
|[setWorkstationID](../../../connect/jdbc/reference/setworkstationid-method-sqlserverdatasource.md)|Define o nome do computador cliente usado para se conectar à fonte de dados.|  
|[setXopenStates](../../../connect/jdbc/reference/setxopenstates-method-sqlserverdatasource.md)|Define um valor **booliano** que indica se a conversão de estados SQL em estados compatíveis com XOPEN está habilitada.|  
|[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md)|Retorna um objeto que implementa a interface especificada para permitir o acesso aos métodos específicos do [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)].|  
  
## <a name="inherited-methods"></a>Métodos herdados  
  
|Classe herdada de:|Métodos|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>Consulte Também  
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
