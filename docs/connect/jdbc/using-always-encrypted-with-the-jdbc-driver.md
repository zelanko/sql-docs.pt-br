---
title: Como usar Always Encrypted com o JDBC Driver | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 271c0438-8af1-45e5-b96a-4b1cabe32707
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 31f81cb2e12360956d14d1706b119233add94a35
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594097"
---
# <a name="using-always-encrypted-with-the-jdbc-driver"></a>Como usar o Always Encrypted com o driver JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Esta página fornece informações sobre como desenvolver aplicativos Java usando [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md) e o Microsoft JDBC Driver 6,0 (ou superior) para SQL Server.

O Always Encrypted permite que os clientes criptografem dados confidenciais e nunca revelem os dados nem as chaves de criptografia para o SQL Server ou o Banco de Dados SQL do Azure. Um driver habilitado para Always Encrypted, como o Microsoft JDBC Driver 6.0 (ou superior) for SQL Server, consegue esse comportamento criptografando e descriptografando de modo transparente dados confidenciais no aplicativo cliente. O driver determina automaticamente quais parâmetros de consulta correspondem às colunas de banco de dados confidenciais (protegidas com o Always Encrypted) e criptografa os valores desses parâmetros antes de passar os dados para o SQL Server ou o Banco de Dados SQL do Azure. Da mesma forma, o driver descriptografa de modo transparente os dados recuperados das colunas de banco de dados criptografadas nos resultados da consulta. Para obter mais informações, consulte [Always Encrypted (Mecanismo de Banco de Dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) e [referência de API Always Encrypted para o driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).

## <a name="prerequisites"></a>Prerequisites
- Verifique se o Microsoft JDBC Driver 6,0 (ou superior) para SQL Server está instalado em seu computador de desenvolvimento. 
- Baixe e instale os arquivos de política de jurisdição de força ilimitada de Java Cryptography Extension (JCE).  Leia o arquivo Leiame incluído no arquivo zip para instruções de instalação e detalhes relevantes sobre problemas possíveis de importação/exportação.  

    - Se você estiver usando o mssql-jdbc-X.X.X.jre7.jar ou o sqljdbc41.jar, os arquivos de política poderão ser baixados de [Download dos arquivos de política de jurisdição de força ilimitada do JCE (Java Cryptography Extension) 7](https://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)

    - Se você estiver usando o mssql-jdbc-X.X.X.jre8.jar ou o sqljdbc42.jar, os arquivos de política poderão ser baixados de [Download dos arquivos de política de jurisdição de força ilimitada do JCE (Java Cryptography Extension) 8](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)

    - Se estiver usando o mssql-jdbc-X. X. X. jre9. jar, nenhum arquivo de política precisará ser baixado. A política de jurisdição em Java 9 usa como padrão a criptografia de força ilimitada.

## <a name="working-with-column-master-key-stores"></a>Como trabalhar com repositórios de chaves mestras de coluna
Para criptografar ou descriptografar dados para colunas criptografadas, SQL Server mantém as chaves de criptografia de coluna. As chaves de criptografia de coluna são armazenadas em formato criptografado nos metadados do banco de dados. Cada chave de criptografia de coluna tem uma chave mestra de coluna correspondente usada para criptografar a chave de criptografia de coluna. Os metadados do banco de dados não contêm as chaves mestras de coluna. Essas chaves só são mantidas pelo cliente. No entanto, os metadados do banco de dados contêm informações sobre onde as chaves mestras de coluna são armazenadas em relação ao cliente. Por exemplo, os metadados do banco de dados podem dizer que o repositório de chaves que contém uma chave mestra de coluna é o repositório de certificados do Windows e o certificado específico usado para criptografar e descriptografar está localizado em um caminho específico dentro do repositório de certificados do Windows. Se o cliente tiver acesso a esse certificado no repositório de certificados do Windows, ele poderá obter o certificado. O certificado pode então ser usado para descriptografar a chave de criptografia da coluna. Em seguida, essa chave de criptografia pode ser usada para descriptografar ou criptografar dados para colunas criptografadas que usam essa chave de criptografia de coluna.

O Provedor de Dados .NET Framework para SQL Server se comunica com um repositório de chaves usando um provedor de repositórios de chaves mestras de coluna – que é uma instância de uma classe derivada da Classe **SqlColumnEncryptionKeyStoreProvider**.

### <a name="using-built-in-column-master-key-store-providers"></a>Usando provedores internos de repositórios de chaves mestras de coluna
O Microsoft JDBC Driver para SQL Server vem com os seguintes provedores internos de repositório de chaves mestras de coluna. Alguns desses provedores são previamente registrados com os nomes de provedor específicos (usados para pesquisar o provedor) e alguns exigem credenciais adicionais ou um registro explícito.

| Classe                                                 | Descrição                                        | Nome (de pesquisa) do provedor  | Está previamente registrado? |
| :---------------------------------------------------- | :------------------------------------------------- | :---------------------- | :----------------- |
| **SQLServerColumnEncryptionAzureKeyVaultProvider**    | Um provedor de um repositório de chaves para o Azure Key Vault. | AZURE_KEY_VAULT         | Não                 |
| **SQLServerColumnEncryptionCertificateStoreProvider** | Um provedor para o Repositório de Certificados do Windows.      | MSSQL_CERTIFICATE_STORE | Sim                |
| **SQLServerColumnEncryptionJavaKeyStoreProvider**     | Um provedor para o repositório de chaves Java                   | MSSQL_JAVA_KEYSTORE     | Sim                |

Para os provedores de repositório de chaves previamente registrados, você não precisa fazer nenhuma alteração no código do aplicativo para usar esses provedores, mas observe os seguintes itens:

- Você (ou seu DBA) precisa verificar se o nome do provedor configurado nos metadados da chave mestra de coluna está correto e se o caminho da chave mestra de coluna está em conformidade com o formato do caminho da chave válido para determinado provedor. É recomendável configurar as chaves usando ferramentas como o SQL Server Management Studio, que gera automaticamente os nomes de provedor válidos e os caminhos de chaves ao emitir a instrução CREATE COLUMN MASTER KEY (Transact-SQL).
- Garanta que seu aplicativo possa acessar a chave no repositório de chaves. Essa tarefa pode envolver a concessão de acesso para o aplicativo à chave e/ou ao repositório de chaves, dependendo do repositório de chaves, ou a execução de outras etapas de configuração específicas do repositório de chaves. Por exemplo, para usar o SQLServerColumnEncryptionJavaKeyStoreProvider, você precisa fornecer o local e a senha do keystore nas propriedades de conexão. 

Todos esses provedores de repositório de chaves são descritos mais detalhadamente nas seções a seguir. Você só precisa implementar um provedor de keystore para usar Always Encrypted.

### <a name="using-azure-key-vault-provider"></a>Usando o provedor do Cofre de Chaves do Azure
O Azure Key Vault é uma opção conveniente para armazenar e gerenciar chaves mestras de coluna do Always Encrypted (especialmente se o seu aplicativo está hospedado no Azure). O Microsoft JDBC Driver para SQL Server inclui um provedor interno, SQLServerColumnEncryptionAzureKeyVaultProvider, para aplicativos que têm chaves armazenadas no Azure Key Vault. O nome deste provedor é AZURE_KEY_VAULT. Para usar o provedor de repositório de Azure Key Vault, um desenvolvedor de aplicativo precisa criar o cofre e as chaves em Azure Key Vault e criar um registro de aplicativo no Azure Active Directory. O aplicativo registrado deve receber as permissões obter, descriptografar, criptografar, desencapsular chave, encapsular chave e verificar nas políticas de acesso definidas para o cofre de chaves criado para uso com Always Encrypted. Para obter mais informações sobre como configurar o cofre de chaves e criar uma chave mestra de coluna, consulte [Azure Key Vault passo a passo](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/) e [criando chaves mestras de coluna no Azure Key Vault](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md#creating-column-master-keys-in-azure-key-vault).

Para os exemplos nesta página, se você tiver criado uma chave mestra de coluna com base em Azure Key Vault e uma chave de criptografia de coluna usando SQL Server Management Studio, o script T-SQL para recriá-las poderá ser semelhante a este exemplo com seu próprio **específico KEY_PATH** e **ENCRYPTED_VALUE**:

```sql
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'AZURE_KEY_VAULT',
    KEY_PATH = N'https://<MyKeyValutName>.vault.azure.net:443/keys/Always-Encrypted-Auto1/c61f01860f37302457fa512bb7e7f4e8'
)

CREATE COLUMN ENCRYPTION KEY [MyCEK]
WITH VALUES
(
    COLUMN_MASTER_KEY = [MyCMK],
    ALGORITHM = 'RSA_OAEP',
    ENCRYPTED_VALUE = 0x01BA000001680074507400700073003A002F002F006400610076006...
)
```

Para usar o Azure Key Vault, os aplicativos cliente precisam criar uma instância do SQLServerColumnEncryptionAzureKeyVaultProvider e registrá-lo com o driver.

Aqui está um exemplo de inicialização de SQLServerColumnEncryptionAzureKeyVaultProvider:  

```java
SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
```

**clientID** é a ID do aplicativo de um registro de aplicativo em uma instância de Azure Active Directory. **Clientkey vazio** é uma senha de chave registrada no aplicativo, que fornece acesso à API para o Azure Key Vault.

Depois que o aplicativo cria uma instância de SQLServerColumnEncryptionAzureKeyVaultProvider, o aplicativo deve registrar a instância com o driver usando o método SQLServerConnection. registerColumnEncryptionKeyStoreProviders (). É altamente recomendável que a instância seja registrada usando o nome de pesquisa padrão, AZURE_KEY_VAULT, que pode ser obtido chamando a API SQLServerColumnEncryptionAzureKeyVaultProvider. getName (). Usar o nome padrão permitirá que você use ferramentas como o SQL Server Management Studio ou o PowerShell para provisionar e gerenciar Always Encrypted chaves (as ferramentas usam o nome padrão para gerar o objeto de metadados para a chave mestra de coluna). O exemplo a seguir mostra o registro do provedor de Azure Key Vault. Para obter mais informações sobre o método SQLServerConnection. registerColumnEncryptionKeyStoreProviders (), consulte [Always Encrypted referência da API para o driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).

```java
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
keyStoreMap.put(akvProvider.getName(), akvProvider);
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
```

> [!IMPORTANT]
>  Se você usar o provedor de repositório de chaves Azure Key Vault, a implementação Azure Key Vault do driver JDBC terá dependências nessas bibliotecas (do GitHub) que devem ser incluídas no aplicativo:
>
>  [azure-sdk-for-java](https://github.com/Azure/azure-sdk-for-java)
>
>  [azure-activedirectory-library-for-java libraries](https://github.com/AzureAD/azure-activedirectory-library-for-java)
>
> Para obter um exemplo de como incluir essas dependências em um projeto Maven, consulte [baixar dependências ADAL4J e AKV com o Apache Maven](https://github.com/Microsoft/mssql-jdbc/wiki/Download-ADAL4J-And-AKV-Dependencies-with-Apache-Maven)

### <a name="using-windows-certificate-store-provider"></a>Uso do Provedor do Repositório de Certificados do Windows
O SQLServerColumnEncryptionCertificateStoreProvider pode ser usado para armazenar chaves mestras de coluna no Repositório de Certificados do Windows. Use o assistente de Always Encrypted SQL Server Management Studio (SSMS) ou outras ferramentas com suporte para criar as definições de chave mestra de coluna e chave de criptografia de coluna no banco de dados. O mesmo assistente pode ser usado para gerar um certificado autoassinado no repositório de certificados do Windows que pode ser usado como uma chave mestra de coluna para os dados de Always Encrypted. Para obter mais informações sobre a chave mestra de coluna e a sintaxe T-SQL da chave de criptografia de coluna, consulte [criar chave mestra de coluna](../../t-sql/statements/create-column-master-key-transact-sql.md) e [criar chave de criptografia de coluna](../../t-sql/statements/create-column-encryption-key-transact-sql.md) respectivamente.

O nome do SQLServerColumnEncryptionCertificateStoreProvider é MSSQL_CERTIFICATE_STORE e pode ser consultado pela API getName () do objeto do provedor. Ele é registrado automaticamente pelo driver e pode ser usado sem qualquer alteração no aplicativo.

Para os exemplos nesta página, se você tiver criado uma chave mestra de coluna baseada no repositório de certificados do Windows e uma chave de criptografia de coluna usando SQL Server Management Studio, o script T-SQL para recriá-los pode ser semelhante a este exemplo com seu próprio **específico KEY_PATH** e **ENCRYPTED_VALUE**:

```sql
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',
    KEY_PATH = N'CurrentUser/My/A2A91F59C461B559E4D962DA9D2BC6131B32CB91'
)

CREATE COLUMN ENCRYPTION KEY [MyCEK]
WITH VALUES
(
    COLUMN_MASTER_KEY = [MyCMK],
    ALGORITHM = 'RSA_OAEP',
    ENCRYPTED_VALUE = 0x016E000001630075007200720065006E0074007500730065007200...
)
```

> [!IMPORTANT]
> Embora os outros provedores de repositório de chaves neste artigo estejam disponíveis em todas as plataformas com suporte pelo driver, a implementação SQLServerColumnEncryptionCertificateStoreProvider do driver JDBC está disponível somente em sistemas operacionais Windows. Ele tem uma dependência no sqljdbc_auth. dll que está disponível no pacote de driver. Para usar esse provedor, copie o arquivo sqljdbc_auth.dll para um diretório no caminho do sistema Windows no computador em que o driver JDBC está instalado. Como alternativa, você pode definir a propriedade do sistema java.libary.path para especificar o diretório de sqljdbc_auth.dll. Se você estiver executando uma Máquina Virtual Java (JVM) de 32 bits, use o arquivo sqljdbc_auth.dll na pasta x86, mesmo se o sistema operacional for a versão x64. Se estiver executando uma JVM de 64 bits em um processador x64, use o arquivo sqljdbc_auth.dll na pasta x64. Por exemplo, se você estiver usando a JVM de 32 bits e o driver JDBC estiver instalado no diretório padrão, você poderá especificar o local da DLL usando o seguinte argumento de VM (máquina virtual) quando o aplicativo Java for iniciado: `-Djava.library.path=C:\Microsoft JDBC Driver <version> for SQL Server\sqljdbc_<version>\enu\auth\x86`

### <a name="using-java-key-store-provider"></a>Como usar o provedor de repositório de chaves Java
O driver JDBC vem com uma implementação de provedor de repositório de chaves interno para o Repositório de Chaves Java. Se a propriedade de cadeia de conexão **keyStoreAuthentication** estiver presente na cadeia de conexão e estiver definida como "JavaKeyStorePassword", o driver instanciará e registrará automaticamente o provedor para o repositório de chaves Java. O nome do provedor de repositório de chaves da JVM é MSSQL_JVM_KEYSTORE. Esse nome também pode ser consultado usando a API SQLServerColumnEncryptionJavaKeyStoreProvider. getName (). 

Há três propriedades de cadeia de conexão que permitem que um aplicativo cliente especifique as credenciais que o driver precisa para autenticar no repositório de chaves Java. O driver Inicializa o provedor com base nos valores dessas três propriedades na cadeia de conexão.

**keyStoreAuthentication:** identifica o repositório de chaves Java a ser usado. Com o Microsoft JDBC Driver 6,0 e superior para SQL Server, você pode autenticar para o repositório de chaves Java somente por meio dessa propriedade. Para o repositório de chaves Java, o valor dessa propriedade deve ser `JavaKeyStorePassword`.

**keyStoreLocation:** o caminho para o arquivo de repositório de chaves Java que armazena a chave mestra de coluna. O caminho inclui o nome de arquivo do repositório de chaves.

**keyStoreSecret:** o segredo/senha a ser usado para o repositório de chaves, bem como para a chave. Para usar o repositório de chaves Java, o keystore e a senha de chave devem ser iguais.

Aqui está um exemplo de como fornecer essas credenciais na cadeia de conexão:

```java
String connectionUrl = "jdbc:sqlserver://<server>:<port>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path_to_the_keystore_file>;keyStoreSecret=<keystore_key_password>";
```

Você também pode obter ou definir essas configurações usando o objeto SQLServerDataSource. Confira [Referência de API do Always Encrypted para o JDBC Driver](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)

O driver JDBC instancia automaticamente o SQLServerColumnEncryptionJavaKeyStoreProvider quando essas credenciais estão presentes nas propriedades da conexão.

### <a name="creating-a-column-master-key-for-the-java-key-store"></a>Criando uma chave mestra de coluna (CMK) para o repositório de chaves da JVM
O SQLServerColumnEncryptionJavaKeyStoreProvider pode ser usado com os tipos de repositório de chaves JKS ou PKCS12. Para criar ou importar uma chave para usar com esse provedor, use o utilitário Java [keytool](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html) Utility. A chave deve ter a mesma senha que o repositório de chaves em si. Aqui está um exemplo de como criar uma chave pública e sua chave privada associada usando o utilitário keytool:

```
keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.jks -storepass mypassword -validity 360 -keysize 2048 -storetype jks
```

Esse comando cria uma chave pública e a encapsula em um certificado autoassinado X. 509, que é armazenado no repositório de chaves ' keystore. jks ' junto com sua chave privada associada. Essa entrada no keystore é identificada pelo alias ' AlwaysEncryptedKey '.

Veja um exemplo do mesmo usando um tipo de armazenamento PKCS12:

```
keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.pfx -storepass mypassword -validity 360 -keysize 2048 -storetype pkcs12 -keypass mypassword
```

Se o keystore for do tipo PKCS12, o utilitário keytool não solicitará uma senha de chave e a senha de chave precisará ser fornecida com a opção-Keypass, pois o SQLServerColumnEncryptionJavaKeyStoreProvider requer que o keystore e a chave tenham o mesmo la.

Você também pode exportar um certificado do repositório de certificados do Windows no formato. pfx e usá-lo com o SQLServerColumnEncryptionJavaKeyStoreProvider. O certificado exportado também pode ser importado para o repositório de chaves Java como um tipo de keystore de JKS.

Depois de criar a entrada keytool, crie os metadados da chave mestra de coluna no banco de dados, que precisa do nome do provedor do repositório de chaves e do caminho da chave. Para obter mais informações sobre como criar metadados de chave mestra de coluna, consulte [criar chave mestra de coluna](../../t-sql/statements/create-column-master-key-transact-sql.md). Para SQLServerColumnEncryptionJavaKeyStoreProvider, o caminho da chave é apenas o alias da chave e o nome do SQLServerColumnEncryptionJavaKeyStoreProvider é ' MSSQL_JAVA_KEYSTORE '. Você também pode consultar esse nome usando a API pública getName () da classe SQLServerColumnEncryptionJavaKeyStoreProvider. 

A sintaxe T-SQL para criar a chave mestra de coluna é:

```sql
CREATE COLUMN MASTER KEY [<CMK_name>]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'<key_alias>'
)
```

Para o ' AlwaysEncryptedKey ' criado acima, a definição da chave mestra de coluna seria:

```sql
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'AlwaysEncryptedKey'
)
```

> [!NOTE]
> A funcionalidade interna do SQL Server Management Studio não pode criar definições de chave mestra de coluna para o repositório de chaves Java. Os comandos T-SQL devem ser usados programaticamente.

### <a name="creating-a-column-encryption-key-for-the-java-key-store"></a>Criando uma Chave de Criptografia de Coluna (CEK) para o repositório de chave da JVM
A SQL Server Management Studio ou qualquer outra ferramenta não pode ser usada para criar chaves de criptografia de coluna usando chaves mestras de coluna no repositório de chaves Java. O aplicativo cliente deve criar a chave de criptografia de coluna programaticamente usando a classe SQLServerColumnEncryptionJavaKeyStoreProvider. Para obter mais informações, consulte [usando provedores de repositório de chave mestra de coluna para provisionamento de chave programática](#using-column-master-key-store-providers-for-programmatic-key-provisioning).

### <a name="implementing-a-custom-column-master-key-store-provider"></a>Implementando um provedor personalizado de repositórios de chaves mestras de coluna
Se você quiser armazenar chaves mestras de coluna em um repositório de chaves que não tem suporte em um provedor existente, será possível implementar um provedor personalizado estendendo a Classe SQLServerColumnEncryptionKeyStoreProvider e registrando o provedor usando o método SQLServerConnection.registerColumnEncryptionKeyStoreProviders().

```java
public class MyCustomKeyStore extends SQLServerColumnEncryptionKeyStoreProvider{  
    private String name = "MY_CUSTOM_KEYSTORE";

    public void setName(String name)
    {
        this.name = name;
    }

    public String getName()
    {
        return name;
    }

    public byte[] encryptColumnEncryptionKey(String masterKeyPath, String encryptionAlgorithm, byte[] plainTextColumnEncryptionKey)
    {
        // Logic for encrypting the column encryption key
    }

    public byte[] decryptColumnEncryptionKey(String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey)
    {
        // Logic for decrypting the column encryption key
    }
}
```

Registre o provedor:

```java
SQLServerColumnEncryptionKeyStoreProvider storeProvider = new MyCustomKeyStore();
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
keyStoreMap.put(storeProvider.getName(), storeProvider);
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
```

## <a name="using-column-master-key-store-providers-for-programmatic-key-provisioning"></a>Usando provedores de repositórios de chaves mestras de coluna para o provisionamento programático de chaves
Ao acessar colunas criptografadas, o Microsoft JDBC Driver for SQL Server encontra de modo transparente e chama o provedor de repositório de chaves mestras de coluna certo para descriptografar as chaves de criptografia de coluna. Normalmente, o código normal do aplicativo não chama diretamente os provedores de repositórios de chaves mestras de coluna. No entanto, você pode criar uma instância e chamar um provedor programaticamente para provisionar e gerenciar chaves de Always Encrypted. Essa etapa pode ser feita para gerar uma chave de criptografia de coluna criptografada e descriptografar uma chave de criptografia de coluna como rotação de chave mestra de coluna, por exemplo. Para obter mais informações, consulte [Overview of Key Management for Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)(Visão geral do gerenciamento de chaves do Sempre Criptografado).

Caso você use um provedor de repositório de chaves personalizado, poderá ser necessário implementar suas próprias ferramentas de gerenciamento. Ao usar as chaves armazenadas em repositórios de chaves, para as quais os provedores internos existem, ou no Cofre de Chaves do Azure, é possível usar as ferramentas existentes, como SQL Server Management Studio ou PowerShell, para gerenciar e provisionar as chaves. Ao usar chaves armazenadas no repositório de chaves Java, você precisa provisionar chaves programaticamente. O exemplo a seguir ilustra o uso da classe SQLServerColumnEncryptionJavaKeyStoreProvider para criptografar a chave com uma chave armazenada no repositório de chaves Java.

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionJavaKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerException;

/**
 * This program demonstrates how to create a column encryption key programmatically for the Java Key Store.
 */
public class AlwaysEncrypted {
    // Alias of the key stored in the keystore.
    private static String keyAlias = "<provide key alias>";

    // Name by which the column master key will be known in the database.
    private static String columnMasterKeyName = "MyCMK";

    // Name by which the column encryption key will be known in the database.
    private static String columnEncryptionKey = "MyCEK";

    // The location of the keystore.
    private static String keyStoreLocation = "C:\\Dev\\Always Encrypted\\keystore.jks";

    // The password of the keystore and the key.
    private static char[] keyStoreSecret = "********".toCharArray();

    /**
     * Name of the encryption algorithm used to encrypt the value of the column encryption key. The algorithm for the system providers must be
     * RSA_OAEP.
     */
    private static String algorithm = "RSA_OAEP";

    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;";

        try (Connection connection = DriverManager.getConnection(connectionUrl);
                Statement statement = connection.createStatement();) {

            // Instantiate the Java Key Store provider.
            SQLServerColumnEncryptionKeyStoreProvider storeProvider = new SQLServerColumnEncryptionJavaKeyStoreProvider(keyStoreLocation,
                    keyStoreSecret);

            byte[] encryptedCEK = getEncryptedCEK(storeProvider);

            /**
             * Create column encryption key For more details on the syntax, see:
             * https://docs.microsoft.com/sql/t-sql/statements/create-column-encryption-key-transact-sql Encrypted column encryption key first needs
             * to be converted into varbinary_literal from bytes, for which byteArrayToHex() is used.
             */
            String createCEKSQL = "CREATE COLUMN ENCRYPTION KEY "
                    + columnEncryptionKey
                    + " WITH VALUES ( "
                    + " COLUMN_MASTER_KEY = "
                    + columnMasterKeyName
                    + " , ALGORITHM =  '"
                    + algorithm
                    + "' , ENCRYPTED_VALUE =  0x"
                    + byteArrayToHex(encryptedCEK)
                    + " ) ";
            statement.executeUpdate(createCEKSQL);
            System.out.println("Column encryption key created with name : " + columnEncryptionKey);
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static byte[] getEncryptedCEK(SQLServerColumnEncryptionKeyStoreProvider storeProvider) throws SQLServerException {
        String plainTextKey = "You need to give your plain text";

        // plainTextKey has to be 32 bytes with current algorithm supported
        byte[] plainCEK = plainTextKey.getBytes();

        // This will give us encrypted column encryption key in bytes
        byte[] encryptedCEK = storeProvider.encryptColumnEncryptionKey(keyAlias, algorithm, plainCEK);

        return encryptedCEK;
    }

    public static String byteArrayToHex(byte[] a) {
        StringBuilder sb = new StringBuilder(a.length * 2);
        for (byte b : a)
            sb.append(String.format("%02x", b).toUpperCase());
        return sb.toString();
    }
}
```

## <a name="enabling-always-encrypted-for-application-queries"></a>Habilitando o Always Encrypted para consultas de aplicativo
A maneira mais fácil para habilitar a criptografia de parâmetros e a descriptografia dos resultados de consulta que têm como destino as colunas criptografadas é configurando o valor da palavra-chave da cadeia de conexão **columnEncryptionSetting** como **Habilitado**.

A cadeia de conexão a seguir é um exemplo de habilitação de Always Encrypted no driver JDBC:

```java
String connectionUrl = "jdbc:sqlserver://<server>:<port>;user=<user>;password=<password>;databaseName=<database>;columnEncryptionSetting=Enabled;";
SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionUrl);
```

O código a seguir é um exemplo equivalente usando o objeto SQLServerDataSource:

```java
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName("<server>");
ds.setPortNumber(<port>);
ds.setUser("<user>");
ds.setPassword("<password>");
ds.setDatabaseName("<database>");
ds.setColumnEncryptionSetting("Enabled");
SQLServerConnection con = (SQLServerConnection) ds.getConnection();
```

O Sempre Criptografado também pode ser habilitado para consultas individuais. Confira [Controle do impacto sobre o desempenho do Always Encrypted](#controlling-the-performance-impact-of-always-encrypted) abaixo para saber mais. Habilitar Always Encrypted não é suficiente para o êxito da criptografia ou descriptografia. Você também precisa garantir que:
- O aplicativo tem as permissões de banco de dados *VIEW ANY COLUMN MASTER KEY DEFINITION* e *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* , necessárias para acessar os metadados sobre as chaves do Always Encrypted no banco de dados. Para obter detalhes, veja [Permissões em Always Encrypted (Mecanismo de Banco de Dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions).
- O aplicativo pode acessar a chave mestra de coluna que protege as chaves de criptografia de coluna, o que criptografa as colunas de banco de dados consultadas. Para usar o provedor de repositório de chaves Java, você precisa fornecer credenciais adicionais na cadeia de conexão. Para obter mais informações, consulte [usando o provedor de repositório de chaves Java](#using-java-key-store-provider).

### <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>Configuração de como os valores de java.sql.Time são enviados ao servidor
A propriedade de conexão **sendTimeAsDatetime** é usada para configurar como o valor java.sql.Time é enviado para o servidor. Quando definido como false, o valor de hora é enviado como um tipo de SQL Server hora. Quando definido como true, o valor de time é enviado como um tipo DateTime. Se uma coluna de tempo for criptografada, a propriedade **sendTimeAsDatetime** deverá ser falsa, pois as colunas criptografadas não oferecerão suporte à conversão de tempo em DateTime. Observe também que essa propriedade é, por padrão, true, portanto, ao usar colunas de tempo criptografado, você precisará defini-la como false. Caso contrário, o driver gerará uma exceção. A partir da versão 6,0 do driver, a classe SQLServerConnection tem dois métodos para configurar o valor dessa propriedade programaticamente:
 
* public void setSendTimeAsDatetime (Boolean sendTimeAsDateTimeValue)
* public boolean getSendTimeAsDatetime()

Para obter mais informações sobre essa propriedade, consulte [configurar como os valores de Java. Sql. time são enviados para o servidor](configuring-how-java-sql-time-values-are-sent-to-the-server.md).

### <a name="configuring-how-string-values-are-sent-to-the-server"></a>Configurando como os valores de cadeia de caracteres são enviados ao servidor
A propriedade de conexão **sendStringParametersAsUnicode** é usada para configurar como os valores de cadeia de caracteres são enviados para SQL Server. Se definida como true, os parâmetros String serão enviados ao servidor no formato Unicode. Se definido como false, os parâmetros de cadeia de caracteres são enviados em formato não-Unicode, como ASCII ou MBCS, em vez de Unicode. O valor padrão para essa propriedade é true. Quando Always Encrypted está habilitado e uma coluna char/varchar/varchar (max) é criptografada, o valor de **sendStringParametersAsUnicode** deve ser definido como false. Se essa propriedade for definida como true, o driver gerará uma exceção ao descriptografar dados de uma coluna Encrypted char/varchar/varchar (max) que tem caracteres Unicode. Para obter mais informações, veja [Configuração das propriedades de conexão](../../connect/jdbc/setting-the-connection-properties.md).
  
## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>Recuperação e modificação de dados em colunas criptografadas
Depois de habilitar Always Encrypted para consultas de aplicativo, você pode usar as APIs JDBC padrão para recuperar ou modificar dados em colunas de banco de dado criptografado. Se seu aplicativo tiver as permissões de banco de dados necessárias e puder acessar a chave mestra de coluna, o driver criptografará todos os parâmetros de consulta que se destinam a colunas criptografadas e descriptografará os dados que são recuperados de colunas criptografadas.

Se o Sempre Criptografado não estiver habilitado, as consultas com parâmetros que se destinam a colunas criptografadas falharão. As consultas ainda podem recuperar dados de colunas criptografadas, desde que a consulta não tenha parâmetros que se destinem a colunas criptografadas. No entanto, o driver não tentará descriptografar nenhum valor recuperado de colunas criptografadas, e o aplicativo receberá os dados binários criptografados (como matrizes de bytes).

A tabela abaixo resume o comportamento das consultas dependendo se Always Encrypted está habilitado ou não:

| Característica da consulta                                                                           | O Always Encrypted está habilitado e o aplicativo pode acessar as chaves e os metadados da chave                                                                                                                        | O Sempre Criptografado está habilitado e o aplicativo não pode acessar as chaves nem os metadados da chave | O Sempre Criptografado está desabilitado                                                                                        |
| :--------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :-------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------ |
| Consultas com parâmetros que se destinam a colunas criptografadas.                                           | Os valores de parâmetro são criptografados de modo transparente.                                                                                                                                                           | Erro                                                                             | Erro                                                                                                               |
| Consultas que recuperam dados de colunas criptografadas sem parâmetros que se destinam a colunas criptografadas. | Os resultados das colunas criptografadas são descriptografados de modo transparente. O aplicativo recebe valores de texto não criptografado dos tipos de dados JDBC correspondentes aos tipos do SQL Server configurados para as colunas criptografadas. | Erro                                                                             | Os resultados das colunas criptografadas não são descriptografados. O aplicativo recebe valores criptografados como matrizes de bytes (byte[]). |

### <a name="inserting-and-retrieving-encrypted-data-examples"></a>Inserindo e recuperando exemplos de dados criptografados

Os exemplos a seguir ilustram como recuperar e modificar dados em colunas criptografadas. Os exemplos assumem a tabela de destino com o esquema a seguir e as colunas SSN e DataDeNascimento criptografadas. Se você tiver configurado uma chave mestra de coluna chamada "MyCMK" e uma chave de criptografia de coluna chamada "MyCEK" (conforme descrito nas seções de provedores de repositório de chaves anteriores), você poderá criar a tabela usando este script:

```sql
CREATE TABLE [dbo].[Patients]([PatientId] [int] IDENTITY(1,1),
 [SSN] [char](11) COLLATE Latin1_General_BIN2
 ENCRYPTED WITH (ENCRYPTION_TYPE = DETERMINISTIC,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = MyCEK) NOT NULL,
 [FirstName] [nvarchar](50) NULL,
 [LastName] [nvarchar](50) NULL,
 [BirthDate] [date]
 ENCRYPTED WITH (ENCRYPTION_TYPE = RANDOMIZED,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = MyCEK) NOT NULL
 PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY])
 GO
```

Para cada exemplo de código Java, você precisará inserir o código específico do repositório de chaves no local indicado.

Se você estiver usando um provedor de keystore Azure Key Vault:

```java
    String clientID = "<Azure Application ID>";
    String clientKey = "<Azure Application API Key Password>";
    SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
    Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
    keyStoreMap.put(akvProvider.getName(), akvProvider);
    SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
    String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;";
```

Se você estiver usando um provedor de repositório de chaves do repositório de certificados do Windows:

```java
    String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;";
```

Se você estiver usando um provedor de keystore do repositório de chaves Java:

```java
    String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path to jks or pfx file>;keyStoreSecret=<keystore secret/password>";
```

### <a name="inserting-data-example"></a>Inserindo exemplo de dados

Este exemplo insere uma linha na tabela Pacientes. Observe os seguintes itens:

- Não há nada específico de criptografia no código de exemplo. O Microsoft JDBC Driver para SQL Server detecta e criptografa automaticamente os parâmetros que se destinam a colunas criptografadas. Esse comportamento torna a criptografia transparente para o aplicativo.
- Os valores inseridos nas colunas de banco de dados, incluindo as colunas criptografadas, são passados como parâmetros associados. Embora o uso de parâmetros seja opcional ao enviar valores para colunas não criptografadas (mesmo que seja altamente recomendável, pois ajuda a prevenir a injeção de SQL), ele é necessário para valores que se destinam a colunas criptografadas. Se os valores inseridos nas colunas criptografadas foram passados como literais inseridos na instrução de consulta, a consulta falharia porque o driver não seria capaz de determinar os valores nas colunas criptografadas de destino e não criptografaria os valores. Como resultado, o servidor os rejeitaria como incompatíveis com as colunas criptografadas.
- Todos os valores impressos pelo programa estarão em texto não criptografado, já que o Microsoft JDBC Driver for SQL Server descriptografará de modo transparente os dados recuperados das colunas criptografadas.
- Se você estiver fazendo uma pesquisa usando uma cláusula WHERE, o valor usado na cláusula WHERE precisará ser passado como um parâmetro para que o driver possa criptografá-lo de forma transparente antes de enviá-lo ao banco de dados. No exemplo a seguir, o SSN é passado como um parâmetro, mas o LastName é passado como um literal, pois LastName não está criptografado.
- O método setter usado para o parâmetro de destino da coluna SSN é SetString (), que é mapeado para o tipo de dados char/varchar SQL Server. Se, para esse parâmetro, o método setter usado tiver sido setNString(), que mapeia para nchar/nvarchar, a consulta falhará, já que o Always Encrypted não é compatível com conversões de valores nchar/nvarchar criptografados em valores char/varchar criptografados.

```java
// <Insert keystore-specific code here>
try (Connection sourceConnection = DriverManager.getConnection(connectionUrl);
        PreparedStatement insertStatement = sourceConnection.prepareStatement("INSERT INTO [dbo].[Patients] VALUES (?, ?, ?, ?)")) {
    insertStatement.setString(1, "795-73-9838");
    insertStatement.setString(2, "Catherine");
    insertStatement.setString(3, "Abel");
    insertStatement.setDate(4, Date.valueOf("1996-09-10"));
    insertStatement.executeUpdate();
    System.out.println("1 record inserted.\n");
}
// Handle any errors that may have occurred.
catch (SQLException e) {
    e.printStackTrace();
}
```

### <a name="retrieving-plaintext-data-example"></a>Exemplo de recuperação de dados de texto não criptografado

O exemplo a seguir demonstra a filtragem de dados com base em valores criptografados e a recuperação de dados de texto não criptografado de colunas criptografadas. Observe os seguintes itens:

- O valor usado na cláusula WHERE a ser filtrado na coluna SSN precisa ser passado como um parâmetro para que Microsoft JDBC Driver for SQL Server possa criptografá-lo de modo transparente antes de enviá-lo ao banco de dados.
- Todos os valores impressos pelo programa estarão em texto não criptografado, já que o Microsoft JDBC Driver for SQL Server descriptografará de modo transparente os dados recuperados das colunas SSN e BirthDate.

> [!NOTE]
> se as colunas forem criptografadas usando a criptografia determinística, as consultas poderão executar comparações de igualdade nelas. Para obter mais informações, veja [Seleção de criptografia determinística ou aleatória no Always Encrypted (Mecanismo de Banco de Dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption).

```java
// <Insert keystore-specific code here>
try (Connection connection = DriverManager.getConnection(connectionUrl);
        PreparedStatement selectStatement = connection
                .prepareStatement("\"SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN = ?;\"");) {
    selectStatement.setString(1, "795-73-9838");
    ResultSet rs = selectStatement.executeQuery();
    while (rs.next()) {
        System.out.println("SSN: " + rs.getString("SSN") + ", FirstName: " + rs.getString("FirstName") + ", LastName:"
                + rs.getString("LastName") + ", Date of Birth: " + rs.getString("BirthDate"));
    }
}
// Handle any errors that may have occurred.
catch (SQLException e) {
    e.printStackTrace();
}
```

### <a name="retrieving-encrypted-data-example"></a>Exemplo de recuperação de dados criptografados

Se o Always Encrypted não estiver habilitado, uma consulta ainda poderá recuperar dados de colunas criptografadas, desde que a consulta não tenha parâmetros que se destinam a colunas criptografadas.

O exemplo a seguir ilustra como recuperar dados binários criptografados de colunas criptografadas. Observe os seguintes itens:

- Como o Always Encrypted não está habilitado na cadeia de conexão, a consulta retornará valores criptografados de SSN e BirthDate como matrizes de bytes (o programa converte os valores em cadeias de caracteres).
- Uma consulta que recupera dados de colunas criptografadas com o Sempre Criptografado desabilitado pode ter parâmetros, desde que nenhum dos parâmetros se destinem a uma coluna criptografada. A consulta a seguir filtra por LastName, que não é criptografado no banco de dados. Se a consulta filtrar por SSN ou BirthDate, a consulta falhará.

```java
try (Connection sourceConnection = DriverManager.getConnection(connectionUrl);
        PreparedStatement selectStatement = sourceConnection
                .prepareStatement("SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE LastName = ?;");) {

    selectStatement.setString(1, "Abel");
    ResultSet rs = selectStatement.executeQuery();
    while (rs.next()) {
        System.out.println("SSN: " + rs.getString("SSN") + ", FirstName: " + rs.getString("FirstName") + ", LastName:"
                + rs.getString("LastName") + ", Date of Birth: " + rs.getString("BirthDate"));
    }
}
// Handle any errors that may have occurred.
catch (SQLException e) {
    e.printStackTrace();
}
```

### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>Evitando problemas comuns ao consultar colunas criptografadas

Esta seção descreve as categorias comuns de erros ao consultar colunas criptografadas de aplicativos Java e algumas diretrizes sobre como evitá-las.

### <a name="unsupported-data-type-conversion-errors"></a>Erros de conversão de tipo de dados sem suporte

O Always Encrypted dá suporte a algumas conversões de tipos de dados criptografados. Confira [Always Encrypted (Mecanismo de Banco de Dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) para obter a lista detalhada de conversões de tipo compatíveis. Isto é o que você pode fazer para evitar erros de conversão de tipo de dados. Certifique-se de que:

- Você usa os métodos setter apropriados ao passar valores para parâmetros que se destinam a colunas criptografadas. Defina os tipos de parâmetros que se destinam a colunas criptografadas, para que o tipo de dados do SQL Server do parâmetro seja exatamente o mesmo que o tipo da coluna de destino ou para que haja suporte para uma conversão do tipo de dados do SQL Server do parâmetro no tipo da coluna de destino. Métodos de API foram adicionados às classes SQLServerPreparedStatement, SQLServerCallableStatement e SQLServerResultSet para passar parâmetros correspondentes a tipos de dados SQL Server específicos. Por exemplo, se uma coluna não estiver criptografada, você poderá usar o método setTimestamp () para passar um parâmetro para um datetime2 ou para uma coluna DateTime. Mas quando uma coluna é criptografada, você precisará usar o método exato que representa o tipo da coluna no banco de dados. Por exemplo, use setTimestamp () para passar valores para uma coluna datetime2 criptografada e use SetDateTime () para passar valores para uma coluna de data e hora criptografada. Consulte [referência de API de Always Encrypted para o driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md) para obter uma lista completa de novas APIs.
- a precisão e escala dos parâmetros que se destinam a colunas dos tipos de dados decimais e numéricos do SQL Server são iguais à precisão e escala configuradas para a coluna de destino. Métodos de API foram adicionados às classes SQLServerPreparedStatement, SQLServerCallableStatement e SQLServerResultSet para aceitar precisão e escala junto com valores de dados para parâmetros/colunas que representam tipos de dados decimais e numéricos. Consulte [referência de API de Always Encrypted para o driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md) para obter uma lista completa de APIs novas/sobrecarregadas.  
- a precisão dos parâmetros que se destinam a colunas datetime2, datetimeoffset ou a tipos de dados temporais do SQL Server não é maior do que a precisão da coluna de destino, em consultas que modificam os valores da coluna de destino. Métodos de API foram adicionados às classes SQLServerPreparedStatement, SQLServerCallableStatement e SQLServerResultSet para aceitar a precisão/escala de segundos fracionários, juntamente com valores de dados para parâmetros que representam esses tipos de dados. Para obter uma lista completa de APIs novas/sobrecarregadas, consulte [Always Encrypted referência da API para o driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).

### <a name="errors-due-to-incorrect-connection-properties"></a>Erros devido a propriedades de conexão incorretas

Esta seção descreve como definir adequadamente as configurações de conexão para usar Always Encrypted dados. Como os tipos de dados criptografados dão suporte a conversões limitadas, as configurações de conexão **sendTimeAsDatetime** e **sendStringParametersAsUnicode** precisam de uma configuração adequada ao usar colunas criptografadas. Certifique-se de que:

- [sendTimeAsDatetime](setting-the-connection-properties.md) configuração de conexão é definida como false ao inserir dados em colunas de tempo criptografado. [Configurando como os valores de java.sql.Time são enviados ao servidor](configuring-how-java-sql-time-values-are-sent-to-the-server.md)
- [a configuração de conexão](setting-the-connection-properties.md) sendStringParametersAsUnicode é definida como true (ou é deixada como padrão) ao inserir dados em colunas char/varchar/varchar (max) criptografadas.

### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>Erros devido à passagem de texto sem formatação em vez de valores criptografados

Qualquer valor que se destina a uma coluna criptografada precisa ser criptografado no aplicativo. Uma tentativa de inserir/modificar ou de filtrar por um valor de texto não criptografado em uma coluna criptografada resultará em um erro semelhante a este:

```java
com.microsoft.sqlserver.jdbc.SQLServerException: Operand type clash: varchar is incompatible with varchar(8000) encrypted with (encryption_type = 'DETERMINISTIC', encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'MyCEK', column_encryption_key_database_name = 'ae') collation_name = 'SQL_Latin1_General_CP1_CI_AS'
```

Para evitar esses tipos de erros, garanta que:

- Always Encrypted esteja habilitado para as consultas de aplicativo que se destinam a colunas criptografadas (na cadeia de conexão ou para uma consulta específica).
- Você usa instruções e parâmetros preparados para enviar dados direcionados a colunas criptografadas. O exemplo a seguir mostra uma consulta filtrada incorretamente por um literal/constante em uma coluna criptografada (SSN), em vez de passar o literal para dentro como um parâmetro. Esta consulta falhará:

```java
ResultSet rs = connection.createStatement().executeQuery("SELECT * FROM Customers WHERE SSN='795-73-9838'");
```

## <a name="force-encryption-on-input-parameters"></a>Forçar a criptografia em parâmetros de entrada

O recurso de criptografia forçada impõe a criptografia de um parâmetro ao usar Always Encrypted. Se forçar criptografia for usado e o SQL Server informar o driver de que o parâmetro não precisa ser criptografado, a consulta que estiver o parâmetro falhará. Essa propriedade fornece proteção adicional contra ataques de segurança que envolvem um SQL Server comprometido fornecendo metadados de criptografia incorretos ao cliente, o que pode levar à divulgação de dados. Os métodos set * nas classes SQLServerPreparedStatement e SQLServerCallableStatement e os métodos Update\* na classe SQLServerResultSet estão sobrecarregados para aceitar um argumento booliano para especificar a configuração de criptografia forçada. Se o valor desse argumento for false, o driver não forçará a criptografia em parâmetros. Se forçar criptografia for definida como true, o parâmetro de consulta será enviado somente se a coluna de destino for criptografada e Always Encrypted estiver habilitada na conexão ou na instrução. O uso dessa propriedade fornece uma camada extra de segurança, garantindo que o driver não envie dados por engano para SQL Server como texto sem formatação quando for esperado que ele seja criptografado.

Para obter mais informações sobre os métodos SQLServerPreparedStatement e SQLServerCallableStatement que estão sobrecarregados com a configuração de criptografia forçada, consulte [Always Encrypted referência de API para o driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)  

## <a name="controlling-the-performance-impact-of-always-encrypted"></a>Controle do impacto sobre o desempenho do Always Encrypted

Como o Always Encrypted é uma tecnologia de criptografia do lado do cliente, a maior parte da sobrecarga de desempenho é observada no lado do cliente, não no banco de dados. Além do custo das operações de criptografia e descriptografia, outras fontes de sobrecarga de desempenho no lado do cliente são:

- Viagens de ida e volta adicionais ao banco de dados para recuperar metadados dos parâmetros de consulta.
- Chamadas a um repositório de chaves mestras de coluna para acessar uma chave mestra de coluna.

Esta seção descreve as otimizações de desempenho internas no Microsoft JDBC Driver for SQL Server e como você pode controlar o impacto dos dois fatores acima sobre o desempenho.

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>Controlando as viagens de ida e volta para recuperar metadados dos parâmetros de consulta

Se o Always Encrypted estiver habilitado para uma conexão, por padrão, o driver chamará [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) para cada consulta parametrizada, passando a instrução de consulta (sem nenhum valor de parâmetro) para o SQL Server. O [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) analisa a instrução de consulta para descobrir se os parâmetros precisam ser criptografados e, se for o caso, para cada um, retornará as informações relacionadas à criptografia que permitirão ao driver criptografar os valores de parâmetro. Esse comportamento garante um alto nível de transparência para o aplicativo cliente. Desde que o aplicativo use parâmetros para passar valores que se destinam a colunas criptografadas para o driver, o aplicativo (e o desenvolvedor do aplicativo) não precisa saber quais consultas acessam colunas criptografadas.

### <a name="setting-always-encrypted-at-the-query-level"></a>Configurando o Always Encrypted no nível da consulta

Para controlar o impacto no desempenho da recuperação de metadados de criptografia para consultas parametrizadas, é possível habilitar o Always Encrypted para consultas individuais, em vez de configurá-lo para a conexão. Assim, você pode garantir que sys.sp_describe_parameter_encryption seja invocado apenas para consultas que você sabe que têm parâmetros que se destinam a colunas criptografadas. No entanto, observe que, ao fazer isso, você reduz a transparência da criptografia: se você alterar as propriedades de criptografia das colunas de banco de dados, poderá ser necessário alterar o código do aplicativo para alinhá-lo às alterações de esquema.

Para controlar o comportamento de Always Encrypted de consultas individuais, você precisa configurar objetos de instrução individuais passando uma enumeração, SQLServerStatementColumnEncryptionSetting, que especifica como os dados serão enviados e recebidos durante a leitura e gravação colunas criptografadas para essa instrução específica. Veja algumas diretrizes úteis:

- Se a maioria das consultas que um aplicativo cliente enviar por uma conexão de banco de dados acessa colunas criptografadas, use estas diretrizes:

    - Defina a palavra-chave da cadeia de conexão **columnEncryptionSetting** como **Habilitada**.
    - Defina SQLServerStatementColumnEncryptionSetting.Disabled para consultas individuais que não acessam nenhuma coluna criptografada. Essa configuração desabilitará a chamada a sys.sp_describe_parameter_encryption, além de ser uma tentativa de descriptografar todos os valores no conjunto de resultados.
    - Defina SQLServerStatementColumnEncryptionSetting.ResultSet para consultas individuais que não têm parâmetros que exijam criptografia, mas que recuperam dados de colunas criptografadas. Essa configuração desabilitará a chamada a sys.sp_describe_parameter_encryption e a criptografia de parâmetros. A consulta poderá descriptografar os resultados das colunas de criptografia.

- Se a maioria das consultas que um aplicativo cliente enviar por uma conexão de banco de dados não acessa colunas criptografadas, use estas diretrizes:

    - Defina a palavra-chave da cadeia de conexão **columnEncryptionSetting** como **Desabilitada**.
    - Defina SQLServerStatementColumnEncryptionSetting.Enabled para consultas individuais que têm parâmetros que precisam ser criptografados. Essa configuração habilitará a chamada a sys.sp_describe_parameter_encryption, além da descriptografia de todos os resultados de consulta recuperados de colunas criptografadas.
    - Defina SQLServerStatementColumnEncryptionSetting.ResultSet para consultas que não têm parâmetros que exijam criptografia, mas que recuperam dados de colunas criptografadas. Essa configuração desabilitará a chamada a sys.sp_describe_parameter_encryption e a criptografia de parâmetros. A consulta poderá descriptografar os resultados das colunas de criptografia.

As configurações de SQLServerStatementColumnEncryptionSetting não podem ser usadas para ignorar a criptografia e obter acesso a dados de texto sem formatação. Para obter mais informações sobre como configurar a criptografia de coluna em uma instrução, consulte [Always Encrypted referência de API para o driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).  

No exemplo abaixo, Always Encrypted está desabilitado para a conexão de banco de dados. A consulta emitida pelo aplicativo tem um parâmetro que se destina à coluna LastName não criptografada. A consulta recupera dados das colunas SSN e BirthDate que são criptografadas. Nesse caso, a chamada a sys.sp_describe_parameter_encryption para recuperar os metadados de criptografia não é necessária. No entanto, a descriptografia dos resultados da consulta precisa ser habilitada para que o aplicativo possa receber valores de texto não criptografado das duas colunas criptografadas. A configuração de SqlCommandColumnEncryptionSetting.ResultSet é usada para garantir isso.

```java
// Assumes the same table definition as in Section "Retrieving and modifying data in encrypted columns"
// where only SSN and BirthDate columns are encrypted in the database.
String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<database>;user=<user>;password=<password>;" 
        + "keyStoreAuthentication=JavaKeyStorePassword;"
        + "keyStoreLocation=<keyStoreLocation>" 
        + "keyStoreSecret=<keyStoreSecret>;";

String filterRecord = "SELECT FirstName, LastName, SSN, BirthDate FROM " + tableName + " WHERE LastName = ?";

try (SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionUrl);
        PreparedStatement selectStatement = connection.prepareStatement(filterRecord, ResultSet.TYPE_FORWARD_ONLY, ResultSet.CONCUR_READ_ONLY,
                connection.getHoldability(), SQLServerStatementColumnEncryptionSetting.ResultSetOnly);) {

    selectStatement.setString(1, "Abel");
    ResultSet rs = selectStatement.executeQuery();
    while (rs.next()) {
        System.out.println("First name: " + rs.getString("FirstName"));
        System.out.println("Last name: " + rs.getString("LastName"));
        System.out.println("SSN: " + rs.getString("SSN"));
        System.out.println("Date of Birth: " + rs.getDate("BirthDate"));
    }
}
// Handle any errors that may have occurred.
catch (SQLException e) {
    e.printStackTrace();
}
```

### <a name="column-encryption-key-caching"></a>Cache de chaves de criptografia de coluna

Para reduzir o número de chamadas a um repositório de chaves mestras de coluna para descriptografar chaves de criptografia de coluna, o Microsoft JDBC Driver for SQL Server armazena em cache as chaves de criptografia de coluna de texto não criptografado na memória. Depois de receber o valor da chave de criptografia de coluna criptografado dos metadados do banco de dados, o driver primeiro tentará encontrar a chave de criptografia de coluna de texto não criptografado correspondente ao valor da chave criptografado. O driver chamará o repositório de chaves que contém a chave mestra de coluna apenas se não conseguir encontrar o valor da chave de criptografia de coluna criptografado no cache.

Você pode configurar um valor de vida útil para as entradas de chave de criptografia de coluna no cache usando a API, setColumnEncryptionKeyCacheTtl (), na classe SQLServerConnection. O valor de vida útil padrão para as entradas de chave de criptografia de coluna no cache é de duas horas. Para desativar o cache, use um valor de 0. Para definir qualquer valor de vida útil, use a seguinte API:

```java
SQLServerConnection.setColumnEncryptionKeyCacheTtl (int columnEncryptionKeyCacheTTL, TimeUnit unit)
```

Por exemplo, para definir um valor de vida útil de 10 minutos, use:

```java
SQLServerConnection.setColumnEncryptionKeyCacheTtl (10, TimeUnit.MINUTES)
```

Somente dias, horas, minutos ou segundos têm suporte como a unidade de tempo.  

## <a name="copying-encrypted-data-using-sqlserverbulkcopy"></a>Copiando dados criptografados usando SqlBulkCopy

Com SQLServerBulkCopy, você pode copiar dados que já estão criptografados e armazenados em uma tabela para outra tabela sem descriptografá-los. Para fazer isso:

- Verifique se a configuração de criptografia da tabela de destino é idêntica à configuração da tabela de origem. Em particular, as duas tabelas devem ter as mesmas colunas criptografadas, e as colunas devem ser criptografadas usando os mesmos tipos de criptografia e as mesmas chaves de criptografia. Se qualquer coluna de destino for criptografada de modo diferente da coluna de origem correspondente, você não poderá descriptografar os dados na tabela de destino após a operação de cópia. Os dados serão corrompidos.
- Configure ambas as conexões de banco de dados para a tabela de origem e a tabela de destino sem o Always Encrypted habilitado.
- Defina a opção allowEncryptedValueModifications. Para obter mais informações, consulte [usando cópia em massa com o driver JDBC](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md).

> [!NOTE]
> Tenha cuidado ao especificar AllowEncryptedValueModifications, pois isso pode levar à corrupção de banco de dados, porque o Microsoft JDBC Driver for SQL Server não verifica se os dados estão realmente criptografados ou se estão criptografados corretamente usando o mesmo tipo de criptografia, algoritmo e chave que a coluna de destino.

## <a name="see-also"></a>Confira também

[Always Encrypted (mecanismo de banco de dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)
