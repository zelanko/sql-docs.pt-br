---
title: Usando o Always Encrypted com o JDBC driver | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 271c0438-8af1-45e5-b96a-4b1cabe32707
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2f9eded908271973415987155de5cf1efdc906db
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51600966"
---
# <a name="using-always-encrypted-with-the-jdbc-driver"></a>Como usar o Always Encrypted com o driver JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Esta página fornece informações sobre como desenvolver aplicativos Java usando [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md) e o Microsoft JDBC Driver 6.0 (ou superior) para o SQL Server.

O Always Encrypted permite que os clientes criptografem dados confidenciais e nunca revelem os dados nem as chaves de criptografia para o SQL Server ou o Banco de Dados SQL do Azure. Um driver habilitado para Always Encrypted, como o Microsoft JDBC Driver 6.0 (ou superior) for SQL Server, consegue esse comportamento criptografando e descriptografando de modo transparente dados confidenciais no aplicativo cliente. O driver determina automaticamente quais consulta parâmetros correspondem às colunas de banco de dados sempre criptografados e criptografa os valores desses parâmetros antes de enviar ao SQL Server ou banco de dados SQL. Da mesma forma, o driver descriptografa de modo transparente os dados recuperados das colunas de banco de dados criptografadas nos resultados da consulta. Para obter mais informações, consulte [Always Encrypted (mecanismo de banco de dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) e [sempre criptografados referência da API para o Driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).

## <a name="prerequisites"></a>Prerequisites
- Certifique-se de que Microsoft JDBC Driver 6.0 (ou superior) para SQL Server está instalado no computador de desenvolvimento. 
- Baixe e instale os arquivos de política de jurisdição de força ilimitada de Java Cryptography Extension (JCE).  Leia o arquivo Leiame incluído no arquivo zip para instruções de instalação e detalhes relevantes sobre problemas possíveis de importação/exportação.  

    - Se você estiver usando o mssql-jdbc-X.X.X.jre7.jar ou o sqljdbc41.jar, os arquivos de política poderão ser baixados de [Download dos arquivos de política de jurisdição de força ilimitada do JCE (Java Cryptography Extension) 7](https://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)

    - Se você estiver usando o mssql-jdbc-X.X.X.jre8.jar ou o sqljdbc42.jar, os arquivos de política poderão ser baixados de [Download dos arquivos de política de jurisdição de força ilimitada do JCE (Java Cryptography Extension) 8](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)

    - Se usar o mssql-jdbc-X.X.X.jre9.jar, nenhum arquivo de política precisa ser baixado. A política de jurisdição em Java 9 assume como padrão para criptografia de segurança ilimitado.

## <a name="working-with-column-master-key-stores"></a>Como trabalhar com repositórios de chaves mestras de coluna
Para criptografar ou descriptografar dados para colunas criptografadas, o SQL Server mantém as chaves de criptografia de coluna. As chaves de criptografia de coluna são armazenadas em formato criptografado nos metadados do banco de dados. Cada chave de criptografia de coluna tem uma chave mestra de coluna correspondente usada para criptografar a chave de criptografia de coluna. Os metadados do banco de dados não contém chaves mestras de coluna. Essas chaves só são mantidas pelo cliente. No entanto os metadados do banco de dados contém informações sobre onde as chaves mestras de coluna são armazenadas em relação ao cliente. Por exemplo, os metadados do banco de dados podem dizer que o repositório de chaves que contém a chave mestra da coluna é a Store de certificado do Windows e o certificado específico usado para criptografar e descriptografar está localizado em um caminho específico dentro de Store de certificado do Windows. Se o cliente tem acesso a esse certificado na Store de certificado do Windows, ele poderá obter o certificado. O certificado, em seguida, pode ser usado para descriptografar a chave de criptografia de coluna. Em seguida, essa chave de criptografia pode ser usada para descriptografar ou criptografar os dados para colunas criptografadas que usam essa chave de criptografia de coluna.

O Microsoft JDBC Driver para SQL Server se comunica com um repositório de chaves usando um provedor de repositório de chave mestra de coluna, que é uma instância de uma classe derivado de **SQLServerColumnEncryptionKeyStoreProvider**.

### <a name="using-built-in-column-master-key-store-providers"></a>Usando provedores internos de repositórios de chaves mestras de coluna
O Microsoft JDBC Driver para SQL Server vem com os seguintes provedores de repositório de chave mestra de coluna interna. Alguns desses provedores são previamente registrados com os nomes de provedor específico (usados para pesquisar o provedor) e alguns exigem credenciais adicionais ou registro explícito.

| Classe                                                 | Descrição                                        | Nome (de pesquisa) do provedor  | Pré-registrados? |
| :---------------------------------------------------- | :------------------------------------------------- | :---------------------- | :----------------- |
| **SQLServerColumnEncryptionAzureKeyVaultProvider**    | Um provedor para um repositório de chaves para o Azure Key Vault. | AZURE_KEY_VAULT         | não                 |
| **SQLServerColumnEncryptionCertificateStoreProvider** | Um provedor para o Repositório de Certificados do Windows.      | MSSQL_CERTIFICATE_STORE | Sim                |
| **SQLServerColumnEncryptionJavaKeyStoreProvider**     | Um provedor do repositório de chaves Java                   | MSSQL_JAVA_KEYSTORE     | Sim                |

Para os provedores de repositório de chaves previamente registrado, você não precisa fazer nenhuma alteração de código do aplicativo para usar esses provedores, mas observe os seguintes itens:

- Você (ou seu DBA) precisa verificar se o nome do provedor configurado nos metadados da chave mestra de coluna está correto e se o caminho da chave mestra de coluna está em conformidade com o formato do caminho da chave válido para determinado provedor. É recomendável configurar as chaves usando ferramentas como o SQL Server Management Studio, que gera automaticamente os nomes de provedor válidos e os caminhos de chaves ao emitir a instrução CREATE COLUMN MASTER KEY (Transact-SQL).
- Garanta que seu aplicativo possa acessar a chave no repositório de chaves. Essa tarefa pode envolver a concessão de acesso para o aplicativo à chave e/ou ao repositório de chaves, dependendo do repositório de chaves, ou a execução de outras etapas de configuração específicas do repositório de chaves. Por exemplo, para usar o SQLServerColumnEncryptionJavaKeyStoreProvider, você precisa fornecer o local e a senha do repositório de chaves nas propriedades da conexão. 

Todos esses provedores de repositório de chaves são descritos mais detalhadamente nas seções a seguir. Você só precisa implementar um provedor de repositório de chaves para usar o Always Encrypted.

### <a name="using-azure-key-vault-provider"></a>Usando o provedor do Cofre de Chaves do Azure
O Azure Key Vault é uma opção conveniente para armazenar e gerenciar chaves mestras de coluna do Always Encrypted (especialmente se o seu aplicativo está hospedado no Azure). O Microsoft JDBC Driver para SQL Server inclui um provedor interno, SQLServerColumnEncryptionAzureKeyVaultProvider, para aplicativos que têm chaves armazenadas no cofre de chaves do Azure. O nome deste provedor é AZURE_KEY_VAULT. Para usar o provedor de armazenamento do Azure Key Vault, um desenvolvedor de aplicativo precisa para criar o cofre e as chaves no cofre de chaves do Azure e criar um registro de aplicativo no Azure Active Directory. O aplicativo registrado deve ser concedido obter, descriptografar, criptografar e verifique se, Wrap Key e Unwrap Key permissões nas políticas de acesso definidas para o Cofre de chaves criado para uso com o sempre criptografado. Para obter mais informações sobre como configurar o Cofre de chaves e crie uma chave mestra de coluna, consulte [Azure Key Vault – passo a passo](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/) e [Criando chaves mestras de coluna no Azure Key Vault](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md#creating-column-master-keys-in-azure-key-vault).

Para os exemplos nesta página, se você tiver criado um cofre de chaves do Azure com base em uma chave mestra de coluna e a chave de criptografia de coluna usando o SQL Server Management Studio, o script T-SQL para recriá-los pode parecer semelhante a este exemplo com seu próprio específico **KEY_ CAMINHO** e **ENCRYPTED_VALUE**:

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

Para usar o Azure Key Vault, os aplicativos cliente precisam instanciar o SQLServerColumnEncryptionAzureKeyVaultProvider e registrá-lo com o driver.

Aqui está um exemplo de inicializar SQLServerColumnEncryptionAzureKeyVaultProvider:  

```java
SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
```

**clientID** é a ID do aplicativo de um registro de aplicativo em uma instância do Active Directory do Azure. **clientKey** é uma senha de chave registrada sob esse aplicativo, que fornece acesso à API para o Azure Key Vault.

Depois que o aplicativo cria uma instância de SQLServerColumnEncryptionAzureKeyVaultProvider, o aplicativo deve registrar a instância com o driver usando o método registercolumnencryptionkeystoreproviders (). É altamente recomendável que a instância é registrada usando o nome de pesquisa padrão, AZURE_KEY_VAULT, que pode ser obtido chamando a API SQLServerColumnEncryptionAzureKeyVaultProvider.getName(). Usando o nome padrão permitirá que você use ferramentas como o SQL Server Management Studio ou o PowerShell para provisionar e gerenciar chaves Always Encrypted (as ferramentas usam o nome padrão para gerar o objeto de metadados para a chave mestra de coluna). O exemplo a seguir mostra como registrar o provedor do Azure Key Vault. Para obter mais informações sobre o método registercolumnencryptionkeystoreproviders (), consulte [Always Encrypted referência da API para o Driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).

```java
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
keyStoreMap.put(akvProvider.getName(), akvProvider);
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
```

> [!IMPORTANT]
>  Se você usar o provedor de repositório de chaves do Azure Key Vault, a implementação do Azure Key Vault do driver JDBC tem dependências nessas bibliotecas (do GitHub) que deve ser incluído no seu aplicativo:
>
>  [Azure sdk para java](https://github.com/Azure/azure-sdk-for-java)
>
>  [bibliotecas do Azure-activedirectory-library-for-java](https://github.com/AzureAD/azure-activedirectory-library-for-java)
>
> Para obter um exemplo de como incluir essas dependências em um projeto Maven, consulte [baixar ADAL4J AKV dependências e com o Apache Maven](https://github.com/Microsoft/mssql-jdbc/wiki/Download-ADAL4J-And-AKV-Dependencies-with-Apache-Maven)

### <a name="using-windows-certificate-store-provider"></a>Uso do Provedor do Repositório de Certificados do Windows
O SQLServerColumnEncryptionCertificateStoreProvider pode ser usado para armazenar chaves mestras de coluna no Repositório de Certificados do Windows. Use o assistente Always Encrypted SQL Server Management Studio (SSMS) ou outras ferramentas com suporte para criar definições de chave da chave mestra de coluna e a criptografia de coluna no banco de dados. O mesmo assistente pode ser usado para gerar um certificado autoassinado na Store de certificado do Windows que pode ser usado como uma chave mestra de coluna para os dados sempre criptografados. Para obter mais informações sobre a chave mestra de coluna e a sintaxe de T-SQL de chave da criptografia de coluna, consulte [CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md) e [criar chave de criptografia de coluna](../../t-sql/statements/create-column-encryption-key-transact-sql.md) , respectivamente.

O nome da SQLServerColumnEncryptionCertificateStoreProvider é MSSQL_CERTIFICATE_STORE e pode ser consultado por API GetName () do objeto de provedor. Ele é registrado automaticamente pelo driver e pode ser usado diretamente sem qualquer alteração de aplicativo.

Para os exemplos nesta página, se você tiver criado um Store de certificado do Windows com base em uma chave mestra de coluna e a chave de criptografia de coluna usando o SQL Server Management Studio, o script T-SQL para recriá-los pode parecer semelhante a este exemplo com seu próprio específicas **KEY_PATH** e **ENCRYPTED_VALUE**:

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
> Enquanto os outros provedores de repositório de chaves neste artigo estão disponíveis em todas as plataformas com suporte pelo driver, a implementação de SQLServerColumnEncryptionCertificateStoreProvider do driver JDBC está disponível no Windows somente nos sistemas operacionais. Ele tem uma dependência no sqljdbc_auth que está disponível no pacote de driver. Para usar esse provedor, copie o arquivo sqljdbc_auth.dll para um diretório no caminho do sistema Windows no computador em que o driver JDBC está instalado. Como alternativa, você pode definir a propriedade do sistema java.libary.path para especificar o diretório de sqljdbc_auth.dll. Se você estiver executando uma Máquina Virtual Java (JVM) de 32 bits, use o arquivo sqljdbc_auth.dll na pasta x86, mesmo se o sistema operacional for a versão x64. Se estiver executando uma JVM de 64 bits em um processador x64, use o arquivo sqljdbc_auth.dll na pasta x64. Por exemplo, se você estiver usando a JVM de 32 bits e o driver JDBC estiver instalado no diretório padrão, você poderá especificar o local da DLL usando o seguinte argumento de VM (máquina virtual) quando o aplicativo Java for iniciado: `-Djava.library.path=C:\Microsoft JDBC Driver <version> for SQL Server\sqljdbc_<version>\enu\auth\x86`

### <a name="using-java-key-store-provider"></a>Usando o provedor de Store de chave do Java
O driver JDBC vem com uma implementação de provedor de repositório de chaves interno para o Repositório de Chaves Java. Se o **keyStoreAuthentication** propriedade de cadeia de caracteres de conexão está presente na cadeia de conexão e ele é definido como "JavaKeyStorePassword", o driver automaticamente cria uma instância e registra o provedor para Java chave Store. O nome do provedor de Store de chave Java é MSSQL_JAVA_KEYSTORE. Esse nome também pode ser consultado usando a API SQLServerColumnEncryptionJavaKeyStoreProvider.getName(). 

Há três propriedades de cadeia de caracteres de conexão que permitem que um aplicativo cliente especificar as credenciais que o driver precisa autenticar para o Java chave Store. O driver inicializa o provedor com base nos valores dessas três propriedades na cadeia de conexão.

**keyStoreAuthentication:** identifica o Store de chave Java para usar. Com o Microsoft JDBC Driver 6.0 e superior para o SQL Server, você pode autenticar para o Store de chave Java somente por meio dessa propriedade. Para a Store de chave Java, o valor dessa propriedade deve ser `JavaKeyStorePassword`.

**keyStoreLocation:** o caminho para o arquivo de Store de chave do Java que armazena a chave mestra de coluna. O caminho inclui o nome do arquivo de repositório de chaves.

**keyStoreSecret:** a segredo e a senha a ser usado para o repositório de chaves, bem como para a chave. Para usar o Java chave Store, o repositório de chaves e a senha da chave devem ser o mesmo.

Aqui está um exemplo de fornecer essas credenciais na cadeia de conexão:

```java
String connectionUrl = "jdbc:sqlserver://<server>:<port>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path_to_the_keystore_file>;keyStoreSecret=<keystore_key_password>";
```

Você também pode obter ou definir essas configurações usando o objeto SQLServerDataSource. Para obter mais informações, consulte [Always Encrypted referência da API para o Driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).

O driver JDBC automaticamente cria uma instância de SQLServerColumnEncryptionJavaKeyStoreProvider quando essas credenciais estiverem presentes nas propriedades de conexão.

### <a name="creating-a-column-master-key-for-the-java-key-store"></a>Criando uma chave mestra de coluna para a Store de chave do Java
O SQLServerColumnEncryptionJavaKeyStoreProvider pode ser usado com tipos de repositório de chaves JKS ou PKCS12. Criar ou importar uma chave para uso com este provedor de usar o Java [keytool](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html) utilitário. A chave deve ter a mesma senha como o repositório de chaves em si. Aqui está um exemplo de como criar uma chave pública e da chave privada associada usando o utilitário keytool:

```
keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.jks -storepass mypassword -validity 360 -keysize 2048 -storetype jks
```

Este comando cria uma chave pública e o encapsula em um X.509 autoassinado que o certificado, que é armazenado no repositório de chaves jks juntamente com sua chave privada associada. Essa entrada no repositório de chaves é identificada pelo alias 'AlwaysEncryptedKey'.

Aqui está um exemplo do mesmo usando um tipo de repositório PKCS12:

```
keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.pfx -storepass mypassword -validity 360 -keysize 2048 -storetype pkcs12 -keypass mypassword
```

Se o repositório de chaves é do tipo PKCS12, o utilitário keytool não solicita uma senha de chave e a senha da chave deve ser fornecido com a opção - keypass como o SQLServerColumnEncryptionJavaKeyStoreProvider exige que o repositório de chaves e a chave têm a mesma senha.

Você também pode exportar um certificado do repositório de certificados do Windows no formato. pfx e usá-lo com o SQLServerColumnEncryptionJavaKeyStoreProvider. O certificado exportado também pode ser importado para a Store de chave Java como um tipo de repositório de chaves JKS.

Depois de criar a entrada keytool, crie os metadados da chave mestra de coluna no banco de dados, o que precisa, o nome do provedor de repositório de chaves e o caminho da chave. Para obter mais informações sobre como criar dados de metadados de chave mestra de coluna, consulte [CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md). Para SQLServerColumnEncryptionJavaKeyStoreProvider, o caminho da chave é apenas o alias da chave e o nome da SQLServerColumnEncryptionJavaKeyStoreProvider é 'MSSQL_JAVA_KEYSTORE'. Você também pode consultar esse nome usando a API pública de GetName () da classe SQLServerColumnEncryptionJavaKeyStoreProvider. 

A sintaxe do T-SQL para criar a chave mestra de coluna é:

```sql
CREATE COLUMN MASTER KEY [<CMK_name>]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'<key_alias>'
)
```

Para o 'AlwaysEncryptedKey' criada acima, a definição da chave mestra de coluna deverá ser:

```sql
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'AlwaysEncryptedKey'
)
```

> [!NOTE]
> O funcionalidade do Studio internos de gerenciamento do SQL Server não é possível criar definições de chave mestra de coluna para a Store de chave Java. Comandos T-SQL devem ser usados de forma programática.

### <a name="creating-a-column-encryption-key-for-the-java-key-store"></a>Criando uma chave de criptografia de coluna para a Store de chave do Java
O SQL Server Management Studio ou qualquer outra ferramenta não pode ser usada para criar a coluna de chaves de criptografia usando as chaves mestras de coluna na Store de chave do Java. O aplicativo cliente deve criar a chave de criptografia de coluna programaticamente usando a classe SQLServerColumnEncryptionJavaKeyStoreProvider. Para obter mais informações, consulte [usando provedores de repositório de chaves mestras de coluna para o provisionamento programático de chaves](#using-column-master-key-store-providers-for-programmatic-key-provisioning).

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
Ao acessar colunas criptografadas, o Microsoft JDBC Driver for SQL Server encontra de modo transparente e chama o provedor de repositório de chaves mestras de coluna certo para descriptografar as chaves de criptografia de coluna. Normalmente, o código normal do aplicativo não chama diretamente os provedores de repositórios de chaves mestras de coluna. No entanto, você pode criar uma instância e chamar um provedor de forma programática para provisionar e gerenciar chaves Always Encrypted. Esta etapa pode ser feita para gerar uma chave de criptografia de coluna criptografada e descriptografar uma chave de criptografia de coluna como a rotação de chave mestra de coluna de parte, por exemplo. Para obter mais informações, consulte [Overview of Key Management for Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)(Visão geral do gerenciamento de chaves do Sempre Criptografado).

Caso você use um provedor de repositório de chaves personalizado, poderá ser necessário implementar suas próprias ferramentas de gerenciamento. Ao usar chaves armazenadas no Windows Store de certificado ou no Azure Key Vault, você pode usar ferramentas existentes, como o SQL Server Management Studio ou o PowerShell, gerenciar e provisionar as chaves. Ao usar chaves armazenadas em do Store de chave Java, você precisa provisionar chaves programaticamente. O exemplo a seguir ilustra o uso da classe SQLServerColumnEncryptionJavaKeyStoreProvider para criptografar a chave com uma chave armazenada na Store de chave do Java.

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
    private static String keyAlias = "<proide key alias>";

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

A cadeia de conexão a seguir está um exemplo de habilitar o Always Encrypted no driver JDBC:

```java
String connectionUrl = "jdbc:sqlserver://<server>:<port>;user=<user>;password=<password>;databaseName=<database>;columnEncryptionSetting=Enabled;";
SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionUrl);
```

O código a seguir está um exemplo equivalente usando o objeto SQLServerDataSource:

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

O Sempre Criptografado também pode ser habilitado para consultas individuais. Para obter mais informações, consulte [controlando o impacto no desempenho do Always Encrypted](#controlling-the-performance-impact-of-always-encrypted). Habilitar Always Encrypted não é suficiente para o êxito da criptografia ou descriptografia. Você também precisa garantir que:
- O aplicativo tem as permissões de banco de dados *VIEW ANY COLUMN MASTER KEY DEFINITION* e *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* , necessárias para acessar os metadados sobre as chaves do Always Encrypted no banco de dados. Para obter detalhes, veja [Permissões em Always Encrypted (Mecanismo de Banco de Dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions).
- O aplicativo pode acessar a chave mestra de coluna que protege as chaves de criptografia de coluna, o que criptografa as colunas de banco de dados consultadas. Para usar o provedor de Store de chave do Java, você precisa fornecer credenciais adicionais na cadeia de conexão. Para obter mais informações, consulte [provedor de Store de chave do Java usando](#using-java-key-store-provider).

### <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>Configuração de como os valores de java.sql.Time são enviados ao servidor
A propriedade de conexão **sendTimeAsDatetime** é usada para configurar como o valor java.sql.Time é enviado para o servidor. Quando definido como false, o valor de hora é enviado como um tipo de hora do SQL Server. Quando definido como true, o valor é enviado como um tipo de data e hora de tempo. Se uma coluna de hora for criptografada, o **sendTimeAsDatetime** propriedade deve ser false, como colunas criptografadas não dão suporte a conversão de tempo para a data e hora. Observe também que essa propriedade é por padrão true, então ao usar colunas criptografadas de tempo você terá que defini-lo como false. Caso contrário, o driver lançará uma exceção. A partir da versão 6.0 do driver, a classe SQLServerConnection tem dois métodos para configurar o valor dessa propriedade por meio de programação:
 
* setSendTimeAsDatetime public void (sendTimeAsDateTimeValue boolean)
* public boolean getSendTimeAsDatetime()

Para obter mais informações sobre essa propriedade, consulte [time configurando como os valores são enviados para o servidor](configuring-how-java-sql-time-values-are-sent-to-the-server.md).

### <a name="configuring-how-string-values-are-sent-to-the-server"></a>Configurando como os valores de cadeia de caracteres são enviados ao servidor
O **sendStringParametersAsUnicode** propriedade de conexão é usada para configurar como os valores de cadeia de caracteres são enviados para o SQL Server. Se definida como true, os parâmetros String serão enviados ao servidor no formato Unicode. Se definido como false, parâmetros de cadeia de caracteres é enviado no formato de não-Unicode, como MBCS, em vez de Unicode ou ASCII. O valor padrão para essa propriedade é true. Quando o Always Encrypted estiver habilitado e uma coluna char/varchar/varchar(max) é criptografada, o valor de **sendStringParametersAsUnicode** deve ser definido como false. Se essa propriedade é definida como true, o driver lançará uma exceção ao descriptografar dados de uma coluna criptografada char/varchar/varchar(max) que tem caracteres Unicode. Para obter mais informações sobre essa propriedade, consulte [definindo as propriedades de Conexão](../../connect/jdbc/setting-the-connection-properties.md).
  
## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>Recuperação e modificação de dados em colunas criptografadas
Depois de habilitar o Always Encrypted para consultas de aplicativo, você pode usar APIs padrão do JDBC para recuperar ou modificar dados em colunas de banco de dados criptografado. Se seu aplicativo tem as permissões de banco de dados necessários e pode acessar a chave mestra de coluna, o driver criptografará quaisquer parâmetros de consulta que se destinam a colunas criptografadas e descriptografar dados que são recuperados de colunas criptografadas.

Se o Sempre Criptografado não estiver habilitado, as consultas com parâmetros que se destinam a colunas criptografadas falharão. As consultas ainda podem recuperar dados de colunas criptografadas, desde que a consulta não tenha parâmetros que se destinem a colunas criptografadas. No entanto, o driver não tentará descriptografar nenhum valor recuperado de colunas criptografadas, e o aplicativo receberá os dados binários criptografados (como matrizes de bytes).

A tabela abaixo resume o comportamento das consultas dependendo se Always Encrypted está habilitado ou não:

| Característica da consulta                                                                           | O Always Encrypted está habilitado e o aplicativo pode acessar as chaves e os metadados da chave                                                                                                                        | O Sempre Criptografado está habilitado e o aplicativo não pode acessar as chaves nem os metadados da chave | O Sempre Criptografado está desabilitado                                                                                        |
| :--------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :-------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------ |
| Consultas com parâmetros que se destinam a colunas criptografadas.                                           | Os valores de parâmetro são criptografados de modo transparente.                                                                                                                                                           | Erro                                                                             | Erro                                                                                                               |
| Consultas que recuperam dados de colunas criptografadas sem parâmetros que se destinam a colunas criptografadas. | Os resultados das colunas criptografadas são descriptografados de modo transparente. O aplicativo recebe valores de texto não criptografado dos tipos de dados JDBC correspondentes aos tipos do SQL Server configurados para as colunas criptografadas. | Erro                                                                             | Os resultados das colunas criptografadas não são descriptografados. O aplicativo recebe valores criptografados como matrizes de bytes (byte[]). |

### <a name="inserting-and-retrieving-encrypted-data-examples"></a>Inserir e recuperar dados criptografados exemplos

Os exemplos a seguir ilustram como recuperar e modificar dados em colunas criptografadas. Os exemplos pressupõem que a tabela de destino com o esquema a seguir e as colunas SSN e BirthDate criptografadas. Se você tiver configurado uma chave mestra de coluna chamada "MyCMK" e uma chave de criptografia de coluna chamada "MyCEK" (conforme descrito nas seções anteriores de provedores de repositório de chaves), você pode criar a tabela usando esse script:

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

Se você estiver usando um provedor de repositório de chaves do Azure Key Vault:

```java
    String clientID = "<Azure Application ID>";
    String clientKey = "<Azure Application API Key Password>";
    SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
    Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
    keyStoreMap.put(akvProvider.getName(), akvProvider);
    SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
    String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;";
```

Se você estiver usando um provedor de repositório de chaves do Windows Store de certificado:

```java
    String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;";
```

Se você estiver usando um provedor de repositório de chaves Java chave Store:

```java
    String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path to jks or pfx file>;keyStoreSecret=<keystore secret/password>";
```

### <a name="inserting-data-example"></a>Inserindo exemplo de dados

Este exemplo insere uma linha na tabela Pacientes. Observe os seguintes itens:

- Não há nada específico de criptografia no código de exemplo. O Microsoft JDBC Driver para SQL Server detecta automaticamente e criptografa os parâmetros que se destinam a colunas criptografadas. Esse comportamento torna a criptografia transparente para o aplicativo.
- Os valores inseridos nas colunas de banco de dados, incluindo as colunas criptografadas, são passados como parâmetros usando SQLServerPreparedStatement. Embora o uso de parâmetros seja opcional ao enviar valores para colunas não criptografadas (mesmo que seja altamente recomendável, pois ajuda a prevenir a injeção de SQL), ele é necessário para valores que se destinam a colunas criptografadas. Se os valores inseridos nas colunas criptografadas foram passados como literais inseridos na instrução de consulta, a consulta falharia, pois o driver não seria capaz de determinar os valores em colunas criptografadas de destino e ele não criptografa os valores. Como resultado, o servidor os rejeitaria como incompatíveis com as colunas criptografadas.
- Todos os valores impressos pelo programa estarão em texto não criptografado, já que o Microsoft JDBC Driver for SQL Server descriptografará de modo transparente os dados recuperados das colunas criptografadas.
- Se você estiver fazendo uma pesquisa usando uma cláusula WHERE, o valor usado na cláusula WHERE precisa para ser passado como um parâmetro para que o driver de modo transparente pode criptografá-lo antes de enviá-la para o banco de dados. No exemplo a seguir, o SSN é passado como um parâmetro, mas o sobrenome é passado como um literal, como LastName não está criptografado.
- O método de setter usado para o parâmetro se destina à coluna SSN é Setstring, que mapeia para o tipo de dados do SQL Server char/varchar. Se, para esse parâmetro, o método setter usado tiver sido setNString(), que mapeia para nchar/nvarchar, a consulta falhará, já que o Always Encrypted não é compatível com conversões de valores nchar/nvarchar criptografados em valores char/varchar criptografados.

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

- Você usa os métodos de setter apropriado quando passar valores para parâmetros que se destinam a colunas criptografadas. Certifique-se de que o tipo de dados do SQL Server do parâmetro é exatamente o mesmo que o tipo da coluna de destino ou uma conversão do tipo de dados do SQL Server do parâmetro para o tipo de destino da coluna é suportada. Métodos de API foram adicionados às classes SQLServerPreparedStatement e SQLServerCallableStatement SQLServerResultSet para passar parâmetros correspondentes aos tipos de dados específicos do SQL Server. Por exemplo, se uma coluna não é criptografada você pode usar o método setTimestamp() para passar um parâmetro para um datetime2 ou para uma coluna de data e hora. Mas, quando uma coluna é criptografada, você terá que usar o método exato que representa o tipo da coluna no banco de dados. Por exemplo, use setTimestamp() para passar valores para uma coluna criptografada datetime2 e use setDateTime() para passar valores para uma coluna de datetime criptografados. Ver [Always Encrypted referência da API para o Driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md) para obter uma lista completa das novas APIs.
- a precisão e escala dos parâmetros que se destinam a colunas dos tipos de dados decimais e numéricos do SQL Server são iguais à precisão e escala configuradas para a coluna de destino. Métodos de API foram adicionados às classes SQLServerPreparedStatement e SQLServerCallableStatement SQLServerResultSet para aceitar a precisão e escala junto com os valores de dados para/as colunas de parâmetros que representam os tipos de dados decimais e numéricos. Ver [Always Encrypted referência da API para o Driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md) para obter uma lista completa das APIs de novos/sobrecarregado.  
- precisão/escala de frações de parâmetros que se destinam a colunas datetime2, datetimeoffset ou tipos de dados do SQL Server de hora não for maior que a precisão ou escala de frações de segundos para a coluna de destino em consultas que modificam os valores da coluna de destino . Métodos de API foram adicionados às classes SQLServerPreparedStatement e SQLServerCallableStatement SQLServerResultSet para aceitar a precisão/escala de frações juntamente com os valores de dados para parâmetros que representam a esses tipos de dados. Para obter uma lista completa das APIs de novos/sobrecarregados, consulte [Always Encrypted referência da API para o Driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).

### <a name="errors-due-to-incorrect-connection-properties"></a>Erros devido a propriedades de conexão incorretas

Esta seção descreve como definir as configurações de conexão corretamente para usar dados de Always Encrypted. Porque os tipos de dados criptografados dá suporte a conversões limitadas, o **sendTimeAsDatetime** e **sendStringParametersAsUnicode** configurações de conexão precisam de configuração apropriada ao usar colunas criptografadas. Certifique-se de que:

- [sendTimeAsDatetime](setting-the-connection-properties.md) configuração de conexão é definida como false quando inserindo dados em colunas de tempo de criptografadas. Para obter mais informações, consulte [configurando como os valores time são enviados para o servidor](configuring-how-java-sql-time-values-are-sent-to-the-server.md).
- [sendStringParametersAsUnicode](setting-the-connection-properties.md) configuração de conexão é definida como true (ou é deixado como o padrão) quando inserindo dados em char/varchar/varchar(max) a colunas criptografadas.

### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>Erros devido à passagem de texto sem formatação em vez de valores criptografados

Qualquer valor que se destina a uma coluna criptografada precisa ser criptografado no aplicativo. Uma tentativa de inserir/modificar ou de filtrar por um valor de texto não criptografado em uma coluna criptografada resultará em um erro semelhante a este:

```java
com.microsoft.sqlserver.jdbc.SQLServerException: Operand type clash: varchar is incompatible with varchar(8000) encrypted with (encryption_type = 'DETERMINISTIC', encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'MyCEK', column_encryption_key_database_name = 'ae') collation_name = 'SQL_Latin1_General_CP1_CI_AS'
```

Para evitar esses tipos de erros, garanta que:

- Always Encrypted é habilitado para as consultas de aplicativo que se destinam a colunas criptografadas (na cadeia de conexão ou para uma consulta específica).
- use as instruções preparadas e parâmetros para enviar dados direcionamento a colunas criptografadas. O exemplo a seguir mostra uma consulta filtrada incorretamente por um literal/constante em uma coluna criptografada (SSN), em vez de passar o literal para dentro como um parâmetro. Essa consulta falhará:

```java
ResultSet rs = connection.createStatement().executeQuery("SELECT * FROM Customers WHERE SSN='795-73-9838'");
```

## <a name="force-encryption-on-input-parameters"></a>Forçar a criptografia em parâmetros de entrada

O recurso de Forçar criptografia impõe a criptografia de um parâmetro ao usar o Always Encrypted. Se forçar criptografia for usado e o SQL Server informar o driver de que o parâmetro não precisa ser criptografado, a consulta que estiver o parâmetro falhará. Essa propriedade fornece proteção adicional contra ataques de segurança que envolvem um SQL Server comprometido fornecendo metadados de criptografia incorretos ao cliente, o que pode levar à divulgação de dados. Os métodos em classes SQLServerPreparedStatement e SQLServerCallableStatement e a atualização de conjunto *\* métodos na classe SQLServerResultSet são sobrecarregados para aceitar um argumento booliano para especificar a configuração de criptografia de força. Se o valor desse argumento for false, o driver não força a criptografia em parâmetros. Se Forçar criptografia for definida como true, a consulta de parâmetro só é enviado se a coluna de destino está criptografada e Always Encrypted estiver habilitado, a conexão ou a instrução. Usar esta propriedade fornece uma camada extra de segurança, garantindo que o driver não por engano envia dados para o SQL Server como texto sem formatação que deve ser criptografado.

Para obter mais informações sobre os métodos de SQLServerPreparedStatement e SQLServerCallableStatement são sobrecarregados com a configuração de criptografia de força, consulte [sempre criptografados referência da API para o Driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)  

## <a name="controlling-the-performance-impact-of-always-encrypted"></a>Controle do impacto sobre o desempenho do Always Encrypted

Como o Always Encrypted é uma tecnologia de criptografia do lado do cliente, a maior parte da sobrecarga de desempenho é observada no lado do cliente, não no banco de dados. Além do custo das operações de criptografia e descriptografia, outras fontes de sobrecarga de desempenho no lado do cliente são:

- Viagens de ida e volta adicionais ao banco de dados para recuperar metadados dos parâmetros de consulta.
- Chamadas a um repositório de chaves mestras de coluna para acessar uma chave mestra de coluna.

Esta seção descreve as otimizações de desempenho internas no Microsoft JDBC Driver for SQL Server e como você pode controlar o impacto dos dois fatores acima sobre o desempenho.

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>Controlando as viagens de ida e volta para recuperar metadados dos parâmetros de consulta

Se o Always Encrypted estiver habilitado para uma conexão, por padrão, o driver chamará [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) para cada consulta parametrizada, passando a instrução de consulta (sem nenhum valor de parâmetro) para o SQL Server. O [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) analisa a instrução de consulta para descobrir se os parâmetros precisam ser criptografados e, se for o caso, para cada um, retornará as informações relacionadas à criptografia que permitirão ao driver criptografar os valores de parâmetro. Esse comportamento garante um alto nível de transparência para o aplicativo cliente. Desde que o aplicativo usa parâmetros para passar valores que se destinam a colunas criptografadas para o driver, o aplicativo (e o desenvolvedor do aplicativo) não precisam saber quais consultas acessam colunas criptografadas.

### <a name="setting-always-encrypted-at-the-query-level"></a>Configurando o Always Encrypted no nível da consulta

Para controlar o impacto no desempenho da recuperação de metadados de criptografia para consultas parametrizadas, é possível habilitar o Always Encrypted para consultas individuais, em vez de configurá-lo para a conexão. Assim, você pode garantir que sys.sp_describe_parameter_encryption seja invocado apenas para consultas que você sabe que têm parâmetros que se destinam a colunas criptografadas. No entanto, observe que, ao fazer isso, você reduz a transparência da criptografia: se você alterar as propriedades de criptografia das colunas de banco de dados, poderá ser necessário alterar o código do aplicativo para alinhá-lo às alterações de esquema.

Para controlar o comportamento de Always Encrypted de consultas individuais, você precisa configurar os objetos de instrução individual, passando um Enum, SQLServerStatementColumnEncryptionSetting, que especifica como os dados serão enviados e recebidos durante a leitura e gravação colunas criptografadas para essa instrução específica. Veja algumas diretrizes úteis:

- Se a maioria das consultas que um aplicativo cliente enviar por uma conexão de banco de dados acessa colunas criptografadas, use estas diretrizes:

    - Defina a palavra-chave da cadeia de conexão **columnEncryptionSetting** como **Habilitada**.
    - Defina SQLServerStatementColumnEncryptionSetting.Disabled para consultas individuais que não acessam nenhuma coluna criptografada. Essa configuração desabilitará a chamada a sys.sp_describe_parameter_encryption, além de ser uma tentativa de descriptografar todos os valores no conjunto de resultados.
    - Defina SQLServerStatementColumnEncryptionSetting.ResultSet para consultas individuais que não têm parâmetros que exijam criptografia, mas que recuperam dados de colunas criptografadas. Essa configuração desabilitará a chamada a sys.sp_describe_parameter_encryption e a criptografia de parâmetros. A consulta poderá descriptografar os resultados das colunas de criptografia.

- Se a maioria das consultas que um aplicativo cliente enviar por uma conexão de banco de dados não acessa colunas criptografadas, use estas diretrizes:

    - Defina a palavra-chave da cadeia de conexão **columnEncryptionSetting** como **Desabilitada**.
    - Defina SQLServerStatementColumnEncryptionSetting.Enabled para consultas individuais que têm parâmetros que precisam ser criptografados. Essa configuração habilitará a chamada a sys.sp_describe_parameter_encryption, além da descriptografia de todos os resultados de consulta recuperados de colunas criptografadas.
    - Defina SQLServerStatementColumnEncryptionSetting.ResultSet para consultas que não têm parâmetros que exijam criptografia, mas que recuperam dados de colunas criptografadas. Essa configuração desabilitará a chamada a sys.sp_describe_parameter_encryption e a criptografia de parâmetros. A consulta poderá descriptografar os resultados das colunas de criptografia.

As configurações de SQLServerStatementColumnEncryptionSetting não podem ser usadas para ignorar a criptografia e obter acesso aos dados de texto sem formatação. Para obter mais informações sobre como configurar a criptografia de coluna em uma instrução, consulte [Always Encrypted referência da API para o Driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).  

No exemplo abaixo, Always Encrypted está desabilitado para a conexão de banco de dados. A consulta emitida pelo aplicativo tem um parâmetro que se destina à coluna LastName não criptografada. A consulta recupera dados das colunas SSN e BirthDate que são criptografadas. Nesse caso, a chamada a sys.sp_describe_parameter_encryption para recuperar os metadados de criptografia não é necessária. No entanto, a descriptografia dos resultados da consulta precisa ser habilitada para que o aplicativo possa receber valores de texto não criptografado das duas colunas criptografadas. A configuração SQLServerStatementColumnEncryptionSetting.ResultSet é usada para garantir que.

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

Você pode configurar um valor time-to-live para as entradas de chave de criptografia de coluna no cache usando a API, setColumnEncryptionKeyCacheTtl(), na classe SQLServerConnection. O valor de tempo de vida padrão para as entradas de chave de criptografia de coluna no cache é duas horas. Para desativar o cache, use um valor de 0. Para definir qualquer valor time-to-live, use a seguinte API:

```java
SQLServerConnection.setColumnEncryptionKeyCacheTtl (int columnEncryptionKeyCacheTTL, TimeUnit unit)
```

Por exemplo, para definir um valor de tempo de vida de 10 minutos, use:

```java
SQLServerConnection.setColumnEncryptionKeyCacheTtl (10, TimeUnit.MINUTES)
```

Apenas dias, horas, minutos ou segundos têm suporte como a unidade de tempo.  

## <a name="copying-encrypted-data-using-sqlserverbulkcopy"></a>Copiando dados criptografados usando SQLServerBulkCopy

Com SQLServerBulkCopy, você pode copiar dados que já estão criptografados e armazenados em uma tabela para outra tabela sem descriptografá-los. Para fazer isso:

- Verifique se a configuração de criptografia da tabela de destino é idêntica à configuração da tabela de origem. Em particular, as duas tabelas devem ter as mesmas colunas criptografadas, e as colunas devem ser criptografadas usando os mesmos tipos de criptografia e as mesmas chaves de criptografia. Se qualquer coluna de destino for criptografada de modo diferente da coluna de origem correspondente, você não poderá descriptografar os dados na tabela de destino após a operação de cópia. Os dados serão corrompidos.
- Configure ambas as conexões de banco de dados para a tabela de origem e a tabela de destino sem o Always Encrypted habilitado.
- Defina a opção allowEncryptedValueModifications. Para obter mais informações, consulte [usando a cópia em massa com o Driver JDBC](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md).

> [!NOTE]
> Tenha cuidado ao especificar AllowEncryptedValueModifications, pois isso pode levar à corrupção de banco de dados, porque o Microsoft JDBC Driver for SQL Server não verifica se os dados estão realmente criptografados ou se estão criptografados corretamente usando o mesmo tipo de criptografia, algoritmo e chave que a coluna de destino.

## <a name="see-also"></a>Consulte Também

[Always Encrypted (mecanismo de banco de dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)
