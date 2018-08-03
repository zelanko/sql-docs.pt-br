---
title: Referência da API do Always Encrypted para o JDBC Driver | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6962a2aa-9508-4d4f-a78c-905e2bc68615
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f1b720a607b702e93643d70b40a5e6ab036f2f56
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/27/2018
ms.locfileid: "39279247"
---
# <a name="always-encrypted-api-reference-for-the-jdbc-driver"></a>Referência da API do Always Encrypted para o JDBC Driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Always Encrypted permite que os clientes criptografem os dados confidenciais em aplicativos de cliente e nunca revelem as chaves de criptografia para o SQL Server. Um driver habilitado para Always Encrypted instalado no computador cliente obtém essa funcionalidade criptografando e descriptografando dados confidenciais automaticamente no aplicativo cliente do SQL Server. O driver criptografa as colunas de dados confidenciais antes de passar os dados para o SQL Server e reconfigura automaticamente as consultas para que a semântica do aplicativo seja preservada. Da mesma forma, o driver descriptografa de modo transparente os dados armazenados em colunas de banco de dados criptografadas dos resultados da consulta. Para obter mais informações, consulte [Always Encrypted (mecanismo de banco de dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) e [usando o Always Encrypted com o Driver JDBC](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md).  
  
> [!NOTE]  
>  Há suporte para o Always Encrypted apenas no Microsoft JDBC Driver 6.0 ou superior para o SQL Server com o SQL Server 2016.  
  
 ## <a name="always-encrypted-api-references"></a>Referências da API do Always Encrypted
 
 Existem diversas novas adições e modificações para a API do driver JDBC para uso em aplicativos cliente que usam Sempre Criptografado.  
  
 **Classe SQLServerConnection**  
  
|Nome|Descrição|  
|----------|-----------------|  
|Nova palavra-chave de cadeia de conexão:<br /><br /> columnEncryptionSetting|columnEncryptionSetting=Enabled habilita a funcionalidade Always Encrypted na conexão e columnEncryptionSetting=Disabled a desabilita. Os valores aceitos são Enabled/Disabled. O padrão é Disabled.|  
|Novos métodos:<br /><br /> setColumnEncryptionTrustedMasterKeyPaths de void estático público (mapa < cadeia de caracteres, lista\<cadeia de caracteres >> trustedKeyPaths)<br /><br /> updateColumnEncryptionTrustedMasterKeyPaths de void estático público (lista de servidor de cadeia de caracteres\<cadeia de caracteres > trustedKeyPaths)<br /><br /> removeColumnEncryptionTrustedMasterKeyPaths nulo estático público (servidor de cadeia de caracteres)|Permite que você defina/atualize/remova uma lista de caminhos de chave confiáveis para um servidor de banco de dados. Se, durante o processamento de uma consulta de aplicativo, o driver receber um caminho de chave que não esteja na lista, a consulta falhará. Essa propriedade fornece proteção adicional contra ataques de segurança que envolvem o envio de um SQL Server comprometido fornecendo caminhos de chave falsos, que podem levar à perda das credenciais do repositório de chaves.|  
|Novo método:<br /><br /> public static Map<String, List\<String>> getColumnEncryptionTrustedMasterKeyPaths()|Retorna uma lista de caminhos confiáveis de chave para um servidor de banco de dados.|  
|Novo método:<br /><br /> public static void registerColumnEncryptionKeyStoreProviders (Map\<String, SQLServerColumnEncryptionKeyStoreProvider> clientKeyStoreProviders)|Permite que você registre os provedores de repositório de chaves personalizado. É um dicionário que mapeia nomes de provedor de repositório de chaves para implementações do provedor de repositório de chaves.<br /><br /> Para usar o repositório de chaves da JVM, você precisa criar uma instância de um objeto SQLServerColumnEncryptionJVMKeyStoreProvider com credenciais do repositório de chaves da JVM e registrá-lo com o driver. O nome desse provedor precisa ser ‘MSSQL_JVM_KEYSTORE’.<br /><br /> Para usar o armazenamento do Azure Key Vault, você precisa instanciar um objeto de SQLServerColumnEncryptionAzureKeyStoreProvider e registrá-lo com o driver. O nome para este provedor deve ser 'AZURE_KEY_VAULT'.|
|public final boolean getSendTimeAsDatetime()|Retorna a configuração da propriedade de conexão sendTimeAsDatetime.|
|setSendTimeAsDatetime public void (sendTimeAsDateTimeValue boolean)|Modifica a configuração da propriedade de conexão sendTimeAsDatetime.|

 **Classe SQLServerConnectionPoolProxy**
|Nome|Descrição|  
|----------|-----------------|  
|public final boolean getSendTimeAsDatetime()|Retorna a configuração da propriedade de conexão sendTimeAsDatetime.|
|setSendTimeAsDatetime public void (sendTimeAsDateTimeValue boolean)|Modifica a configuração da propriedade de conexão sendTimeAsDatetime.|
     
  
 **Classe SQLServerDataSource**  
  
|Nome|Descrição|  
|----------|-----------------|  
|public void setColumnEncryptionSetting(String columnEncryptionSetting)|Habilita/desabilita a funcionalidade Sempre Criptografado para o objeto de fonte de dados.<br /><br /> O padrão é Disabled.|  
|público getcolumnencryptionsetting () de cadeia de caracteres|Recupera a configuração da funcionalidade Sempre Criptografado para o objeto de fonte de dados.|
|setKeyStoreAuthentication public void (keyStoreAuthentication de cadeia de caracteres)|Define o nome que identifica um repositório de chaves. Somente valor com suporte é o **JavaKeyStorePassword** para identificar o Store de chave Java.<br/><br/>O padrão é nulo.|
|público getKeyStoreAuthentication() de cadeia de caracteres|Obtém o valor da configuração keyStoreAuthentication para o objeto de fonte de dados.|
|setKeyStoreSecret public void (keyStoreSecret de cadeia de caracteres)|Define a senha para o repositório de chaves Java. A senha para o repositório de chaves e a chave deve ser o mesmo. Observe que keyStoreAuthentication deve ser definida com **JavaKeyStorePassword**.|
|setKeyStoreLocation public void (keyStoreLocation de cadeia de caracteres)|Define o local, incluindo o nome de arquivo para o repositório de chaves Java. Observe que keyStoreAuthentication deve ser definida com **JavaKeyStorePassword**.|
|público getKeyStoreLocation() de cadeia de caracteres|Recupera o keyStoreLocation para a Store de chave Java.|
  
 **Classe SQLServerColumnEncryptionJavaKeyStoreProvider**  
  
 A implementação do provedor de repositórios de chaves para o Repositório de Chaves do Java. Essa classe permite o uso de certificados armazenados no repositório de chaves do Java como chaves mestras de coluna.  
  
 Construtores  
  
|Nome|Descrição|  
|----------|-----------------|  
|SQLServerColumnEncryptionJavaKeyStoreProvider pública (keyStoreLocation de cadeia de caracteres, char [] keyStoreSecret)|Provedor de repositório de chaves para a Store de chave Java.|  
  
 Métodos  
  
|Nome|Descrição|  
|----------|-----------------|  
|public byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey)|Descriptografa o valor criptografado especificado de uma coluna da chave de criptografia. O valor criptografado deve ser criptografado usando o certificado com o caminho da chave especificado e o algoritmo especificado.<br /><br /> **O formato do caminho da chave deve ser um dos seguintes:**<br /><br /> Impressão digital: < certificate_thumbprint ><br /><br /> Alias: < certificate_alias ><br /><br /> (Substitui SQLServerColumnEncryptionKeyStoreProvider. decryptColumnEncryptionKey (cadeia de caracteres, cadeia de caracteres, Byte[]).)|  
|public byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] plainTextColumnEncryptionKey)|Criptografa uma chave de criptografia de coluna usando o certificado com o caminho da chave especificado e o algoritmo especificado.<br /><br /> **O formato do caminho da chave deve ser um dos seguintes:**<br /><br /> Impressão digital: < certificate_thumbprint ><br /><br /> Alias: < certificate_alias ><br /><br /> (Substitui SQLServerColumnEncryptionKeyStoreProvider. encryptColumnEncryptionKey (cadeia de caracteres, cadeia de caracteres, Byte[]).)|  
|setName public void (nome de cadeia de caracteres)|Define o nome deste provedor de repositório de chaves.|
|public String getName ()|Obtém o nome deste provedor de repositório de chaves.|
  
 **Classe SQLServerColumnEncryptionAzureKeyVaultProvider**  
  
 A implementação do provedor de repositórios de chaves para o Azure Key Vault. Essa classe permite usar chaves armazenadas no cofre de chaves do Azure como chaves mestras de coluna.  
  
 Construtores  
  
|Nome|Descrição|  
|----------|-----------------|  
|público SQLServerColumnEncryptionAzureKeyVaultProvider (cadeia de caracteres clientId, clientKey de cadeia de caracteres)|Provedor de repositório de chaves para o Azure Key Vault.  Você precisa fornecer o identificador e a chave do cliente solicitando o token para autenticar no Azure Key Vault.|  
  
 Métodos  
  
|Nome|Descrição|  
|----------|-----------------|  
|public byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey)|Descriptografa o valor criptografado especificado de uma coluna da chave de criptografia. O valor criptografado deve ser criptografado usando a chave mestra de ID da chave de coluna usando o algoritmo especificado. <br />(Substitui SQLServerColumnEncryptionKeyStoreProvider. decryptColumnEncryptionKey (cadeia de caracteres, cadeia de caracteres, Byte[]).)|  
|public byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] columnEncryptionKey)|Criptografa uma chave de criptografia de coluna usando a chave mestra de coluna especificada e usando o algoritmo especificado. <br />(Substitui SQLServerColumnEncryptionKeyStoreProvider. encryptColumnEncryptionKey (cadeia de caracteres, cadeia de caracteres, Byte[]).)|  
|setName public void (nome de cadeia de caracteres)|Define o nome deste provedor de repositório de chaves.|
|public String getName ()|Obtém o nome deste provedor de repositório de chaves.|  
  
  
 **Interface SQLServerKeyVaultAuthenticationCallback**  
  
 Essa interface contém um método de autenticação do Azure Key Vault, que deve ser implementado pelo usuário.  
  
 Métodos  
  
|Nome|Descrição|  
|----------|-----------------|  
|público getAccessToken de cadeia de caracteres (autoridade de cadeia de caracteres, o recurso de cadeia de caracteres, o escopo de cadeia de caracteres);|O método precisa ser substituído. O método é usado para obter um token para o Azure Key Vault acesso.|  
  
 **Classe SQLServerColumnEncryptionKeyStoreProvider**  
  
 Estenda a classe para implementar um provedor personalizado de repositório de chave.  
  
|Nome|Descrição|  
|----------|-----------------|  
|SQLServerColumnEncryptionKeyStoreProvider|Classe base para todos os provedores de repositório de chaves. Um provedor personalizado precisa derivar dessa classe e substituir suas funções de membro e, em seguida, registrá-lo usando SQLServerConnection. registerColumnEncryptionKeyStoreProviders().|  
  
 Métodos  
  
|Nome|Descrição|  
|----------|-----------------|  
|public abstract byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte [] encryptedColumnEncryptionKey)|Método de classe base para descriptografar o valor especificado de uma coluna da chave de criptografia. O valor criptografado deve ser criptografado usando a chave mestra de coluna com o caminho de chave e o algoritmo especificados.|  
|byte abstrato público [] encryptColumnEncryptionKey (cadeia de caracteres masterKeyPath, encryptionAlgorithm de cadeia de caracteres, byte [] columnEncryptionKey)|Método da classe base para criptografar a criptografia de uma coluna de chave usando a chave mestra de coluna com o caminho da chave especificado e usar o algoritmo especificado.|
|setName void abstrata pública (nome de cadeia de caracteres)|Define o nome deste provedor de repositório de chaves.|
|público GetName abstrata de cadeia de caracteres|Obtém o nome deste provedor de repositório de chaves.|  
  
 Métodos sobrecarregados ou novos no **SQLServerPreparedStatement** classe  
  
|Nome|Descrição|  
|----------|-----------------|  
|público setBigDecimal void (int parameterIndex, BigDecimal x, int precisão, escala de int)<br /><br /> público setObject void (parameterIndex int, o objeto x, int targetSqlType, precisão de inteiros, escala de int)<br /><br /> público setObject void (parameterIndex int, o objeto x, SQLType targetSqlType, precisão de inteiros, escala de número inteiro)<br /><br /> público setTime void (int parameterIndex, time, int escala x)<br /><br /> público setTimestamp void (int parameterIndex, timestamp, int escala x) <br />público setDateTimeOffset void (int parameterIndex, DateTimeOffset, int escala x)|Esses métodos são sobrecarregados com uma precisão ou um argumento de escala ou ambos para dar suporte ao Always Encrypted para tipos de dados específicos que exigem a precisão e informações de escala.|  
|público setMoney void (int parameterIndex, BigDecimal x)<br /><br /> público setSmallMoney void (int parameterIndex, BigDecimal x)<br /><br /> público setUniqueIdentifier void (parameterIndex int, cadeia de caracteres guid)<br /><br /> público setDateTime void (int parameterIndex, timestamp x)<br /><br /> público setSmallDateTime void (int parameterIndex, timestamp x)|Esses métodos são adicionados para dar suporte ao Always Encrypted para o dinheiro de tipos de dados, smallmoney, uniqueidentifier, datetime e smalldatetime. <br/><br/>Observe que o método setTimestamp() existente é usado para enviar valores de parâmetro para a coluna criptografada datetime2. Para datetime criptografados e colunas do tipo smalldatetime usar os novos setDateTime() de métodos e setSmallDateTime() respectivamente.|  
|público setBigDecimal void final (int parameterIndex, BigDecimal x, int precisão, escala de int, boolean forceEncrypt)<br /><br /> setMoney public void final (int parameterIndex, BigDecimal x forceEncrypt boolean)<br /><br /> setSmallMoney public void final (int parameterIndex, BigDecimal x forceEncrypt boolean)<br /><br /> público setBoolean void final (parameterIndex int x boolean, boolean forceEncrypt)<br /><br /> público setByte void final (parameterIndex int, byte x forceEncrypt boolean)<br /><br /> público setBytes void final (parameterIndex int, byte x[], boolean forceEncrypt)<br /><br /> público setUniqueIdentifier void final (parameterIndex int, cadeia de caracteres guid, booliano forceEncrypt)<br /><br /> público setDouble void final (parameterIndex int, double x, forceEncrypt boolean)<br /><br /> público setFloat void final (parameterIndex int, float x, forceEncrypt boolean)<br /><br /> público setInt void final (int parameterIndex, valor int, boolean forceEncrypt)<br /><br /> público setLong void final (parameterIndex int, long x, forceEncrypt boolean)<br /><br /> público setObject final (parameterIndex int, o objeto x, int targetSqlType, precisão de inteiros, escala de int, boolean forceEncrypt)<br /><br /> público setObject void final (parameterIndex int, o objeto x, SQLType targetSqlType, precisão de inteiros, escala de inteiro, booliano forceEncrypt)<br /><br /> público setShort void final (int parameterIndex x curto, forceEncrypt boolean)<br /><br /> público final void setString (int parameterIndex, str de cadeia de caracteres, booliano forceEncrypt)<br /><br /> público setNString void final (parameterIndex int, o valor de cadeia de caracteres, booliano forceEncrypt)<br /><br /> público setTime void final (int parameterIndex, time, int escala x, forceEncrypt boolean)<br /><br /> público setTimestamp void final (int parameterIndex, timestamp, int escala x, forceEncrypt boolean)<br /><br /> público setDateTimeOffset void final (int parameterIndex, DateTimeOffset, int escala x, forceEncrypt boolean)<br /><br /> público setDateTime void final (int parameterIndex, timestamp x forceEncrypt boolean)<br /><br /> público setSmallDateTime void final (int parameterIndex, timestamp x forceEncrypt boolean)<br /><br /> público setDate void final (int parameterIndex, java.sql.Date x java.util.Calendar cal, forceEncrypt boolean)<br /><br /> público setTime void final (int parameterIndex, time x java.util.Calendar cal, forceEncrypt boolean)<br /><br /> público setTimestamp void final (int parameterIndex, timestamp x java.util.Calendar cal, forceEncrypt boolean)|Define o parâmetro designado como o valor Java fornecido.<br /><br /> Se o forceEncrypt booliano é definido como true, a consulta de parâmetro será ser definido somente se a coluna de designação é criptografada e Always Encrypted estiver habilitado, a conexão ou a instrução.<br /><br /> Se o forceEncrypt booliano é definido como false, o driver não força a criptografia em parâmetros.|  
  
 Métodos sobrecarregados ou novos no **SQLServerCallableStatement** classe  
  
|Nome|Descrição|  
|----------|-----------------|  
|público registerOutParameter void (int parameterIndex, sqlType int, int precisão, escala de int)<br /><br /> public void registerOutParameter(int parameterIndex, SQLType sqlType, int precision, int scale)<br /><br /> público registerOutParameter void (parameterName de cadeia de caracteres, sqlType int, int precisão, escala de int)<br /><br /> public void registerOutParameter(String parameterName, SQLType sqlType, int precision, int scale)<br />público setBigDecimal void (parameterName de cadeia de caracteres, BigDecimal bd, int precisão, escala de int)<br /><br /> público setTime void (parameterName de cadeia de caracteres, time t, escala de int)<br /><br /> público setTimestamp void (parameterName de cadeia de caracteres, t timestamp, int escala)<br /><br /> público setDateTimeOffset void (parameterName de cadeia de caracteres, t DateTimeOffset, escala de int)<br/><br/>público setObject void final (sCol de cadeia de caracteres, objeto x, int targetSqlType, precisão de inteiros, escala de int)|Esses métodos são sobrecarregados com uma precisão ou um argumento de escala ou ambos para dar suporte ao Always Encrypted para tipos de dados específicos que exigem a precisão e informações de escala.|  
|público setDateTime void (parameterName de cadeia de caracteres, timestamp x)<br /><br /> público setSmallDateTime void (parameterName de cadeia de caracteres, timestamp x)<br /><br /> público setUniqueIdentifier void (parameterName de cadeia de caracteres, cadeia de caracteres guid)<br /><br /> público setMoney void (parameterName de cadeia de caracteres, bd BigDecimal)<br /><br /> público setSmallMoney void (parameterName de cadeia de caracteres, bd BigDecimal)<br/><br/>público Timestamp getDateTime (int index)<br/><br/>público Timestamp getDateTime (cadeia de caracteres sCol)<br/><br/>público getDateTime Timestamp (índice int, o cal de calendário)<br/><br/>público Timestamp getSmallDateTime (int index)<br/><br/>público Timestamp getSmallDateTime (cadeia de caracteres sCol)<br/><br/>público getSmallDateTime Timestamp (índice int, o cal de calendário)<br/><br/>público getSmallDateTime Timestamp (nome de cadeia de caracteres, o cal de calendário)<br/><br/>público BigDecimal getMoney (int index)<br/><br/>público BigDecimal getMoney (cadeia de caracteres sCol)<br/><br/>público BigDecimal getSmallMoney (int index)<br/><br/>público BigDecimal getSmallMoney (cadeia de caracteres sCol)|Esses métodos são adicionados para dar suporte ao Always Encrypted para o dinheiro de tipos de dados, smallmoney, uniqueidentifier, datetime e smalldatetime. <br/><br/>Observe que o método setTimestamp() existente é usado para enviar valores de parâmetro para a coluna criptografada datetime2. Para datetime criptografados e colunas do tipo smalldatetime usar os novos setDateTime() de métodos e setSmallDateTime() respectivamente.|  
|público setObject void (parameterName de cadeia de caracteres, o objeto, n int, int m, forceEncrypt boolean)<br /><br /> público setObject void (parameterName de cadeia de caracteres, Object obj, SQLType jdbcType, escala de int, boolean forceEncrypt)<br /><br /> público setDate void (parameterName de cadeia de caracteres, java.sql.Date x c de calendário, forceEncrypt boolean)<br /><br /> público setTime void (parameterName de cadeia de caracteres, time t, escala de int, boolean forceEncrypt)<br /><br /> público setTime void (parameterName de cadeia de caracteres, time x c de calendário, forceEncrypt boolean)<br /><br /> público setDateTime void (parameterName de cadeia de caracteres, timestamp x forceEncrypt boolean)<br /><br /> público setDateTimeOffset void (parameterName de cadeia de caracteres, t DateTimeOffset, escala de int, boolean forceEncrypt)<br /><br /> público setSmallDateTime void (parameterName de cadeia de caracteres, timestamp x forceEncrypt boolean)<br /><br /> público setTimestamp void (parameterName de cadeia de caracteres, timestamp t, escala de int, boolean forceEncrypt)<br /><br /> público setTimestamp void (parameterName de cadeia de caracteres, timestamp x forceEncrypt boolean)<br /><br /> público setUniqueIdentifier void (parameterName de cadeia de caracteres, cadeia de caracteres guid, booliano forceEncrypt)<br /><br /> público setBytes void (parameterName de cadeia de caracteres, byte [] b, forceEncrypt boolean)<br /><br /> público setByte void (parameterName de cadeia de caracteres, byte b, forceEncrypt boolean)<br /><br /> público setString void (parameterName de cadeia de caracteres, cadeia de caracteres s, forceEncrypt boolean)<br /><br /> público setNString void final (parameterName de cadeia de caracteres, o valor de cadeia de caracteres, booliano forceEncrypt)<br /><br /> público setMoney void (parameterName de cadeia de caracteres, bd BigDecimal, forceEncrypt boolean)<br /><br /> público setSmallMoney void (parameterName de cadeia de caracteres, bd BigDecimal, forceEncrypt boolean)<br /><br /> público setBigDecimal void (parameterName de cadeia de caracteres, bd BigDecimal, int precisão, escala de int, boolean forceEncrypt)<br /><br /> público setDouble void (parameterName de cadeia de caracteres, duplo d, forceEncrypt boolean)<br /><br /> público setFloat void (parameterName de cadeia de caracteres, float f, forceEncrypt boolean)<br /><br /> público setInt void (parameterName de cadeia de caracteres, int i, forceEncrypt boolean)<br /><br /> público setLong void (parameterName de cadeia de caracteres longa l, forceEncrypt boolean)<br /><br /> público setShort void (parameterName de cadeia de caracteres curta s, forceEncrypt boolean)<br /><br /> público setBoolean void (parameterNames de cadeia de caracteres, booliano b, forceEncrypt boolean)<br/><br/>público setTimeStamp void (cadeia de caracteres sCol, timestamp x c de calendário, forceEncrypt booliano)|Define o parâmetro designado como o valor Java fornecido.<br /><br /> Se o forceEncrypt booliano é definido como true, a consulta de parâmetro será ser definido somente se a coluna de designação é criptografada e Always Encrypted estiver habilitado, a conexão ou a instrução.<br /><br /> Se o forceEncrypt booliano é definido como false, o driver não força a criptografia em parâmetros.|
 

 Métodos sobrecarregados ou novos no **SQLServerResultSet** classe  
  
|Nome|Descrição|  
|----------|-----------------|  
|público getUniqueIdentifier de cadeia de caracteres (columnIndex int)<br/><br/>público getUniqueIdentifier de cadeia de caracteres (cadeia de caracteres columnLabel)<br/><br/>   timestamp público getDateTime (columnIndex int) <br/><br/> timestamp público getDateTime (columnName de cadeia de caracteres)   <br/><br/> timestamp público getDateTime (columnIndex int, o cal de calendário)   <br/><br/>timestamp público getDateTime (cadeia de caracteres colName, cal de calendário)    <br/><br/>timestamp público getSmallDateTime (columnIndex int)    <br/><br/> timestamp público getSmallDateTime (columnName de cadeia de caracteres)   <br/><br/> timestamp público getSmallDateTime (columnIndex int, o cal de calendário)   <br/><br/> timestamp público getSmallDateTime (cadeia de caracteres colName, cal de calendário)   <br/><br/>  público BigDecimal getMoney (columnIndex int)  <br/><br/> público BigDecimal getMoney (columnName de cadeia de caracteres)   <br/><br/> público BigDecimal getSmallMoney (columnIndex int)   <br/><br/>  público BigDecimal getSmallMoney (columnName de cadeia de caracteres)  <br/><br/>público updateMoney void (columnName de cadeia de caracteres, BigDecimal x)    <br/><br/>  público updateSmallMoney void (columnName de cadeia de caracteres, BigDecimal x)  <br/><br/>     público updateDateTime void (int index, timestamp x) <br/><br/> público updateSmallDateTime void (int index, timestamp x) |Esses métodos são adicionados para dar suporte ao Always Encrypted para dinheiro de tipos de dados, smallmoney, uniqueidentifier, datetime e smalldatetime. <br/><br/>Observe que o método updateTimestamp() existente é usado para atualizar as colunas datetime2 criptografado. Para datetime criptografados e colunas do tipo smalldatetime usar os novos updateDateTime() de métodos e updateSmallDateTime() respectivamente.|
|público updateBoolean void (índice de int, boolean x, forceEncrypt booliano)  <br/><br/>  público updateByte void (índice de int, byte x forceEncrypt boolean)  <br/><br/>  público updateShort void (índice int x curto, forceEncrypt boolean)  <br/><br/> público updateInt void (índice de int, int x forceEncrypt boolean)   <br/><br/>  público updateLong void (índice int, long x, forceEncrypt boolean)  <br/><br/> público updateFloat void (índice de int, float x, forceEncrypt boolean)   <br/><br/> público updateDouble void (índice de int, double x, forceEncrypt boolean)   <br/><br/> updateMoney public void (int index, BigDecimal x forceEncrypt boolean)   <br/><br/>  updateMoney public void (columnName de cadeia de caracteres, BigDecimal x forceEncrypt boolean)  <br/><br/> updateSmallMoney public void (int index, BigDecimal x forceEncrypt boolean)   <br/><br/>  updateSmallMoney public void (columnName de cadeia de caracteres, BigDecimal x forceEncrypt boolean)  <br/><br/> público updateBigDecimal void (int index, BigDecimal x, a precisão de inteiros, escala de número inteiro, booliano forceEncrypt)   <br/><br/>  público updateString void (int columnIndex, stringValue de cadeia de caracteres, booliano forceEncrypt)  <br/><br/>  público updateNString void (int columnIndex, ncadeia de caracteres de cadeia de caracteres, booliano forceEncrypt)  <br/><br/>  público updateNString void (columnLabel de cadeia de caracteres, ncadeia de caracteres de cadeia de caracteres, booliano forceEncrypt)  <br/><br/> público updateBytes void (índice int, byte x[], boolean forceEncrypt)   <br/><br/>  público updateDate void (índice de int, java.sql.Date x forceEncrypt boolean)  <br/><br/> updateTime void pública (int index, time, x, escala de número inteiro, booliano forceEncrypt)   <br/><br/> público updateTimestamp void (int index, timestamp, int escala x, forceEncrypt boolean)   <br/><br/> público updateDateTime void (int index, timestamp, x, escala de número inteiro, booliano forceEncrypt)   <br/><br/> público updateSmallDateTime void (int index, timestamp, x, escala de número inteiro, booliano forceEncrypt)   <br/><br/>  público updateDateTimeOffset void (int index, DateTimeOffset, x, escala de número inteiro, booliano forceEncrypt)  <br/><br/> updateUniqueIdentifier public void (índice de int, cadeia de caracteres x forceEncrypt boolean)    <br/><br/>  público updateObject void (índice int, o objeto x, int precisão, escala de int, boolean forceEncrypt)  <br/><br/>  público updateObject void (int index, Object obj, SQLType targetSqlType, escala de int, boolean forceEncrypt)  <br/><br/> público updateBoolean void (columnName de cadeia de caracteres, x boolean, boolean forceEncrypt)    <br/><br/>  público updateByte void (columnName de cadeia de caracteres, byte x forceEncrypt boolean)  <br/><br/>  público updateShort void (columnName de cadeia de caracteres curta x, forceEncrypt boolean)  <br/><br/> público updateInt void (columnName de cadeia de caracteres, int x forceEncrypt boolean)   <br/><br/>   público updateLong void (columnName de cadeia de caracteres longa x, forceEncrypt boolean) <br/><br/>  público updateFloat void (columnName de cadeia de caracteres, float x, forceEncrypt boolean)  <br/><br/>  público updateDouble void (columnName de cadeia de caracteres, duplo x, forceEncrypt boolean)  <br/><br/> updateBigDecimal public void (columnName de cadeia de caracteres, BigDecimal x forceEncrypt boolean)   <br/><br/>  público updateBigDecimal void (columnName de cadeia de caracteres, BigDecimal x, a precisão de inteiros, escala de número inteiro, booliano forceEncrypt)  <br/><br/> updateString public void (columnName de cadeia de caracteres, cadeia de caracteres x forceEncrypt boolean)   <br/><br/>  público updateBytes void (columnName de cadeia de caracteres, byte x[], boolean forceEncrypt)  <br/><br/> público updateDate void (columnName de cadeia de caracteres, java.sql.Date x forceEncrypt boolean)   <br/><br/>  updateTime void pública (columnName de cadeia de caracteres, time, int escala x, forceEncrypt boolean)  <br/><br/>  público updateTimestamp void (columnName de cadeia de caracteres, timestamp, int escala x, forceEncrypt boolean)  <br/><br/> público updateDateTime void (columnName de cadeia de caracteres, timestamp, int escala x, forceEncrypt boolean)   <br/><br/>  público updateSmallDateTime void (columnName de cadeia de caracteres, timestamp, int escala x, forceEncrypt boolean)  <br/><br/>  público updateDateTimeOffset void (columnName de cadeia de caracteres, DateTimeOffset, int escala x, forceEncrypt boolean)  <br/><br/>  updateUniqueIdentifier public void (columnName de cadeia de caracteres, cadeia de caracteres x forceEncrypt boolean)<br/><br/>público updateObject void (columnName de cadeia de caracteres, objeto x, int precisão, escala de int, boolean forceEncrypt)<br/><br/>público updateObject void (columnName de cadeia de caracteres, Object obj, SQLType targetSqlType, escala de int, boolean forceEncrypt)|Atualize a coluna designada como o valor java fornecido.<br/><br/>Se o forceEncrypt booliano é definido como true, a coluna será apenas ser definida se ela é criptografada e Always Encrypted estiver habilitado, a conexão ou a instrução.<br/><br/>Se o forceEncrypt booliano é definido como false, o driver não força a criptografia em parâmetros.|

  
Novos tipos no **microsoft.sql.Types** classe
|Nome|Descrição|  
|----------|-----------------|  
|DATETIME, SMALLDATETIME, MONEY, SMALLMONEY, GUID|Usar esses tipos como tipos SQL de destino ao enviar valores de parâmetro **criptografado** datetime, smalldatetime, money, smallmoney, colunas uniqueidentifier usando métodos setObject()/updateObject() API.|  
  
  
 **SQLServerStatementColumnEncryptionSetting Enum**  
  
 Especifica como os dados serão enviados e recebidos durante a leitura e gravação de colunas criptografadas. Dependendo da consulta específica, o impacto no desempenho pode ser reduzido ignorando o processamento do driver Always Encrypted quando colunas criptografadas não estão sendo usadas. Observe que essas configurações não podem ser usadas para ignorar a criptografia e obter acesso aos dados de texto sem formatação.  
  
 **Sintaxe**  
  
```java
Public enum  SQLServerStatementColumnEncryptionSetting  
```  
  
 **Membros**  
  
|Nome|Descrição|  
|----------|-----------------|  
|UseConnectionSetting|Especifica que o comando deve usar como padrão para a configuração Always Encrypted na cadeia de conexão.|  
|Habilitado|Habilita o Always Encrypted para a consulta.|  
|ResultSetOnly|Especifica que somente os resultados do comando devem ser processados pela rotina do Always Encrypted no driver. Use esse valor quando o comando não tem parâmetros que exigem criptografia.|  
|Desabilitado|Desabilita o Always Encrypted para a consulta.|  
  
 A configuração de nível de instrução para AE é adicionada à classe SQLServerConnection e à classe SQLServerConnectionPoolProxy. Os seguintes métodos nessas classes são sobrecarregados com a nova configuração.  
  
|Nome|Descrição|  
|----------|-----------------|  
|público createStatement de instrução (int nType, nConcur int, int statementHoldability, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)|Cria um objeto de instrução que irá gerar objetos do conjunto de resultados com o determinado tipo, simultaneidade, colocação em espera e configuração de criptografia de coluna.|  
|público prepareCall CallableStatement (cadeia de caracteres sql, nType int, int nConcur, int statementHoldability, SQLServerStatementColumnEncryptionSetting stmtColEncSetiing)|Cria um objeto CallableStatement com a configuração de criptografia de coluna especificada que irá gerar objetos do conjunto de resultados com o determinado tipo, simultaneidade e colocação em espera.|  
|público prepareStatement PreparedStatement (cadeia de caracteres sql, int autogeneratedKeys, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)|Cria um objeto PreparedStatement com a configuração de criptografia de coluna especificada que tem a capacidade de recuperar as chaves geradas automaticamente.|  
|público prepareStatement PreparedStatement (cadeia de caracteres sql, cadeia de caracteres [] columnNames, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)|Cria um objeto PreparedStatement com a configuração de criptografia de coluna especificada que irá gerar objetos do conjunto de resultados com os nomes de coluna especificada.|  
|público prepareStatement PreparedStatement (cadeia de caracteres sql, int [] columnIndexes, SQLServerStatementColumnEncryptionSetting stmtColEncSetting|Cria um objeto PreparedStatement com a configuração de criptografia de coluna especificada que irá gerar objetos do conjunto de resultados com os índices de coluna especificada.|  
|público prepareStatement PreparedStatement (cadeia de caracteres sql, nType int, int nConcur, int nHold, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)|Cria um objeto PreparedStatement com a configuração de criptografia de coluna especificada que irá gerar objetos do conjunto de resultados com o determinado tipo, simultaneidade e colocação em espera.|  
  
> [!NOTE]  
>  Se o Always Encrypted está desabilitada para uma consulta e a consulta tenha parâmetros que precisam ser criptografados (parâmetros que correspondem a colunas criptografadas), a consulta falhará.  
>   
>  Se o Always Encrypted está desabilitada para uma consulta e a consulta retorna resultados de colunas criptografadas, a consulta retornará valores criptografados. Os valores criptografados terá o tipo de dados varbinary.  
  
 ## <a name="see-also"></a>Consulte Também  
 [Use Always Encrypted com o Driver JDBC](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)  
  

