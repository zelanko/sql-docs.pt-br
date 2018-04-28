---
title: Requisitos de sistema para o Driver JDBC | Microsoft Docs
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
ms.topic: article
ms.assetid: 447792bb-f39b-49b4-9fd0-1ef4154c74ab
caps.latest.revision: 73
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Active
ms.openlocfilehash: a7ad308b0ca7ea617ab9f6e2882f800e6aa92d58
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="system-requirements-for-the-jdbc-driver"></a>Requisitos de sistema para o JDBC Driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Para acessar dados de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] usando o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], você deve ter os seguintes componentes instalados no seu computador:  
  
-   [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]  
  
     Você pode baixar o Microsoft JDBC Driver dos links abaixo Microsoft Download Center: 
     * [Microsoft JDBC Driver 6.4 para SQL Server](http://go.microsoft.com/fwlink/?linkid=868290)
     * [Microsoft JDBC Driver 6.2 para SQL Server](http://go.microsoft.com/fwlink/?linkid=852460)
     * [Microsoft JDBC Driver 6.0 para SQL Server](http://go.microsoft.com/fwlink/?linkid=841535)
     * [Microsoft JDBC Driver 4.2 para SQL Server](http://go.microsoft.com/fwlink/?linkid=841534) 
     * [Microsoft JDBC Driver 4.1 para SQL Server](http://go.microsoft.com/fwlink/?linkid=841533) 
  
-   Java Runtime Environment  
  
## <a name="java-runtime-environment-requirements"></a>Requisitos do Java Runtime Environment  
 Começando com o Microsoft JDBC Driver 6.4 para SQL Server, Sun Java SE Development Kit (JDK) 9.0 e 9.0 do Java Runtime Environment (JRE) têm suporte.

 Começando com o 4.2 do Microsoft JDBC Driver para SQL Server, Sun Java SE Development Kit (JDK) 8.0 e Java Runtime Environment (JRE) 8.0 que têm suporte. Suporte para a API de especificação do Java Database Connectivity (JDBC) foi estendido para incluir a API do JDBC 4.1 e 4.2.  
  
 A partir do Microsoft JDBC Driver 4.1 para o SQL Server, o Sun Java SE Development Kit (JDK) 7.0 e Java Runtime Environment (JRE) 7.0 têm suporte.  
  
 Começando com o [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], o suporte do driver JDBC para API da especificação do Java Database Connectivity (JDBC) foi estendido para incluir a API do JDBC 4.0. A API do JDBC 4.0 foi introduzida como parte do Sun Java SE Development Kit (JDK) 6.0 e do JRE (Java Runtime Environment) 6.0. O JDBC 4.0 é um superconjunto da API do JDBC 3.0.  
  
 Quando você implanta o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] em sistemas operacionais Windows e UNIX, você deve usar os pacotes de instalação, *sqljdbc\<versão > _enu.exe* e *sqljdbc\<versão > _ ENU.tar.gz*, respectivamente. Para obter mais informações sobre como implantar o Driver JDBC, consulte [Implantando o Driver JDBC](../../connect/jdbc/deploying-the-jdbc-driver.md) tópico.  
  
**Microsoft JDBC Driver 6.4 para SQL Server:**  

  O JDBC Driver 6.4 inclui três bibliotecas de classe JAR em cada pacote de instalação: **mssql-jdbc-6.4.0.jre7.jar**, **mssql-jdbc-6.4.0.jre8.jar**, e **mssql-jdbc-6.4.0.jre9.jar** .

  O JDBC Driver 6.4 foi projetado para trabalhar com e suporte por todos os principais Sun máquinas virtuais Java equivalentes, mas é testado no Sun JRE 7.0, 8.0 e 9.0.
  
  O exemplo a seguir resume o suporte fornecido pelos três arquivos JAR incluídos com o Microsoft JDBC Drivers 6.4 para SQL Server:  
  
  |JAR|Conformidade de versão do JDBC|Versão do Java recomendada|Description|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-6.4.0.jre7.jar|4.1|7|Requer um Java Runtime Environment (JRE) 7.0. Usando o JRE 6.0 ou inferior lança uma exceção.<br /><br /> Novos recursos no 6.4 incluem: autenticação do AD do Azure para o Linux, o método de senha do Principal para o Kerberos, a detecção automática de TERRITÓRIO no SPN para autenticação de domínio cruzado, delegação restrita de Kerberos, o tempo limite da consulta, o tempo limite do soquete e preparada reutilização de identificador de instrução. |  
|mssql-jdbc-6.4.0.jre8.jar|4.2|8|Requer um Java Runtime Environment (JRE) 8.0. Usando o JRE 7.0 ou inferior lança uma exceção.<br /><br /> Novos recursos no 6.4 incluem: autenticação do AD do Azure para o Linux, o método de senha do Principal para o Kerberos, a detecção automática de TERRITÓRIO no SPN para autenticação de domínio cruzado, delegação restrita de Kerberos, o tempo limite da consulta, o tempo limite do soquete e preparada reutilização de identificador de instrução. |    
|mssql-jdbc-6.4.0.jre9.jar|4.3|9|Requer um Java Runtime Environment (JRE) 9.0. Usando o JRE 8.0 ou inferior lança uma exceção.<br /><br /> Novos recursos no 6.4 incluem: autenticação do AD do Azure para o Linux, o método de senha do Principal para o Kerberos, a detecção automática de TERRITÓRIO no SPN para autenticação de domínio cruzado, delegação restrita de Kerberos, o tempo limite da consulta, o tempo limite do soquete e preparada reutilização de identificador de instrução. |    


  O JDBC Driver 6.4 também está disponível no repositório Central Maven e pode adicionado a um projeto de Maven adicionando o código a seguir o POM. XML 
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.4.0.jre9</version>
</dependency>
```    
**Microsoft JDBC Driver 6.2 para SQL Server:**  
  
  O JDBC Driver 6.2 inclui duas bibliotecas de classes JAR em cada pacote de instalação: **mssql-jdbc-6.2.1.jre7.jar**, e **mssql-jdbc-6.2.1.jre8.jar**. 
  
 O JDBC Driver 6.2 foi projetado para trabalhar com e suporte por todos os principais Sun máquinas virtuais Java equivalentes, mas é testado no Sun JRE 5.0, 6.0, 7.0 e 8.0. 
  
 O exemplo a seguir resume o suporte fornecido pelos dois arquivos JAR incluídos com o Microsoft JDBC Drivers 6.0 e 4.2 para SQL Server:  
  
|JAR|Conformidade de versão do JDBC|Versão do Java recomendada|Description|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-6.2.1.jre7.jar|4.1|7|Requer um Java Runtime Environment (JRE) 7.0. Usando o JRE 6.0 ou inferior lança uma exceção.<br /><br /> Novos recursos no 6.2 incluem: autenticação do AD do Azure para o Linux, o método de senha do Principal para o Kerberos, a detecção automática de TERRITÓRIO no SPN para autenticação de domínio cruzado, delegação restrita de Kerberos, o tempo limite da consulta, o tempo limite do soquete e preparada Identificador de instrução usar novamente. |  
|mssql-jdbc-6.2.1.jre8.jar|4.2|8|Requer um Java Runtime Environment (JRE) 8.0. Usando o JRE 7.0 ou inferior lança uma exceção.<br /><br /> Novos recursos no 6.2 incluem: autenticação do AD do Azure para o Linux, o método de senha do Principal para o Kerberos, a detecção automática de TERRITÓRIO no SPN para autenticação de domínio cruzado, delegação restrita de Kerberos, o tempo limite da consulta, o tempo limite do soquete e preparada reutilização do identificador de instrução|    

  O JDBC Driver 6.2 também está disponível no repositório Central Maven e pode adicionado a um projeto de Maven adicionando o código a seguir o POM. XML 
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```    

 **Microsoft JDBC Driver 6.0 e 4.2 para SQL Server:**  
  
  Os Drivers JDBC 6.0 e 4.2 incluem duas bibliotecas de classes JAR em cada pacote de instalação: **sqljdbc41.jar**, e **sqljdbc42.jar**. 
  
 Os Drivers JDBC 6.0 e 4.2 são projetados para trabalhar com e suporte por todos os principais Sun máquinas virtuais Java equivalentes, mas é testado no Sun JRE 5.0, 6.0, 7.0 e 8.0. 
  
 O exemplo a seguir resume o suporte fornecido pelos dois arquivos JAR incluídos com o Microsoft JDBC Drivers 6.0 e 4.2 para SQL Server:  
  
|JAR|Conformidade de versão do JDBC|Versão do Java recomendada|Description|  
|---------|-----------------------------|----------------------|-----------------|   
|sqljdbc41.jar|4.1|7|Requer um Java Runtime Environment (JRE) 7.0. Usando o JRE 6.0 ou inferior lança uma exceção.<br /><br /> Os novos recursos em pacotes 4.2 & 6.0 incluem: conformidade JDBC 4.1 e cópia em massa<br /><br /> Além disso, os novos recursos no pacote 6.0 incluem: sempre criptografado, parâmetros com valor de tabela, autenticação do Azure Active Directory, conexões transparentes para grupos de disponibilidade AlwaysOn, aperfeiçoamento na recuperação de metadados de parâmetro para preparado consultas e o nome de domínio internacionalizado (IDN)|  
|sqljdbc42.jar|4.2|8|Requer um Java Runtime Environment (JRE) 8.0. Usando o JRE 7.0 ou inferior lança uma exceção.<br /><br /> Os novos recursos em pacotes 4.2 & 6.0 incluem: conformidade JDBC 4.1, conformidade JDBC 4.2 e cópia em massa<br /><br /> Além disso, os novos recursos no pacote 6.0 incluem: sempre criptografado, parâmetros com valor de tabela, autenticação do Azure Active Directory, conexões transparentes para grupos de disponibilidade AlwaysOn, aperfeiçoamento na recuperação de metadados de parâmetro para preparado consultas e o nome de domínio internacionalizado (IDN)|  
  
 **Microsoft JDBC Driver 4.1 para SQL Server:**  
  
 O JDBC Driver 4.1 inclui uma biblioteca de classes JAR em cada pacote de instalação: **sqljdbc41.jar**.  
    
|JAR|Description|  
|---------|-----------------|  
|sqljdbc41.jar|**sqljdbc41.jar** biblioteca de classes dá suporte para a API do JDBC 4.0. Ela inclui todos os recursos do driver JDBC 4.0, bem como os métodos da API do JDBC 4.0. Não há suporte para JDBC 4.1 (lança uma exceção "SQLFeatureNotSupportedException").<br /><br /> **sqljdbc41.jar** biblioteca de classes requer um Java Runtime Environment (JRE) 7.0. Usando **sqljdbc41.jar** JRE 6.0 e 5.0 lançará uma exceção.<br /><br /> 
  
 Observe que o JDBC driver foi projetado para funcionar (e ter o devido suporte) em todas as principais máquinas virtuais Java equivalentes a Sun, mas é testado no Sun JRE 5.0, 6.0 e 7.0.  
  
 A seguir resume o suporte fornecido pelo arquivo JAR incluído com o Microsoft JDBC Driver 4.1 para SQL Server.  
  
|JAR|Versão JDBC|JRE (pode ser executado)|JDK (pode ser compilado)|  
|---------|------------------|---------------------|-------------------------|   
|sqljdbc41.jar|4|7|7 6 5|  
  
## <a name="sql-server-requirements"></a>Requisitos do SQL Server  
 O driver JDBC oferece suporte a conexões de banco de dados do SQL Azure e SQL Server. Para o Microsoft JDBC Driver 4.2 e 4.1 para SQL Server, o suporte começa com o SQL Server 2008.
  
## <a name="operating-system-requirements"></a>Requisitos do sistema operacional  
 O driver JDBC foi desenvolvido para funcionar em qualquer sistema operacional que ofereça suporte ao uso de uma JVM (Máquina Virtual Java). Porém, só os sistemas operacionais Sun Solaris, SUSE Linux e Windows foram testados oficialmente.  
  
## <a name="supported-languages"></a>Idiomas com suporte  
 O driver JDBC oferece suporte a todos os [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] agrupamentos de coluna. Para obter mais informações sobre os agrupamentos com suporte pelo driver JDBC, consulte [recursos internacionais do JDBC Driver](../../connect/jdbc/international-features-of-the-jdbc-driver.md).  
  
 Para obter mais informações sobre agrupamentos, consulte "Trabalhando com agrupamentos" [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Manuais Online.  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral do JDBC Driver](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
