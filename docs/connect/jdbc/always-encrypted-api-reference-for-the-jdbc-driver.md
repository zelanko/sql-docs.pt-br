---
title: Referência da API do Always Encrypted para o JDBC Driver | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6962a2aa-9508-4d4f-a78c-905e2bc68615
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8b975fcc9fae02ec5e54d48191e3ab8aa5ac0ee8
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922655"
---
# <a name="always-encrypted-api-reference-for-the-jdbc-driver"></a>Referência da API do Always Encrypted para o JDBC Driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Always Encrypted permite que os clientes criptografem os dados confidenciais em aplicativos de cliente e nunca revelem as chaves de criptografia para o SQL Server. Um driver habilitado para Always Encrypted instalado no computador cliente obtém essa funcionalidade criptografando e descriptografando dados confidenciais automaticamente no aplicativo cliente do SQL Server. O driver criptografa as colunas de dados confidenciais antes de passar os dados para o SQL Server e reconfigura automaticamente as consultas para que a semântica do aplicativo seja preservada. Da mesma forma, o driver descriptografa de modo transparente os dados armazenados em colunas de banco de dados criptografadas dos resultados da consulta. Para obter mais informações, confira [Always Encrypted (Mecanismo de Banco de Dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) e [Como usar Always Encrypted com o JDBC Driver](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md).  
  
> [!NOTE]  
>  Há suporte para o Always Encrypted apenas no Microsoft JDBC Driver 6.0 ou superior para o SQL Server com o SQL Server 2016.  
  
 ## <a name="always-encrypted-api-references"></a>Referências da API do Always Encrypted
 
 Existem diversas novas adições e modificações para a API do driver JDBC para uso em aplicativos cliente que usam Sempre Criptografado.  
  
 **Classe SQLServerConnection**  
  
|Nome|DESCRIÇÃO|  
|----------|-----------------|  
|Nova palavra-chave de cadeia de conexão:<br /><br /> columnEncryptionSetting|columnEncryptionSetting=Enabled habilita a funcionalidade Always Encrypted na conexão e columnEncryptionSetting=Disabled a desabilita. Os valores aceitos são Enabled/Disabled. O padrão é Disabled.|  
|Nova palavra-chave da cadeia de conexão: (MS JDBC 7.4 em diante)<br /><br /> keyVaultProviderClientId <br /><br /> keyVaultProviderClientKey |keyVaultProviderClientId=\<ClientID>;keyVaultProviderClientKey=\<ClientKey> <br/><br/> Registra o SQLServerColumnEncryptionAzureKeyVaultProvider e usa os valores ClientID e ClientKey para recuperar a chave mestra de coluna do Azure Key Vault|  
|Novos métodos:<br /><br /> `public static void setColumnEncryptionTrustedMasterKeyPaths(Map<String, List\<String>> trustedKeyPaths)`<br /><br /> `public static void updateColumnEncryptionTrustedMasterKeyPaths(String server, List\<String> trustedKeyPaths)`<br /><br /> `public static void removeColumnEncryptionTrustedMasterKeyPaths(String server)`|Permite que você defina/atualize/remova uma lista de caminhos de chave confiáveis para um servidor de banco de dados. Se, durante o processamento de uma consulta de aplicativo, o driver receber um caminho de chave que não esteja na lista, a consulta falhará. Essa propriedade fornece proteção adicional contra ataques de segurança que envolvem o envio de um SQL Server comprometido fornecendo caminhos de chave falsos, que podem levar à perda das credenciais do repositório de chaves.|  
|Novo método:<br /><br /> `public static Map<String, List\<String>> getColumnEncryptionTrustedMasterKeyPaths()`|Retorna uma lista de caminhos confiáveis de chave para um servidor de banco de dados.|  
|Novo método:<br /><br /> `public static void registerColumnEncryptionKeyStoreProviders (Map\<String, SQLServerColumnEncryptionKeyStoreProvider> clientKeyStoreProviders)`|Permite que você registre os provedores de repositório de chaves personalizado. É um dicionário que mapeia nomes de provedor de repositório de chaves para implementações do provedor de repositório de chaves.<br /><br /> Para usar o repositório de chaves da JVM, você precisa criar uma instância de um objeto SQLServerColumnEncryptionJVMKeyStoreProvider com credenciais do repositório de chaves da JVM e registrá-lo com o driver. O nome desse provedor deve ser "MSSQL_JVM_KEYSTORE".<br /><br /> Para usar o repositório do Azure Key Vault, você precisa criar uma instância de um objeto SQLServerColumnEncryptionAzureKeyStoreProvider e registrá-lo com o driver. O nome deste provedor deve ser 'AZURE_KEY_VAULT'.|
|`public final boolean getSendTimeAsDatetime()`|Retorna a configuração da propriedade de conexão sendTimeAsDatetime.|
|`public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)`|Modifica a configuração da propriedade de conexão sendTimeAsDatetime.|

 **SQLServerConnectionPoolProxy class**
 
|Nome|DESCRIÇÃO|  
|----------|-----------------|  
|`public final boolean getSendTimeAsDatetime()` | Retorna a configuração da propriedade de conexão sendTimeAsDatetime.|
|`public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)` | Modifica a configuração da propriedade de conexão sendTimeAsDatetime.|
     
  
 **Classe SQLServerDataSource**  
  
|Nome|DESCRIÇÃO|  
|----------|-----------------|  
|`public void setColumnEncryptionSetting(String columnEncryptionSetting)`|Habilita/desabilita a funcionalidade Sempre Criptografado para o objeto de fonte de dados.<br /><br /> O padrão é Disabled.|  
|`public String getColumnEncryptionSetting()`|Recupera a configuração da funcionalidade Sempre Criptografado para o objeto de fonte de dados.|
|`public void setKeyStoreAuthentication(String keyStoreAuthentication)`|Define o nome que identifica um repositório de chaves. O único valor compatível é **JavaKeyStorePassword** para identificar o repositório de chaves Java.<br/><br/>O padrão é nulo.|
|`public String getKeyStoreAuthentication()`|Obtém o valor da configuração keyStoreAuthentication para o objeto de fonte de dados.|
|`public void setKeyStoreSecret(String keyStoreSecret)`|Define a senha para o repositório de chaves Java. A senha do repositório de chaves e a chave devem ser iguais. Observe que keyStoreAuthentication deve ser definido com **JavaKeyStorePassword**.|
|`public void setKeyStoreLocation(String keyStoreLocation)`|Define a localização, incluindo o nome do arquivo para o repositório de chaves Java. Observe que keyStoreAuthentication deve ser definido com **JavaKeyStorePassword**.|
|`public String getKeyStoreLocation()`|Recupera o keyStoreLocation para o Repositório de Chaves Java.|
  
 **Classe SQLServerColumnEncryptionJavaKeyStoreProvider**  
  
 A implementação do provedor de repositórios de chaves para o Repositório de Chaves do Java. Essa classe permite o uso de certificados armazenados no repositório de chaves do Java como chaves mestras de coluna.  
  
 Construtores  
  
|Nome|DESCRIÇÃO|  
|----------|-----------------|  
|`public SQLServerColumnEncryptionJavaKeyStoreProvider (String keyStoreLocation, char[] keyStoreSecret)`|Provedor do repositório de chaves para o Repositório de Chaves Java.|  
  
 Métodos  
  
|Nome|DESCRIÇÃO|  
|----------|-----------------|  
|`public byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey)`|Descriptografa o valor criptografado especificado de uma coluna da chave de criptografia. O valor criptografado deve ser criptografado usando o certificado com o caminho da chave especificado e o algoritmo especificado.<br /><br /> **O formato do caminho da chave deve ser um dos seguintes:**<br /><br /> Thumbprint:<certificate_thumbprint><br /><br /> Alias:<certificate_alias><br /><br /> (Substitui SQLServerColumnEncryptionKeyStoreProvider. decryptColumnEncryptionKey(String, String, Byte[]).)|  
|`public byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] plainTextColumnEncryptionKey)`|Criptografa uma chave de criptografia de coluna usando o certificado com o caminho da chave especificado e o algoritmo especificado.<br /><br /> **O formato do caminho da chave deve ser um dos seguintes:**<br /><br /> Thumbprint:<certificate_thumbprint><br /><br /> Alias:<certificate_alias><br /><br /> (Substitui SQLServerColumnEncryptionKeyStoreProvider. encryptColumnEncryptionKey(String, String, Byte[]).)|  
|`public void setName (String name)`|Define o nome deste provedor de repositório de chaves.|
|`public String getName ()`|Obtém o nome deste provedor de repositório de chaves.|
  
 **Classe SQLServerColumnEncryptionAzureKeyVaultProvider**  
  
 A implementação do provedor de repositórios de chaves para o Azure Key Vault. Essa classe habilita o uso de chaves armazenadas no Azure Key Vault como chaves mestras de coluna.  
  
 Construtores  
  
|Nome|DESCRIÇÃO|  
|----------|-----------------|  
|`public SQLServerColumnEncryptionAzureKeyVaultProvider (String clientId, String clientKey)`|Provedor do repositório de chaves para o Azure Key Vault.  Você precisa fornecer o identificador e a chave do cliente solicitando que o token autentique-se no Azure Key Vault.|  
  
 Métodos  
  
|Nome|DESCRIÇÃO|  
|----------|-----------------|  
| `public byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey)` | Descriptografa uma CEK (chave de criptografia de coluna) criptografada. Essa descriptografia é realizada com um algoritmo de criptografia RSA que usa a chave assimétrica especificada pelo caminho da chave mestra.<br />(Substitui SQLServerColumnEncryptionKeyStoreProvider. decryptColumnEncryptionKey(String, String, Byte[]).) |  
| `public byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] columnEncryptionKey)` | Criptografa uma chave de criptografia de coluna, fornecendo a chave mestra de coluna especificada para o algoritmo especificado.<br />(Substitui SQLServerColumnEncryptionKeyStoreProvider. encryptColumnEncryptionKey(String, String, Byte[]).) |  
|`public void setName (String name)`|Define o nome deste provedor de repositório de chaves.|
|`public String getName ()`|Obtém o nome deste provedor de repositório de chaves.|  
  
  
 **SQLServerKeyVaultAuthenticationCallback Interface**  
  
 Essa interface contém um método para autenticação do Azure Key Vault, que deve ser implementado pelo usuário.  
  
 Métodos  
  
|Nome|DESCRIÇÃO|  
|----------|-----------------|  
|`public String getAccessToken(String authority, String resource, String scope);`|O método precisa ser substituído. O método é usado para obter o token de acesso para o Azure Key Vault.|  
  
 **Classe SQLServerColumnEncryptionKeyStoreProvider**  
  
 Estenda a classe para implementar um provedor personalizado de repositório de chave.  
  
|Nome|DESCRIÇÃO|  
|----------|-----------------|  
|SQLServerColumnEncryptionKeyStoreProvider|Classe base para todos os provedores de repositório de chaves. Um provedor personalizado precisa derivar dessa classe e substituir suas funções de membro e, em seguida, registrá-lo usando SQLServerConnection. registerColumnEncryptionKeyStoreProviders().|  
  
 Métodos  
  
|Nome|DESCRIÇÃO|  
|----------|-----------------|  
|`public abstract byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte [] encryptedColumnEncryptionKey)`|Método de classe base para descriptografar o valor especificado de uma coluna da chave de criptografia. O valor criptografado deve ser criptografado usando a chave mestra de coluna com o caminho de chave e o algoritmo especificados.|  
|`public abstract byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[]  columnEncryptionKey)`|Método da classe base para criptografar a criptografia de uma coluna de chave usando a chave mestra de coluna com o caminho da chave especificado e usar o algoritmo especificado.|
|`public abstract void setName(String name)`|Define o nome deste provedor de repositório de chaves.|
|`public abstract String getName()`|Obtém o nome deste provedor de repositório de chaves.|  
  
 Métodos novos ou sobrecarregados na classe **SQLServerPreparedStatement**  
  
|Nome|DESCRIÇÃO|  
|----------|-----------------|  
|`public void setBigDecimal(int parameterIndex, BigDecimal x, int precision, int scale)`<br /><br /> `public void setObject(int parameterIndex, Object x, int targetSqlType, Integer precision, int scale)`<br /><br /> `public void setObject(int parameterIndex, Object x, SQLType targetSqlType, Integer precision, Integer scale)`<br /><br /> `public void setTime(int parameterIndex, java.sql.Time x, int scale)`<br /><br /> `public void setTimestamp(int parameterIndex, java.sql.Timestamp x, int scale)` <br />`public void setDateTimeOffset(int parameterIndex, microsoft.sql.DateTimeOffset x, int scale)`|Esses métodos são sobrecarregados com uma precisão ou um argumento de escala ou ambos para dar suporte a Always Encrypted para tipos de dados específicos que exigem informações de precisão e escala.|  
|`public void setMoney(int parameterIndex, BigDecimal x)`<br /><br /> `public void setSmallMoney(int parameterIndex, BigDecimal x)`<br /><br /> `public void setUniqueIdentifier(int parameterIndex, String guid)`<br /><br /> `public void setDateTime(int parameterIndex, java.sql.Timestamp x)`<br /><br /> `public void setSmallDateTime(int parameterIndex, java.sql.Timestamp x)`|Esses métodos são adicionados para dar suporte a Always Encrypted para os tipos de dados money, smallmoney, uniqueidentifier, datetime e smalldatetime. <br/><br/>Observe que o método `setTimestamp()` existente é usado para enviar valores de parâmetro para a coluna datetime2 criptografada. Para colunas datetime e smalldatetime criptografadas, use os novos métodos `setDateTime()` e `setSmallDateTime()`, respectivamente.|  
|`public final void setBigDecimal(int parameterIndex, BigDecimal x, int precision, int scale, boolean forceEncrypt)`<br /><br /> `public final void setMoney(int parameterIndex, BigDecimal x, boolean forceEncrypt)`<br /><br /> `public final void setSmallMoney(int parameterIndex, BigDecimal x, boolean forceEncrypt)`<br /><br /> `public final void setBoolean(int parameterIndex, boolean x, boolean forceEncrypt)`<br /><br /> `public final void setByte(int parameterIndex, byte x, boolean forceEncrypt)`<br /><br /> `public final void setBytes(int parameterIndex, byte x[], boolean forceEncrypt)`<br /><br /> `public final void setUniqueIdentifier(int parameterIndex, String guid, boolean forceEncrypt)`<br /><br /> `public final void setDouble(int parameterIndex, double x, boolean forceEncrypt)`<br /><br /> `public final void setFloat(int parameterIndex, float x, boolean forceEncrypt)`<br /><br /> `public final void setInt(int parameterIndex, int value, boolean forceEncrypt)`<br /><br /> `public final void setLong(int parameterIndex, long x, boolean forceEncrypt)`<br /><br /> `public final setObject(int parameterIndex, Object x, int targetSqlType, Integer precision, int scale, boolean forceEncrypt)`<br /><br /> `public final void setObject(int parameterIndex, Object x, SQLType targetSqlType, Integer precision, Integer scale, boolean forceEncrypt)`<br /><br /> `public final void setShort(int parameterIndex, short x, boolean forceEncrypt)`<br /><br /> `public final void setString(int parameterIndex, String str, boolean forceEncrypt)`<br /><br /> `public final void setNString(int parameterIndex, String value, boolean forceEncrypt)`<br /><br /> `public final void setTime(int parameterIndex, java.sql.Time x, int scale, boolean forceEncrypt)`<br /><br /> `public final void setTimestamp(int parameterIndex, java.sql.Timestamp x, int scale, boolean forceEncrypt)`<br /><br /> `public final void setDateTimeOffset(int parameterIndex, microsoft.sql.DateTimeOffset x, int scale, boolean forceEncrypt)`<br /><br /> `public final void setDateTime(int parameterIndex, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public final void setSmallDateTime(int parameterIndex, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public final void setDate(int parameterIndex, java.sql.Date x, java.util.Calendar cal, boolean forceEncrypt)`<br /><br /> `public final void setTime(int parameterIndex, java.sql.Time x, java.util.Calendar cal, boolean forceEncrypt)`<br /><br /> `public final void setTimestamp(int parameterIndex, java.sql.Timestamp x, java.util.Calendar cal, boolean forceEncrypt)`|Define o parâmetro designado como o valor Java fornecido.<br /><br /> Se o booliano forceEncrypt for definido como true, o parâmetro de consulta só será definido se a coluna de designação for criptografada e Always Encrypted estiver habilitada na conexão ou na instrução.<br /><br /> Se o forceEncrypt booliano for definido como false, o driver não forçará a criptografia em parâmetros.|  
  
 Métodos novos ou sobrecarregados na classe **SQLServerCallableStatement**  
  
|Nome|DESCRIÇÃO|  
|----------|-----------------|  
|`public void registerOutParameter(int parameterIndex, int sqlType, int precision, int scale)`<br /><br /> `public void registerOutParameter(int parameterIndex, SQLType sqlType, int precision, int scale)`<br /><br /> `public void registerOutParameter(String parameterName, int sqlType, int precision, int scale)`<br /><br /> `public void registerOutParameter(String parameterName, SQLType sqlType, int precision, int scale)`<br />`public void setBigDecimal(String parameterName, BigDecimal bd, int precision, int scale)`<br /><br /> `public void setTime(String parameterName, java.sql.Time t, int scale)`<br /><br /> `public void setTimestamp(String parameterName, java.sql.Timestamp t, int scale)`<br /><br /> `public void setDateTimeOffset(String parameterName, microsoft.sql.DateTimeOffset t, int scale)`<br/><br/>`public final void setObject(String sCol, Object x, int targetSqlType, Integer precision, int scale)`|Esses métodos são sobrecarregados com uma precisão ou um argumento de escala ou ambos para dar suporte a Always Encrypted para tipos de dados específicos que exigem informações de precisão e escala.|  
|`public void setDateTime(String parameterName, java.sql.Timestamp x)`<br /><br /> `public void setSmallDateTime(String parameterName, java.sql.Timestamp x)`<br /><br /> `public void setUniqueIdentifier(String parameterName, String guid)`<br /><br /> `public void setMoney(String parameterName, BigDecimal bd)`<br /><br /> `public void setSmallMoney(String parameterName, BigDecimal bd)`<br/><br/>`public Timestamp getDateTime(int index)`<br/><br/>`public Timestamp getDateTime(String sCol)`<br/><br/>`public Timestamp getDateTime(int index, Calendar cal)`<br/><br/>`public Timestamp getSmallDateTime(int index)`<br/><br/>`public Timestamp getSmallDateTime(String sCol)`<br/><br/>`public Timestamp getSmallDateTime(int index, Calendar cal)`<br/><br/>`public Timestamp getSmallDateTime(String name, Calendar cal)`<br/><br/>`public BigDecimal getMoney(int index)`<br/><br/>`public BigDecimal getMoney(String sCol)`<br/><br/>`public BigDecimal getSmallMoney(int index)`<br/><br/>`public BigDecimal getSmallMoney(String sCol)`|Esses métodos são adicionados para dar suporte a Always Encrypted para os tipos de dados money, smallmoney, uniqueidentifier, datetime e smalldatetime. <br/><br/>Observe que o método `setTimestamp()` existente é usado para enviar valores de parâmetro para a coluna datetime2 criptografada. Para colunas datetime e smalldatetime criptografadas, use os novos métodos `setDateTime()` e `setSmallDateTime()`, respectivamente.|  
|`public void setObject(String parameterName, Object o, int n, int m, boolean forceEncrypt)`<br /><br /> `public void setObject(String parameterName, Object obj, SQLType jdbcType, int scale, boolean forceEncrypt)`<br /><br /> `public void setDate(String parameterName, java.sql.Date x, Calendar c, boolean forceEncrypt)`<br /><br /> `public void setTime(String parameterName, java.sql.Time t, int scale, boolean forceEncrypt)`<br /><br /> `public void setTime(String parameterName, java.sql.Time x, Calendar c, boolean forceEncrypt)`<br /><br /> `public void setDateTime(String parameterName, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public void setDateTimeOffset(String parameterName, microsoft.sql.DateTimeOffset t, int scale, boolean forceEncrypt)`<br /><br /> `public void setSmallDateTime(String parameterName, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public void setTimestamp(String parameterName, java.sql.Timestamp t, int scale, boolean forceEncrypt)`<br /><br /> `public void setTimestamp(String parameterName, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public void setUniqueIdentifier(String parameterName, String guid, boolean forceEncrypt)`<br /><br /> `public void setBytes(String parameterName, byte[] b, boolean forceEncrypt)`<br /><br /> `public void setByte(String parameterName, byte b, boolean forceEncrypt)`<br /><br /> `public void setString(String parameterName, String s, boolean forceEncrypt)`<br /><br /> `public final void setNString(String parameterName, String value, boolean forceEncrypt)<br /><br /> public void setMoney(String parameterName, BigDecimal bd, boolean forceEncrypt)`<br /><br /> `public void setSmallMoney(String parameterName, BigDecimal bd, boolean forceEncrypt)`<br /><br /> `public void setBigDecimal(String parameterName, BigDecimal bd, int precision, int scale, boolean forceEncrypt)`<br /><br /> `public void setDouble(String parameterName, double d, boolean forceEncrypt)`<br /><br /> `public void setFloat(String parameterName, float f, boolean forceEncrypt)`<br /><br /> `public void setInt(String parameterName, int i, boolean forceEncrypt)`<br /><br /> `public void setLong(String parameterName, long l, boolean forceEncrypt)`<br /><br /> `public void setShort(String parameterName, short s, boolean forceEncrypt)`<br /><br /> `public void setBoolean(String parameterNames, boolean b, boolean forceEncrypt)`<br/><br/>`public void setTimeStamp(String sCol, java.sql.Timestamp x, Calendar c, Boolean forceEncrypt)`|Define o parâmetro designado como o valor Java fornecido.<br /><br /> Se o booliano forceEncrypt for definido como true, o parâmetro de consulta só será definido se a coluna de designação for criptografada e Always Encrypted estiver habilitada na conexão ou na instrução.<br /><br /> Se o forceEncrypt booliano for definido como false, o driver não forçará a criptografia em parâmetros.|
 

 Métodos novos ou sobrecarregados na classe **SQLServerResultSet**  
  
|Nome|DESCRIÇÃO|  
|----------|-----------------|  
|`public String getUniqueIdentifier(int columnIndex)`<br/><br/>`public String getUniqueIdentifier(String columnLabel)`<br/><br/>   `public java.sql.Timestamp getDateTime(int columnIndex)` <br/><br/> `public java.sql.Timestamp getDateTime(String columnName)`   <br/><br/> `public java.sql.Timestamp getDateTime(int columnIndex, Calendar cal)`   <br/><br/>`public java.sql.Timestamp getDateTime(String colName, Calendar cal)`    <br/><br/>`public java.sql.Timestamp getSmallDateTime(int columnIndex)`    <br/><br/> `public java.sql.Timestamp getSmallDateTime(String columnName)`   <br/><br/> `public java.sql.Timestamp getSmallDateTime(int columnIndex, Calendar cal)`   <br/><br/> `public java.sql.Timestamp getSmallDateTime(String colName, Calendar cal)`   <br/><br/>  `public BigDecimal getMoney(int columnIndex)`  <br/><br/> `public BigDecimal getMoney(String columnName)`   <br/><br/> `public BigDecimal getSmallMoney(int columnIndex)`   <br/><br/>  `public BigDecimal getSmallMoney(String columnName)`  <br/><br/>`public void updateMoney(String columnName, BigDecimal x)`    <br/><br/>  `public void updateSmallMoney(String columnName, BigDecimal x)`  <br/><br/>     `public void updateDateTime(int index, java.sql.Timestamp x)` <br/><br/> `public void updateSmallDateTime(int index, java.sql.Timestamp x)` |Esses métodos são adicionados para dar suporte a Always Encrypted para os tipos de dados money, smallmoney, uniqueidentifier, datetime e smalldatetime. <br/><br/>Observe que o método de `updateTimestamp()` existente é usado para atualizar colunas datetime2 criptografadas. Para colunas datetime e smalldatetime criptografadas, use os novos métodos `updateDateTime()` e `updateSmallDateTime()`, respectivamente.|
|`public void updateBoolean(int index, boolean x, boolean forceEncrypt)`  <br/><br/>  `public void updateByte(int index, byte x, boolean forceEncrypt)`  <br/><br/>  `public void updateShort(int index, short x, boolean forceEncrypt)`  <br/><br/> `public void updateInt(int index, int x, boolean forceEncrypt)`   <br/><br/>  `public void updateLong(int index, long x, boolean forceEncrypt)`  <br/><br/> `public void updateFloat(int index, float x, boolean forceEncrypt)`   <br/><br/> `public void updateDouble(int index, double x, boolean forceEncrypt)`   <br/><br/> `public void updateMoney(int index, BigDecimal x, boolean forceEncrypt)`   <br/><br/>  `public void updateMoney(String columnName, BigDecimal x, boolean forceEncrypt)`  <br/><br/> `public void updateSmallMoney(int index, BigDecimal x, boolean forceEncrypt)`   <br/><br/>  `public void updateSmallMoney(String columnName, BigDecimal x, boolean forceEncrypt)`  <br/><br/> `public void updateBigDecimal(int index, BigDecimal x, Integer precision, Integer scale, boolean forceEncrypt)`   <br/><br/>  `public void updateString(int columnIndex, String stringValue, boolean forceEncrypt)`  <br/><br/>  `public void updateNString(int columnIndex, String nString, boolean forceEncrypt)`  <br/><br/>  `public void updateNString(String columnLabel, String nString, boolean forceEncrypt)`  <br/><br/> `public void updateBytes(int index, byte x[], boolean forceEncrypt)   <br/><br/>  public void updateDate(int index, java.sql.Date x, boolean forceEncrypt)`  <br/><br/> `public void updateTime(int index, java.sql.Time x, Integer scale, boolean forceEncrypt)`   <br/><br/> `public void updateTimestamp(int index, java.sql.Timestamp x, int scale, boolean forceEncrypt)`   <br/><br/> `public void updateDateTime(int index, java.sql.Timestamp x, Integer scale, boolean forceEncrypt)`   <br/><br/> `public void updateSmallDateTime(int index, java.sql.Timestamp x, Integer scale, boolean forceEncrypt)`   <br/><br/>  `public void updateDateTimeOffset(int index, microsoft.sql.DateTimeOffset x, Integer scale, boolean forceEncrypt)`  <br/><br/> `public void updateUniqueIdentifier(int index, String x, boolean forceEncrypt)`    <br/><br/>  `public void updateObject(int index, Object x, int precision, int scale, boolean forceEncrypt)`  <br/><br/>  `public void updateObject(int index, Object obj, SQLType targetSqlType, int scale, boolean forceEncrypt)`  <br/><br/> `public void updateBoolean(String columnName, boolean x, boolean forceEncrypt)`    <br/><br/>  `public void updateByte(String columnName, byte x, boolean forceEncrypt)`  <br/><br/>  `public void updateShort(String columnName, short x, boolean forceEncrypt)`  <br/><br/> `public void updateInt(String columnName, int x, boolean forceEncrypt)`   <br/><br/>   `public void updateLong(String columnName, long x, boolean forceEncrypt)` <br/><br/>  `public void updateFloat(String columnName, float x, boolean forceEncrypt)`  <br/><br/>  `public void updateDouble(String columnName, double x, boolean forceEncrypt)  <br/><br/> public void updateBigDecimal(String columnName, BigDecimal x, boolean forceEncrypt)`   <br/><br/>  `public void updateBigDecimal(String columnName, BigDecimal x, Integer precision, Integer scale, boolean forceEncrypt)`  <br/><br/> `public void updateString(String columnName, String x, boolean forceEncrypt)`   <br/><br/>  `public void updateBytes(String columnName, byte x[], boolean forceEncrypt)`  <br/><br/> `public void updateDate(String columnName, java.sql.Date x, boolean forceEncrypt)`   <br/><br/>  `public void updateTime(String columnName, java.sql.Time x, int scale, boolean forceEncrypt)`  <br/><br/>  `public void updateTimestamp(String columnName, java.sql.Timestamp x, int scale, boolean forceEncrypt)`  <br/><br/> `public void updateDateTime(String columnName, java.sql.Timestamp x, int scale, boolean forceEncrypt)`   <br/><br/>  `public void updateSmallDateTime(String columnName, java.sql.Timestamp x, int scale, boolean forceEncrypt)`  <br/><br/>  `public void updateDateTimeOffset(String columnName, microsoft.sql.DateTimeOffset x, int scale, boolean forceEncrypt)`  <br/><br/>  `public void updateUniqueIdentifier(String columnName, String x, boolean forceEncrypt)`<br/><br/>`public void updateObject(String columnName, Object x, int precision, int scale, boolean forceEncrypt)`<br/><br/>`public void updateObject(String columnName, Object obj, SQLType targetSqlType, int scale, boolean forceEncrypt)`|Atualize a coluna designada para o valor Java fornecido.<br/><br/>Se o booliano forceEncrypt for definido como true, a coluna somente será definida se criptografado e Always Encrypted estiverem habilitados na conexão ou na instrução.<br/><br/>Se o forceEncrypt booliano for definido como false, o driver não forçará a criptografia em parâmetros.|

  
Novos tipos na classe **microsoft.sql.types**

|Nome|DESCRIÇÃO|  
|----------|-----------------|  
|DATETIME, SMALLDATETIME, MONEY, SMALLMONEY, GUID|Use esses tipos como os tipos SQL de destino ao enviar valores de **parâmetro** para as colunas DateTime criptografado, smalldatetime, Money, `setObject()/updateObject()` smallmoney e uniqueidentifier usando métodos de API.|  
  
  
 **SQLServerStatementColumnEncryptionSetting Enum**  
  
 Especifica como os dados serão enviados e recebidos durante a leitura e a gravação de colunas criptografadas. Dependendo de sua consulta específica, o impacto no desempenho pode ser reduzido ignorando o processamento do driver Always Encrypted quando colunas não criptografadas estão sendo usadas. Observe que essas configurações não podem ser usadas para ignorar a criptografia e obter acesso a dados de texto sem formatação.  
  
 **Sintaxe**  
  
```java
Public enum  SQLServerStatementColumnEncryptionSetting  
```  
  
 **Membros**  
  
|Nome|DESCRIÇÃO|  
|----------|-----------------|  
|UseConnectionSetting|Especifica que o comando deve usar como padrão a configuração de Always Encrypted na cadeia de conexão.|  
|habilitado|Habilita Always Encrypted para a consulta.|  
|ResultSetOnly|Especifica que somente os resultados do comando devem ser processados pela rotina de Always Encrypted no driver. Use esse valor quando o comando não tiver parâmetros que exijam criptografia.|  
|Desabilitado|Desabilita Always Encrypted para a consulta.|  
  
 A configuração de nível de instrução para criptografia AE é adicionada à classe SQLServerConnection e à classe SQLServerConnectionPoolProxy. Os métodos a seguir nessas classes são sobrecarregados com a nova configuração.  
  
|Nome|DESCRIÇÃO|  
|----------|-----------------|  
|`public Statement createStatement(int nType, int nConcur, int statementHoldability, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)`|Cria um objeto de instrução que gerará objetos ResultSet com as configurações de tipo, simultaneidade, suspensão e criptografia de coluna fornecidas.|  
|`public CallableStatement prepareCall(String sql, int nType, int nConcur, int statementHoldability, SQLServerStatementColumnEncryptionSetting stmtColEncSetiing)`|Cria um objeto CallableStatement com a configuração de criptografia de coluna fornecida que gerará objetos ResultSet com o tipo, a simultaneidade e a suspensão fornecidos.|  
|`public PreparedStatement prepareStatement(String sql, int autogeneratedKeys, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)`|Cria um objeto PreparedStatement com a configuração de criptografia de coluna fornecida que tem a capacidade de recuperar as chaves geradas automaticamente.|  
|`public PreparedStatement prepareStatement(String sql, String[] columnNames, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)`|Cria um objeto PreparedStatement com a configuração de criptografia de coluna fornecida que gerará os objetos ResultSet com os nomes de coluna fornecidos.|  
|`public PreparedStatement prepareStatement(String sql, int[] columnIndexes, SQLServerStatementColumnEncryptionSetting stmtColEncSetting`|Cria um objeto PreparedStatement com a configuração de criptografia de coluna fornecida que gerará os objetos ResultSet com os índices de coluna fornecidos.|  
|`public PreparedStatement prepareStatement(String sql, int nType, int nConcur, int nHold, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)`|Cria um objeto PreparedStatement com a configuração de criptografia de coluna fornecida que gerará objetos ResultSet com o tipo, a simultaneidade e a suspensão fornecidos.|  
  
> [!NOTE]  
>  Se Always Encrypted estiver desabilitado para uma consulta e a consulta tiver parâmetros que precisam ser criptografados (parâmetros que correspondem a colunas criptografadas), a consulta falhará.  
>   
>  Se Always Encrypted estiver desabilitado para uma consulta e a consulta retornar resultados de colunas criptografadas, a consulta retornará valores criptografados. Os valores criptografados terão o tipo de dados varbinary.  
  
 ## <a name="see-also"></a>Confira também  
 [Como usar Always Encrypted com o JDBC Driver](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)  
  

