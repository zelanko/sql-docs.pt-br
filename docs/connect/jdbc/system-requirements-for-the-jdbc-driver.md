---
title: Requisitos de sistema para o JDBC Driver | Microsoft Docs
ms.custom: ''
ms.date: 04/16/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 447792bb-f39b-49b4-9fd0-1ef4154c74ab
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 244f5383add437b8bd4985045bd9edc8538805e3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66798285"
---
# <a name="system-requirements-for-the-jdbc-driver"></a>Requisitos de sistema para o JDBC Driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Para acessar dados de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou de um [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] usando o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], você deve ter os seguintes componentes instalados no computador:

- [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] ([baixar](download-microsoft-jdbc-driver-for-sql-server.md))
- Java Runtime Environment

## <a name="java-runtime-environment-requirements"></a>Requisitos do Java Runtime Environment  

 Começando com o Microsoft JDBC Driver 7.2 para SQL Server, há suporte para o JDK (Java Development Kit) 11.0 e o JRE (Java Runtime Environment) 11.0.
 
 Começando com o Microsoft JDBC Driver 7.0 para SQL Server, há suporte para o JDK (Java Development Kit) 10.0 e o JRE (Java Runtime Environment) 10.0.

 Começando com o Microsoft JDBC Driver 6.4 para SQL Server, há suporte para o JDK (Java Development Kit) 9.0 e o JRE (Java Runtime Environment) 9.0.

 Começando com o Microsoft JDBC Driver 4.2 para SQL Server, há suporte para o JDK (Java Development Kit) 8.0 e o JRE (Java Runtime Environment) 8.0. Suporte para a API de especificação do Java Database Connectivity (JDBC) foi estendido para incluir a API do JDBC 4.1 e 4.2.
  
 Começando com o Microsoft JDBC Driver 4.1 para SQL Server, há suporte para o JDK (Java Development Kit) 7.0 e o JRE (Java Runtime Environment) 7.0.
  
 Começando com o [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], o suporte para o JDBC driver para a API da Especificação do JDBC (Java Database Connectivity) foi estendido para incluir a API do JDBC 4.0. A API do JDBC 4.0 foi introduzida como parte do JDK (Java Development Kit) 6.0 e do JRE (Java Runtime Environment) 6.0. O JDBC 4.0 é um superconjunto da API do JDBC 3.0.
  
 Quando você implanta o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] nos sistemas operacionais Windows e UNIX, deve usar os pacotes de instalação *sqljdbc_\<version>_enu.exe* e *sqljdbc_\<version>_enu.tar.gz*, respectivamente. Para saber mais sobre como implantar o JDBC Driver, confira o tópico [Implantando o JDBC Driver](../../connect/jdbc/deploying-the-jdbc-driver.md).  

**Microsoft JDBC Driver 7.2 para SQL Server:**  

  O JDBC Driver 7.2 inclui duas bibliotecas de classes JAR em cada pacote de instalação: **mssql-jdbc-7.2.2.jre8.jar** e **mssql-jdbc-7.2.2.jre11.jar**.

  O JDBC Driver 7.2 foi desenvolvido para funcionar e ser compatível com todas as principais máquinas virtuais Java, mas foi testado somente nas versões 8.0 e 11.0 do OpenJDK e nas versões 8.0 e 11.0 do Azul Zulu JRE.
  
  Veja a seguir um resumo do suporte fornecido pelos dois arquivos JAR incluídos no Microsoft JDBC Drivers 7.2 para SQL Server:  
  
  |JAR|Conformidade de versão do JDBC|Versão do Java recomendada|Descrição|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-7.2.2.jre8.jar|4.2|8|Requer um Java Runtime Environment (JRE) 8.0. O uso do JRE 7.0 ou inferior lança uma exceção.<br /><br /> Os novos recursos no 7.2 incluem: suporte ao JDK 11, autenticação da Identidade de Serviço Gerenciada (MSI) do Active Directory, suporte a OSGi, APIs de SQLServerError. |    
|mssql-jdbc-7.2.2.jre11.jar|4.3|10|Requer um JRE (Java Runtime Environment) 11.0. O uso do JRE 10.0 ou inferior lança uma exceção.<br /><br /> Os novos recursos no 7.2 incluem: suporte ao JDK 11, autenticação da Identidade de Serviço Gerenciada (MSI) do Active Directory, suporte a OSGi, APIs de SQLServerError. |    


  O JDBC Driver 7.2 também está disponível no repositório Maven Central e pode ser incluído a um projeto Maven adicionando o código a seguir no POM.XML:  
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.2.2.jre11</version>
</dependency>
```
 
**Microsoft JDBC Driver 7.0 para SQL Server:**  

  O JDBC Driver 7.0 inclui duas bibliotecas de classes JAR em cada pacote de instalação: **mssql-jdbc-7.0.0.jre8.jar** e **mssql-jdbc-7.0.0.jre10.jar**.

  O JDBC Driver 7.0 foi desenvolvido para funcionar e ser compatível com todas as principais máquinas virtuais Java, mas foi testado somente no OpenJDK 8.0 e 10.0.
  
  A seguir, um resumo do suporte fornecido pelos dois arquivos JAR incluídos com o Microsoft JDBC Drivers 7.0 for SQL Server:  
  
  |JAR|Conformidade de versão do JDBC|Versão do Java recomendada|Descrição|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-7.0.0.jre8.jar|4.2|8|Requer um Java Runtime Environment (JRE) 8.0. O uso do JRE 7.0 ou inferior lança uma exceção.<br /><br /> Os novos recursos no 7.0 incluem: suporte ao JDK 10, atualização do nível de compatibilidade padrão para especificações JDBC 4.2, suporte a Tipos de Dados Espaciais, propriedade de conexão cancelQueryTimeout, métodos de Limite de Solicitação, propriedade de conexão useBulkCopyForBatchInsert, Dados de Descoberta e informação de classificação, extensão do recurso de UTF-8 e suporte a CityHash. |    
|mssql-jdbc-7.0.0.jre10.jar|4.3|10|Requer um JRE (Java Runtime Environment) 10.0. O uso do JRE 9.0 ou inferior lança uma exceção.<br /><br /> Os novos recursos no 7.0 incluem: suporte ao JDK 10, atualização do nível de compatibilidade padrão para especificações JDBC 4.2, suporte a Tipos de Dados Espaciais, propriedade de conexão cancelQueryTimeout, métodos de Limite de Solicitação, propriedade de conexão useBulkCopyForBatchInsert, Dados de Descoberta e informação de classificação, extensão do recurso de UTF-8 e suporte a CityHash. |    


  O JDBC Driver 7.0 também está disponível no repositório Maven Central e pode ser incluído a um projeto Maven adicionando o código a seguir no POM.XML:  
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.0.0.jre10</version>
</dependency>
```
  
**Microsoft JDBC Driver 6.4 for SQL Server:**  

  O JDBC Driver 6.4 inclui três bibliotecas de classes JAR em cada pacote de instalação: **mssql-jdbc-6.4.0.jre7.jar**, **mssql-jdbc-6.4.0.jre8.jar** e **mssql-jdbc-6.4.0.jre9.jar**.

  O JDBC Driver 6.4 foi desenvolvido para funcionar e ser compatível com todas as principais máquinas virtuais Java, mas foi testado somente no OpenJDK 7.0, 8.0 e 9.0.
  
  A seguir, um resumo do suporte fornecido pelos três arquivos JAR incluídos com o Microsoft JDBC Drivers 6.4 for SQL Server:  
  
  |JAR|Conformidade de versão do JDBC|Versão do Java recomendada|Descrição|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-6.4.0.jre7.jar|4.1|7|Requer um Java Runtime Environment (JRE) 7.0. O uso do JRE 6.0 ou inferior lança uma exceção.<br /><br /> Os novos recursos da versão 6.4 incluem: autenticação do Azure AD para Linux, o método de entidade de segurança/senha para o Kerberos, a detecção automática de REALM no SPN para autenticação de domínio cruzado, delegação restrita do Kerberos, tempo limite para consulta, tempo limite de soquete e reutilização de identificador de instrução preparada. |  
|mssql-jdbc-6.4.0.jre8.jar|4.2|8|Requer um Java Runtime Environment (JRE) 8.0. O uso do JRE 7.0 ou inferior lança uma exceção.<br /><br /> Os novos recursos da versão 6.4 incluem: autenticação do Azure AD para Linux, o método de entidade de segurança/senha para o Kerberos, a detecção automática de REALM no SPN para autenticação de domínio cruzado, delegação restrita do Kerberos, tempo limite para consulta, tempo limite de soquete e reutilização de identificador de instrução preparada. |    
|mssql-jdbc-6.4.0.jre9.jar|4.3|9|Requer um JRE (Java Runtime Environment) 9.0. O uso do JRE 8.0 ou inferior lança uma exceção.<br /><br /> Os novos recursos da versão 6.4 incluem: autenticação do Azure AD para Linux, o método de entidade de segurança/senha para o Kerberos, a detecção automática de REALM no SPN para autenticação de domínio cruzado, delegação restrita do Kerberos, tempo limite para consulta, tempo limite de soquete e reutilização de identificador de instrução preparada. |

O JDBC Driver 6.4 também está disponível no repositório Maven Central e pode ser incluído a um projeto Maven adicionando o código a seguir no POM.XML 

 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.4.0.jre9</version>
</dependency>
```

**Microsoft JDBC Driver 6.2 for SQL Server:**  
  
  O JDBC Driver 6.2 inclui duas bibliotecas de classes JAR em cada pacote de instalação: **mssql-jdbc-6.2.2.jre7.jar** e **mssql-jdbc-6.2.2.jre8.jar**. 
  
 O JDBC Driver 6.2 foi desenvolvido para funcionar e ser compatível com todas as principais máquinas virtuais Java, mas foi testado somente no Sun JRE 5.0, 6.0, 7.0 e 8.0.
  
 A seguir, um resumo do suporte fornecido pelos dois arquivos JAR incluídos com os Microsoft JDBC Drivers 6.0 e 4.2 para o SQL Server:  
  
|JAR|Conformidade de versão do JDBC|Versão do Java recomendada|Descrição|  
|---------|-----------------------------|----------------------|-----------------|
|mssql-jdbc-6.2.2.jre7.jar|4.1|7|Requer um Java Runtime Environment (JRE) 7.0. O uso do JRE 6.0 ou inferior lança uma exceção.<br /><br /> Novos recursos no 6.2 incluem: autenticação do Azure AD para Linux, o método de entidade de segurança/senha para o Kerberos, a detecção automática de REALM no SPN para autenticação de domínio cruzado, delegação restrita do Kerberos, tempo limite para consulta, tempo limite de soquete e reutilização de identificador de instrução preparada. |  
|mssql-jdbc-6.2.3.jre8.jar|4.2|8|Requer um Java Runtime Environment (JRE) 8.0. O uso do JRE 7.0 ou inferior lança uma exceção.<br /><br /> Os novos recursos da versão 6.2 incluem: autenticação do Azure AD para Linux, o método de entidade de segurança/senha para o Kerberos, a detecção automática de REALM no SPN para autenticação de domínio cruzado, delegação restrita do Kerberos, tempo limite para consulta, tempo limite de soquete e reutilização de identificador de instrução preparada|    

  O JDBC Driver 6.2 também está disponível no repositório Maven Central e pode ser incluído a um projeto Maven adicionando o código a seguir no POM.XML 
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.2.jre8</version>
</dependency>
```    

 **Microsoft JDBC Driver 6.0 e 4.2 for SQL Server:**  
  
  O JDBC Driver 6.0 e o 4.2 incluem duas bibliotecas de classes JAR em cada pacote de instalação: **sqljdbc41.jar** e **sqljdbc42.jar**. 
  
 Os JDBC Drivers 6.0 e 4.2 foram desenvolvidos para funcionar e ser compatíveis com todas as principais máquinas virtuais Java, mas foram testados somente no Sun JRE 5.0, 6.0, 7.0 e 8.0.
  
 A seguir, um resumo do suporte fornecido pelos dois arquivos JAR incluídos com os Microsoft JDBC Drivers 6.0 e 4.2 para o SQL Server:  
  
|JAR|Conformidade de versão do JDBC|Versão do Java recomendada|Descrição|  
|---------|-----------------------------|----------------------|-----------------|   
|sqljdbc41.jar|4.1|7|Requer um Java Runtime Environment (JRE) 7.0. O uso do JRE 6.0 ou inferior lança uma exceção.<br /><br /> Os novos recursos nos pacotes 6.0 e 4.2 incluem: conformidade com o JDBC 4.1 e cópia em massa<br /><br /> Além disso, os novos recursos somente no pacote 6.0 incluem: Always Encrypted, parâmetros com valor de tabela, autenticação do Azure Active Directory, conexões transparentes para grupos de disponibilidade AlwaysOn, melhoria na recuperação de metadados de parâmetro para consultas preparadas e nome de domínio internacionalizado (IDN)|  
|sqljdbc42.jar|4.2|8|Requer um Java Runtime Environment (JRE) 8.0. O uso do JRE 7.0 ou inferior lança uma exceção.<br /><br /> Os novos recursos dos pacotes 6.0 e 4.2 incluem: conformidade com o JDBC 4.1, conformidade com o JDBC 4.2 e cópia em massa<br /><br /> Além disso, os novos recursos somente no pacote 6.0 incluem: Always Encrypted, parâmetros com valor de tabela, autenticação do Azure Active Directory, conexões transparentes para grupos de disponibilidade AlwaysOn, melhoria na recuperação de metadados de parâmetro para consultas preparadas e nome de domínio internacionalizado (IDN)|  
  
 **Microsoft JDBC Driver 4.1 for SQL Server:**  
  
 O JDBC Driver 4.1 inclui uma biblioteca de classes JAR em cada pacote de instalação: **sqljdbc41.jar**.  
    
|JAR|Descrição|  
|---------|-----------------|  
|sqljdbc41.jar|A biblioteca de classes **sqljdbc41.jar** dá suporte à API do JDBC 4.0. Ele inclui todos os recursos do driver JDBC 4.0, bem como métodos de API do JDBC 4.0. Não há suporte para o JDBC 4.1 (gera uma exceção "SQLFeatureNotSupportedException").<br /><br /> A biblioteca de classes **sqljdbc41.jar** requer um JRE (Java Runtime Environment) 7.0. O uso do **sqljdbc41.jar** no JRE 6.0 e 5.0 lança uma exceção.<br /><br /> 
  
 O JDBC Driver foi desenvolvido para funcionar e ser compatível com todas as principais máquinas virtuais Java, mas foi testado somente no Sun JRE 5.0, 6.0 e 7.0.
  
 A seguir, um resumo do suporte fornecido pelo arquivo JAR incluído com o Microsoft JDBC Driver 4.1 para o SQL Server.  
  
|JAR|Versão JDBC|JRE (pode ser executado)|JDK (pode ser compilado)|  
|---------|------------------|---------------------|-------------------------|   
|sqljdbc41.jar|4|7|7 6 5|  
  
## <a name="sql-server-requirements"></a>Requisitos do SQL Server  
 O driver JDBC dá suporte a conexões ao Banco de Dados SQL do Azure e ao SQL Server. Para o Microsoft JDBC Driver 4.2 e 4.1 para SQL Server, o suporte começa com o SQL Server 2008.
  
## <a name="operating-system-requirements"></a>Requisitos do sistema operacional  
 O driver JDBC foi desenvolvido para funcionar em qualquer sistema operacional que ofereça suporte ao uso de uma JVM (Máquina Virtual Java). Porém, só os sistemas operacionais Sun Solaris, SUSE Linux e Windows foram testados oficialmente.  
  
## <a name="supported-languages"></a>Idiomas com suporte  
 O driver JDBC dá suporte a todas as ordenações de coluna do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para saber mais sobre as ordenações com suporte no driver JDBC, confira os [recursos internacionais do JDBC Driver](../../connect/jdbc/international-features-of-the-jdbc-driver.md).  
  
 Para obter mais informações sobre ordenações, consulte "Trabalhando com ordenações" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do JDBC Driver](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
