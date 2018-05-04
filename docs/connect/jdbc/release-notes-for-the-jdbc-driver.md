---
title: Notas de versão para o Driver JDBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
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
ms.assetid: 074f211e-984a-4b76-bb15-ee36f5946f12
caps.latest.revision: 206
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c450b8a41c87ec28f0c576f6a8a468e901cdfa2a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="release-notes-for-the-jdbc-driver"></a>Notas de versão do Driver JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

## <a name="updates-in-microsoft-jdbc-driver-64-for-sql-server"></a>Atualizações do Microsoft JDBC Driver 6.4 para SQL Server
O Microsoft JDBC Driver 6.4 para o SQL Server é totalmente compatível com as especificações do JDBC 4.1 e 4.2. Os jars contidos no pacote 6.4 são nomeados de acordo com a compatibilidade de versão do Java. Por exemplo, o arquivo mssql-jdbc-6.4.0.jre8.jar do pacote 6.4 é recomendado a ser usado com Java 8. 

**Suporte para JDK 9**  
  
Suporte para Java Development Kit (JDK) versão 9.0, além de JDK 8.0 e 7.0.
  
**Conformidade do JDBC 4.3**  
  
Suporte para especificação de Java 4.3 de API de conectividade de banco de dados, além de 4.1 e 4.2. Os métodos da API do JDBC 4.3 são adicionados, mas ainda não implementados. Para obter detalhes, consulte [JDBC 4.3 conformidade para o Driver JDBC](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md).
 
**Adicionada nova propriedade de conexão: sslProtocol**

Adicionar uma nova propriedade de conexão que permite aos usuários especificar a palavra-chave de protocolo TLS. Os valores possíveis são: "TLS", "TLSv1", "TLSv1.1", "TLSv1.2". Consulte [SSLProtocol](https://github.com/Microsoft/mssql-jdbc/wiki/SSLProtocol) para obter detalhes.

**Preterido a propriedade de conexão: fipsProvider**

A propriedade de Conexão "fipsProvider" é removida da lista de propriedades de conexão aceitos. Consulte os detalhes [aqui](https://github.com/Microsoft/mssql-jdbc/pull/460).

**Propriedades de conexão adicional para especificar TrustManager personalizado**

Driver agora oferece suporte à especificação TrustManager personalizado com propriedades de conexão de "trustManagerConstructorArg" e "trustManagerClass" adicionado. Isso permite a especificação dinâmica de um conjunto de certificados confiáveis em uma base por conexão sem modificar as configurações globais para o ambiente da JVM.

**Adicionado suporte para datetime/smallDatetime em parâmetros com valor de tabela (TVP)**

Driver agora dá suporte a tipos de dados DATETIME e SMALLDATETIME ao usar parâmetros com valor de tabela (TVP).

**Adicionado suporte para o tipo de dados sql_variant**

O Driver JDBC agora dá suporte a tipos de dados sql_variant a ser usado com o SQL Server. Sql_variant também é compatível com recursos como parâmetros com valor de tabela (TVP) e BulkCopy com abaixo limitações:

1. Para valores de data: ao usar TVP para popular uma tabela que contém os valores de data/datetime/smalldatetime armazenados na coluna sql_variant, chamar métodos getDateTime()/getSmallDateTime()/getDate() no conjunto de resultados não funciona e gera a seguinte exceção:
    ```
    java.lang.String cannot be cast to java.sql.Timestamp
    ```
    Solução alternativa: use métodos "getString ()" ou "GetObject ()".

2. Usar TVP com SQL Variant para valores nulos

Se você estiver usando um TVP para popular uma tabela e enviar o valor NULL para o tipo de coluna sql_variant, você encontrará uma exceção ao Inserir valor NULL com tipo de coluna sql_variant em TVP não é suportado atualmente.

**Implementado preparadas cache de metadados**

O Driver JDBC implementou o cache de metadados de instrução preparada para melhorar o desempenho. Driver agora dá suporte a cache de metadados de instrução preparada no driver com as propriedades de conexão "disableStatementPooling" e "statementPoolingCacheSize". Por padrão, esse recurso está desabilitado. Mais informações podem ser encontradas [aqui](../../connect/jdbc/prepared-statement-metadata-caching-for-the-jdbc-driver.md)

**Adicionado suporte para autenticação integrada do AAD no Linux/Mac**

O Driver JDBC agora também oferece suporte à autenticação integrada do Azure Active Directory em todos os sistemas operacionais (Linux/Windows/Mac) com o Kerberos. Como alternativa, em sistemas operacionais, os usuários podem autenticar com sqljdbc_auth.dll.

**Versão atualizada do ADAL4J para 1.4.0**

O Driver JDBC atualizou sua dependência maven ao azure Active Directory-biblioteca-para-java (ADAL4J) para a versão 1.4.0. Para obter mais informações sobre dependências, consulte [aqui](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)

## <a name="updates-in-microsoft-jdbc-driver-62-for-sql-server"></a>Atualizações do Microsoft JDBC Driver 6.2 para SQL Server
O Microsoft JDBC Driver 6.2 para o SQL Server é totalmente compatível com as especificações do JDBC 4.1 e 4.2. Os jars contidos no pacote 6.0 são nomeados de acordo com a compatibilidade de versão do Java. Por exemplo, o arquivo mssql-jdbc-6.2.1.jre8.jar do pacote 6.2 é recomendado para ser usado com Java 8. 

> [!NOTE]  
>  Um problema com o aperfeiçoamento de cache de metadados foi encontrado no RTW de 6.2 JDBC lançadas em 29 de junho de 2017. A melhoria foi revertida e novo jars (versão 6.2.1) foram lançadas em 17 de julho de 2017 no [Microsoft Download Center](https://go.microsoft.com/fwlink/?linkid=852460), [GitHub](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1), e [Maven Central](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.sqlserver%22%20AND%20a%3A%22mssql-jdbc%22). Atualize seus projetos para usar o 6.2.1 jars de versão. Consulte [notas de versão](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1) para obter mais detalhes.

**Suporte do Azure Active Directory (AAD) para Linux**

Conecte-se seus aplicativos do Linux para o banco de dados do SQL Azure usando a autenticação do AAD por meio de métodos de token de acesso e nome de usuário e senha.

**Federal Information Processing Standard (FIPS) habilitado JVMs**

O Driver JDBC agora pode ser usado em JVMs executados no modo de conformidade FIPS 140 para atender aos padrões federais e conformidade. 

**Aprimoramentos de autenticação do Kerberos** 

O Driver JDBC agora tem suporte para: 
* Método de senha do principal para aplicativos em que a configuração de Kerberos não pode ser modificado ou não é possível recuperar um novo token ou keytab. Esse método pode ser usado para autenticar para um SQL Server que permite apenas a autenticação Kerberos. 
* Autenticação entre realms usando a autenticação integrada do Kerberos sem definir explicitamente o SPN do servidor. O driver agora automaticamente calcula o REALM mesmo quando ele não foi fornecido.
* Delegação restrita de Kerberos, aceitando representada credenciais de usuário como um objeto de credencial GSS por meio da fonte de dados. Essa credencial representado, em seguida, é usada para estabelecer uma conexão Kerberos. 

**Tempos limite adicionado**

O Driver JDBC agora dá suporte a configurável limite a seguir que pode alterar com base nas necessidades do aplicativo: 
* Tempo limite da consulta para controlar o número de segundos a aguardar antes de um tempo limite ocorre ao executar uma consulta. 
* Tempo limite de soquete para especificar o número de milissegundos de espera antes que ocorra um tempo limite em um soquete de leitura ou aceitar. 

## <a name="updates-in-microsoft-jdbc-driver-61-for-sql-server"></a>Atualizações do Microsoft JDBC Driver 6.1 para SQL Server

O 6.1 do Microsoft JDBC Driver para SQL Server é totalmente compatível com as especificações do JDBC 4.1 e 4.2. Essa é a versão do código-fonte aberto inicial do Driver JDBC e contém os arquivos de mssql-jdbc-6.1.0.jre7.jar mssql-jdbc-6.1.0.jre8.jar, que correspondem à compatibilidade de versão do Java. 

## <a name="updates-in-microsoft-jdbc-driver-60-for-sql-server"></a>Atualizações do Microsoft JDBC Driver 6.0 para SQL Server

O Microsoft JDBC Driver 6.0 para SQL Server é totalmente compatível com as especificações do JDBC 4.1 e 4.2. Os jars contidos no pacote 6.0 são nomeados de acordo com sua conformidade com a versão de API do JDBC. Por exemplo, o arquivo sqljdbc42.jar do pacote 6.0 é API do JDBC 4.2 compatíveis. Da mesma forma, o arquivo sqljdbc41.jar é compatível com a API do JDBC 4.1.

Para garantir que o sqljdbc41.jar ou sqljdbc42.jar à direita, execute as seguintes linhas de código. Se a saída for "versão do Driver: 6.0.7507.100", você tem o pacote do JDBC Driver 6.0.
```
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```  
 **Sempre Criptografado**  
  
 Suporte para o recurso recém-lançado sempre criptografado no SQL Server 2016, um novo recurso de segurança que garante que os dados confidenciais nunca sejam vistos em texto não criptografado em uma instância do SQL Server. O Always Encrypted funciona por criptografia transparente de dados no aplicativo, de forma que o SQL Server apenas manipulará os dados criptografados e os valores do texto não criptografado. Mesmo se a instância do SQL ou o computador host estiverem comprometido, tudo que um invasor pode obter é texto cifrado de dados confidenciais. Para obter detalhes, consulte [usar sempre criptografado com o Driver JDBC](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md).  
  
 **Nome de domínio internacionalizado (IDN)**  
  
 Suporte para nomes de domínio internacionalizados (IDNs) para nomes de servidor. Para obter detalhes, consulte usando nomes de domínio internacionais sobre o [recursos internacionais do JDBC Driver](../../connect/jdbc/international-features-of-the-jdbc-driver.md) página.  
  
 **Consulta parametrizada**  
  
 Agora dá suporte para recuperar metadados de parâmetro com instruções preparadas para consultas complexas, como subconsultas e/ou junções. Observe que essa melhoria estará disponível somente ao usar o SQL Server 2012 e versões mais recentes.  
  
 **Active Directory do Azure (AAD)**  
  
 Autenticação do AAD é um mecanismo para se conectar ao banco de dados SQL v12 usando identidades no AAD. Use autenticação do AAD para gerenciar centralmente as identidades de usuários de banco de dados e como uma alternativa para autenticação do SQL Server. O JDBC Driver 6.0 permite que você especifique suas credenciais do AAD na cadeia de caracteres de conexão JDBC para se conectar ao banco de dados de SQL do Azure.  Para obter detalhes, consulte a propriedade de autenticação no [definindo as propriedades de Conexão](../../connect/jdbc/setting-the-connection-properties.md) página.  
  
 **Parâmetros com valor de tabela**  
  
 Os parâmetros com valor de tabela fornecem uma maneira fácil de marshaling em várias linhas de dados de um aplicativo cliente para o SQL Server sem exigir várias viagens de ida e volta ou uma lógica especial do lado do servidor para processar os dados. Você pode usar parâmetros com valor de tabela para encapsular linhas de dados em um aplicativo cliente e enviar os dados para o servidor em um único comando com parâmetros. As linhas de dados de entrada são armazenadas em uma variável de tabela, em seguida, pode ser operada usando Transact-SQL. Para obter detalhes, consulte [Using Table-Valued parâmetros](../../connect/jdbc/using-table-valued-parameters.md).  
  
 **Grupos de disponibilidade do AlwaysOn (AG)**  
  
 O driver agora dá suporte a conexões transparentes para grupos de disponibilidade AlwaysOn. O driver rapidamente descobre a topologia do AlwaysOn atual de sua infraestrutura de servidor e se conecta ao servidor ativo atual transparente.  
  
## <a name="updates-in-microsoft-jdbc-driver-42-for-sql-server-and-later"></a>Atualizações do Microsoft JDBC Driver 4.2 e posterior para SQL Server  
O Microsoft JDBC Driver 4.2 para SQL Server é totalmente compatível com as especificações do JDBC 4.1 e 4.2. Os jars contidos no pacote 4.2 são nomeados de acordo com sua conformidade com a versão de API do JDBC. Por exemplo, o arquivo sqljdbc42.jar do pacote 4.2 é API do JDBC 4.2 compatíveis. Da mesma forma, o arquivo sqljdbc41.jar é compatível com a API do JDBC 4.1.

Para garantir que o sqljdbc41.jar ou sqljdbc42.jar à direita, execute as seguintes linhas de código. Se a saída for "versão do Driver: 4.2.6420.100", você tem o pacote do JDBC Driver 4.2.
```
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```
 **Suporte para JDK 8**  
  
 Suporte para Java Development Kit (JDK) versão 8.0, além de JDK 7.0, 6.0 e 5.0.  
  
 **Conformidade JDBC 4.1 e 4.2**  
  
 Suporte para especificações de API do Java Database Connectivity 4.1 e 4.2, além do 4.0. Para obter detalhes, consulte [conformidade JDBC 4.1 para o Driver JDBC](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md) e [conformidade do JDBC 4.2 para o Driver JDBC](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md).  
  
 **Cópia em massa**  
  
 O recurso de cópia em massa é usado para copiar rapidamente grandes quantidades de dados em tabelas ou exibições em bancos de dados do SQL Server. Para obter detalhes, consulte [usando cópia em massa com o Driver JDBC](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md).  
  
 **Opção de reversão de transação XA**  
  
 Novas opções de tempo limite adicionadas para reversão automática existente de transações não preparadas. Para obter detalhes, consulte [Noções básicas sobre as transações XA](../../connect/jdbc/understanding-xa-transactions.md).  
  
 **Nova propriedade de Conexão Principal Kerberos**  
  
 Uma nova propriedade de conexão foi adicionada para facilitar a flexibilidade com conexões de Kerberos. Para obter detalhes, consulte [usando a autenticação integrada Kerberos para se conectar ao SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md).  
  
## <a name="updates-in-microsoft-jdbc-driver-41-for-sql-server-and-later"></a>Atualizações do Microsoft JDBC Driver 4.1 e posterior para SQL Server  
 **Suporte para JDK 7**  
  
 Suporte para JDK (Java Development Kit) versão 7.0, além de JDK 6.0 e 5.0.  
  
## <a name="itanium-not-supported-for-jdbc-driver-64-60-42-and-41-applications"></a>Itanium sem suporte para aplicativos do JDBC Driver 6.4, 6.0, 4.2 e 4.1  
  
 Não há suporte para o Microsoft JDBC Drivers 6.4, 6.0, 4.2 e 4.1 para aplicativos do SQL Server para ser executado em um computador Itanium.  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral do JDBC Driver](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  

