---
title: Notas de versão para o JDBC Driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 074f211e-984a-4b76-bb15-ee36f5946f12
caps.latest.revision: 206
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1ec71defcba0a6f122d3c3ff9a098e163f07079c
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38021110"
---
# <a name="release-notes-for-the-jdbc-driver"></a>Notas de versão do JDBC Driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

## <a name="updates-in-microsoft-jdbc-driver-64-for-sql-server"></a>Atualizações no Microsoft JDBC Driver 6.4 for SQL Server
O Microsoft JDBC Driver 6.4 para SQL Server é totalmente compatível com as especificações do JDBC 4.1 e 4.2. Os jars contidos no pacote 6,4 são nomeados de acordo com a compatibilidade de versão de Java. Por exemplo, o arquivo mssql-jdbc-6.4.0.jre8.jar do pacote de 6,4 é recomendado a ser usado com o Java 8. 

**Suporte para JDK 9**  
  
Suporte para JDK (Java Development Kit) versão 9.0, além de JDK 8.0 e 7.0.
  
**Conformidade do JDBC 4.3**  
  
Suporte para a especificação da API do Java Database Connectivity 4.3, além de 4.1 e 4.2. Os métodos da API do JDBC 4.3 são adicionados, mas ainda não implementados. Para obter detalhes, consulte [conformidade do JDBC 4.3 para o JDBC Driver](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md).
 
**Adicionada nova propriedade de conexão: sslProtocol**

Adicionada uma nova propriedade de conexão que permite aos usuários especificar a palavra-chave de protocolo TLS. Os valores possíveis são: "TLS", "TLSv1", "TLSv1.1", "TLSv1.2". Ver [SSLProtocol](https://github.com/Microsoft/mssql-jdbc/wiki/SSLProtocol) para obter detalhes.

**Preterido de propriedade de conexão: fipsProvider**

A propriedade de Conexão "fipsProvider" é removida da lista de propriedades de conexão aceitos. Consulte os detalhes [aqui](https://github.com/Microsoft/mssql-jdbc/pull/460).

**Propriedades de conexão adicional para especificação de TrustManager personalizado**

Driver agora dá suporte à especificação de TrustManager personalizado com adicionado "trustManagerClass" e "trustManagerConstructorArg" propriedades de conexão. Isso permite a especificação dinâmica de um conjunto de certificados confiáveis em uma base por conexão sem modificar as configurações globais para o ambiente da JVM.

**Adicionado suporte para datetime/smallDatetime em parâmetros com valor de tabela (TVP)**

O driver agora tem suporte para os dataTypes DATETIME e SMALLDATETIME ao usar TVP (Parâmetros com Valor de Tabela).

**Adicionado suporte para o tipo de dados sql_variant**

O Driver JDBC agora oferece suporte a tipos de dados sql_variant a ser usado com o SQL Server. Sql_variant também tem suporte com recursos como parâmetros com valor de tabela (TVP) e BulkCopy com abaixo limitações:

1. Para valores de data: ao usar TVP para popular uma tabela que contém os valores datetime/smalldatetime/date armazenados na coluna sql_variant, chamar métodos de getDateTime()/getSmallDateTime()/getDate() em resultset não funciona e gera a seguinte exceção:
    ```
    java.lang.String cannot be cast to java.sql.Timestamp
    ```
    Solução alternativa: use os métodos "getString()" ou "getObject()".

2. Uso de TVP com SQL Variant para valores nulos

Se você estiver usando um TVP para popular uma tabela e enviar o valor NULL para o tipo de coluna sql_variant, você encontrará uma exceção ao Inserir valor NULL com tipo de coluna sql_variant no TVP não é suportado atualmente.

**Implementado instrução preparada Caching de metadados**

O Driver JDBC tiver implementado o cache de metadados de instrução preparada para melhorar o desempenho. Driver agora dá suporte a cache de metadados de instrução preparada no driver com as propriedades de conexão de "disableStatementPooling" e "statementPoolingCacheSize". Por padrão, esse recurso está desabilitado. Encontre mais informações [aqui](../../connect/jdbc/prepared-statement-metadata-caching-for-the-jdbc-driver.md)

**Adicionado suporte para a autenticação integrada do AAD no Linux/Mac**

O JDBC Driver agora também é compatível com a Autenticação Integrada do Azure Active Directory em todos os sistemas operacionais compatíveis (Linux/Windows/Mac) com Kerberos. Como alternativa, em sistemas de operacionais do Windows, os usuários possam autenticar com sqljdbc_auth.

**Versão atualizada do ADAL4J para 1.4.0**

O Driver JDBC atualizou sua dependência do maven no azure-activedirectory-library-for-java (ADAL4J) para a versão 1.4.0. Para obter mais informações sobre dependências, consulte [aqui](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)

## <a name="updates-in-microsoft-jdbc-driver-62-for-sql-server"></a>Atualizações no Microsoft JDBC Driver 6.2 for SQL Server
O Microsoft JDBC Driver 6.2 para SQL Server é totalmente compatível com as especificações do JDBC 4.1 e 4.2. Os jars contidos no pacote 6.0 são nomeados de acordo com a compatibilidade de versão de Java. Por exemplo, o arquivo mssql-jdbc-6.2.1.jre8.jar do pacote 6.2 é recomendado a ser usado com o Java 8. 

> [!NOTE]  
>  Um problema com o aperfeiçoamento de cache de metadados foi encontrado na RTW do 6.2 JDBC lançado em 29 de junho de 2017. A melhoria foi revertida e jars novo (versão 6.2.1) foram lançadas em 17 de julho de 2017 sobre os [Microsoft Download Center](https://go.microsoft.com/fwlink/?linkid=852460), [GitHub](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1), e [Central do Maven](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.sqlserver%22%20AND%20a%3A%22mssql-jdbc%22). Atualize seus projetos para usar o 6.2.1 jars de versão. Exiba [notas de versão](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1) para obter mais detalhes.

**Suporte do Azure Active Directory (AAD) para Linux**

Conecte seus aplicativos do Linux para o banco de dados do SQL Azure usando a autenticação do AAD por meio de métodos de token de acesso e o nome de usuário e senha.

**Federal FIPS Information Processing Standard () habilitada JVMs**

O Driver JDBC agora pode ser usado em JVMs que são executados no modo de conformidade FIPS 140 para atender aos padrões federais e a conformidade. 

**Melhorias de autenticação do Kerberos** 

O Driver JDBC agora tem suporte para: 
* Método de entidade de segurança/senha para aplicativos em que a configuração do Kerberos não pode ser modificado ou não é possível recuperar um novo token ou keytab. Esse método pode ser usado para autenticar para um SQL Server que permite somente a autenticação Kerberos. 
* Autenticação entre realms usando a autenticação integrada do Kerberos sem definir explicitamente o SPN do servidor. O driver agora computará automaticamente o REALM, mesmo quando ele não foi fornecido.
* Delegação restrita de Kerberos, aceitando representada as credenciais do usuário como um objeto de credencial GSS por meio da fonte de dados. Essa credencial representada, em seguida, é usada para estabelecer uma conexão Kerberos. 

**Tempos limite adicionado**

O Driver JDBC agora oferece suporte a configurável limite a seguir que você pode alterar com base nas necessidades do seu aplicativo: 
* Tempo limite da consulta para controlar o número de segundos a aguardar antes que um tempo limite ocorra quando a execução de uma consulta. 
* Tempo limite de soquete para especificar o número de milissegundos de espera antes que ocorra um tempo limite em um soquete de leitura ou aceitar. 

## <a name="updates-in-microsoft-jdbc-driver-61-for-sql-server"></a>Atualizações no Microsoft JDBC Driver 6.1 for SQL Server

O 6.1 do Microsoft JDBC Driver para SQL Server é totalmente compatível com as especificações do JDBC 4.1 e 4.2. Essa é a versão inicial do software livre do Driver JDBC e contém os arquivos de mssql-jdbc-6.1.0.jre7.jar mssql-jdbc-6.1.0.jre8.jar, que correspondem à compatibilidade de versão de Java. 

## <a name="updates-in-microsoft-jdbc-driver-60-for-sql-server"></a>Atualizações no Microsoft JDBC Driver 6.0 for SQL Server

O Microsoft JDBC Driver 6.0 para SQL Server é totalmente compatível com as especificações do JDBC 4.1 e 4.2. Os jars contidos no pacote 6.0 são nomeados de acordo com sua conformidade com a versão de API do JDBC. Por exemplo, o arquivo sqljdbc42.jar do pacote 6.0 é compatível com JDBC API 4.2. Da mesma forma, o arquivo de sqljdbc41.jar está em conformidade com a API do JDBC 4.1.

Para garantir que você tem o sqljdbc41.jar ou sqljdbc42.jar à direita, execute as seguintes linhas de código. Se a saída é "versão do Driver: 6.0.7507.100", você tem o pacote do JDBC Driver 6.0.
```
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```  
 **Sempre Criptografado**  
  
 Suporte para o recurso recém-lançado Always Encrypted no SQL Server 2016, um novo recurso de segurança que garante que os dados confidenciais nunca sejam vistos em texto não criptografado em uma instância do SQL Server. O Always Encrypted funciona por criptografia transparente de dados no aplicativo, de forma que o SQL Server apenas manipulará os dados criptografados e os valores do texto não criptografado. Mesmo se a instância do SQL ou o computador host estiverem comprometidos, tudo que um invasor poderá obter será texto cifrado de dados confidenciais. Para obter detalhes, veja [Uso de Always Encrypted com o driver ODBC em Linux](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md).  
  
 **IDN (nome de domínio internacionalizado)**  
  
 Suporte para nomes de domínio internacionalizados (IDNs) para nomes de servidor. Para detalhes, consulte usando nomes de domínio internacionais sobre o [recursos internacionais do JDBC Driver](../../connect/jdbc/international-features-of-the-jdbc-driver.md) página.  
  
 **Consulta parametrizada**  
  
 Agora dá suporte para recuperar metadados de parâmetro com instruções preparadas para consultas complexas, como subconsultas e/ou junções. Observe que essa melhoria estará disponível somente ao usar o SQL Server 2012 e versões mais recentes.  
  
 **AAD (Azure Active Directory)**  
  
 Autenticação do AAD é um mecanismo para se conectar ao banco de dados SQL v12 usando identidades no AAD. Use a autenticação do AAD para gerenciar centralmente as identidades de usuários do banco de dados e como uma alternativa à autenticação do SQL Server. O JDBC Driver 6.0 permite que você especifique suas credenciais do AAD na cadeia de conexão JDBC para se conectar ao BD SQL do Azure.  Para obter detalhes, consulte a propriedade de autenticação sobre o [definindo as propriedades de Conexão](../../connect/jdbc/setting-the-connection-properties.md) página.  
  
 **Parâmetros com valor de tabela**  
  
 Os parâmetros com valor de tabela fornecem uma maneira fácil de realizar marshaling em várias linhas de dados de um aplicativo cliente do SQL Server sem exigir várias viagens de ida e volta ou uma lógica especial do lado do servidor para processar os dados. Você pode usar parâmetros com valor de tabela para encapsular linhas de dados em um aplicativo cliente e enviar os dados para o servidor em um único comando parametrizado. As linhas de dados de entrada são armazenadas em uma variável de tabela que pode ser operada usando o Transact-SQL. Para obter detalhes, consulte [Using Table-Valued parâmetros](../../connect/jdbc/using-table-valued-parameters.md).  
  
 **AG (Grupos de Disponibilidade) AlwaysOn**  
  
 O driver agora dá suporte a conexões transparentes para grupos de disponibilidade AlwaysOn. O driver descobre rapidamente a topologia AlwaysOn atual de sua infraestrutura de servidor e se conecta ao servidor ativo atual de maneira transparente.  
  
## <a name="updates-in-microsoft-jdbc-driver-42-for-sql-server-and-later"></a>Atualizações do Microsoft JDBC Driver 4.2 e posterior para SQL Server  
O Microsoft JDBC Driver 4.2 para SQL Server é totalmente compatível com as especificações do JDBC 4.1 e 4.2. Os jars contidos no pacote 4.2 são nomeados de acordo com sua conformidade com a versão de API do JDBC. Por exemplo, o arquivo sqljdbc42.jar do pacote 4.2 é compatível com JDBC API 4.2. Da mesma forma, o arquivo de sqljdbc41.jar está em conformidade com a API do JDBC 4.1.

Para garantir que você tem o sqljdbc41.jar ou sqljdbc42.jar à direita, execute as seguintes linhas de código. Se a saída é "versão do Driver: 4.2.6420.100", você tem o pacote do JDBC Driver 4.2.
```
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```
 **Suporte para JDK 8**  
  
 Suporte para JDK (Java Development Kit) versão 8.0, além de JDK 7.0, 6.0 e 5.0.  
  
 **Conformidade com JDBC 4.1 e 4.2**  
  
 Suporte para especificações de API do Java Database Connectivity 4.1 e 4.2, além do 4.0. Para obter detalhes, consulte [conformidade JDBC 4.1 para o Driver JDBC](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md) e [conformidade do JDBC 4.2 para o JDBC Driver](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md).  
  
 **Cópia em massa**  
  
 O recurso de cópia em massa é usado para copiar rapidamente grandes quantidades de dados em tabelas ou exibições em bancos de dados do SQL Server. Para obter detalhes, consulte [usando a cópia em massa com o Driver JDBC](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md).  
  
 **Opção de reversão de transação XA**  
  
 Novas opções de tempo limite adicionadas para reversão automática existente de transações não preparadas. Para obter detalhes, consulte [Noções básicas sobre transações de XA](../../connect/jdbc/understanding-xa-transactions.md).  
  
 **Nova propriedade de conexão principal Kerberos**  
  
 Uma nova propriedade de conexão foi adicionada para facilitar a flexibilidade com conexões de Kerberos. Para obter detalhes, veja [Como usar a autenticação integrada do Kerberos para se conectar ao SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md).  
  
## <a name="updates-in-microsoft-jdbc-driver-41-for-sql-server-and-later"></a>Atualizações do Microsoft JDBC Driver 4.1 e posterior para SQL Server  
 **Suporte para JDK 7**  
  
 Suporte para JDK (Java Development Kit) versão 7.0, além de JDK 6.0 e 5.0.  
  
## <a name="itanium-not-supported-for-jdbc-driver-64-60-42-and-41-applications"></a>Aplicativos JDBC Driver 6.4, 6.0, 4.2 e 4.1 não são compatíveis com Itanium  
  
 Não há suporte para execução de aplicativos Microsoft JDBC Drivers 6.4, 6.0, 4.2 e 4.1 for SQL Server em um computador Itanium.  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do JDBC Driver](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  

