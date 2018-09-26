---
title: Extensão da linguagem Java no SQL Server 2019 | Microsoft Docs
description: Execute o código Java em 2019 do SQL Server usando a extensão da linguagem Java.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/24/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8acb0a72435306cdec8740ffb41ff499eea61fac
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2018
ms.locfileid: "46714839"
---
# <a name="java-language-extension-in-sql-server-2019"></a>Extensão da linguagem Java no SQL Server 2019 

A partir do SQL Server 2019, você pode executar código Java personalizado [estrutura de extensibilidade](../concepts/extensibility-framework.md) como um complemento para a instância do mecanismo de banco de dados. 

A estrutura de extensibilidade é uma arquitetura para a execução de código externo: Java (começando no SQL Server 2019), [Python (a partir do SQL Server 2017)](../concepts/extension-python.md), e [R (a partir do SQL Server 2016)](../concepts/extension-r.md). Execução de código é isolada de processos do mecanismo de core, mas totalmente integrada com a execução da consulta do SQL Server. Isso significa que você pode enviar dados de qualquer consulta do SQL Server para o tempo de execução externo e consumir ou manter os resultados de volta no SQL Server.

Assim como acontece com qualquer extensão de linguagem de programação, o sistema de procedimento armazenado [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) é a interface para a execução de código previamente compilado do Java.

## <a name="1---feature-installation"></a>1 - instalação de recurso

Execute a instalação do SQL Server de 2019 no Windows ou Linux para instalar a extensão da linguagem Java. Uma instância do mecanismo de banco de dados SQL Server 2019 é necessária. Você não pode adicionar integração Java para versões anteriores.

No Windows, inicie o [Assistente de instalação](../install/sql-machine-learning-services-windows-install.md). Na seleção de recursos, selecione **serviços de Machine Learning (no banco de dados)**. Embora a integração do Java não vem com bibliotecas de aprendizado de máquina, essa é a opção no programa de instalação fornece a estrutura de extensibilidade. Você pode omitir o R e Python, se desejar.

No Linux, instale o [mecanismo de banco de dados](https://docs.microsoft.com/sql/linux/sql-server-linux-setup), bem como o [pacote de extensibilidade e pacote de extensão Java](../../linux/sql-server-linux-setup-machine-learning.md).

Os exemplos a seguir ilustram a sintaxe para cada sistema de operacional Linux.

```bash
# RedHat install commands
sudo yum install mssql-server-extensibility
sudo yum install mssql-server-extensibility-java

# Ubuntu install commands
sudo apt-get install mssql-server-extensibility
sudo apt-get install mssql-server-extensibility-java

# USE install commands
sudo zypper install mssql-server-extensibility
sudo zypper install mssql-server-extensibility-java
```

## <a name="2---configuration"></a>2 - configuração

Usando o SQL Server Management Studio ou outra ferramenta que executa o script Transact-SQL, configure a execução do script externo na instância do mecanismo de banco de dados.

  ```sql
  EXEC sp_configure 'external scripts enabled', 1
  RECONFIGURE WITH OVERRIDE
-- No restart is required after this step as of SQl Server 2019
 ```

## <a name="3---bring-your-own-java"></a>3 - traga seu próprio código Java

Uma diferença de anterior integrações de linguagem como R e Python é que você controle quais JVM é usado com o SQL Server.

| Versão do Java | Sistema Operacional |
|--------------|------------------|
| [1.10 do Java](http://jdk.java.net/10/)   | Windows |
| Java 1.8   | Linux | 

Considerando que é compatível com Java, versões anteriores podem funcionar, mas as versões com suporte e testadas para esta versão antecipada do CTP estão listadas na tabela.

> [!Note]
>Para executar o Java com o SQL Server, tecnicamente precisar apenas o [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre10-downloads-4417026.html) instalado (JRE). O JDK é um desenvolvimento de kit, incluindo o compilador Java e outro desenvolvimento relacionados de pacotes. Se você já tiver um ambiente de desenvolvimento e só precisa de um tempo de execução Java na máquina do servidor, você pode ignorar as instruções de instalação do JDK e apenas instalar o JRE.

## <a name="jdk-on-windows"></a>JDK no Windows

Baixe a versão do Windows do [Java SE Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk10-downloads-4416644.html).

Instalar o JDK em arquivos /Program padrão / leitura de pasta se você quiser evitar a necessidade de conceder a permissão para **todos os pacotes de aplicativos** e o **SQLRUserGroup** grupos de segurança em um local alternativo . A mesma diretriz se aplica para o acesso a suas pastas de classpath de Java, onde você mantém seus arquivos. class ou. jar. 

> [!Note]
> O modelo de autorização e isolamento para extensões foi alterado nesta versão. Para obter mais informações, consulte [diferenças em uma instalação de serviços do SQL Server Machine 2019 Learning](../install/sql-machine-learning-services-ver15.md).

<a name="perms-nonwindows"></a>

### <a name="grant-access-to-non-default-jdk-folder-windows-only"></a>Conceder acesso a pasta do JDK de não-padrão (somente Windows)

Você pode ignorar esta etapa se você tiver instalado o JDK/JRE na pasta padrão. Para uma instalação de pasta não padrão, execute os seguintes scripts de PowerShell para conceder acesso para o **SQLRUsergroup** e contas de serviço do SQL Server (em ALL_APPLICATION_PACKAGES) para acessar o JVM e o classpath de Java.

#### <a name="sqlrusergroup-permissions"></a>Permissões de SQLRUserGroup

```powershell
$Acl = Get-Acl "<YOUR PATH TO JDK / CLASSPATH>"
$Ar = New-Object  system.security.accesscontrol.filesystemaccessrule("SQLRUsergroup","FullControl","Allow")
$Acl.SetAccessRule($Ar)
Set-Acl ""<YOUR PATH TO JDK / CLASSPATH>" $Acl 
```

#### <a name="appcontainer-permissions"></a>Permissões do AppContainer

```powershell
$Acl = Get-Acl "<YOUR PATH TO JDK / CLASSPATH>" 
$Ar = New-Object  system.security.accesscontrol.filesystemaccessrule("ALL APPLICATION PACKAGES","FullControl","Allow") 
$Acl.SetAccessRule($Ar) 
Set-Acl "<YOUR PATH TO JDK / CLASSPATH>" $Acl 
```

### <a name="add-the-jdk-path-to-javahome"></a>Adicione o caminho do JDK para JAVA_HOME
Você também precisa adicionar o caminho de instalação do JDK/JRE (por exemplo, "C:\Program Files\Java\jdk-10.0.2") a uma variável de ambiente do sistema que você nomeie "JAVA_HOME". 

Para criar uma variável de sistema, use o painel de controle > sistema e segurança > sistema acessem **propriedades avançadas do sistema**. Clique em **variáveis de ambiente** e, em seguida, crie uma nova variável de sistema para JAVA_HOME.

![Variável de ambiente para o início do Java](../media/java/env-variable-java-home.png "de instalação para Java")

## <a name="jdk-on-linux"></a>JDK no Linux

No Linux, o pacote mssql-server-extensibilidade-java instala automaticamente JRE 1.8 se ele não ainda estiver instalado. Ele também adicionará o caminho da JVM para uma variável de ambiente chamada JAVA_HOME.

## <a name="limitations-in-ctp-20"></a>Limitações no CTP 2.0

* O número de valores nos buffers de entrada e saídas não pode exceder `MAX_INT (2^31-1)` , já que é o número máximo de elementos que podem ser alocados em uma matriz em Java.

* Não há suporte para parâmetros de saída em sp_execute_external_script nesta versão.

* Não há suporte de tipo de dados LOB para conjuntos de dados de entrada e saída nesta versão. Ver [tipos de dados Java e o SQL Server](java-sql-datatypes.md) para obter detalhes sobre quais dados os tipos têm suporte neste CTP.

* Transmissão usando o parâmetro de sp_execute_external_script @r_rowsPerRead não tem suporte neste CTP.

* Particionamento usando o parâmetro de sp_execute_external_script @input_data_1_partition_by_columns não tem suporte neste CTP.

## <a name="next-steps"></a>Próximas etapas

+ [Como chamar o Java no SQL Server](howto-call-java-from-sql.md)
+ [Exemplo de Java no SQL Server](java-first-sample.md)
+ [Tipos de dados Java e o SQL Server](java-sql-datatypes.md)