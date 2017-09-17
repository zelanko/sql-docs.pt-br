---
title: "Notas de versão para o Driver JDBC | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 074f211e-984a-4b76-bb15-ee36f5946f12
caps.latest.revision: 206
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bd65725237fd625c40f8755e636bb4f6fa2c55ea
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="release-notes-for-the-jdbc-driver"></a>Notas de versão do Driver JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

## <a name="updates-in-microsoft-jdbc-driver-62-for-sql-server"></a>Atualizações do Microsoft JDBC Driver 6.2 para SQL Server
O Microsoft JDBC Driver 6.2 para o SQL Server é totalmente compatível com as especificações do JDBC 4.1 e 4.2. Os jars contidos no pacote 6.0 são nomeados de acordo com a compatibilidade de versão do Java. Por exemplo, o arquivo mssql-jdbc-6.2.1.jre8.jar do pacote 6.2 é recomendado para ser usado com Java 8. 

**Observação:** um problema com o aperfeiçoamento de cache de metadados foi encontrado no RTW de 6.2 JDBC lançadas em 29 de junho de 2017. A melhoria foi revertida e novo jars (versão 6.2.1) foram lançadas em 17 de julho de 2017 no [Microsoft Download Center](https://go.microsoft.com/fwlink/?linkid=852460), [GitHub](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1), e [Maven Central](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.sqlserver%22%20AND%20a%3A%22mssql-jdbc%22). Atualize seus projetos para usar o 6.2.1 jars de versão. Consulte [notas de versão](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1) para obter mais detalhes.

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
  
## <a name="updates-in-microsoft-jdbc-driver-40-for-sql-server-and-later"></a>Atualizações do Microsoft JDBC Driver 4.0 e posterior para SQL Server  
 **Informações sobre como se conectar a um banco de dados SQL do Azure**  
  
 Agora há um tópico com informações sobre como se conectar a um banco de dados SQL do Azure. Consulte [se conectar a um banco de dados do SQL Azure](../../connect/jdbc/connecting-to-an-azure-sql-database.md) para obter mais informações.  
  
 **Suporte para alta disponibilidade, recuperação de desastres**  
  
 Suporte para conexões de recuperação de desastres de alta disponibilidade para grupos de disponibilidade do AlwaysOn no [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]. Consulte [suporte do Driver JDBC para alta disponibilidade, recuperação de desastres](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md) para obter mais informações.  
  
 **Usando a autenticação integrada do Kerberos para se conectar ao SQL Server**  
  
 Suporte para autenticação integrada do Kerberos tipo 4 para aplicativos para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados. Para obter mais informações, consulte [usando a autenticação integrada Kerberos para se conectar ao SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md). (Kerberos tipo 2 a autenticação integrada está disponível no [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] versões anteriores à 4.0.)  
  
 **Acessar informações de diagnóstico nos logs de eventos estendidos**  
  
 Você pode acessar informações no log de eventos estendidos do servidor para entender as falhas de conexão. Para obter mais informações, consulte [acessando informações de diagnóstico no Log de eventos estendidos](../../connect/jdbc/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
 **Suporte adicional para colunas esparsas**  
  
 Se seu aplicativo já acessa dados em uma tabela que usa colunas esparsas, você deverá ver um aumento no desempenho. Você pode obter informações sobre colunas (incluindo informações de coluna esparsa) com [getColumns método &#40; SQLServerDatabaseMetaData &#41; ](../../connect/jdbc/reference/getcolumns-method-sqlserverdatabasemetadata.md). Para obter mais informações sobre [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] colunas esparsas, consulte [usando colunas esparsas](http://go.microsoft.com/fwlink/?LinkId=224244).  
  
 **Xid.getFormatId**  
  
 A partir do [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], o driver JDBC passará o identificador de formato do aplicativo para o servidor de banco de dados. Para obter o comportamento atualizado, verifique se o sqljdbc_xa.dll no servidor está atualizado. Para obter mais informações sobre como copiar uma versão atualizada do sqljdbc_xa.dll para o servidor, consulte [Noções básicas sobre as transações XA](../../connect/jdbc/understanding-xa-transactions.md).  
  
## <a name="itanium-not-supported-for-jdbc-driver-60-42-41-and-40-applications"></a>Itanium sem suporte para aplicativos do JDBC Driver 6.0, 4.2, 4.1 e 4.0  
  
 Não há suporte para o Microsoft JDBC Drivers 6.0, 4.2, 4.1 e 4.0 para aplicativos do SQL Server para ser executado em um computador Itanium.  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral do JDBC Driver](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  

