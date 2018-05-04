---
title: Sempre criptografado referência de API para o Driver JDBC | Microsoft Docs
ms.custom: ''
ms.date: 1/19/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6962a2aa-9508-4d4f-a78c-905e2bc68615
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 09c72dbbfaa9863d63575f91eee2bbc2bb50ddb8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="always-encrypted-api-reference-for-the-jdbc-driver"></a>Sempre criptografado referência de API para o Driver JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Always Encrypted permite que os clientes criptografem os dados confidenciais em aplicativos de cliente e nunca revelem as chaves de criptografia para o SQL Server. Um driver Always Encrypted habilitado instalado no computador cliente realiza isso automaticamente criptografando e descriptografando dados confidenciais no aplicativo cliente do SQL Server. O driver criptografa as colunas de dados confidenciais antes de passar os dados para o SQL Server e reconfigura automaticamente as consultas para que a semântica do aplicativo seja preservada. Da mesma forma, o driver de modo transparente descriptografa os dados armazenados em colunas de banco de dados criptografado que estão contidas nos resultados da consulta. Para obter mais informações, consulte [sempre criptografados (mecanismo de banco de dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) e [usar sempre criptografado com o Driver JDBC](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md).  
  
> [!NOTE]  
>  Sempre criptografado é suportada apenas pelo Microsoft JDBC Driver 6.0 ou superior para o SQL Server com o SQL Server 2016.  
  
 ## <a name="always-encrypted-api-references"></a>Sempre criptografado referências de API
 
 Existem diversas novas adições e modificações para a API do driver JDBC para uso em aplicativos cliente que usam Sempre Criptografado.  
  
 **Classe SQLServerConnection**  
  
|Nome|Description|  
|----------|-----------------|  
|Nova palavra-chave de cadeia de conexão:<br /><br /> columnEncryptionSetting|columnEncryptionSetting = Enabled habilita a funcionalidade sempre criptografado para a conexão e columnEncryptionSetting = Disabled a desabilita. Os valores aceitos são Enabled/Disabled. O padrão é Disabled.|  
|Novos métodos:<br /><br /> setColumnEncryptionTrustedMasterKeyPaths de void estático público (mapa < cadeia de caracteres, lista\<cadeia de caracteres >> trustedKeyPaths)<br /><br /> updateColumnEncryptionTrustedMasterKeyPaths de void estático público (lista de servidor de cadeia de caracteres\<cadeia de caracteres > trustedKeyPaths)<br /><br /> removeColumnEncryptionTrustedMasterKeyPaths void estático público (servidor de cadeia de caracteres)|Permite conjunto/atualizar/remover uma lista de caminhos confiáveis de chave para um servidor de banco de dados. Se durante o processamento de uma consulta de aplicativo o driver receber um caminho de chave que não esteja na lista, a consulta falhará. Esta propriedade fornece proteção adicional contra ataques de segurança que envolvem um SQL Server comprometido fornecendo falsos caminhos principais, que podem levar a vazar credenciais de repositório de chaves.|  
|Novo método:<br /><br /> Mapa estático público < cadeia de caracteres, lista\<cadeia de caracteres >> getColumnEncryptionTrustedMasterKeyPaths()|Retorna uma lista de caminhos confiáveis de chave para um servidor de banco de dados.|  
|Novo método:<br /><br /> registerColumnEncryptionKeyStoreProviders de void estático público (mapa\<cadeia de caracteres, SQLServerColumnEncryptionKeyStoreProvider > clientKeyStoreProviders)|Permite que você registre os provedores de repositório de chaves personalizado. É um dicionário que mapeia nomes de provedor de repositório de chaves para implementações do provedor de repositório de chaves.<br /><br /> Para usar o repositório de chaves da JVM, você precisa instanciar um objeto SQLServerColumnEncryptionJVMKeyStoreProvider com credenciais de repositório de chaves da JVM e registrá-lo com o driver. O nome para esse provedor deve ser 'MSSQL_JVM_KEYSTORE'.<br /><br /> Para usar o repositório de Cofre de chaves do Azure, você precisa instanciar um objeto SQLServerColumnEncryptionAzureKeyStoreProvider e registrá-lo com o driver. O nome para esse provedor deve ser 'AZURE_KEY_VAULT'.|
|público getSendTimeAsDatetime() booliano final|Retorna a configuração da propriedade de conexão sendTimeAsDatetime.|
|setSendTimeAsDatetime public void (boolean sendTimeAsDateTimeValue)|Modifica a configuração da propriedade de conexão sendTimeAsDatetime.|

 **Classe SQLServerConnectionPoolProxy**
|Nome|Description|  
|----------|-----------------|  
|público getSendTimeAsDatetime() booliano final|Retorna a configuração da propriedade de conexão sendTimeAsDatetime.|
|setSendTimeAsDatetime public void (boolean sendTimeAsDateTimeValue)|Modifica a configuração da propriedade de conexão sendTimeAsDatetime.|
     
  
 **Classe SQLServerDataSource**  
  
|Nome|Description|  
|----------|-----------------|  
|setColumnEncryptionSetting public void (cadeia de caracteres columnEncryptionSetting))|Habilita/desabilita a funcionalidade Sempre Criptografado para o objeto de fonte de dados.<br /><br /> O padrão é Disabled.|  
|público getcolumnencryptionsetting () de cadeia de caracteres|Recupera a configuração da funcionalidade Sempre Criptografado para o objeto de fonte de dados.|
|setKeyStoreAuthentication public void (cadeia de caracteres keyStoreAuthentication)|Define o nome que identifica um repositório de chaves. Somente o valor com suporte é "JavaKeyStorePassword" para identifiying o repositório de chaves Java.<br/><br/>O padrão é nulo.|
|público getKeyStoreAuthentication() de cadeia de caracteres|Obtém o valor da configuração keyStoreAuthentication para o objeto de fonte de dados.|
|setKeyStoreSecret public void (cadeia de caracteres keyStoreSecret)|Define a senha para o armazenamento de chaves Java. Observe que, para o provedor de armazenamento de chaves Java a senha para o armazenamento de chaves e a chave deve ser o mesmo. Observe que, keyStoreAuthentication deve ser definido com "JavaKeyStorePassword".|
|setKeyStoreLocation public void (cadeia de caracteres keyStoreLocation)|Define o local, incluindo o nome do arquivo para o armazenamento de chaves Java. Observe que, keyStoreAuthentication deve ser definido com "JavaKeyStorePassword".|
|público getKeyStoreLocation() de cadeia de caracteres|Recupera o keyStoreLocation para o repositório de chaves Java.|
  
 **Classe SQLServerColumnEncryptionJavaKeyStoreProvider**  
  
 A implementação do provedor de repositório de chaves para repositório de chaves Java. Essa classe permite o uso de certificados armazenados no armazenamento de chaves Java como chaves mestras de coluna.  
  
 Construtores  
  
|Nome|Description|  
|----------|-----------------|  
|público SQLServerColumnEncryptionJavaKeyStoreProvider (cadeia de caracteres keyStoreLocation, char [] keyStoreSecret)|Provedor de repositório de chaves para o repositório de chaves Java.|  
  
 Métodos  
  
|Nome|Description|  
|----------|-----------------|  
|público byte [] decryptColumnEncryptionKey (cadeia de caracteres masterKeyPath, encryptionAlgorithm de cadeia de caracteres, byte [] encryptedColumnEncryptionKey)|Descriptografa o valor criptografado especificado de uma coluna da chave de criptografia. O valor criptografado deve ser criptografado usando o certificado com o caminho da chave especificado e o algoritmo especificado.<br /><br /> **O formato do caminho da chave deve ser um dos seguintes:**<br /><br /> Impressão digital: < certificate_thumbprint ><br /><br /> Alias: < certificate_alias ><br /><br /> (Substitui o SQLServerColumnEncryptionKeyStoreProvider. decryptColumnEncryptionKey(String, String, Byte[]).)|  
|público byte [] encryptColumnEncryptionKey (cadeia de caracteres masterKeyPath, encryptionAlgorithm de cadeia de caracteres, byte [] plainTextColumnEncryptionKey)|Criptografa uma chave de criptografia de coluna usando o certificado com o caminho da chave especificado e o algoritmo especificado.<br /><br /> **O formato do caminho da chave deve ser um dos seguintes:**<br /><br /> Impressão digital: < certificate_thumbprint ><br /><br /> Alias: < certificate_alias ><br /><br /> (Substitui o SQLServerColumnEncryptionKeyStoreProvider. encryptColumnEncryptionKey(String, String, Byte[]).)|  
|setName public void (nome de cadeia de caracteres)|Define o nome desse provedor de repositório de chaves.|
|público () getName de cadeia de caracteres|Obtém o nome desse provedor de repositório de chaves.|
  
 **Classe SQLServerColumnEncryptionAzureKeyVaultProvider**  
  
 A implementação do provedor de repositório de chaves para o Cofre de chaves do Azure. Essa classe permite usar chaves armazenadas no cofre de chaves do Azure como chaves mestras de coluna.  
  
 Construtores  
  
|Nome|Description|  
|----------|-----------------|  
|público SQLServerColumnEncryptionAzureKeyVaultProvider (cadeia de caracteres clientId, clientKey de cadeia de caracteres)|Provedor de repositório de chaves para o Cofre de chaves do Azure.  Você precisa fornecer o identificador e a chave do cliente solicitar o token para autenticar para o Cofre de chaves do Azure.|  
  
 Métodos  
  
|Nome|Description|  
|----------|-----------------|  
|público byte [] decryptColumnEncryptionKey (cadeia de caracteres masterKeyPath, encryptionAlgorithm de cadeia de caracteres, byte [] encryptedColumnEncryptionKey)|Descriptografa o valor criptografado especificado de uma coluna da chave de criptografia. O valor criptografado deve ser criptografada usando a chave da coluna especificada IDmaster chave e o algoritmo especificado. <br />(Substitui o SQLServerColumnEncryptionKeyStoreProvider. decryptColumnEncryptionKey(String, String, Byte[]).)|  
|público byte [] encryptColumnEncryptionKey (cadeia de caracteres masterKeyPath, encryptionAlgorithm de cadeia de caracteres, byte [] columnEncryptionKey)|Criptografa uma chave de criptografia de coluna usando a chave mestra de coluna especificada e o algoritmo especificado. <br />(Substitui o SQLServerColumnEncryptionKeyStoreProvider. encryptColumnEncryptionKey(String, String, Byte[]).)|  
|setName public void (nome de cadeia de caracteres)|Define o nome desse provedor de repositório de chaves.|
|público () getName de cadeia de caracteres|Obtém o nome desse provedor de repositório de chaves.|  
  
  
 **SQLServerKeyVaultAuthenticationCallback Interface**  
  
 Essa interface contém um método de autenticação de Cofre de chaves do Azure, que deve ser implementada por usuário.  
  
 Métodos  
  
|Nome|Description|  
|----------|-----------------|  
|público getAccessToken de cadeia de caracteres (autoridade de cadeia de caracteres, cadeia de caracteres, o escopo de cadeia de caracteres);|O método deve ser substituído. O método é usado para obter acesso token Cofre de chaves do Azure.|  
  
 **Classe SQLServerColumnEncryptionKeyStoreProvider**  
  
 Estenda a classe para implementar um provedor personalizado de repositório de chave.  
  
|Nome|Description|  
|----------|-----------------|  
|SQLServerColumnEncryptionKeyStoreProvider|Classe base para todos os provedores de repositório de chaves. Um provedor personalizado deve derivar dessa classe e substituir suas funções de membro e, em seguida, registrá-lo usando SQLServerConnection. registerColumnEncryptionKeyStoreProviders().|  
  
 Métodos  
  
|Nome|Description|  
|----------|-----------------|  
|public abstract byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte [] encryptedColumnEncryptionKey)|Método de classe base para descriptografar o valor especificado de uma coluna da chave de criptografia. O valor criptografado deve ser criptografado usando a chave mestra de coluna com o caminho da chave especificado e o algoritmo especificado.|  
|byte abstrato público [] encryptColumnEncryptionKey (cadeia de caracteres masterKeyPath, encryptionAlgorithm de cadeia de caracteres, byte [] columnEncryptionKey)|Método da classe base para criptografar a criptografia de uma coluna de chave usando a chave mestra de coluna com o caminho da chave especificado e usar o algoritmo especificado.|
|setName public void abstrato (nome de cadeia de caracteres)|Define o nome desse provedor de repositório de chaves.|
|público GetName abstrata de cadeia de caracteres|Obtém o nome desse provedor de repositório de chaves.|  
  
 Métodos sobrecarregados ou novos no **SQLServerPreparedStatement** classe  
  
|Nome|Description|  
|----------|-----------------|  
|público setBigDecimal void (int parameterIndex, BigDecimal x int precisão, escala de int)<br /><br /> público setObject void (int parameterIndex, x do objeto, targetSqlType int, inteiro precisão, escala de int)<br /><br /> público setObject void (int parameterIndex, x do objeto, SQLType targetSqlType, inteiro precisão, escala de número inteiro)<br /><br /> público setTime void (parameterIndex int, Java.SQL. time int escala x)<br /><br /> público setTimestamp void (parameterIndex int, Java.SQL. timestamp, int escala x) <br />público setDateTimeOffset void (int parameterIndex, Microsoft.SQL int escala x)|Esses métodos estão sobrecarregados com uma precisão ou um argumento de escala ou ambos para dar suporte ao sempre criptografado para tipos de dados específicos que requerem precisão e informações de escala.|  
|público setMoney void (int parameterIndex, BigDecimal x)<br /><br /> público setSmallMoney void (int parameterIndex, BigDecimal x)<br /><br /> público setUniqueIdentifier void (int parameterIndex, cadeia de caracteres guid)<br /><br /> público setDateTime void (parameterIndex int, Java.SQL. timestamp x)<br /><br /> público setSmallDateTime void (parameterIndex int, Java.SQL. timestamp x)|Esses métodos são adicionados para dar suporte ao sempre criptografado para o dinheiro de tipos de dados, smallmoney, uniqueidentifier, datetime e smalldatetime. <br/><br/>Observe que o método setTimestamp() existente é usado para enviar valores de parâmetro para a coluna criptografada datetime2. Para colunas do tipo smalldatetime e de datetime criptografado usar o novo setDateTime() de métodos e setSmallDateTime(), respectivamente.|  
|público setBigDecimal void final (int parameterIndex, BigDecimal x int precisão, escala de int, boolean forceEncrypt)<br /><br /> setMoney public void final (int parameterIndex, BigDecimal x forceEncrypt booleano)<br /><br /> setSmallMoney public void final (int parameterIndex, BigDecimal x forceEncrypt booleano)<br /><br /> público setBoolean void final (parameterIndex int, boolean x, boolean forceEncrypt)<br /><br /> público setByte void final (parameterIndex int, byte x forceEncrypt booleano)<br /><br /> público setBytes void final (parameterIndex int, byte x[], boolean forceEncrypt)<br /><br /> público setUniqueIdentifier void final (int parameterIndex, cadeia de caracteres guid, booliano forceEncrypt)<br /><br /> público setDouble void final (parameterIndex int, double x, boolean forceEncrypt)<br /><br /> público setFloat void final (parameterIndex int, float x, boolean forceEncrypt)<br /><br /> público setInt anulada final (int parameterIndex, o valor int, boolean forceEncrypt)<br /><br /> público setLong void final (parameterIndex int, long x, boolean forceEncrypt)<br /><br /> público setObject final (int parameterIndex, x do objeto, targetSqlType int, precisão inteiro, escala de int, boolean forceEncrypt)<br /><br /> público setObject void final (int parameterIndex, x do objeto, SQLType targetSqlType, precisão inteiro, escala de número inteiro, booliano forceEncrypt)<br /><br /> público setShort void final (int parameterIndex, x curto, boolean forceEncrypt)<br /><br /> público final void setString (int parameterIndex, cadeia de caracteres str, boolean forceEncrypt)<br /><br /> público setNString void final (int parameterIndex, o valor de cadeia de caracteres, forceEncrypt booleano)<br /><br /> público setTime void final (parameterIndex int, Java.SQL. time x, escala de int, boolean forceEncrypt)<br /><br /> público setTimestamp void final (parameterIndex int, Java.SQL. timestamp, int escala x, boolean forceEncrypt)<br /><br /> público setDateTimeOffset void final (int parameterIndex, Microsoft.SQL x, escala de int, boolean forceEncrypt)<br /><br /> público setDateTime void final (parameterIndex int, Java.SQL. timestamp x forceEncrypt booleano)<br /><br /> público setSmallDateTime void final (parameterIndex int, Java.SQL. timestamp x forceEncrypt booleano)<br /><br /> público setDate void final (parameterIndex int, Java.SQL x java.util.Calendar cal, boolean forceEncrypt)<br /><br /> público setTime void final (parameterIndex int, Java.SQL. time x java.util.Calendar cal, boolean forceEncrypt)<br /><br /> público setTimestamp void final (parameterIndex int, Java.SQL. timestamp x java.util.Calendar cal, boolean forceEncrypt)|Define o parâmetro designado como o valor java fornecido.<br /><br /> Se o forceEncrypt boolean é definido como true, a consulta de parâmetro só será definido se a coluna de designação está criptografada e sempre criptografado está habilitado, a conexão ou a instrução.<br /><br /> Se o forceEncrypt boolean é definido como false, o driver não forçará a criptografia em parâmetros.|  
  
 Métodos sobrecarregados ou novos no **SQLServerCallableStatement** classe  
  
|Nome|Description|  
|----------|-----------------|  
|público registerOutParameter void (int parameterIndex, sqlType int, int precisão, escala de int)<br /><br /> público registerOutParameter void (int parameterIndex, SQLType sqlType, int precisão, escala de int)<br /><br /> público registerOutParameter void (parameterName de cadeia de caracteres, sqlType int, int precisão, escala de int)<br /><br /> público registerOutParameter void (parameterName de cadeia de caracteres, SQLType sqlType, int precisão, escala de int)<br />público setBigDecimal void (parameterName de cadeia de caracteres, BigDecimal bd, int precisão, escala de int)<br /><br /> público setTime void (parameterName de cadeia de caracteres, Java.SQL. time t, escala de int)<br /><br /> público setTimestamp void (parameterName de cadeia de caracteres, t Java.SQL. timestamp, int escala)<br /><br /> público setDateTimeOffset void (parameterName de cadeia de caracteres, Microsoft.SQL t, escala de int)<br/><br/>público setObject void final (sCol de cadeia de caracteres, objeto x, targetSqlType int, inteiro precisão, escala de int)|Esses métodos estão sobrecarregados com uma precisão ou um argumento de escala ou ambos para dar suporte ao sempre criptografado para tipos de dados específicos que requerem precisão e informações de escala.|  
|público setDateTime void (nome do parâmetro String, Java.SQL. timestamp x)<br /><br /> público setSmallDateTime void (nome do parâmetro String, Java.SQL. timestamp x)<br /><br /> público setUniqueIdentifier void (parameterName de cadeia de caracteres, cadeia de caracteres guid)<br /><br /> público setMoney void (cadeia de caracteres parameterName, bd BigDecimal)<br /><br /> público setSmallMoney void (cadeia de caracteres parameterName, bd BigDecimal)<br/><br/>público Timestamp getDateTime (int index)<br/><br/>público Timestamp getDateTime (cadeia de caracteres sCol)<br/><br/>público getDateTime Timestamp (índice de int, calendário cal)<br/><br/>público Timestamp getSmallDateTime (int index)<br/><br/>público Timestamp getSmallDateTime (cadeia de caracteres sCol)<br/><br/>público getSmallDateTime Timestamp (índice de int, calendário cal)<br/><br/>público getSmallDateTime Timestamp (nome de cadeia de caracteres, calendário cal)<br/><br/>público BigDecimal getMoney (int index)<br/><br/>público BigDecimal getMoney (cadeia de caracteres sCol)<br/><br/>público BigDecimal getSmallMoney (int index)<br/><br/>público BigDecimal getSmallMoney (cadeia de caracteres sCol)|Esses métodos são adicionados para dar suporte ao sempre criptografado para o dinheiro de tipos de dados, smallmoney, uniqueidentifier, datetime e smalldatetime. <br/><br/>Observe que o método setTimestamp() existente é usado para enviar valores de parâmetro para a coluna criptografada datetime2. Para colunas do tipo smalldatetime e de datetime criptografado usar o novo setDateTime() de métodos e setSmallDateTime(), respectivamente.|  
|público setObject void (parameterName de cadeia de caracteres, o objeto, int n, m int, boolean forceEncrypt)<br /><br /> público setObject void (parameterName de cadeia de caracteres, objeto obj, SQLType jdbcType, escala de int, boolean forceEncrypt)<br /><br /> público setDate void (parameterName String, Java.SQL x c de calendário, boolean forceEncrypt)<br /><br /> público setTime void (parameterName de cadeia de caracteres, Java.SQL. time t, escala de int, boolean forceEncrypt)<br /><br /> público setTime void (parameterName String, Java.SQL. time x c de calendário, boolean forceEncrypt)<br /><br /> público setDateTime void (parameterName de cadeia de caracteres, Java.SQL. timestamp x forceEncrypt booleano)<br /><br /> público setDateTimeOffset void (parameterName de cadeia de caracteres, Microsoft.SQL t, escala de int, boolean forceEncrypt)<br /><br /> público setSmallDateTime void (parameterName de cadeia de caracteres, Java.SQL. timestamp x forceEncrypt booleano)<br /><br /> público setTimestamp void (parameterName de cadeia de caracteres, Java.SQL. timestamp t, escala de int, boolean forceEncrypt)<br /><br /> público setTimestamp void (parameterName de cadeia de caracteres, Java.SQL. timestamp x forceEncrypt booleano)<br /><br /> público setUniqueIdentifier void (parameterName de cadeia de caracteres, cadeia de caracteres guid, booliano forceEncrypt)<br /><br /> público setBytes void (parameterName de cadeia de caracteres, byte [] b, boolean forceEncrypt)<br /><br /> público setByte void (parameterName de cadeia de caracteres, byte b, boolean forceEncrypt)<br /><br /> público setString void (parameterName de cadeia de caracteres, s de cadeia de caracteres, forceEncrypt booleano)<br /><br /> público setNString void final (parameterName de cadeia de caracteres, o valor de cadeia de caracteres, forceEncrypt booliano)<br /><br /> público setMoney void (parameterName de cadeia de caracteres, BigDecimal bd, boolean forceEncrypt)<br /><br /> público setSmallMoney void (parameterName de cadeia de caracteres, BigDecimal bd, boolean forceEncrypt)<br /><br /> público setBigDecimal void (parameterName de cadeia de caracteres, BigDecimal bd, int precisão, escala de int, boolean forceEncrypt)<br /><br /> público setDouble void (parameterName de cadeia de caracteres, duplo d, boolean forceEncrypt)<br /><br /> público setFloat void (parameterName de cadeia de caracteres, float f, boolean forceEncrypt)<br /><br /> público setInt void (parameterName de cadeia de caracteres, int i, boolean forceEncrypt)<br /><br /> público setLong void (parameterName de cadeia de caracteres longa l, boolean forceEncrypt)<br /><br /> público setShort void (parameterName de cadeia de caracteres curta s, forceEncrypt boolean)<br /><br /> público setBoolean void (parameterNames de cadeia de caracteres, booleano b, boolean forceEncrypt)<br/><br/>público setTimeStamp void (sCol String, Java.SQL. timestamp x c de calendário, Boolean forceEncrypt)|Define o parâmetro designado como o valor java fornecido.<br /><br /> Se o forceEncrypt boolean é definido como true, a consulta de parâmetro só será definido se a coluna de designação está criptografada e sempre criptografado está habilitado, a conexão ou a instrução.<br /><br /> Se o forceEncrypt boolean é definido como false, o driver não forçará a criptografia em parâmetros.|
 

 Métodos sobrecarregados ou novos no **SQLServerResultSet** classe  
  
|Nome|Description|  
|----------|-----------------|  
|público getUniqueIdentifier de cadeia de caracteres (int columnIndex)<br/><br/>público getUniqueIdentifier de cadeia de caracteres (columnLabel de cadeia de caracteres)<br/><br/>   public java.sql.Timestamp getDateTime(int columnIndex) <br/><br/> getDateTime Java.SQL. timestamp pública (columnName de cadeia de caracteres)   <br/><br/> getDateTime Java.SQL. timestamp pública (int columnIndex, calendário cal)   <br/><br/>público Java.SQL. timestamp getDateTime (cadeia de caracteres colName, calendário cal)    <br/><br/>public java.sql.Timestamp getSmallDateTime(int columnIndex)    <br/><br/> getSmallDateTime Java.SQL. timestamp pública (columnName de cadeia de caracteres)   <br/><br/> getSmallDateTime Java.SQL. timestamp pública (int columnIndex, calendário cal)   <br/><br/> público Java.SQL. timestamp getSmallDateTime (cadeia de caracteres colName, calendário cal)   <br/><br/>  público BigDecimal getMoney (int columnIndex)  <br/><br/> público BigDecimal getMoney (columnName de cadeia de caracteres)   <br/><br/> público BigDecimal getSmallMoney (int columnIndex)   <br/><br/>  público BigDecimal getSmallMoney (columnName de cadeia de caracteres)  <br/><br/>público updateMoney void (columnName de cadeia de caracteres, BigDecimal x)    <br/><br/>  público updateSmallMoney void (columnName de cadeia de caracteres, BigDecimal x)  <br/><br/>     público updateDateTime void (índice de int, Java.SQL. timestamp x) <br/><br/> público updateSmallDateTime void (índice de int, Java.SQL. timestamp x) |Esses métodos são adicionados para dar suporte ao sempre criptografado para o dinheiro de tipos de dados, smallmoney, uniqueidentifier, datetime e smalldatetime. <br/><br/>Observe que o método updateTimestamp() existente será usado para atualizar colunas datetime2 criptografados. Para colunas do tipo smalldatetime e de datetime criptografado usar o novo updateDateTime() de métodos e updateSmallDateTime(), respectivamente.|
|público updateBoolean void (índice int, boolean x, boolean forceEncrypt)  <br/><br/>  público updateByte void (índice de int, byte x forceEncrypt boolean)  <br/><br/>  público updateShort void (índice int, x curto, boolean forceEncrypt)  <br/><br/> público updateInt void (índice de int, int x forceEncrypt booleano)   <br/><br/>  público updateLong void (índice int, long x, forceEncrypt boolean)  <br/><br/> público updateFloat void (índice de int, float x, boolean forceEncrypt)   <br/><br/> público updateDouble void (índice int, double x, boolean forceEncrypt)   <br/><br/> updateMoney public void (int index, BigDecimal x forceEncrypt booleano)   <br/><br/>  updateMoney public void (columnName de cadeia de caracteres, BigDecimal x forceEncrypt booleano)  <br/><br/> updateSmallMoney public void (int index, BigDecimal x forceEncrypt booleano)   <br/><br/>  updateSmallMoney public void (columnName de cadeia de caracteres, BigDecimal x forceEncrypt booleano)  <br/><br/> público updateBigDecimal void (int index, BigDecimal x, a precisão de inteiro, escala de número inteiro, booliano forceEncrypt)   <br/><br/>  público updateString void (int columnIndex, stringValue de cadeia de caracteres, forceEncrypt booleano)  <br/><br/>  público updateNString void (int columnIndex, nString de cadeia de caracteres, forceEncrypt booleano)  <br/><br/>  público updateNString void (columnLabel de cadeia de caracteres, cadeia de caracteres nString, forceEncrypt booliano)  <br/><br/> público updateBytes void (índice int, byte x[], boolean forceEncrypt)   <br/><br/>  público updateDate void (índice de int, Java.SQL x forceEncrypt boolean)  <br/><br/> público updateTime void (índice de int, Java.SQL. time x, escala de número inteiro, booliano forceEncrypt)   <br/><br/> público updateTimestamp void (índice de int, Java.SQL. timestamp, int escala x, boolean forceEncrypt)   <br/><br/> público updateDateTime void (índice de int, Java.SQL. timestamp x, escala de número inteiro, booliano forceEncrypt)   <br/><br/> público updateSmallDateTime void (índice de int, Java.SQL. timestamp x, escala de número inteiro, booliano forceEncrypt)   <br/><br/>  público updateDateTimeOffset void (int index, Microsoft.SQL x, escala de número inteiro, booliano forceEncrypt)  <br/><br/> updateUniqueIdentifier public void (índice de int, String x forceEncrypt boolean)    <br/><br/>  público updateObject void (int index, x do objeto, int precisão, escala de int, boolean forceEncrypt)  <br/><br/>  público updateObject void (int índice, objeto obj, SQLType targetSqlType, escala de int, boolean forceEncrypt)  <br/><br/> público updateBoolean void (columnName de cadeia de caracteres, booleano x, boolean forceEncrypt)    <br/><br/>  público updateByte void (columnName de cadeia de caracteres, byte x forceEncrypt booleano)  <br/><br/>  público updateShort void (columnName de cadeia de caracteres, x curto, boolean forceEncrypt)  <br/><br/> público updateInt void (columnName de cadeia de caracteres, int x forceEncrypt booleano)   <br/><br/>   público updateLong void (columnName de cadeia de caracteres longa x, boolean forceEncrypt) <br/><br/>  público updateFloat void (columnName de cadeia de caracteres, float x, boolean forceEncrypt)  <br/><br/>  público updateDouble void (columnName de cadeia de caracteres, duplo x, boolean forceEncrypt)  <br/><br/> updateBigDecimal public void (columnName de cadeia de caracteres, BigDecimal x forceEncrypt booleano)   <br/><br/>  público updateBigDecimal void (columnName de cadeia de caracteres, BigDecimal x, a precisão de inteiro, escala de número inteiro, booliano forceEncrypt)  <br/><br/> updateString public void (columnName de cadeia de caracteres, cadeia de caracteres x forceEncrypt booleano)   <br/><br/>  público updateBytes void (columnName de cadeia de caracteres, byte x[], boolean forceEncrypt)  <br/><br/> público updateDate void (columnName de cadeia de caracteres, Java.SQL x forceEncrypt booleano)   <br/><br/>  público updateTime void (columnName String, Java.SQL. time x, escala de int, boolean forceEncrypt)  <br/><br/>  público updateTimestamp void (columnName String, Java.SQL. timestamp, int escala x, boolean forceEncrypt)  <br/><br/> público updateDateTime void (columnName String, Java.SQL. timestamp, int escala x, boolean forceEncrypt)   <br/><br/>  público updateSmallDateTime void (columnName String, Java.SQL. timestamp, int escala x, boolean forceEncrypt)  <br/><br/>  público updateDateTimeOffset void (columnName de cadeia de caracteres, Microsoft.SQL x, escala de int, boolean forceEncrypt)  <br/><br/>  updateUniqueIdentifier public void (columnName de cadeia de caracteres, cadeia de caracteres x forceEncrypt booleano)<br/><br/>público updateObject void (columnName de cadeia de caracteres, objeto x, int precisão, escala de int, boolean forceEncrypt)<br/><br/>público updateObject void (columnName de cadeia de caracteres, objeto obj, SQLType targetSqlType, escala de int, boolean forceEncrypt)|Atualize a coluna designada como o valor java fornecido.<br/><br/>Se o forceEncrypt boolean é definido como true, a coluna só será definida se ele é criptografado e sempre criptografado está habilitado, a conexão ou a instrução.<br/><br/>Se o forceEncrypt boolean é definido como false, o driver não forçará a criptografia em parâmetros.|

  
Novos tipos em **microsoft.sql.Types** classe
|Nome|Description|  
|----------|-----------------|  
|DATETIME, SMALLDATETIME, MONEY, SMALLMONEY, GUID|Use esses tipos como tipos SQL de destino ao enviar valores de parâmetro para **criptografado** datetime, smalldatetime, money, smallmoney, colunas uniqueidentifier usando métodos setObject()/updateObject() API.|  
  
  
 **SQLServerStatementColumnEncryptionSetting Enum**  
  
 Especifica como os dados serão enviados e recebidos durante a leitura e gravação de colunas criptografadas. Dependendo da consulta específica, o impacto no desempenho pode ser reduzido, ignorando o driver sempre criptografado de processamento quando colunas criptografadas não estão sendo usadas. Observe que essas configurações não podem ser usadas para ignorar a criptografia e obter acesso aos dados de texto sem formatação.  
  
 **Sintaxe**  
  
```  
Public enum  SQLServerStatementColumnEncryptionSetting  
```  
  
 **Membros**  
  
|Nome|Description|  
|----------|-----------------|  
|UseConnectionSetting|Especifica que o comando deve padrão para a configuração do sempre criptografado na cadeia de conexão.|  
|Ativado|Habilita o sempre criptografado para a consulta.|  
|ResultSetOnly|Especifica que somente os resultados do comando devem ser processados pela rotina sempre criptografado no driver. Use esse valor quando o comando não tem parâmetros que necessite de criptografia.|  
|Desabilitado|Desabilita o sempre criptografado para a consulta.|  
  
 A configuração de nível de instrução para AE são adicionados para a classe SQLServerConnection e a classe SQLServerConnectionPoolProxy. Os seguintes métodos nessas classes estão sobrecarregados com a nova configuração.  
  
|Nome|Description|  
|----------|-----------------|  
|público createStatement de instrução (int nType nConcur int, int statementHoldability, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)|Cria um objeto de instrução que irá gerar objetos de conjunto de resultados com a configuração de criptografia determinado tipo, a simultaneidade, a colocação em espera e a coluna.|  
|público prepareCall CallableStatement (cadeia de caracteres sql, nType int, nConcur int, int statementHoldability, SQLServerStatementColumnEncryptionSetting stmtColEncSetiing)|Cria um objeto CallableStatement com a configuração de criptografia de coluna especificada que irá gerar o conjunto de resultados objetos com determinado tipo, simultaneidade e colocação em espera.|  
|público prepareStatement PreparedStatement (cadeia de caracteres sql, int autogeneratedKeys SQLServerStatementColumnEncryptionSetting stmtColEncSetting.)|Cria um objeto PreparedStatement com a configuração de criptografia de determinada coluna que tem a capacidade de recuperar as chaves geradas automaticamente.|  
|public PreparedStatement prepareStatement(String sql, String[] columnNames, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)|Cria um objeto PreparedStatement com a configuração de criptografia de coluna especificada que irá gerar objetos de conjunto de resultados com os nomes de coluna especificada.|  
|public PreparedStatement prepareStatement(String sql, int[] columnIndexes, SQLServerStatementColumnEncryptionSetting stmtColEncSetting|Cria um objeto PreparedStatement com a configuração de criptografia de coluna especificada que irá gerar objetos de conjunto de resultados com os índices de coluna especificada.|  
|public PreparedStatement prepareStatement( String sql, int nType, int nConcur, int nHold, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)|Cria um objeto PreparedStatement com a configuração de criptografia de coluna especificada que irá gerar o conjunto de resultados objetos com determinado tipo, simultaneidade e colocação em espera.|  
  
> [!NOTE]  
>  Se o sempre criptografado está desabilitado para uma consulta e a consulta tiver parâmetros que precisam ser criptografados (parâmetros que correspondem a colunas criptografadas), a consulta falhará.  
>   
>  Se o sempre criptografado está desabilitado para uma consulta e a consulta retorna resultados de colunas criptografadas, a consulta retornará valores criptografados. Os valores criptografados terá o tipo de dados varbinary.  
  
 ## <a name="see-also"></a>Consulte também  
 [Use Always Encrypted com o Driver JDBC](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)  
  

