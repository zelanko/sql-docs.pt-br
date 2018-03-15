---
title: Usando o sempre criptografado com o driver JDBC | Microsoft Docs
ms.custom: 
ms.date: 3/14/2018
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
ms.assetid: 271c0438-8af1-45e5-b96a-4b1cabe32707
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: af8b651364f58c3c4261666d5d6531e99e620efe
ms.sourcegitcommit: 6b1618aa3b24bf6759b00a820e09c52c4996ca10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/15/2018
---
# <a name="using-always-encrypted-with-the-jdbc-driver"></a>Usando o sempre criptografado com o driver JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Esta página fornece informações sobre como desenvolver aplicativos do Java usando [sempre criptografado](../../relational-databases/security/encryption/always-encrypted-database-engine.md) e o Microsoft JDBC Driver 6.0 (ou superior) para o SQL Server.

Sempre criptografado permite que os clientes criptografem dados confidenciais e nunca revelem os dados ou as chaves de criptografia do SQL Server ou banco de dados do SQL Azure. Um sempre criptografado habilitado driver, como o Microsoft JDBC Driver 6.0 (ou superior) para o SQL Server, atinge esse comportamento criptografando e descriptografando dados confidenciais no aplicativo cliente de forma transparente. O driver determina automaticamente qual consulta parâmetros correspondem a colunas de banco de dados sempre criptografados e criptografa os valores desses parâmetros antes de enviar para o SQL Server ou banco de dados do SQL Azure. Da mesma forma, o driver descriptografa de modo transparente os dados recuperados das colunas de banco de dados criptografadas nos resultados da consulta. Para obter mais informações, consulte [sempre criptografados (mecanismo de banco de dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) e [sempre criptografados referência da API para o Driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).

## <a name="prerequisites"></a>Prerequisites
- Certifique-se de que Microsoft JDBC Driver 6.0 (ou superior) para o SQL Server está instalado no computador de desenvolvimento. 
- Baixe e instale os arquivos de política de jurisdição de força ilimitada de Java Cryptography Extension (JCE).  Certifique-se de ler o arquivo Leiame incluído no arquivo zip para instruções de instalação e os detalhes relevantes sobre os problemas possíveis de importação/exportação.  

    - Se usar o mssql-jdbc-X.X.X.jre7.jar ou sqljdbc41.jar, os arquivos de política podem ser baixados de [baixar arquivos de política de jurisdição de força ilimitada do Java Cryptography Extension (JCE) 7](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)

    - Se usar o mssql-jdbc-X.X.X.jre8.jar ou sqljdbc42.jar, os arquivos de política podem ser baixados de [baixar arquivos de política de jurisdição de força ilimitada do Java Cryptography Extension (JCE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)

    - Se usando o X.X.X.jre9.jar mssql-jdbc, nenhum arquivo de política deve ser baixado. A política de jurisdição em Java 9 segue o padrão de criptografia de nível ilimitado.

## <a name="working-with-column-master-key-stores"></a>Trabalhando com repositórios de chave mestra de coluna
Para criptografar ou descriptografar dados para colunas criptografadas, o SQL Server mantém as chaves de criptografia de coluna. Chaves de criptografia de coluna são armazenadas em formato criptografado nos metadados do banco de dados. Cada chave de criptografia de coluna tem uma chave de mestre de coluna correspondente que é usada para criptografar a chave de criptografia de coluna. Os metadados do banco de dados não contém as chaves mestras de coluna. Essas chaves só são mantidas pelo cliente. No entanto os metadados do banco de dados contêm informações sobre onde as chaves mestras de coluna são armazenadas em relação ao cliente. Por exemplo, os metadados do banco de dados podem dizer que o armazenamento de chaves que contém a chave mestra da coluna é o repositório de certificados do Windows e o certificado específico usado para criptografar e descriptografar está localizado em um caminho específico dentro do repositório de certificados do Windows. Se o cliente tem acesso ao certificado no repositório de certificados do Windows, ele poderá obter o certificado. O certificado, em seguida, pode ser usado para descriptografar a chave de criptografia de coluna. Em seguida, essa chave de criptografia pode ser usado para descriptografar ou criptografar dados para colunas criptografadas que usam essa chave de criptografia de coluna.

O Microsoft JDBC Driver para SQL Server se comunica com um armazenamento de chaves usando um provedor de repositório de chaves mestras de coluna, que é uma instância de uma classe derivado de **SQLServerColumnEncryptionKeyStoreProvider**.

### <a name="using-built-in-column-master-key-store-providers"></a>Usando provedores internos de repositórios de chaves mestras de coluna
O Microsoft JDBC Driver para SQL Server vem com os seguintes provedores de armazenamento de chave mestra de coluna interna. Alguns desses provedores são previamente registrados com os nomes de provedor específico (usados para pesquisar o provedor) e alguns exigir credenciais adicionais ou registro explícito.

| Classe | Description | Nome (de pesquisa) do provedor |Pré-registrados?|
|:---|:---|:---|:---|
|**SQLServerColumnEncryptionAzureKeyVaultProvider**| Um provedor para um armazenamento de chaves para o Cofre de chaves do Azure.| AZURE_KEY_VAULT|não|
|**SQLServerColumnEncryptionCertificateStoreProvider**| Um provedor para o repositório de certificados do Windows.|MSSQL_CERTIFICATE_STORE|Sim
|**SQLServerColumnEncryptionJavaKeyStoreProvider**| Um provedor de armazenamento de chaves Java|MSSQL_JAVA_KEYSTORE|Sim|

Para os provedores de armazenamento de chaves previamente registrado, você não precisa fazer alterações de código de aplicativo para usar estes provedores, mas observe os seguintes itens:

- Você (ou seu DBA) precisa verificar se o nome do provedor configurado nos metadados de chave mestra de coluna está correto e o caminho da chave mestra de coluna está em conformidade com o formato do caminho da chave é válido para um determinado provedor. É recomendável que você configure as chaves usando ferramentas como o SQL Server Management Studio, que gera automaticamente os nomes de provedor válido e caminhos de chaves ao emitir a instrução CREATE COLUMN MASTER KEY (Transact-SQL).
- Certifique-se de que seu aplicativo pode acessar a chave no armazenamento de chaves. Essa tarefa pode envolver concedendo acesso ao seu aplicativo para a chave e/ou o armazenamento de chaves, dependendo do repositório de chaves, ou executar outras etapas de configuração de armazenamento de chaves específico. Por exemplo, para usar o SQLServerColumnEncryptionJavaKeyStoreProvider, você precisa fornecer o local e a senha da chave de armazenamento nas propriedades de conexão. 

Todos esses provedores de armazenamento de chaves são descritos mais detalhadamente nas seções a seguir. Você só precisa implementar um provedor de armazenamento de chaves para usar sempre criptografado.

### <a name="using-azure-key-vault-provider"></a>Usando o provedor do Cofre de Chaves do Azure
Cofre de chaves do Azure é uma opção conveniente para armazenar e gerenciar chaves mestras de coluna para sempre criptografado (especialmente se o aplicativo está hospedado no Azure). O Microsoft JDBC Driver para SQL Server inclui um provedor interno, SQLServerColumnEncryptionAzureKeyVaultProvider, para aplicativos que têm chaves armazenadas no cofre de chaves do Azure. O nome deste provedor é AZURE_KEY_VAULT. Para usar o provedor de armazenamento de Cofre de chaves do Azure, um desenvolvedor de aplicativos precisa criar o cofre e as chaves no cofre de chaves do Azure e criar um registro de aplicativo no Azure Active Directory. O aplicativo registrado deve ser concedida obter, descriptografar, Encrypt, desencapsular chave, Key Wrap e verifique se permissões nas políticas de acesso definidas para o Cofre de chaves criado para uso com o sempre criptografado. Para obter mais informações sobre como configurar o Cofre de chaves e criar uma chave mestra de coluna, consulte [Cofre de chaves do Azure – passo](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/) e [Criando chaves mestras de coluna no cofre de chaves do Azure](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md#creating-column-master-keys-in-azure-key-vault).

Para os exemplos nesta página, se você tiver criado um cofre de chaves do Azure com base em uma chave mestra de coluna e a chave de criptografia de coluna usando o SQL Server Management Studio, o script T-SQL para recriá-los pode ser semelhante a este exemplo com sua própria específico **KEY_ CAMINHO** e **ENCRYPTED_VALUE**:

```
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

Para usar o Cofre de chaves do Azure, os aplicativos cliente precisam instanciar o SQLServerColumnEncryptionAzureKeyVaultProvider e registrá-lo com o driver.

Aqui está um exemplo de inicialização SQLServerColumnEncryptionAzureKeyVaultProvider:  

```
SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
```

**clientID** é a ID do aplicativo de um registro de aplicativo em uma instância do Active Directory do Azure. **clientKey** uma senha de chave que está registrada no aplicativo, que fornece acesso à API para o Cofre de chaves do Azure.

Depois que o aplicativo cria uma instância de SQLServerColumnEncryptionAzureKeyVaultProvider, o aplicativo deve registrar a instância com o driver usando o método registercolumnencryptionkeystoreproviders (). É altamente recomendável que a instância é registrada usando o nome de pesquisa padrão, AZURE_KEY_VAULT, que pode ser obtida chamando a API SQLServerColumnEncryptionAzureKeyVaultProvider.getName(). Usando o nome padrão permitirá que você use ferramentas como o SQL Server Management Studio ou o PowerShell para provisionar e gerenciar chaves Always Encrypted (ferramentas de usam o nome padrão para gerar o objeto de metadados para a chave mestra de coluna). O exemplo a seguir mostra como registrar o provedor do Azure Key Vault. Para obter mais informações sobre o método registercolumnencryptionkeystoreproviders (), consulte [sempre criptografados referência da API para o Driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).

```
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
keyStoreMap.put(akvProvider.getName(), akvProvider);
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
```

> [!IMPORTANT]
>  Se você usar o provedor de armazenamento de chaves do Cofre de chaves do Azure, a implementação do Cofre de chaves do Azure do driver JDBC tem dependências nessas bibliotecas (do GitHub) que devem ser incluídas com seu aplicativo:
>
>  [azure-sdk-for-java](https://github.com/Azure/azure-sdk-for-java)
>
>  [azure-activedirectory-library-for-java libraries](https://github.com/AzureAD/azure-activedirectory-library-for-java)
>
> Para obter um exemplo de como incluir essas dependências em um projeto Maven, consulte [baixar ADAL4J AKV dependências e com o Apache Maven](https://github.com/Microsoft/mssql-jdbc/wiki/Download-ADAL4J-And-AKV-Dependencies-with-Apache-Maven)

### <a name="using-windows-certificate-store-provider"></a>Usando o provedor de repositório de certificados do Windows
O SQLServerColumnEncryptionCertificateStoreProvider pode ser usado para armazenar chaves mestras de coluna no repositório de certificados do Windows. Use o Assistente do SQL Server Management Studio (SSMS) sempre criptografado ou outras ferramentas com suporte para criar a chave mestra de coluna e a criptografia de coluna definições de chave no banco de dados. O mesmo assistente pode ser usado para gerar um certificado autoassinado no repositório de certificados do Windows que pode ser usado como uma chave mestra de coluna para os dados sempre criptografados. Para obter mais informações sobre a chave mestra de coluna e a sintaxe de T-SQL de chave da criptografia de coluna, consulte [CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md) e [criar chave de criptografia de coluna](../../t-sql/statements/create-column-encryption-key-transact-sql.md) respectivamente.

O nome do SQLServerColumnEncryptionCertificateStoreProvider é MSSQL_CERTIFICATE_STORE e pode ser consultado com o API GetName do objeto de provedor. Ele é registrado automaticamente pelo driver e pode ser usado diretamente sem qualquer alteração de aplicativo.

Para os exemplos nesta página, se você tiver criado um repositório de certificados do Windows com base em uma chave mestra de coluna e a chave de criptografia de coluna usando o SQL Server Management Studio, o script T-SQL para recriá-los pode parecer semelhante a este exemplo com sua própria específico **KEY_PATH** e **ENCRYPTED_VALUE**:

```
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
> A implementação SQLServerColumnEncryptionCertificateStoreProvider do driver JDBC está disponível com sistemas operacionais somente Windows e tem uma dependência de sqljdbc_auth.dll que está disponível no pacote de driver. Para usar esse provedor, copie o arquivo sqljdbc_auth.dll para um diretório no caminho do sistema Windows no computador onde o driver JDBC está instalado. Como alternativa, você pode definir a propriedade do sistema java.libary.path para especificar o diretório de sqljdbc_auth.dll. Se você estiver executando uma Máquina Virtual Java (JVM) de 32 bits, use o arquivo sqljdbc_auth.dll na pasta x86, mesmo se o sistema operacional for a versão x64. Se estiver executando uma JVM de 64 bits em um processador x64, use o arquivo sqljdbc_auth.dll na pasta x64. Por exemplo, se você estiver usando o JVM de 32 bits e o driver JDBC está instalado no diretório padrão, você pode especificar o local da DLL usando o seguinte argumento de máquina virtual (VM) quando o aplicativo Java for iniciado: `-Djava.library.path=C:\Microsoft JDBC Driver <version> for SQL Server\sqljdbc_<version>\enu\auth\x86`

### <a name="using-java-key-store-provider"></a>Usando o provedor de armazenamento de chaves Java
O driver JDBC vem com uma implementação de provedor de armazenamento de chaves interno para o repositório de chaves Java. Se o **keyStoreAuthentication** propriedade de cadeia de caracteres de conexão está presente na cadeia de conexão e é definido como "JavaKeyStorePassword", o driver automaticamente cria e registra o provedor de armazenamento de chaves Java. O nome do provedor de armazenamento de chaves Java é MSSQL_JAVA_KEYSTORE. Esse nome também pode ser consultado usando a API SQLServerColumnEncryptionJavaKeyStoreProvider.getName(). 

Há três propriedades de cadeia de caracteres de conexão que permitem que um aplicativo cliente especificar as credenciais que o driver precisa para autenticar para o repositório de chaves Java. O driver inicializa o provedor com base nos valores dessas propriedades três na cadeia de conexão.

**keyStoreAuthentication:** identifica o repositório de chaves Java para usar. Microsoft JDBC driver 6.0 e superior para o SQL Server, você pode autenticar para o repositório de chaves Java apenas através desta propriedade. Para o repositório de chaves Java, o valor dessa propriedade deve ser `JavaKeyStorePassword`.

**keyStoreLocation:** o caminho para o arquivo de repositório de chaves Java que armazena a chave mestra de coluna. O caminho inclui o nome do arquivo de armazenamento de chaves.

**keyStoreSecret:** a segredo/senha a ser usada para o armazenamento de chaves, bem como para a chave. Para usar o repositório de chaves Java, o armazenamento de chaves e a senha da chave devem ser o mesmo.

Aqui está um exemplo de fornecer essas credenciais na cadeia de conexão:

```
String connectionString = "jdbc:sqlserver://localhost;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path_to_the_keystore_file>;keyStoreSecret=<keystore_key_password>";
```

Você também pode obter ou definir essas configurações usando o objeto SQLServerDataSource. Para obter mais informações, consulte [sempre criptografados referência da API para o Driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).

O driver JDBC cria automaticamente o SQLServerColumnEncryptionJavaKeyStoreProvider quando essas credenciais estão presentes nas propriedades de conexão.

### <a name="creating-a-column-master-key-for-the-java-key-store"></a>Criando uma chave mestra de coluna para o repositório de chaves Java
O SQLServerColumnEncryptionJavaKeyStoreProvider pode ser usado com tipos de armazenamento de chaves JKS ou PKCS12. Para criar ou importar uma chave para uso com este provedor de usar o Java [keytool](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html) utilitário. A chave deve ter a mesma senha que o armazenamento de chaves em si. Aqui está um exemplo de como criar uma chave pública e a chave privada associada usando o utilitário keytool:

```
keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.jks -storepass mypassword -validity 360 -keysize 2048 -storetype jks
```

Este comando cria uma chave pública e organize-os em um x. 509 autoassinado certificado, que é armazenado no armazenamento de chaves jks junto com sua chave privada associada. Esta entrada no armazenamento de chaves é identificada pelo alias 'AlwaysEncryptedKey'.

Aqui está um exemplo do mesmo usando um tipo de repositório PKCS12:

```
keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.pfx -storepass mypassword -validity 360 -keysize 2048 -storetype pkcs12 -keypass mypassword
```

Se o armazenamento de chaves é do tipo PKCS12, o utilitário keytool não solicitará uma senha de chave e a senha da chave deve ser fornecido com a opção - keypass como o SQLServerColumnEncryptionJavaKeyStoreProvider requer que o armazenamento de chaves e a chave têm o mesmo senha.

Você também pode exportar um certificado do repositório de certificados do Windows no formato. pfx e usá-lo com o SQLServerColumnEncryptionJavaKeyStoreProvider. O certificado exportado também pode ser importado para o repositório de chaves Java como um tipo de armazenamento de chaves JKS.

Depois de criar a entrada de keytool, crie os metadados de chave mestra de coluna no banco de dados, o que precisa do nome do provedor de armazenamento de chaves e o caminho da chave. Para obter mais informações sobre como criar metadados de chave mestra de coluna, consulte [CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md). Para SQLServerColumnEncryptionJavaKeyStoreProvider, o caminho da chave é apenas o alias da chave e o nome de SQLServerColumnEncryptionJavaKeyStoreProvider é 'MSSQL_JAVA_KEYSTORE'. Você também pode consultar esse nome usando a API pública GetName da classe SQLServerColumnEncryptionJavaKeyStoreProvider. 

A sintaxe do T-SQL para criar a chave mestra de coluna é:

```
CREATE COLUMN MASTER KEY [<CMK_name>]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'<key_alias>'
)
```

Para o 'AlwaysEncryptedKey' criado acima, a definição da chave mestra de coluna deve ser:

```
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'AlwaysEncryptedKey'
)
```

> [!NOTE]
> O funcionalidade Studio internos de gerenciamento do SQL Server não é possível criar definições de chave mestra de coluna para o repositório de chaves Java. Os comandos T-SQL devem ser usados por meio de programação.

### <a name="creating-a-column-encryption-key-for-the-java-key-store"></a>Criando uma chave de criptografia de coluna para o repositório de chaves Java
O SQL Server Management Studio ou qualquer outra ferramenta não pode ser usada para criar a coluna de chaves de criptografia usando chaves mestras de coluna no repositório de chave Java. O aplicativo cliente deve criar a chave de criptografia de coluna programaticamente usando a classe SQLServerColumnEncryptionJavaKeyStoreProvider. Para obter mais informações, consulte [usando provedores de repositório de chaves mestras de coluna para provisionamento programático de chaves](#using-column-master-key-store-providers-for-programmatic-key-provisioning).

### <a name="implementing-a-custom-column-master-key-store-provider"></a>Implementando um provedor personalizado de repositórios de chaves mestras de coluna
Se você quiser armazenar chaves mestras de coluna em um armazenamento de chaves que não é suportado por um provedor existente, você pode implementar um provedor personalizado estendendo a classe SQLServerColumnEncryptionKeyStoreProvider e registrando o provedor usando o Método registercolumnencryptionkeystoreproviders ().

```
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

```
SQLServerColumnEncryptionKeyStoreProvider storeProvider = new MyCustomKeyStore();
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
keyStoreMap.put(storeProvider.getName(), storeProvider);
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
```

## <a name="using-column-master-key-store-providers-for-programmatic-key-provisioning"></a>Usando provedores de repositórios de chaves mestras de coluna para o provisionamento programático de chaves
Ao acessar colunas criptografadas, o Microsoft JDBC Driver para SQL Server encontra transparente e chama o provedor de armazenamento de chave mestra de coluna da direita para descriptografar as chaves de criptografia de coluna. Normalmente, o código normal do aplicativo não chama diretamente os provedores de repositórios de chaves mestras de coluna. No entanto, você pode criar uma instância e chamar um provedor de forma programática para provisionar e gerenciar chaves Always Encrypted. Esta etapa pode ser feita para gerar uma chave de criptografia de coluna criptografada e descriptografar uma chave de criptografia de coluna como parte rotação de chave mestra de coluna, por exemplo. Para obter mais informações, consulte [Overview of Key Management for Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)(Visão geral do gerenciamento de chaves do Sempre Criptografado).

Se você usar um provedor de armazenamento de chaves personalizado, pode ser necessário implementar suas próprias ferramentas de gerenciamento de chaves. Ao usar chaves armazenadas no repositório de certificados do Windows ou no cofre de chaves do Azure, você pode usar as ferramentas existentes, como o SQL Server Management Studio ou o PowerShell, para gerenciar e provisionar as chaves. Ao usar chaves armazenadas no repositório de chave Java, você precisa provisionar as chaves de forma programática. O exemplo a seguir ilustra o uso da classe SQLServerColumnEncryptionJavaKeyStoreProvider para criptografar a chave com uma chave armazenada no repositório de chave Java.

```
import java.sql.*;
import javax.xml.bind.DatatypeConverter;
import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionJavaKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerException;

/**
 * This program demonstrates how to create a column encryption key programmatically for the Java Key Store.
 */
public class AlwaysEncrypted
{
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
     * Name of the encryption algorithm used to encrypt the value of
     * the column encryption key. The algorithm for the system providers must be RSA_OAEP.
     */
    private static String algorithm = "RSA_OAEP";

    public static void main(String[] args)
    {
        String connectionString = GetConnectionString();
        try
        {
            // Note: if you are not using try-with-resources statements (as here),
            // you must remember to call close() on any Connection, Statement,
            // ResultSet objects that you create.

            // Open a connection to the database.
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
            try (Connection sourceConnection = DriverManager.getConnection(connectionString))
            {
                // Instantiate the Java Key Store provider.
                SQLServerColumnEncryptionKeyStoreProvider storeProvider =
                        new SQLServerColumnEncryptionJavaKeyStoreProvider(
                                keyStoreLocation,
                                keyStoreSecret);

                byte [] encryptedCEK=getEncryptedCEK(storeProvider);

                /**
                 * Create column encryption key
                 * For more details on the syntax, see:
                 * https://docs.microsoft.com/sql/t-sql/statements/create-column-encryption-key-transact-sql
                 * Encrypted column encryption key first needs to be converted into varbinary_literal from bytes, 
                 * for which DatatypeConverter.printHexBinary is used
                 */
                String createCEKSQL = "CREATE COLUMN ENCRYPTION KEY "
                        + columnEncryptionKey
                        + " WITH VALUES ( "
                        + " COLUMN_MASTER_KEY = "
                        + columnMasterKeyName
                        + " , ALGORITHM =  '"
                        + algorithm
                        + "' , ENCRYPTED_VALUE =  0x"
                        + DatatypeConverter.printHexBinary(encryptedCEK)
                        + " ) ";

                try (Statement cekStatement = sourceConnection.createStatement())
                {
                    cekStatement.executeUpdate(createCEKSQL);
                    System.out.println("Column encryption key created with name : " + columnEncryptionKey);
                }
            }
        }
        catch (Exception e)
        {
            // Handle any errors that may have occurred.
            e.printStackTrace();
        }
    }

    // To avoid storing the sourceConnection String in your code,
    // you can retrieve it from a configuration file.
    private static String GetConnectionString()
    {
        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://localhost:1433;" +
                "databaseName=ae2;user=sa;password=********;";

        return connectionUrl;
    }

    private static byte[] getEncryptedCEK(SQLServerColumnEncryptionKeyStoreProvider storeProvider) throws SQLServerException
    {
        /**
         * Following arguments needed by SQLServerColumnEncryptionJavaKeyStoreProvider
         * 1) keyStoreLocation :
         *      Path where keystore is located, including the keystore file name.
         * 2) keyStoreSecret :
         *      Password of the keystore and the key.
         */
        String plainTextKey = "You need to give your plain text";

        // plainTextKey has to be 32 bytes with current algorithm supported
        byte[] plainCEK = plainTextKey.getBytes();

        // This will give us encrypted column encryption key in bytes
        byte[] encryptedCEK = storeProvider.encryptColumnEncryptionKey(
                keyAlias,
                algorithm,
                plainCEK);

        return encryptedCEK;
    }
}
```

## <a name="enabling-always-encrypted-for-application-queries"></a>Habilitando o Always Encrypted para consultas de aplicativo
É a maneira mais fácil de habilitar a criptografia de parâmetros e a descriptografia dos resultados de consulta que se destinam a colunas criptografadas, definindo o valor da **columnEncryptionSetting** palavra-chave de cadeia de caracteres de conexão para **habilitado** .

A cadeia de conexão a seguir é um exemplo de como habilitar o sempre criptografado no driver JDBC:

```
String connectionString = "jdbc:sqlserver://localhost;user=<user>;password=<password>;databaseName=<database>;columnEncryptionSetting=Enabled;";
SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionString);
```

O código a seguir é um exemplo equivalente usando o objeto SQLServerDataSource:

```
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName("localhost");
ds.setUser("<user>");
ds.setPassword("<password>");
ds.setDatabaseName("<database>");
ds.setColumnEncryptionSetting("Enabled");
SQLServerConnection con = (SQLServerConnection) ds.getConnection();
```

O Sempre Criptografado também pode ser habilitado para consultas individuais. Para obter mais informações, consulte [controlando o impacto no desempenho do sempre criptografado](#controlling-the-performance-impact-of-always-encrypted). Habilitando sempre criptografado não é suficiente para a criptografia ou descriptografia tenha êxito. Você também precisa garantir que:
- O aplicativo tem as permissões de banco de dados *VIEW ANY COLUMN MASTER KEY DEFINITION* e *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* , necessárias para acessar os metadados sobre as chaves do Always Encrypted no banco de dados. Para obter detalhes, consulte [permissões em sempre criptografados (mecanismo de banco de dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions).
- O aplicativo pode acessar a chave mestra de coluna que protege as chaves de criptografia de coluna, que criptografar as colunas de banco de dados consultadas. Para usar o provedor de armazenamento de chaves Java, você precisa fornecer credenciais adicionais na cadeia de conexão. Para obter mais informações, consulte [provedor de repositório de chaves Java usando](#using-java-key-store-provider).

### <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>Configurar como os valores são enviados ao servidor
O **sendTimeAsDatetime** propriedade de conexão é usada para configurar como o valor de Java.SQL. time será enviado para o servidor. Quando definido como false, o valor de tempo é enviado como um tipo de tempo do SQL Server. Quando definido como true, o valor é enviado como um tipo de datetime de tempo. Se uma coluna de hora for criptografada, o **sendTimeAsDatetime** propriedade deve ser false, como colunas criptografadas não dão suporte a conversão de tempo para datetime. Observe também que essa propriedade é true, o padrão para ao usar colunas de hora criptografada que defini-lo como false. Caso contrário, o driver lançará uma exceção. Começando com a versão 6.0 do driver, a classe SQLServerConnection tem dois métodos para definir o valor dessa propriedade por meio de programação:
 
* setSendTimeAsDatetime public void (boolean sendTimeAsDateTimeValue)
* public boolean getSendTimeAsDatetime()

Para obter mais informações sobre essa propriedade, consulte [Java.SQL. time configurando como os valores são enviados para o servidor](configuring-how-java-sql-time-values-are-sent-to-the-server.md).

### <a name="configuring-how-string-values-are-sent-to-the-server"></a>Configurar como os valores de cadeia de caracteres são enviados para o servidor
O **sendStringParametersAsUnicode** propriedade de conexão é usada para configurar como os valores de cadeia de caracteres são enviados para o SQL Server. Se definido como true, parâmetros de cadeia de caracteres é enviado para o servidor no formato Unicode. Se definido como false, parâmetros de cadeia de caracteres é enviado em formato não Unicode, como ASCII ou MBCS, em vez de Unicode. O valor padrão desta propriedade é true. Quando sempre criptografado está habilitado e uma coluna char/varchar/varchar(max) é criptografado, o valor de **sendStringParametersAsUnicode** deve ser definida como true (ou ser deixado como o padrão). Se essa propriedade for definida como false, o driver lançará uma exceção ao inserir dados em uma coluna criptografada char/varchar/varchar(max). Para obter mais informações sobre essa propriedade, consulte [definindo as propriedades de Conexão](../../connect/jdbc/setting-the-connection-properties.md).
  
## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>Recuperando e modificando dados em colunas criptografadas
Depois de habilitar o sempre criptografado para consultas de aplicativo, você pode usar APIs padrão do JDBC para recuperar ou modificar dados em colunas de banco de dados criptografado. Se seu aplicativo tem as permissões de banco de dados necessários e pode acessar a chave mestra de coluna, o driver criptografará quaisquer parâmetros de consulta que se destinam a colunas criptografadas e descriptografar dados são recuperados de colunas criptografadas.

Se o Sempre Criptografado não estiver habilitado, as consultas com parâmetros que se destinam a colunas criptografadas falharão. Consultas ainda podem recuperar dados de colunas criptografadas, desde a consulta não tem parâmetros destinam a colunas criptografadas. No entanto, o driver não tentará descriptografar todos os valores recuperados de colunas criptografadas, e o aplicativo receberá dados binários criptografados (como matrizes de bytes).

A tabela a seguir resume o comportamento de consultas dependendo se sempre criptografado está habilitado ou não:

|Característica da consulta | O Sempre Criptografado está habilitado e o aplicativo pode acessar as chaves e os metadados da chave|O Sempre Criptografado está habilitado e o aplicativo não pode acessar as chaves nem os metadados da chave | O Sempre Criptografado está desabilitado|
|:---|:---|:---|:---|
| Consultas com parâmetros que se destinam a colunas criptografadas. | Os valores de parâmetro são criptografados de modo transparente. | Erro | Erro|
| As consultas que recuperam dados de colunas criptografadas sem parâmetros que se destinam a colunas criptografadas.| Os resultados das colunas criptografadas são descriptografados de modo transparente. O aplicativo recebe valores de texto sem formatação dos tipos de dados JDBC correspondentes aos tipos de SQL Server configurados para as colunas criptografadas. | Erro | Os resultados das colunas criptografadas não são descriptografados. O aplicativo recebe valores criptografados como matrizes de bytes (byte[]).

### <a name="inserting-and-retrieving-encrypted-data-examples"></a>Inserir e recuperar os dados criptografados exemplos 
Os exemplos a seguir ilustram como recuperar e modificar dados em colunas criptografadas. Os exemplos assumem que a tabela de destino com o esquema a seguir e as colunas SSN e BirthDate criptografadas. Se você tiver configurado uma chave mestra de coluna denominada "MyCMK" e uma chave de criptografia de coluna chamada "MyCEK" (conforme descrito nas seções anteriores de provedores de armazenamento de chaves), você pode criar a tabela usando esse script:

```
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

Para cada exemplo de código Java, você precisará inserir o código específico do armazenamento de chaves no local indicado.

Se você estiver usando um provedor de armazenamento de chaves do Cofre de chaves do Azure:

```
    String clientID = "<Azure Application ID>";
    String clientKey = "<Azure Application API Key Password>";
    SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
    Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
    keyStoreMap.put(akvProvider.getName(), akvProvider);
    SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
    String connectionString = "jdbc:sqlserver://localhost:1433;databaseName=Clinic;user=sa;password=******;columnEncryptionSetting=Enabled;";
```

Se você estiver usando um provedor de armazenamento de chaves do repositório de certificados do Windows:

```
    String connectionString = "jdbc:sqlserver://localhost:1433;databaseName=Clinic;user=sa;password=******;columnEncryptionSetting=Enabled;";
```

Se você estiver usando um provedor de armazenamento de chaves de armazenamento de chaves Java:

```
    String connectionString = "jdbc:sqlserver://localhost:1433;databaseName=Clinic;user=sa;password=******;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path to jks or pfx file>;keyStoreSecret=<keystore secret/password>";
```

### <a name="inserting-data-example"></a>Inserindo exemplo de dados
Este exemplo insere uma linha na tabela Pacientes. Observe os seguintes itens:
- Não há nada específico de criptografia no código de exemplo. O Microsoft JDBC Driver para SQL Server detecta automaticamente e criptografa os parâmetros que se destinam a colunas criptografadas. Esse comportamento torna a criptografia transparente para o aplicativo.
- Os valores inseridos em colunas de banco de dados, incluindo as colunas criptografadas, são passados como parâmetros usando SQLServerPreparedStatement. Embora o uso de parâmetros é opcional ao enviar valores para colunas não criptografadas (embora, é altamente recomendado, pois ajuda a prevenir a injeção de SQL), é necessário para valores que se destinam a colunas criptografadas. Se os valores inseridos em colunas criptografadas foram passados como literais inseridos na instrução de consulta, a consulta falhará porque o driver não poderá determinar os valores nas colunas criptografadas de destino e não criptografaria os valores. Como resultado, o servidor os rejeitaria como incompatíveis com as colunas criptografadas.
- Todos os valores impressos pelo programa será em texto sem formatação, como o Microsoft JDBC Driver para SQL Server descriptografará de modo transparente os dados recuperados da colunas criptografadas.
- Se você estiver fazendo uma pesquisa usando uma cláusula WHERE, o valor usado na cláusula WHERE precisa para ser passado como um parâmetro para que o driver transparentemente pode criptografá-lo antes de enviá-la para o banco de dados. No exemplo a seguir, o SSN é passado como um parâmetro, mas o sobrenome é passado como um literal como LastName não criptografada.
- O método setter usado para o parâmetro destina à coluna SSN é setString(), que mapeia para o tipo de dados do SQL Server char/varchar. Se, para esse parâmetro, o método setter usado foi setNString(), que é mapeada para nchar/nvarchar, a consulta falhará, pois sempre criptografado não oferece suporte a conversões de valores nchar/nvarchar criptografados em valores char/varchar criptografados.

```
try
{
    <Insert keystore-specific code here>

    Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
    try (Connection sourceConnection = DriverManager.getConnection(connectionString))
    {
        String insertRecord="INSERT INTO [dbo].[Patients] VALUES (?, ?, ?, ?)";
        try (PreparedStatement insertStatement = sourceConnection.prepareStatement(insertRecord))
        {
            insertStatement.setString(1, "795-73-9838");
            insertStatement.setString(2, "Catherine");
            insertStatement.setString(3, "Abel");
            insertStatement.setDate(4, Date.valueOf("1996-09-10"));
            insertStatement.executeUpdate();
            System.out.println("1 record inserted.\n");
        }
    }
}
catch (Exception e)
{
    e.printStackTrace();
}
```

### <a name="retrieving-plaintext-data-example"></a>Recuperando um exemplo de dados de texto sem formatação
O exemplo a seguir demonstra a filtragem de dados com base em valores criptografados e recuperar dados de texto sem formatação de colunas criptografadas. Observe os seguintes itens:
- O valor usado na cláusula WHERE para filtrar a coluna SSN precisa ser passados como um parâmetro para que o Microsoft JDBC Driver para SQL Server pode criptografá-lo transparente antes de enviá-la para o banco de dados.
- Todos os valores impressos pelo programa será em texto sem formatação, como o Microsoft JDBC Driver para SQL Server descriptografará de modo transparente os dados recuperados das colunas SSN e BirthDate.

> [!NOTE]
> Se as colunas são criptografadas usando a criptografia determinística, consultas podem executar comparações de igualdade neles. Para obter mais informações, consulte [criptografia selecionando determinística ou aleatória em sempre criptografados (mecanismo de banco de dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption).

```
try
{
    <Insert keystore-specific code here>

    Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
    try (Connection sourceConnection = DriverManager.getConnection(connectionString))
    {
        String filterRecord="SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN = ?;";
    
        try (PreparedStatement selectStatement = sourceConnection.prepareStatement(filterRecord))
        {
            selectStatement.setString(1, "795-73-9838");
            ResultSet rs = selectStatement.executeQuery();
            while(rs.next())
            {
                System.out.println("SSN: " +rs.getString("SSN") +
                    ", FirstName: " + rs.getString("FirstName") +
                    ", LastName:"+ rs.getString("LastName")+
                    ", Date of Birth: " + rs.getString("BirthDate"));
            }
        }
    }
}
catch (Exception e)  
{  
    e.printStackTrace();  
}
```
  
### <a name="retrieving-encrypted-data-example"></a>Recuperando um exemplo de dados criptografados
Se o Always Encrypted não estiver habilitado, uma consulta ainda poderá recuperar dados de colunas criptografadas, desde que a consulta não tenha parâmetros que se destinam a colunas criptografadas.

O exemplo a seguir ilustra como recuperar dados binários criptografados de colunas criptografadas. Observe os seguintes itens:
- Como o sempre criptografado não está habilitado na cadeia de conexão, a consulta retornará valores criptografados de SSN e BirthDate como matrizes de bytes (o programa converte os valores em cadeias de caracteres).
- Uma consulta que recupera dados de colunas criptografadas com o Sempre Criptografado desabilitado pode ter parâmetros, desde que nenhum dos parâmetros se destinem a uma coluna criptografada. Os seguintes filtros de consulta por LastName, que não são criptografados no banco de dados. Se a consulta filtrar por SSN ou BirthDate, a consulta falhará.

```
try
{
    String connectionString  = "jdbc:sqlserver://localhost:1433;" + "databaseName=Clinic;user=sa;password=******";

    Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
    try (Connection sourceConnection = DriverManager.getConnection(connectionString))
    {
        String filterRecord="SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE LastName = ?;";

        try (PreparedStatement selectStatement = sourceConnection.prepareStatement(filterRecord))
        {
            selectStatement.setString(1, "Abel");
            ResultSet rs = selectStatement.executeQuery();
            while (rs.next())
            {
                System.out.println("SSN: " + rs.getString("SSN") +
                    ", FirstName: " + rs.getString("FirstName") +
                    ", LastName:"+ rs.getString("LastName") +
                    ", Date of Birth: " + rs.getString("BirthDate"));
            }
        }
    }
}
catch (Exception e)
{
    e.printStackTrace();
}
```

### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>Evitando problemas comuns ao consultar colunas criptografadas
Esta seção descreve as categorias de erros comuns ao consultar colunas criptografadas de aplicativos Java e algumas diretrizes sobre como evitá-los.

### <a name="unsupported-data-type-conversion-errors"></a>Erros de conversão de tipo de dados sem suporte
O Always Encrypted dá suporte a algumas conversões de tipos de dados criptografados. Consulte [sempre criptografados (mecanismo de banco de dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) para a lista detalhada de conversões de tipo com suporte. É aqui que você pode fazer para evitar erros de conversão de tipo de dados. Verifique se:

- Você usa os métodos de setter apropriado quando colunas criptografadas, passar valores para parâmetros de destino. Certifique-se de que o tipo de dados do SQL Server do parâmetro é exatamente o mesmo que o tipo da coluna de destino ou uma conversão do tipo de dados do SQL Server do parâmetro para o tipo de destino da coluna é suportada. Métodos da API foram adicionados para as classes SQLServerPreparedStatement e SQLServerCallableStatement SQLServerResultSet passar parâmetros correspondentes aos tipos de dados específicos do SQL Server. Por exemplo, se uma coluna não é criptografada. você pode usar o método setTimestamp() para passar um parâmetro para um datetime2 ou para uma coluna de data e hora. Mas, quando uma coluna é criptografada, será necessário usar o método exato que representa o tipo da coluna no banco de dados. Por exemplo, use setTimestamp() para passar valores para uma coluna criptografada datetime2 e use setDateTime() para passar valores para uma coluna de datetime criptografados. Consulte [sempre criptografados referência da API para o Driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md) para obter uma lista de novas APIs.
- a precisão e escala dos parâmetros que se destinam a colunas dos tipos de dados decimais e numéricos do SQL Server são iguais à precisão e escala configuradas para a coluna de destino. Métodos da API foram adicionados para as classes SQLServerPreparedStatement e SQLServerCallableStatement SQLServerResultSet para aceitar a precisão e escala juntamente com os valores de dados para parâmetros/colunas que representam os tipos de dados decimais e numéricos. Consulte [sempre criptografados referência da API para o Driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md) para obter uma lista completa das APIs novo/sobrecarregado.  
- a precisão ou escala de frações de segundo de parâmetros que se destinam a colunas datetime2, datetimeoffset ou tipos de dados do SQL Server de tempo não é maior do que a precisão ou escala de frações de segundos para a coluna de destino em consultas que modificam os valores da coluna de destino . Métodos da API foram adicionados para as classes SQLServerPreparedStatement e SQLServerCallableStatement SQLServerResultSet para aceitar a precisão ou escala de frações de segundo juntamente com os valores de dados para parâmetros que representam esses tipos de dados. Para obter uma lista completa de novo/sobrecarregado APIs, consulte [sempre criptografados referência da API para o Driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).   

### <a name="errors-due-to-incorrect-connection-properties"></a>Erros devido a propriedades de conexão incorreta
Esta seção descreve como definir as configurações de conexão corretamente para usar dados de sempre criptografado. Como tipos de dados criptografados oferecem suporte a conversões limitadas, o **sendTimeAsDatetime** e **sendStringParametersAsUnicode** configurações de conexão precisam de configuração apropriada ao usar colunas criptografadas. Verifique se: 
- [sendTimeAsDatetime](setting-the-connection-properties.md) configuração de conexão é definida como false quando inserindo dados em colunas de hora criptografadas. Para obter mais informações, consulte [configurando como os valores são enviados para o servidor](configuring-how-java-sql-time-values-are-sent-to-the-server.md).
- [sendStringParametersAsUnicode](setting-the-connection-properties.md) configuração de conexão está definida como true (ou será deixada como o padrão) quando inserindo dados em colunas criptografadas, char/varchar/varchar(max).

### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>Erros devido à passagem de texto sem formatação em vez de valores criptografados
Qualquer valor que se destina a uma coluna criptografada precisa ser criptografado no aplicativo. Uma tentativa de inserir/modificar ou filtrar por um valor de texto sem formatação em uma coluna criptografada resultará em um erro semelhante a esta:

```
com.microsoft.sqlserver.jdbc.SQLServerException: Operand type clash: varchar is incompatible with varchar(8000) encrypted with (encryption_type = 'DETERMINISTIC', encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'MyCEK', column_encryption_key_database_name = 'ae') collation_name = 'SQL_Latin1_General_CP1_CI_AS'
```

Para evitar esses tipos de erros, garanta que:
- sempre criptografado está habilitado para consultas de aplicativo direcionamento colunas criptografadas (para a cadeia de caracteres de conexão ou para uma consulta específica).
- use as instruções preparadas e parâmetros para enviar dados de direcionamento a colunas criptografadas. O exemplo a seguir mostra uma consulta que filtra incorretamente por uma literal ou uma constante em uma coluna criptografada (SSN), em vez de passar o literal em como um parâmetro. Essa consulta falhará:

```
ResultSet rs = connection.createStatement().executeQuery("SELECT * FROM Customers WHERE SSN='795-73-9838'");
```

## <a name="force-encryption-on-input-parameters"></a>Forçar a criptografia em parâmetros de entrada
O recurso de Forçar criptografia impõe a criptografia de um parâmetro ao usar sempre criptografado. Se Forçar criptografia for usada e SQL Server informar o driver que o parâmetro não precisam ser criptografados, a consulta usando o parâmetro falhará. Essa propriedade fornece proteção adicional contra ataques de segurança que envolvem um SQL Server comprometido fornecendo metadados de criptografia incorretos ao cliente, o que pode levar à divulgação de dados. Os métodos em classes SQLServerPreparedStatement e SQLServerCallableStatement e a atualização de conjunto *\* métodos na classe SQLServerResultSet estão sobrecarregados para aceitar um argumento booliano para especificar as configurações de criptografia de força. Se o valor desse argumento for false, o driver não forçará a criptografia em parâmetros. Se Forçar criptografia for definida como true, a consulta de parâmetro é enviado apenas se a coluna de destino está criptografada e sempre criptografado está habilitado, a conexão ou a instrução. Usar esta propriedade fornece uma camada extra de segurança, garantindo que o driver não por engano envia dados para o SQL Server como texto sem formatação quando se espera que sejam criptografados.

Para obter mais informações sobre os métodos SQLServerPreparedStatement e SQLServerCallableStatement que estão sobrecarregados com a configuração de criptografia de força, consulte [sempre criptografados referência da API para o Driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)  

## <a name="controlling-the-performance-impact-of-always-encrypted"></a>Controlando o impacto no desempenho do sempre criptografado
Como sempre criptografado é uma tecnologia de criptografia do lado do cliente, a maioria da sobrecarga de desempenho é observada no lado do cliente, não no banco de dados. O custo das operações de criptografia e descriptografia, além de outras fontes de sobrecarga de desempenho no lado do cliente são:
- Viagens de ida e volta adicionais ao banco de dados para recuperar metadados dos parâmetros de consulta.
- Chamadas a um repositório de chaves mestras de coluna para acessar uma chave mestra de coluna.

Esta seção descreve as otimizações de desempenho internas no Microsoft JDBC Driver para SQL Server e como você pode controlar o impacto de dois fatores acima no desempenho.

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>Controlando as viagens de ida e volta para recuperar metadados dos parâmetros de consulta
Se o sempre criptografado está habilitado para uma conexão, por padrão o driver chamará [sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) para cada consulta parametrizada, passando a instrução de consulta (sem nenhum valor de parâmetro) para o SQL Server. [sys. sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) analisa a instrução de consulta para descobrir se os parâmetros precisam ser criptografados e nesse caso, para cada um retorne as informações relacionadas à criptografia que permitirão ao driver criptografar valores de parâmetro. Esse comportamento garante um alto nível de transparência para o aplicativo cliente. Como o aplicativo usa parâmetros para passar valores que se destinam a colunas criptografadas para o driver, o aplicativo (e o desenvolvedor do aplicativo) não precisa saber quais consultas acessam colunas criptografadas.

### <a name="setting-always-encrypted-at-the-query-level"></a>Configurando o Always Encrypted no nível da consulta
Para controlar o impacto no desempenho de recuperação de metadados de criptografia para consultas parametrizadas, você pode habilitar o sempre criptografado para consultas individuais em vez de configurá-lo para a conexão. Dessa forma, você pode garantir que sp_describe_parameter_encryption é invocada apenas para consultas que você sabe que têm parâmetros que se destinam a colunas criptografadas. No entanto, observe que ao fazer isso, você reduzirá a transparência da criptografia: se você alterar as propriedades de criptografia de suas colunas de banco de dados, talvez seja necessário alterar o código do seu aplicativo para alinhá-lo com as alterações de esquema.

Para controlar o comportamento do sempre criptografado de consultas individuais, você precisa configurar objetos de instrução individual passando um Enum, SQLServerStatementColumnEncryptionSetting, que especifica como os dados serão enviados e recebidos durante a leitura e gravação colunas criptografadas para essa instrução específica. Veja algumas diretrizes úteis:
- Se a maioria das consultas que um aplicativo cliente envia por uma conexão de banco de dados acessa colunas criptografadas, use estas diretrizes:
    - Definir o **columnEncryptionSetting** palavra-chave de cadeia de caracteres de conexão para **habilitado**.
    - Defina SQLServerStatementColumnEncryptionSetting.Disabled para consultas individuais que não acessam colunas criptografadas. Essa configuração desabilitará a chamada sp_describe_parameter_encryption, bem como uma tentativa de descriptografar todos os valores no conjunto de resultados.
    - Defina SQLServerStatementColumnEncryptionSetting.ResultSet para consultas individuais que não têm qualquer parâmetro que exija criptografia, mas que recuperam dados de colunas criptografadas. Essa configuração desativará chamar sp_describe_parameter_encryption e a criptografia de parâmetros. A consulta poderá descriptografar os resultados das colunas de criptografia.
- Se a maioria das consultas que um aplicativo cliente envia por uma conexão de banco de dados não acessa colunas criptografadas, use estas diretrizes:
    - Definir o **columnEncryptionSetting** palavra-chave de cadeia de caracteres de conexão para **desabilitado**.
    - Defina SQLServerStatementColumnEncryptionSetting.Enabled para consultas individuais que têm parâmetros que precisam ser criptografados. Essa configuração permitirá que chamar sp_describe_parameter_encryption como a descriptografia dos resultados de consulta recuperados de colunas criptografadas.
    - Defina SQLServerStatementColumnEncryptionSetting.ResultSet para consultas que não têm qualquer parâmetro que exija criptografia, mas recuperam dados de colunas criptografadas. Essa configuração desativará chamar sp_describe_parameter_encryption e a criptografia de parâmetros. A consulta poderá descriptografar os resultados das colunas de criptografia.

As configurações de SQLServerStatementColumnEncryptionSetting não podem ser usadas para ignorar a criptografia e obter acesso aos dados de texto sem formatação. Para obter mais informações sobre como configurar a criptografia de coluna em uma instrução, consulte [sempre criptografados referência da API para o Driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).  

No exemplo a seguir, sempre criptografado está desabilitado para a conexão de banco de dados. A consulta emitida pelo aplicativo tem um parâmetro que se destina à coluna LastName não criptografada. A consulta recupera dados das colunas SSN e BirthDate que são criptografadas. Nesse caso, a chamada a sys.sp_describe_parameter_encryption para recuperar os metadados de criptografia não é necessária. No entanto, a descriptografia dos resultados da consulta precisa ser habilitado para que o aplicativo possa receber valores de texto sem formatação das duas colunas criptografadas. A configuração SQLServerStatementColumnEncryptionSetting.ResultSet é usada para garantir que.

```
// Assumes the same table definition as in Section "Retrieving and modifying data in encrypted columns"
// where only SSN and BirthDate columns are encrypted in the database.
String connectionUrl = "jdbc:sqlserver://localhost;databaseName=ae;user=sa;password=******;"
        + "keyStoreAuthentication=JavaKeyStorePassword;"
        + "keyStoreLocation=" + keyStoreLocation + ";"
        + "keyStoreSecret=******;";
SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionString);

String filterRecord="SELECT FirstName, LastName, SSN, BirthDate FROM " + tblName + " WHERE LastName = ?";
PreparedStatement selectStatement = connection.prepareStatement(
        filterRecord,
        ResultSet.TYPE_FORWARD_ONLY,
        ResultSet.CONCUR_READ_ONLY,
        connection.getHoldability(),
        SQLServerStatementColumnEncryptionSetting.ResultSetOnly);
selectStatement.setString(1, "Abel");
ResultSet rs = selectStatement.executeQuery();
while(rs.next()) {
    System.out.println("First name: " + rs.getString("FirstName"));
    System.out.println("Last name: " + rs.getString("LastName"));
    System.out.println("SSN: " + rs.getString("SSN"));
    System.out.println("Date of Birth: " + rs.getDate("BirthDate"));
}
rs.close();
selectStatement.close();
connection.close();
```

### <a name="column-encryption-key-caching"></a>Cache de chaves de criptografia de coluna
Para reduzir o número de chamadas para um repositório de chaves mestras de coluna para descriptografar as chaves de criptografia de coluna, o Microsoft JDBC Driver para SQL Server armazena em cache as chaves de criptografia de coluna de texto sem formatação na memória. Depois de receber o valor de chave de criptografia de coluna criptografado dos metadados de banco de dados, o driver primeiro tenta encontrar a chave de criptografia de coluna de texto sem formatação correspondente ao valor de chave criptografado. O driver chama o armazenamento de chaves que contém a chave mestra de coluna apenas se ele não é possível localizar o valor de chave de criptografia de coluna criptografada no cache.

Você pode configurar um valor de tempo de vida para as entradas de chave de criptografia de coluna no cache usando a API, setColumnEncryptionKeyCacheTtl(), na classe SQLServerConnection. O valor de tempo de vida padrão para as entradas de chave de criptografia de coluna no cache é duas horas. Para desativar o cache, use um valor de 0. Para definir qualquer valor de tempo de vida, use a seguinte API:

```
SQLServerConnection.setColumnEncryptionKeyCacheTtl (int columnEncryptionKeyCacheTTL, TimeUnit unit)
```

Por exemplo, para definir um valor de tempo de vida de 10 minutos, use:

```
SQLServerConnection.setColumnEncryptionKeyCacheTtl (10, TimeUnit.MINUTES)
```

Somente dias, horas, minutos ou segundos têm suporte como a unidade de tempo.  

## <a name="copying-encrypted-data-using-sqlserverbulkcopy"></a>Copiando dados criptografados usando SQLServerBulkCopy
Com SQLServerBulkCopy, você pode copiar os dados que já estão criptografados e armazenados em uma tabela para outra tabela sem descriptografá-los. Para fazer isso:

- Verifique se a configuração de criptografia da tabela de destino é idêntica à configuração da tabela de origem. Em particular, ambas as tabelas devem ter as mesmas colunas criptografadas, e as colunas devem ser criptografadas usando os mesmos tipos de criptografia e as mesmas chaves de criptografia. Se qualquer coluna de destino for criptografada diferente da coluna de origem correspondente, você não poderá descriptografar os dados na tabela de destino após a operação de cópia. Os dados serão corrompidos.
- Configure as conexões de banco de dados para a tabela de origem e a tabela de destino sem habilitado para sempre criptografado.
- Defina a opção allowEncryptedValueModifications. Para obter mais informações, consulte [usando cópia em massa com o Driver JDBC](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md).

> [!NOTE]
> Tenha cuidado ao especificar AllowEncryptedValueModifications como essa opção pode levar à corrupção de banco de dados porque o Microsoft JDBC Driver para SQL Server não verifica se os dados estão realmente criptografados ou se foram corretamente criptografado usando a mesma criptografia tipo de algoritmo e chave como a coluna de destino.

## <a name="see-also"></a>Consulte também
[Always Encrypted (mecanismo de banco de dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)
