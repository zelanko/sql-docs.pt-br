---
title: Notas de versão para o JDBC Driver | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 074f211e-984a-4b76-bb15-ee36f5946f12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f24089803b59e86a4fc8f8b98cd7822a11ba6c2e
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51600767"
---
# <a name="release-notes-for-the-jdbc-driver"></a>Notas de versão do JDBC Driver

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

## <a name="updates-in-microsoft-jdbc-driver-70-for-sql-server"></a>Atualizações no Microsoft JDBC Driver 7.0 for SQL Server

O Microsoft JDBC Driver 7.0 para SQL Server é totalmente compatível com a especificação de API do JDBC 4.2. Os jars no pacote 7.0 são nomeados de acordo com a compatibilidade de versão de Java. Por exemplo, o arquivo de mssql-jdbc-7.0.0.jre10.jar do pacote 7.0 deve ser usado com o Java 10.

### <a name="support-for-jdk-10"></a>Suporte para JDK 10

O Microsoft JDBC Driver 7.0 para SQL Server agora é compatível com o Java Development Kit (JDK) versão 10.0, além de JDK 1.8. Essa atualização também expõe do driver 'automático-Module-Name' como `com.microsoft.sqlserver.jdbc` por meio de seu arquivo de manifesto.

### <a name="support-for-spatial-datatypes"></a>Suporte para tipos de dados espaciais

O Microsoft JDBC Driver 7.0 para SQL Server agora fornece suporte para tipos de dados espaciais 'Geography' do SQL Server e 'Geometry'. Para obter mais informações sobre tipos de dados espaciais APIs e como usá-los, consulte [aqui](../../connect/jdbc/use-spatial-datatypes.md).

### <a name="implementation-for-jdbc-43-introduced-javasqlconnection-apis-beginrequest-and-endrequest"></a>A implementação para JDBC 4.3 introduziu as APIs beginRequest() e endRequest() do java.sql.Connection.

O Microsoft JDBC Driver 7.0 para SQL Server agora implementa `beginRequest()` e `endRequest()` APIs de `java.sql.Connection` classe. Essas APIs foram introduzidas com JDBC 4.3 especificações e JDK 9. Para obter mais informações sobre a implementação do driver dessas APIs, consulte [aqui](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md).

### <a name="support-for-sql-data-discovery-and-classification"></a>Suporte para "descoberta e classificação de dados SQL"

O Microsoft JDBC Driver 7.0 para o SQL Server fornece suporte para o recurso 'descoberta de dados SQL e classificação' com qualquer banco de dados de destino que dá suporte a esse recurso. O driver agora expõe `SQLServerResultSet.getSensitivityClassification()` APIs para extrair essas informações de conjunto de resultados de buscado.

Para obter mais informações sobre como usar esse recurso com o Driver JDBC, consulte a amostra [aqui](../../connect/jdbc/data-discovery-classification-sample.md).

### <a name="added-new-connection-property-usebulkcopyforbatchinsert"></a>Adicionada nova propriedade de conexão: useBulkCopyForBatchInsert

O Microsoft JDBC Driver 7.0 para SQL Server apresenta uma nova propriedade de conexão, 'useBulkCopyForBatchInsert', que tem suporte apenas para **Data Warehouse do Azure**.

Esta propriedade é **desabilitada** por padrão e pode ser habilitado para aumentar o desempenho de aplicativos de usuário ao enviar grandes valores de dados de Data warehouse do Azure. Habilitar essa propriedade altera o comportamento das operações de inserção em lotes para alternar para operações de cópia em massa com dados de fornecida pelo usuário. Para obter mais informações sobre essa propriedade e suas limitações, consulte [aqui](../../connect/jdbc/use-bulk-copy-api-batch-insert-operation.md).

### <a name="added-new-connection-property-cancelquerytimeout"></a>Adicionada nova propriedade de conexão: cancelQueryTimeout

Microsoft JDBC Driver 7.0 para SQL Server apresenta a nova propriedade de conexão `cancelQueryTimeout`, para cancelar `queryTimeout` nos `java.sql.Connection` e `java.sql.Statement` objetos.

### <a name="added-azure-key-vault-provider-constructors"></a>Construtores de provedor do Cofre de chaves do Azure adicionada

O Microsoft JDBC Driver 7.0 para SQL Server reintroduz um construtor removido anteriormente, para `SQLServerColumnEncryptionAzureKeyVaultProvider`, quais autenticação permitidos usando um método personalizado implementado no `SQLServerKeyVaultAuthenticationCallback` para buscar um token de acesso.

Novos construtores têm o abaixo da definição:

```java
/* This constructor is added to provide backwards compatibility with 6.0
* version of the driver. It is marked deprecated for removal in next
* stable release.
*/
@Deprecated
public SQLServerColumnEncryptionAzureKeyVaultProvider(
        SQLServerKeyVaultAuthenticationCallback authenticationCallback,
        ExecutorService executorService) throws SQLServerException;

/*New Constructor to replace the above constructor*/
public SQLServerColumnEncryptionAzureKeyVaultProvider(
            SQLServerKeyVaultAuthenticationCallback authenticationCallback) throws SQLServerException;
```

### <a name="updated-adal4j-version-to-160"></a>Versão atualizada do ADAL4J para 1.6.0

O Microsoft JDBC Driver 7.0 para o SQL Server tiver atualizado sua dependência do maven no azure-activedirectory-library-for-java (ADAL4J) para a versão 1.6.0. Saiba mais sobre [dependências](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md).

## <a name="updates-in-microsoft-jdbc-driver-64-for-sql-server"></a>Atualizações no Microsoft JDBC Driver 6.4 for SQL Server

O Microsoft JDBC Driver 6.4 para SQL Server é totalmente compatível com as especificações do JDBC 4.1 e 4.2. Os jars no pacote de 6,4 são nomeados de acordo com a compatibilidade de versão de Java. Por exemplo, o arquivo de mssql-jdbc-6.4.0.jre8.jar do pacote de 6,4 deve ser usado com o Java 8.

### <a name="support-for-jdk-9"></a>Suporte para JDK 9

Suporte para JDK (Java Development Kit) versão 9.0, além de JDK 8.0 e 7.0.

### <a name="jdbc-43-compliance"></a>Conformidade do JDBC 4.3

Suporte para a especificação da API do Java Database Connectivity 4.3, além de 4.1 e 4.2. Os métodos da API do JDBC 4.3 são adicionados, mas ainda não implementados. Para obter detalhes, veja [Conformidade do JDBC 4.3 com o JDBC Driver](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md).

### <a name="added-new-connection-property-sslprotocol"></a>Adicionada nova propriedade de conexão: sslProtocol

Adicionada uma nova propriedade de conexão que permite aos usuários especificar a palavra-chave de protocolo TLS. Os valores possíveis são: "TLS", "TLSv1", "TLSv1.1", "TLSv1.2". Ver [SSLProtocol](https://github.com/Microsoft/mssql-jdbc/wiki/SSLProtocol) para obter detalhes.

### <a name="deprecated-connection-property-fipsprovider"></a>Preterido de propriedade de conexão: fipsProvider

A propriedade de Conexão "fipsProvider" é removida da lista de propriedades de conexão aceitos. Consulte os detalhes [aqui](https://github.com/Microsoft/mssql-jdbc/pull/460).

### <a name="added-connection-properties-for-specifying-custom-trustmanager"></a>Propriedades de conexão adicional para especificação de TrustManager personalizado

Driver agora dá suporte à especificação de TrustManager personalizado com adicionado "trustManagerClass" e "trustManagerConstructorArg" propriedades de conexão. Isso permite a especificação dinâmica de um conjunto de certificados confiáveis em uma base por conexão sem modificar as configurações globais para o ambiente da JVM.

### <a name="added-support-for-datetimesmalldatetime-in-table-valued-parameters-tvp"></a>Adicionado suporte para datetime/smallDatetime em parâmetros com valor de tabela (TVP)

O driver agora tem suporte para os dataTypes DATETIME e SMALLDATETIME ao usar TVP (Parâmetros com Valor de Tabela).

### <a name="added-support-for-sqlvariant-datatype"></a>Adicionado suporte para o tipo de dados sql_variant

O Driver JDBC agora oferece suporte a tipos de dados sql_variant a ser usado com o SQL Server. Sql_variant também tem suporte com recursos como parâmetros com valor de tabela (TVP) e BulkCopy com abaixo limitações:

1. Para valores de data: ao usar TVP para popular uma tabela que contém os valores datetime/smalldatetime/date armazenados na coluna sql_variant, chamar métodos de getDateTime()/getSmallDateTime()/getDate() em resultset não funciona e gera a seguinte exceção: `java java.lang.String cannot be cast to java.sql.Timestamp`
    Solução alternativa: use os métodos "getString()" ou "getObject()".

2. Uso de TVP com SQL Variant para valores nulos

Se você estiver usando um TVP para popular uma tabela e enviar o valor NULL para o tipo de coluna sql_variant, encontrará uma exceção, como inserção valor NULL com tipo de coluna sql_variant no TVP não é suportado atualmente.

### <a name="implemented-prepared-statement-metadata-caching"></a>Implementado instrução preparada Caching de metadados

O Driver JDBC tiver implementado o cache de metadados de instrução preparada para melhorar o desempenho. Driver agora dá suporte a cache de metadados de instrução preparada no driver com as propriedades de conexão de "disableStatementPooling" e "statementPoolingCacheSize". Por padrão, esse recurso está desabilitado. Encontre mais informações [aqui](../../connect/jdbc/prepared-statement-metadata-caching-for-the-jdbc-driver.md)

### <a name="added-support-for-aad-integrated-authentication-on-linuxmac"></a>Adicionado suporte para a autenticação integrada do AAD no Linux/Mac

O JDBC Driver agora também é compatível com a Autenticação Integrada do Azure Active Directory em todos os sistemas operacionais compatíveis (Linux/Windows/Mac) com Kerberos. Como alternativa, em sistemas de operacionais do Windows, os usuários possam autenticar com sqljdbc_auth.

### <a name="updated-adal4j-version-to-140"></a>Versão atualizada do ADAL4J para 1.4.0

O Driver JDBC atualizou sua dependência do maven no azure-activedirectory-library-for-java (ADAL4J) para a versão 1.4.0. Para saber mais sobre dependências, veja [aqui](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)

## <a name="updates-in-microsoft-jdbc-driver-62-for-sql-server"></a>Atualizações no Microsoft JDBC Driver 6.2 for SQL Server

O Microsoft JDBC Driver 6.2 para SQL Server é totalmente compatível com as especificações do JDBC 4.1 e 4.2. Os jars no pacote 6.2 são nomeados de acordo com a compatibilidade de versão de Java. Por exemplo, o arquivo mssql-jdbc-6.2.2.jre8.jar do pacote 6.2 é recomendado a ser usado com o Java 8.

> [!NOTE]  
> Um problema com o aperfeiçoamento de cache de metadados foi encontrado na RTW do 6.2 JDBC lançado em 29 de junho de 2017. A melhoria foi revertida e jars novo (versão 6.2.1) foram lançadas em 17 de julho de 2017. 
>
> Outro aprimoramento para atualizar a versão de biblioteca dependente do Azure Key Vault para 1.0.0 foi feito, e os jars novo (versão 6.2.2) foram lançadas em 19 de outubro de 2017.
>
> Baixar as atualizações mais recentes no JDBC Driver 6.2 na [Microsoft Download Center](https://go.microsoft.com/fwlink/?linkid=852460), [GitHub](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2), e [Central do Maven](https://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.sqlserver%22%20AND%20a%3A%22mssql-jdbc%22). Atualize seus projetos para usar o 6.2.2 jars de versão. Veja as notas de versão para [v6.2.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1) e [v6.2.2](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2) para obter mais detalhes.

### <a name="azure-active-directory-aad-support-for-linux"></a>Suporte do Azure Active Directory (AAD) para Linux

Conecte seus aplicativos do Linux para o banco de dados do SQL Azure usando a autenticação do AAD por meio de métodos de token de acesso e o nome de usuário e senha.

### <a name="federal-information-processing-standard-fips-enabled-jvms"></a>Federal FIPS Information Processing Standard () habilitada JVMs

O Driver JDBC agora pode ser usado em JVMs que são executados no modo de conformidade FIPS 140 para atender aos padrões federais e a conformidade.

### <a name="kerberos-authentication-improvements"></a>Melhorias de autenticação do Kerberos

O Driver JDBC agora tem suporte para:

- Método de entidade de segurança/senha para aplicativos em que a configuração do Kerberos não pode ser modificado ou não é possível recuperar um novo token ou keytab. Esse método pode ser usado para autenticar para um SQL Server que permite somente a autenticação Kerberos.
- Autenticação entre realms usando a autenticação integrada do Kerberos sem definir explicitamente o SPN do servidor. O driver agora computará automaticamente o REALM, mesmo quando ele ainda não foi fornecido.
- Delegação restrita de Kerberos, aceitando representada as credenciais do usuário como um objeto de credencial GSS por meio da fonte de dados. Essa credencial representada, em seguida, é usada para estabelecer uma conexão Kerberos.

### <a name="added-timeouts"></a>Tempos limite adicionado

O Driver JDBC agora oferece suporte a configurável limite a seguir que você pode alterar com base nas necessidades do seu aplicativo:

- Tempo limite da consulta para controlar o número de segundos a aguardar antes que um tempo limite ocorra quando a execução de uma consulta.
- Tempo limite de soquete para especificar o número de milissegundos de espera antes que ocorra um tempo limite em um soquete de leitura ou aceitar.

## <a name="updates-in-microsoft-jdbc-driver-61-for-sql-server"></a>Atualizações no Microsoft JDBC Driver 6.1 for SQL Server

O 6.1 do Microsoft JDBC Driver para SQL Server é totalmente compatível com as especificações do JDBC 4.1 e 4.2. Essa é a versão inicial do código-fonte aberto do Driver JDBC e contém os arquivos de mssql-jdbc-6.1.0.jre7.jar mssql-jdbc-6.1.0.jre8.jar, que correspondem à compatibilidade de versão de Java.

## <a name="updates-in-microsoft-jdbc-driver-60-for-sql-server"></a>Atualizações no Microsoft JDBC Driver 6.0 for SQL Server

O Microsoft JDBC Driver 6.0 para SQL Server é totalmente compatível com as especificações do JDBC 4.1 e 4.2. Os jars no pacote 6.0 são nomeados de acordo com sua conformidade com a versão de API do JDBC. Por exemplo, o arquivo sqljdbc42.jar do pacote 6.0 é compatível com JDBC API 4.2. Da mesma forma, o arquivo de sqljdbc41.jar está em conformidade com a API do JDBC 4.1.

Para garantir que você tem o sqljdbc41.jar ou sqljdbc42.jar à direita, execute as seguintes linhas de código. Se a saída é "versão do Driver: 6.0.7507.100", você tem o pacote do JDBC Driver 6.0.

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="always-encrypted"></a>Always Encrypted

Suporte para o recurso recém-lançado Always Encrypted no SQL Server 2016, um novo recurso de segurança que garante que os dados confidenciais nunca sejam vistos em texto não criptografado em uma instância do SQL Server. O Always Encrypted funciona por criptografia transparente de dados no aplicativo, de forma que o SQL Server apenas manipulará os dados criptografados e os valores do texto não criptografado. Mesmo se a instância do SQL ou o computador host estiverem comprometidos, tudo que um invasor poderá obter será texto cifrado de dados confidenciais. Para obter detalhes, veja [Uso de Always Encrypted com o driver JDBC em Linux](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md).

### <a name="internationalized-domain-name-idn"></a>Nome de domínio internacionalizado (IDN)

Suporte para nomes de domínio internacionalizados (IDNs) para nomes de servidor. Para detalhes, consulte usando nomes de domínio internacionais sobre o [recursos internacionais do JDBC Driver](../../connect/jdbc/international-features-of-the-jdbc-driver.md) página.

### <a name="parameterized-query"></a>Consulta parametrizada

Agora dá suporte para recuperar metadados de parâmetro com instruções preparadas para consultas complexas, como subconsultas e/ou junções. Observe que essa melhoria estará disponível somente ao usar o SQL Server 2012 e versões mais recentes.

### <a name="azure-active-directory-aad"></a>AAD (Azure Active Directory)

Autenticação do AAD é um mecanismo para se conectar ao banco de dados SQL v12 usando identidades no AAD. Use a autenticação do AAD para gerenciar centralmente as identidades de usuários do banco de dados e como uma alternativa à autenticação do SQL Server. O JDBC Driver 6.0 permite que você especifique suas credenciais do AAD na cadeia de conexão JDBC para se conectar ao BD SQL do Azure. Para obter detalhes, consulte a propriedade de autenticação sobre o [definindo as propriedades de Conexão](../../connect/jdbc/setting-the-connection-properties.md) página.

### <a name="table-valued-parameters"></a>Parâmetros com valor de tabela

Os parâmetros com valor de tabela fornecem uma maneira fácil de realizar marshaling em várias linhas de dados de um aplicativo cliente do SQL Server sem exigir várias viagens de ida e volta ou uma lógica especial do lado do servidor para processar os dados. Você pode usar parâmetros com valor de tabela para encapsular linhas de dados em um aplicativo cliente e enviar os dados para o servidor em um único comando parametrizado. As linhas de dados de entrada são armazenadas em uma variável de tabela que pode ser operada usando o Transact-SQL. Para obter detalhes, consulte [Using Table-Valued parâmetros](../../connect/jdbc/using-table-valued-parameters.md).

### <a name="alwayson-availability-groups-ag"></a>AG (Grupos de Disponibilidade) AlwaysOn

O driver agora dá suporte a conexões transparentes para grupos de disponibilidade AlwaysOn. O driver descobre rapidamente a topologia AlwaysOn atual de sua infraestrutura de servidor e se conecta ao servidor ativo atual de maneira transparente.

## <a name="updates-in-microsoft-jdbc-driver-42-for-sql-server-and-later"></a>Atualizações do Microsoft JDBC Driver 4.2 e posterior para SQL Server

O Microsoft JDBC Driver 4.2 para SQL Server é totalmente compatível com as especificações do JDBC 4.1 e 4.2. Os jars no pacote 4.2 são nomeados de acordo com sua conformidade com a versão de API do JDBC. Por exemplo, o arquivo sqljdbc42.jar do pacote 4.2 é compatível com JDBC API 4.2. Da mesma forma, o arquivo de sqljdbc41.jar está em conformidade com a API do JDBC 4.1.

Para garantir que você tem o sqljdbc41.jar ou sqljdbc42.jar à direita, execute as seguintes linhas de código. Se a saída é "versão do Driver: 4.2.6420.100", você tem o pacote do JDBC Driver 4.2.

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="support-for-jdk-8"></a>Suporte para JDK 8

Suporte para JDK (Java Development Kit) versão 8.0, além de JDK 7.0, 6.0 e 5.0.

### <a name="jdbc-41-and-42-compliance"></a>Conformidade do JDBC 4.1 e 4.2

Suporte para especificações de API do Java Database Connectivity 4.1 e 4.2, além do 4.0. Para obter detalhes, consulte [conformidade JDBC 4.1 para o Driver JDBC](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md) e [conformidade do JDBC 4.2 para o JDBC Driver](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md).

### <a name="bulk-copy"></a>Cópia em massa

O recurso de cópia em massa é usado para copiar rapidamente grandes quantidades de dados em tabelas ou exibições em bancos de dados do SQL Server. Para obter detalhes, veja [Como usar a cópia em massa com o JDBC Driver](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md).

### <a name="xa-transaction-rollback-option"></a>Opção de reversão de transação XA

Novas opções de tempo limite adicionadas para reversão automática existente de transações não preparadas. Para obter detalhes, consulte [Noções básicas sobre transações de XA](../../connect/jdbc/understanding-xa-transactions.md).

### <a name="new-kerberos-principal-connection-property"></a>Nova propriedade de conexão principal Kerberos

Uma nova propriedade de conexão foi adicionada para facilitar a flexibilidade com conexões de Kerberos. Para obter detalhes, veja [Como usar a autenticação integrada do Kerberos para se conectar ao SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md).

## <a name="updates-in-microsoft-jdbc-driver-41-for-sql-server-and-later"></a>Atualizações do Microsoft JDBC Driver 4.1 e posterior para SQL Server

### <a name="support-for-jdk-7"></a>Suporte para JDK 7

Suporte para JDK (Java Development Kit) versão 7.0, além de JDK 6.0 e 5.0.

## <a name="itanium-not-supported-for-jdbc-driver-64-60-42-and-41-applications"></a>Aplicativos JDBC Driver 6.4, 6.0, 4.2 e 4.1 não são compatíveis com Itanium

Não há suporte para execução de aplicativos Microsoft JDBC Drivers 6.4, 6.0, 4.2 e 4.1 for SQL Server em um computador Itanium.

## <a name="see-also"></a>Consulte Também

[Visão geral do JDBC Driver](../../connect/jdbc/overview-of-the-jdbc-driver.md)
