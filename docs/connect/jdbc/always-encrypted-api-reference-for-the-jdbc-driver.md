---
title: Referência da API do Always Encrypted para o JDBC Driver | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6962a2aa-9508-4d4f-a78c-905e2bc68615
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 691e1c573e2f96c0727970fac858bcfe761d22fc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47831064"
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
|Novos métodos:<br /><br /> `public static void setColumnEncryptionTrustedMasterKeyPaths(Map<String, List\<String>> trustedKeyPaths)`<br /><br /> `public static void updateColumnEncryptionTrustedMasterKeyPaths(String server, List\<String> trustedKeyPaths)`<br /><br /> `public static void removeColumnEncryptionTrustedMasterKeyPaths(String server)`|Permite que você defina/atualize/remova uma lista de caminhos de chave confiáveis para um servidor de banco de dados. Se, durante o processamento de uma consulta de aplicativo, o driver receber um caminho de chave que não esteja na lista, a consulta falhará. Essa propriedade fornece proteção adicional contra ataques de segurança que envolvem o envio de um SQL Server comprometido fornecendo caminhos de chave falsos, que podem levar à perda das credenciais do repositório de chaves.|  
|Novo método:<br /><br /> `public static Map<String, List\<String>> getColumnEncryptionTrustedMasterKeyPaths()`|Retorna uma lista de caminhos confiáveis de chave para um servidor de banco de dados.|  
|Novo método:<br /><br /> `public static void registerColumnEncryptionKeyStoreProviders (Map\<String, SQLServerColumnEncryptionKeyStoreProvider> clientKeyStoreProviders)`|Permite que você registre os provedores de repositório de chaves personalizado. É um dicionário que mapeia nomes de provedor de repositório de chaves para implementações do provedor de repositório de chaves.<br /><br /> Para usar o repositório de chaves da JVM, você precisa criar uma instância de um objeto SQLServerColumnEncryptionJVMKeyStoreProvider com credenciais do repositório de chaves da JVM e registrá-lo com o driver. O nome desse provedor precisa ser ‘MSSQL_JVM_KEYSTORE’.<br /><br /> Para usar o armazenamento do Azure Key Vault, você precisa instanciar um objeto de SQLServerColumnEncryptionAzureKeyStoreProvider e registrá-lo com o driver. O nome para este provedor deve ser 'AZURE_KEY_VAULT'.|
|`public final boolean getSendTimeAsDatetime()`|Retorna a configuração da propriedade de conexão sendTimeAsDatetime.|
|`public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)`|Modifica a configuração da propriedade de conexão sendTimeAsDatetime.|

 **Classe SQLServerConnectionPoolProxy**
|Nome|Descrição|  
|----------|-----------------|  
|`public final boolean getSendTimeAsDatetime()` | Retorna a configuração da propriedade de conexão sendTimeAsDatetime.|
|`public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)` | Modifica a configuração da propriedade de conexão sendTimeAsDatetime.|
     
  
 **Classe SQLServerDataSource**  
  
|Nome|Descrição|  
|----------|-----------------|  
|`public void setColumnEncryptionSetting(String columnEncryptionSetting)`|Habilita/desabilita a funcionalidade Sempre Criptografado para o objeto de fonte de dados.<br /><br /> O padrão é Disabled.|  
|`public String getColumnEncryptionSetting()`|Recupera a configuração da funcionalidade Sempre Criptografado para o objeto de fonte de dados.|
|`public void setKeyStoreAuthentication(String keyStoreAuthentication)`|Define o nome que identifica um repositório de chaves. Somente valor com suporte é o **JavaKeyStorePassword** para identificar o Store de chave Java.<br/><br/>O padrão é nulo.|
|`public String getKeyStoreAuthentication()`|Obtém o valor da configuração keyStoreAuthentication para o objeto de fonte de dados.|
|`public void setKeyStoreSecret(String keyStoreSecret)`|Define a senha para o repositório de chaves Java. A senha para o repositório de chaves e a chave deve ser o mesmo. Observe que keyStoreAuthentication deve ser definida com **JavaKeyStorePassword**.|
|`public void setKeyStoreLocation(String keyStoreLocation)`|Define o local, incluindo o nome de arquivo para o repositório de chaves Java. Observe que keyStoreAuthentication deve ser definida com **JavaKeyStorePassword**.|
|`public String getKeyStoreLocation()`|Recupera o keyStoreLocation para a Store de chave Java.|
  
 **Classe SQLServerColumnEncryptionJavaKeyStoreProvider**  
  
 A implementação do provedor de repositórios de chaves para o Repositório de Chaves do Java. Essa classe permite o uso de certificados armazenados no repositório de chaves do Java como chaves mestras de coluna.  
  
 Construtores  
  
|Nome|Descrição|  
|----------|-----------------|  
|`public SQLServerColumnEncryptionJavaKeyStoreProvider (String keyStoreLocation, char[] keyStoreSecret)`|Provedor de repositório de chaves para a Store de chave Java.|  
  
 Métodos  
  
|Nome|Descrição|  
|----------|-----------------|  
|`public byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey)`|Descriptografa o valor criptografado especificado de uma coluna da chave de criptografia. O valor criptografado deve ser criptografado usando o certificado com o caminho da chave especificado e o algoritmo especificado.<br /><br /> **O formato do caminho da chave deve ser um dos seguintes:**<br /><br /> Impressão digital: < certificate_thumbprint ><br /><br /> Alias: < certificate_alias ><br /><br /> (Substitui SQLServerColumnEncryptionKeyStoreProvider. decryptColumnEncryptionKey (cadeia de caracteres, cadeia de caracteres, Byte[]).)|  
|`public byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] plainTextColumnEncryptionKey)`|Criptografa uma chave de criptografia de coluna usando o certificado com o caminho da chave especificado e o algoritmo especificado.<br /><br /> **O formato do caminho da chave deve ser um dos seguintes:**<br /><br /> Impressão digital: < certificate_thumbprint ><br /><br /> Alias: < certificate_alias ><br /><br /> (Substitui SQLServerColumnEncryptionKeyStoreProvider. encryptColumnEncryptionKey (cadeia de caracteres, cadeia de caracteres, Byte[]).)|  
|`public void setName (String name)`|Define o nome deste provedor de repositório de chaves.|
|`public String getName ()`|Obtém o nome deste provedor de repositório de chaves.|
  
 **Classe SQLServerColumnEncryptionAzureKeyVaultProvider**  
  
 A implementação do provedor de repositórios de chaves para o Azure Key Vault. Essa classe permite usar chaves armazenadas no cofre de chaves do Azure como chaves mestras de coluna.  
  
 Construtores  
  
|Nome|Descrição|  
|----------|-----------------|  
|`public SQLServerColumnEncryptionAzureKeyVaultProvider (String clientId, String clientKey)`|Provedor de repositório de chaves para o Azure Key Vault.  Você precisa fornecer o identificador e a chave do cliente solicitando o token para autenticar no Azure Key Vault.|  
  
 Métodos  
  
|Nome|Descrição|  
|----------|-----------------|  
| `public byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey)` | Decryptes uma chave de criptografia de coluna criptografada (CEK). Essa descriptografia é realizada por um algoritmo de criptografia RSA que usa a chave assimétrica especificada pelo caminho da chave mestra.<br />(Substitui SQLServerColumnEncryptionKeyStoreProvider. decryptColumnEncryptionKey (cadeia de caracteres, cadeia de caracteres, Byte[]).) |  
| `public byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] columnEncryptionKey)` | Criptografa uma chave de criptografia de coluna, fornecendo a chave mestra da coluna especificada para o algoritmo especificado.<br />(Substitui SQLServerColumnEncryptionKeyStoreProvider. encryptColumnEncryptionKey (cadeia de caracteres, cadeia de caracteres, Byte[]).) |  
|`public void setName (String name)`|Define o nome deste provedor de repositório de chaves.|
|`public String getName ()`|Obtém o nome deste provedor de repositório de chaves.|  
  
  
 **Interface SQLServerKeyVaultAuthenticationCallback**  
  
 Essa interface contém um método de autenticação do Azure Key Vault, que deve ser implementado pelo usuário.  
  
 Métodos  
  
|Nome|Descrição|  
|----------|-----------------|  
|`public String getAccessToken(String authority, String resource, String scope);`|O método precisa ser substituído. O método é usado para obter um token para o Azure Key Vault acesso.|  
  
 **Classe SQLServerColumnEncryptionKeyStoreProvider**  
  
 Estenda a classe para implementar um provedor personalizado de repositório de chave.  
  
|Nome|Descrição|  
|----------|-----------------|  
|SQLServerColumnEncryptionKeyStoreProvider|Classe base para todos os provedores de repositório de chaves. Um provedor personalizado precisa derivar dessa classe e substituir suas funções de membro e, em seguida, registrá-lo usando SQLServerConnection. registerColumnEncryptionKeyStoreProviders().|  
  
 Métodos  
  
|Nome|Descrição|  
|----------|-----------------|  
|`public abstract byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte [] encryptedColumnEncryptionKey)`|Método de classe base para descriptografar o valor especificado de uma coluna da chave de criptografia. O valor criptografado deve ser criptografado usando a chave mestra de coluna com o caminho de chave e o algoritmo especificados.|  
|`public abstract byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[]  columnEncryptionKey)`|Método da classe base para criptografar a criptografia de uma coluna de chave usando a chave mestra de coluna com o caminho da chave especificado e usar o algoritmo especificado.|
|`public abstract void setName(String name)`|Define o nome deste provedor de repositório de chaves.|
|`public abstract String getName()`|Obtém o nome deste provedor de repositório de chaves.|  
  
 Métodos sobrecarregados ou novos no **SQLServerPreparedStatement** classe  
  
|Nome|Descrição|  
|----------|-----------------|  
|`public void setBigDecimal(int parameterIndex, BigDecimal x, int precision, int scale)`<br /><br /> `public void setObject(int parameterIndex, Object x, int targetSqlType, Integer precision, int scale)`<br /><br /> `public void setObject(int parameterIndex, Object x, SQLType targetSqlType, Integer precision, Integer scale)`<br /><br /> `public void setTime(int parameterIndex, java.sql.Time x, int scale)`<br /><br /> `public void setTimestamp(int parameterIndex, java.sql.Timestamp x, int scale)` <br />`public void setDateTimeOffset(int parameterIndex, microsoft.sql.DateTimeOffset x, int scale)`|Esses métodos são sobrecarregados com uma precisão ou um argumento de escala ou ambos para dar suporte ao Always Encrypted para tipos de dados específicos que exigem a precisão e informações de escala.|  
|`public void setMoney(int parameterIndex, BigDecimal x)`<br /><br /> `public void setSmallMoney(int parameterIndex, BigDecimal x)`<br /><br /> `public void setUniqueIdentifier(int parameterIndex, String guid)`<br /><br /> `public void setDateTime(int parameterIndex, java.sql.Timestamp x)`<br /><br /> `public void setSmallDateTime(int parameterIndex, java.sql.Timestamp x)`|Esses métodos são adicionados para dar suporte ao Always Encrypted para o dinheiro de tipos de dados, smallmoney, uniqueidentifier, datetime e smalldatetime. <br/><br/>Observe que o existente `setTimestamp()` método é usado para enviar valores de parâmetro para a coluna criptografada datetime2. Para os novos métodos de uso de colunas criptografadas de datetime e smalldatetime `setDateTime()` e `setSmallDateTime()` , respectivamente.|  
|`public final void setBigDecimal(int parameterIndex, BigDecimal x, int precision, int scale, boolean forceEncrypt)`<br /><br /> `public final void setMoney(int parameterIndex, BigDecimal x, boolean forceEncrypt)`<br /><br /> `public final void setSmallMoney(int parameterIndex, BigDecimal x, boolean forceEncrypt)`<br /><br /> `public final void setBoolean(int parameterIndex, boolean x, boolean forceEncrypt)`<br /><br /> `public final void setByte(int parameterIndex, byte x, boolean forceEncrypt)`<br /><br /> `public final void setBytes(int parameterIndex, byte x[], boolean forceEncrypt)`<br /><br /> `public final void setUniqueIdentifier(int parameterIndex, String guid, boolean forceEncrypt)`<br /><br /> `public final void setDouble(int parameterIndex, double x, boolean forceEncrypt)`<br /><br /> `public final void setFloat(int parameterIndex, float x, boolean forceEncrypt)`<br /><br /> `public final void setInt(int parameterIndex, int value, boolean forceEncrypt)`<br /><br /> `public final void setLong(int parameterIndex, long x, boolean forceEncrypt)`<br /><br /> `public final setObject(int parameterIndex, Object x, int targetSqlType, Integer precision, int scale, boolean forceEncrypt)`<br /><br /> `public final void setObject(int parameterIndex, Object x, SQLType targetSqlType, Integer precision, Integer scale, boolean forceEncrypt)`<br /><br /> `public final void setShort(int parameterIndex, short x, boolean forceEncrypt)`<br /><br /> `public final void setString(int parameterIndex, String str, boolean forceEncrypt)`<br /><br /> `public final void setNString(int parameterIndex, String value, boolean forceEncrypt)`<br /><br /> `public final void setTime(int parameterIndex, java.sql.Time x, int scale, boolean forceEncrypt)`<br /><br /> `public final void setTimestamp(int parameterIndex, java.sql.Timestamp x, int scale, boolean forceEncrypt)`<br /><br /> `public final void setDateTimeOffset(int parameterIndex, microsoft.sql.DateTimeOffset x, int scale, boolean forceEncrypt)`<br /><br /> `public final void setDateTime(int parameterIndex, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public final void setSmallDateTime(int parameterIndex, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public final void setDate(int parameterIndex, java.sql.Date x, java.util.Calendar cal, boolean forceEncrypt)`<br /><br /> `public final void setTime(int parameterIndex, java.sql.Time x, java.util.Calendar cal, boolean forceEncrypt)`<br /><br /> `public final void setTimestamp(int parameterIndex, java.sql.Timestamp x, java.util.Calendar cal, boolean forceEncrypt)`|Define o parâmetro designado como o valor Java fornecido.<br /><br /> Se o forceEncrypt booliano é definido como true, a consulta de parâmetro será ser definido somente se a coluna de designação é criptografada e Always Encrypted estiver habilitado, a conexão ou a instrução.<br /><br /> Se o forceEncrypt booliano é definido como false, o driver não força a criptografia em parâmetros.|  
  
 Métodos sobrecarregados ou novos no **SQLServerCallableStatement** classe  
  
|Nome|Descrição|  
|----------|-----------------|  
|`public void registerOutParameter(int parameterIndex, int sqlType, int precision, int scale)`<br /><br /> `public void registerOutParameter(int parameterIndex, SQLType sqlType, int precision, int scale)`<br /><br /> `public void registerOutParameter(String parameterName, int sqlType, int precision, int scale)`<br /><br /> `public void registerOutParameter(String parameterName, SQLType sqlType, int precision, int scale)`<br />`public void setBigDecimal(String parameterName, BigDecimal bd, int precision, int scale)`<br /><br /> `public void setTime(String parameterName, java.sql.Time t, int scale)`<br /><br /> `public void setTimestamp(String parameterName, java.sql.Timestamp t, int scale)`<br /><br /> `public void setDateTimeOffset(String parameterName, microsoft.sql.DateTimeOffset t, int scale)`<br/><br/>`public final void setObject(String sCol, Object x, int targetSqlType, Integer precision, int scale)`|Esses métodos são sobrecarregados com uma precisão ou um argumento de escala ou ambos para dar suporte ao Always Encrypted para tipos de dados específicos que exigem a precisão e informações de escala.|  
|`public void setDateTime(String parameterName, java.sql.Timestamp x)`<br /><br /> `public void setSmallDateTime(String parameterName, java.sql.Timestamp x)`<br /><br /> `public void setUniqueIdentifier(String parameterName, String guid)`<br /><br /> `public void setMoney(String parameterName, BigDecimal bd)`<br /><br /> `public void setSmallMoney(String parameterName, BigDecimal bd)`<br/><br/>`public Timestamp getDateTime(int index)`<br/><br/>`public Timestamp getDateTime(String sCol)`<br/><br/>`public Timestamp getDateTime(int index, Calendar cal)`<br/><br/>`public Timestamp getSmallDateTime(int index)`<br/><br/>`public Timestamp getSmallDateTime(String sCol)`<br/><br/>`public Timestamp getSmallDateTime(int index, Calendar cal)`<br/><br/>`public Timestamp getSmallDateTime(String name, Calendar cal)`<br/><br/>`public BigDecimal getMoney(int index)`<br/><br/>`public BigDecimal getMoney(String sCol)`<br/><br/>`public BigDecimal getSmallMoney(int index)`<br/><br/>`public BigDecimal getSmallMoney(String sCol)`|Esses métodos são adicionados para dar suporte ao Always Encrypted para o dinheiro de tipos de dados, smallmoney, uniqueidentifier, datetime e smalldatetime. <br/><br/>Observe que o existente `setTimestamp()` método é usado para enviar valores de parâmetro para a coluna criptografada datetime2. Para os novos métodos de uso de colunas criptografadas de datetime e smalldatetime `setDateTime()` e `setSmallDateTime()` , respectivamente.|  
|`public void setObject(String parameterName, Object o, int n, int m, boolean forceEncrypt)`<br /><br /> `public void setObject(String parameterName, Object obj, SQLType jdbcType, int scale, boolean forceEncrypt)`<br /><br /> `public void setDate(String parameterName, java.sql.Date x, Calendar c, boolean forceEncrypt)`<br /><br /> `public void setTime(String parameterName, java.sql.Time t, int scale, boolean forceEncrypt)`<br /><br /> `public void setTime(String parameterName, java.sql.Time x, Calendar c, boolean forceEncrypt)`<br /><br /> `public void setDateTime(String parameterName, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public void setDateTimeOffset(String parameterName, microsoft.sql.DateTimeOffset t, int scale, boolean forceEncrypt)`<br /><br /> `public void setSmallDateTime(String parameterName, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public void setTimestamp(String parameterName, java.sql.Timestamp t, int scale, boolean forceEncrypt)`<br /><br /> `public void setTimestamp(String parameterName, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public void setUniqueIdentifier(String parameterName, String guid, boolean forceEncrypt)`<br /><br /> `public void setBytes(String parameterName, byte[] b, boolean forceEncrypt)`<br /><br /> `public void setByte(String parameterName, byte b, boolean forceEncrypt)`<br /><br /> `public void setString(String parameterName, String s, boolean forceEncrypt)`<br /><br /> `public final void setNString(String parameterName, String value, boolean forceEncrypt)<br /><br /> public void setMoney(String parameterName, BigDecimal bd, boolean forceEncrypt)`<br /><br /> `public void setSmallMoney(String parameterName, BigDecimal bd, boolean forceEncrypt)`<br /><br /> `public void setBigDecimal(String parameterName, BigDecimal bd, int precision, int scale, boolean forceEncrypt)`<br /><br /> `public void setDouble(String parameterName, double d, boolean forceEncrypt)`<br /><br /> `public void setFloat(String parameterName, float f, boolean forceEncrypt)`<br /><br /> `public void setInt(String parameterName, int i, boolean forceEncrypt)`<br /><br /> `public void setLong(String parameterName, long l, boolean forceEncrypt)`<br /><br /> `public void setShort(String parameterName, short s, boolean forceEncrypt)`<br /><br /> `public void setBoolean(String parameterNames, boolean b, boolean forceEncrypt)`<br/><br/>`public void setTimeStamp(String sCol, java.sql.Timestamp x, Calendar c, Boolean forceEncrypt)`|Define o parâmetro designado como o valor Java fornecido.<br /><br /> Se o forceEncrypt booliano é definido como true, a consulta de parâmetro será ser definido somente se a coluna de designação é criptografada e Always Encrypted estiver habilitado, a conexão ou a instrução.<br /><br /> Se o forceEncrypt booliano é definido como false, o driver não força a criptografia em parâmetros.|
 

 Métodos sobrecarregados ou novos no **SQLServerResultSet** classe  
  
|Nome|Descrição|  
|----------|-----------------|  
|`public String getUniqueIdentifier(int columnIndex)`<br/><br/>`public String getUniqueIdentifier(String columnLabel)`<br/><br/>   `public java.sql.Timestamp getDateTime(int columnIndex)` <br/><br/> `public java.sql.Timestamp getDateTime(String columnName)`   <br/><br/> `public java.sql.Timestamp getDateTime(int columnIndex, Calendar cal)`   <br/><br/>`public java.sql.Timestamp getDateTime(String colName, Calendar cal)`    <br/><br/>`public java.sql.Timestamp getSmallDateTime(int columnIndex)`    <br/><br/> `public java.sql.Timestamp getSmallDateTime(String columnName)`   <br/><br/> `public java.sql.Timestamp getSmallDateTime(int columnIndex, Calendar cal)`   <br/><br/> `public java.sql.Timestamp getSmallDateTime(String colName, Calendar cal)`   <br/><br/>  `public BigDecimal getMoney(int columnIndex)`  <br/><br/> `public BigDecimal getMoney(String columnName)`   <br/><br/> `public BigDecimal getSmallMoney(int columnIndex)`   <br/><br/>  `public BigDecimal getSmallMoney(String columnName)`  <br/><br/>`public void updateMoney(String columnName, BigDecimal x)`    <br/><br/>  `public void updateSmallMoney(String columnName, BigDecimal x)`  <br/><br/>     `public void updateDateTime(int index, java.sql.Timestamp x)` <br/><br/> `public void updateSmallDateTime(int index, java.sql.Timestamp x)` |Esses métodos são adicionados para dar suporte ao Always Encrypted para dinheiro de tipos de dados, smallmoney, uniqueidentifier, datetime e smalldatetime. <br/><br/>Observe que o existente `updateTimestamp()` método é usado para atualizar as colunas datetime2 criptografado. Para os novos métodos de uso de colunas criptografadas de datetime e smalldatetime `updateDateTime()` e `updateSmallDateTime()` , respectivamente.|
|`public void updateBoolean(int index, boolean x, boolean forceEncrypt)`  <br/><br/>  `public void updateByte(int index, byte x, boolean forceEncrypt)`  <br/><br/>  `public void updateShort(int index, short x, boolean forceEncrypt)`  <br/><br/> `public void updateInt(int index, int x, boolean forceEncrypt)`   <br/><br/>  `public void updateLong(int index, long x, boolean forceEncrypt)`  <br/><br/> `public void updateFloat(int index, float x, boolean forceEncrypt)`   <br/><br/> `public void updateDouble(int index, double x, boolean forceEncrypt)`   <br/><br/> `public void updateMoney(int index, BigDecimal x, boolean forceEncrypt)`   <br/><br/>  `public void updateMoney(String columnName, BigDecimal x, boolean forceEncrypt)`  <br/><br/> `public void updateSmallMoney(int index, BigDecimal x, boolean forceEncrypt)`   <br/><br/>  `public void updateSmallMoney(String columnName, BigDecimal x, boolean forceEncrypt)`  <br/><br/> `public void updateBigDecimal(int index, BigDecimal x, Integer precision, Integer scale, boolean forceEncrypt)`   <br/><br/>  `public void updateString(int columnIndex, String stringValue, boolean forceEncrypt)`  <br/><br/>  `public void updateNString(int columnIndex, String nString, boolean forceEncrypt)`  <br/><br/>  `public void updateNString(String columnLabel, String nString, boolean forceEncrypt)`  <br/><br/> `public void updateBytes(int index, byte x[], boolean forceEncrypt)   <br/><br/>  public void updateDate(int index, java.sql.Date x, boolean forceEncrypt)`  <br/><br/> `public void updateTime(int index, java.sql.Time x, Integer scale, boolean forceEncrypt)`   <br/><br/> `public void updateTimestamp(int index, java.sql.Timestamp x, int scale, boolean forceEncrypt)`   <br/><br/> `public void updateDateTime(int index, java.sql.Timestamp x, Integer scale, boolean forceEncrypt)`   <br/><br/> `public void updateSmallDateTime(int index, java.sql.Timestamp x, Integer scale, boolean forceEncrypt)`   <br/><br/>  `public void updateDateTimeOffset(int index, microsoft.sql.DateTimeOffset x, Integer scale, boolean forceEncrypt)`  <br/><br/> `public void updateUniqueIdentifier(int index, String x, boolean forceEncrypt)`    <br/><br/>  `public void updateObject(int index, Object x, int precision, int scale, boolean forceEncrypt)`  <br/><br/>  `public void updateObject(int index, Object obj, SQLType targetSqlType, int scale, boolean forceEncrypt)`  <br/><br/> `public void updateBoolean(String columnName, boolean x, boolean forceEncrypt)`    <br/><br/>  `public void updateByte(String columnName, byte x, boolean forceEncrypt)`  <br/><br/>  `public void updateShort(String columnName, short x, boolean forceEncrypt)`  <br/><br/> `public void updateInt(String columnName, int x, boolean forceEncrypt)`   <br/><br/>   `public void updateLong(String columnName, long x, boolean forceEncrypt)` <br/><br/>  `public void updateFloat(String columnName, float x, boolean forceEncrypt)`  <br/><br/>  `public void updateDouble(String columnName, double x, boolean forceEncrypt)  <br/><br/> public void updateBigDecimal(String columnName, BigDecimal x, boolean forceEncrypt)`   <br/><br/>  `public void updateBigDecimal(String columnName, BigDecimal x, Integer precision, Integer scale, boolean forceEncrypt)`  <br/><br/> `public void updateString(String columnName, String x, boolean forceEncrypt)`   <br/><br/>  `public void updateBytes(String columnName, byte x[], boolean forceEncrypt)`  <br/><br/> `public void updateDate(String columnName, java.sql.Date x, boolean forceEncrypt)`   <br/><br/>  `public void updateTime(String columnName, java.sql.Time x, int scale, boolean forceEncrypt)`  <br/><br/>  `public void updateTimestamp(String columnName, java.sql.Timestamp x, int scale, boolean forceEncrypt)`  <br/><br/> `public void updateDateTime(String columnName, java.sql.Timestamp x, int scale, boolean forceEncrypt)`   <br/><br/>  `public void updateSmallDateTime(String columnName, java.sql.Timestamp x, int scale, boolean forceEncrypt)`  <br/><br/>  `public void updateDateTimeOffset(String columnName, microsoft.sql.DateTimeOffset x, int scale, boolean forceEncrypt)`  <br/><br/>  `public void updateUniqueIdentifier(String columnName, String x, boolean forceEncrypt)`<br/><br/>`public void updateObject(String columnName, Object x, int precision, int scale, boolean forceEncrypt)`<br/><br/>`public void updateObject(String columnName, Object obj, SQLType targetSqlType, int scale, boolean forceEncrypt)`|Atualize a coluna designada como o valor java fornecido.<br/><br/>Se o forceEncrypt booliano é definido como true, a coluna será apenas ser definida se ela é criptografada e Always Encrypted estiver habilitado, a conexão ou a instrução.<br/><br/>Se o forceEncrypt booliano é definido como false, o driver não força a criptografia em parâmetros.|

  
Novos tipos no **microsoft.sql.Types** classe
|Nome|Descrição|  
|----------|-----------------|  
|DATETIME, SMALLDATETIME, MONEY, SMALLMONEY, GUID|Usar esses tipos como tipos SQL de destino ao enviar valores de parâmetro **criptografado** datetime, smalldatetime, money, smallmoney, colunas uniqueidentifier usando `setObject()/updateObject()` métodos da API.|  
  
  
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
|`public Statement createStatement(int nType, int nConcur, int statementHoldability, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)`|Cria um objeto de instrução que irá gerar objetos do conjunto de resultados com o determinado tipo, simultaneidade, colocação em espera e configuração de criptografia de coluna.|  
|`public CallableStatement prepareCall(String sql, int nType, int nConcur, int statementHoldability, SQLServerStatementColumnEncryptionSetting stmtColEncSetiing)`|Cria um objeto CallableStatement com a configuração de criptografia de coluna especificada que irá gerar objetos do conjunto de resultados com o determinado tipo, simultaneidade e colocação em espera.|  
|`public PreparedStatement prepareStatement(String sql, int autogeneratedKeys, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)`|Cria um objeto PreparedStatement com a configuração de criptografia de coluna especificada que tem a capacidade de recuperar as chaves geradas automaticamente.|  
|`public PreparedStatement prepareStatement(String sql, String[] columnNames, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)`|Cria um objeto PreparedStatement com a configuração de criptografia de coluna especificada que irá gerar objetos do conjunto de resultados com os nomes de coluna especificada.|  
|`public PreparedStatement prepareStatement(String sql, int[] columnIndexes, SQLServerStatementColumnEncryptionSetting stmtColEncSetting`|Cria um objeto PreparedStatement com a configuração de criptografia de coluna especificada que irá gerar objetos do conjunto de resultados com os índices de coluna especificada.|  
|`public PreparedStatement prepareStatement(String sql, int nType, int nConcur, int nHold, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)`|Cria um objeto PreparedStatement com a configuração de criptografia de coluna especificada que irá gerar objetos do conjunto de resultados com o determinado tipo, simultaneidade e colocação em espera.|  
  
> [!NOTE]  
>  Se o Always Encrypted está desabilitada para uma consulta e a consulta tenha parâmetros que precisam ser criptografados (parâmetros que correspondem a colunas criptografadas), a consulta falhará.  
>   
>  Se o Always Encrypted está desabilitada para uma consulta e a consulta retorna resultados de colunas criptografadas, a consulta retornará valores criptografados. Os valores criptografados terá o tipo de dados varbinary.  
  
 ## <a name="see-also"></a>Consulte Também  
 [Use Always Encrypted com o Driver JDBC](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)  
  

