---
title: Extensão da linguagem Java no SQL Server 2019 - serviços do SQL Server Machine Learning
description: Instalar, configurar e validar a extensão da linguagem Java em SQL Server de 2019 para sistemas Linux e Windows.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/07/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a258573ff7506f2533c2f91edb5751cfd1121dc8
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/15/2018
ms.locfileid: "53431709"
---
# <a name="java-language-extension-in-sql-server-2019"></a>Extensão da linguagem Java no SQL Server 2019 

Na visualização de 2019 do SQL Server no Windows e Linux, você pode executar código Java personalizado [estrutura de extensibilidade](../concepts/extensibility-framework.md) como um complemento para a instância do mecanismo de banco de dados. 

A estrutura de extensibilidade é uma arquitetura para a execução de código externo: Java (começando no SQL Server 2019), [Python (a partir do SQL Server 2017)](../concepts/extension-python.md), e [R (a partir do SQL Server 2016)](../concepts/extension-r.md). Execução de código é isolada de processos do mecanismo de core, mas totalmente integrada com a execução da consulta do SQL Server. Isso significa que você pode enviar dados de qualquer consulta do SQL Server para o tempo de execução externo e consumir ou manter os resultados de volta no SQL Server.

Assim como acontece com qualquer extensão de linguagem de programação, o sistema de procedimento armazenado [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) é a interface para a execução de código previamente compilado do Java.

## <a name="prerequisites"></a>Prerequisites

Uma instância do SQL Server 2019 preview é necessária. Versões anteriores não têm integração Java. 

Requisitos de versão de Java variam entre Windows e Linux. O Java Runtime Environment (JRE) é o requisito mínimo, mas JDKs são úteis se você precisar que o compilador Java ou os pacotes de desenvolvimento. Porque o JDK está completa, se você instalar o JDK, JRE não é necessário.

| Sistema operacional | Versão do Java | Download do JRE | Download do JDK |
|------------------|--------------|--------------|--------------|
| Windows          | 1.10         | [JRE 10](https://www.oracle.com/technetwork/java/javase/downloads/jre10-downloads-4417026.html) | [JDK 10](https://www.oracle.com/technetwork/java/javase/downloads/jdk10-downloads-4416644.html)  |
| Linux            | 1.8          |  [JRE 8](https://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) | [JDK 8](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)  |  

No Linux, o **mssql-server-extensibilidade-java** pacote instala automaticamente o JRE 1.8 se não ainda estiver instalado. Scripts de instalação também adicionam o caminho da JVM para uma variável de ambiente chamada JAVA_HOME.

No Windows, é recomendável instalar o JDK em padrão /Program arquivos / pasta se possível. Caso contrário, a configuração adicional é necessário para conceder permissões para arquivos executáveis. Para obter mais informações, consulte o [conceder permissões (Windows)](#perms-nonwindows) seção neste documento.

> [!Note]
> Considerando que é compatível com Java, versões anteriores podem funcionar, mas as versões com suporte e testadas para esta versão antecipada do CTP estão listadas na tabela.

<a name="install-on-linux"></a>

## <a name="install-on-linux"></a>Instalar no Linux

Você pode instalar o [banco de dados mecanismo e a extensão de Java juntos](../../linux/sql-server-linux-setup-machine-learning.md#install-all), ou adicionar suporte a Java em uma instância existente. Os exemplos a seguir adicionar a extensão de Java a uma instalação existente.  

```bash
# RedHat install commands
sudo yum install mssql-server-extensibility-java

# Ubuntu install commands
sudo apt-get install mssql-server-extensibility-java

# USE install commands
sudo zypper install mssql-server-extensibility-java
```

Quando você instala **mssql-server-extensibilidade-java**, o pacote instala automaticamente o JRE 1.8 se não ainda estiver instalado. Ele também adicionará o caminho da JVM para uma variável de ambiente chamada JAVA_HOME.

Depois de concluir a instalação, a próxima etapa é [configurar a execução do script externo](#configure-script-execution).

> [!Note]
> Em um dispositivo conectado à internet, as dependências de pacote são baixadas e instaladas como parte da instalação do pacote principal. Para obter mais detalhes, incluindo a instalação offline, consulte [instalar o aprendizado de máquina do SQL Server no Linux](../../linux/sql-server-linux-setup-machine-learning.md).

### <a name="grant-permissions-on-linux"></a>Conceder permissões no Linux

Para fornecer permissões para executar as classes Java do SQL Server, você precisará definir permissões.

Para conceder a leitura e acesso para arquivos ou arquivos de classe jar de execução, execute o seguinte **chmod** comando em cada arquivo de classe ou jar. É recomendável colocar seus arquivos de classe em um jar ao trabalhar com o SQL Server. Para obter ajuda na criação de um jar, consulte [como criar um arquivo jar](#create-jar).

```cmd
chmod ug+rx <MyJarFile.jar>
```
Você também precisará conceder permissões de mssql_satellite no arquivo jar ou de diretório para leitura/execução.

* Se você estiver chamando os arquivos de classe do SQL Server, mssql_satellite precisa ler/executará as permissões no *cada* diretório na hierarquia de pastas da raiz até o pai direto.

* Se você estiver chamando um arquivo jar do SQL Server, é suficiente para executar o comando no próprio arquivo jar.

```cmd
chown mssql_satellite:mssql_satellite <directory>
```

```cmd
chown mssql_satellite:mssql_satellite <MyJarFile.jar>
```

<a name="install-on-windows"></a>

## <a name="install-on-windows"></a>Instalar no Windows

1. [Execute a instalação](../install/sql-machine-learning-services-windows-install.md) para instalar o SQL Server de 2019.

2. Quando você chega à seleção de recursos, escolha **serviços de Machine Learning (no banco de dados)**. 

   Embora a integração do Java não vem com bibliotecas de aprendizado de máquina, essa é a opção no programa de instalação fornece a estrutura de extensibilidade. Você pode omitir o R e Python, se desejar.

3. Conclua o Assistente de instalação e, em seguida, continue com as próximas duas tarefas.

### <a name="add-the-javahome-variable"></a>Adicione a variável JAVA_HOME

JAVA_HOME é uma variável de ambiente que especifica o local do interpretador de Java. Nesta etapa, crie uma variável de ambiente do sistema para ele no Windows.

1. Localize e copie o caminho de instalação do JDK/JRE (por exemplo, C:\Program Files\Java\jdk-10.0.2).

  No CTP 2.0, definir JAVA_HOME para a pasta base do jdk funciona somente para Java 1.10. 

  Para Java 1.8, estender o caminho para alcançar o jvm.dll no Windows no seu JDK (por exemplo, "C:\Program Files\Java\jdk1.8.0_181\bin\server". Como alternativa, você pode apontar para uma pasta base do JRE: "C:\Program Files\Java\jre1.8.0_181".

2. No painel de controle, abra **sistema e segurança**, abra **sistema**e clique em **propriedades avançadas do sistema**.

3. Clique em **variáveis de ambiente**.

4. Crie uma nova variável de sistema para JAVA_HOME.

   ![Variável de ambiente para o início do Java](../media/java/env-variable-java-home.png "de instalação para Java")

<a name="perms-nonwindows"></a>

### <a name="grant-access-to-non-default-jdk-folder-windows-only"></a>Conceder acesso a pasta do JDK de não-padrão (somente Windows)

Você pode ignorar esta etapa se você tiver instalado o JDK/JRE na pasta padrão. 

Para uma instalação de pasta não padrão, execute as **icacls** comandos de um *com privilégios elevados* linha para conceder acesso ao **SQLRUsergroup** e contas de serviço do SQL Server (no  **ALL_APPLICATION_PACKAGES**) para acessar o JVM e o classpath de Java. Os comandos serão recursivamente conceder acesso a todos os arquivos e pastas no caminho de diretório especificado.

#### <a name="sqlrusergroup-permissions"></a>Permissões de SQLRUserGroup

Para uma instância nomeada, acrescente o nome de instância ao SQLRUsergroup (por exemplo, `SQLRUsergroupINSTANCENAME`).

```cmd
icacls "<PATH TO CLASS or JAR FILES>" /grant "SQLRUsergroup":(OI)(CI)RX /T
```

#### <a name="appcontainer-permissions"></a>Permissões do AppContainer

```cmd
icacls "PATH to JDK/JRE" /grant "ALL APPLICATION PACKAGES":(OI)(CI)RX /T
```

### <a name="add-the-jre-path-to-javahome"></a>Adicionar o caminho do JRE JAVA_HOME
Você também precisará adicionar o caminho para o JRE na variável de ambiente JAVA_HOME do sistema. Se você tiver apenas um JRE instalado, você pode fornecer o caminho da pasta JRE. No entanto, se você tiver um JDK instalado, você precisará fornecer o caminho completo para a JVM, na pasta do JRE em JDK, como este: "C:\Program Files\Java\jdk1.8.0_191\jre\bin\server".

Para criar uma variável de sistema, use o painel de controle > sistema e segurança > sistema acessem **propriedades avançadas do sistema**. Clique em **variáveis de ambiente** e, em seguida, crie uma nova variável de sistema para JAVA_HOME.

![Variável de ambiente para o início do Java](../media/java/env-variable-java-home.png "de instalação para Java")

<a name="configure-script-execution"></a>

## <a name="configure-script-execution"></a>Configurar a execução do script

Neste ponto, você está quase pronto para executar o código Java no Linux ou Windows. Como última etapa, alterne para o SQL Server Management Studio ou outra ferramenta que executa o script Transact-SQL para habilitar a execução do script externo.

  ```sql
  EXEC sp_configure 'external scripts enabled', 1
  RECONFIGURE WITH OVERRIDE
-- No restart is required after this step as of SQl Server 2019
 ```

## <a name="verify-installation"></a>Verifique a instalação

Para confirmar a instalação está funcionando, criar e executar uma [aplicativo de exemplo](java-first-sample.md) usando o JDK que você acabou de instalar, colocar os arquivos no caminho de classe que você configurou anteriormente.

## <a name="differences-in-ctp-20"></a>Diferenças no CTP 2.0

Se você já estiver familiarizado com os serviços de aprendizado de máquina, o modelo de autorização e isolamento para extensões foi alterado nesta versão. Para obter mais informações, consulte [diferenças em uma instalação de serviços do SQL Server Machine 2019 Learning](../install/sql-machine-learning-services-ver15.md).

## <a name="limitations-in-ctp-20"></a>Limitações no CTP 2.0

* O número de valores nos buffers de entrada e saídas não pode exceder `MAX_INT (2^31-1)` , já que é o número máximo de elementos que podem ser alocados em uma matriz em Java.

* Parâmetros de saída [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) não têm suporte nesta versão.

* Não há suporte de tipo de dados LOB para conjuntos de dados de entrada e saída nesta versão. Ver [tipos de dados Java e o SQL Server](java-sql-datatypes.md) para obter detalhes sobre quais dados os tipos têm suporte neste CTP.

* Transmissão usando o parâmetro de sp_execute_external_script @r_rowsPerRead não tem suporte neste CTP.

* Particionamento usando o parâmetro de sp_execute_external_script @input_data_1_partition_by_columns não tem suporte neste CTP.

<a name="create-jar"></a>

## <a name="how-to-create-a-jar-file-from-class-files"></a>Como criar um arquivo jar de arquivos de classe

Navegue até a pasta que contém o arquivo de classe e execute este comando:

```cmd
jar -cf <MyJar.jar> *.class
```

Verifique se o caminho para **jar.exe** faz parte da variável de caminho do sistema. Como alternativa, especifique o caminho completo para o jar que pode ser encontrado em /bin na pasta do JDK: `C:\Users\MyUser\Desktop\jdk-10.0.2\bin\jar -cf <MyJar.jar> *.class`

## <a name="next-steps"></a>Próximas etapas

+ [Como chamar o Java no SQL Server](howto-call-java-from-sql.md)
+ [Exemplo de Java no SQL Server](java-first-sample.md)
+ [Tipos de dados Java e o SQL Server](java-sql-datatypes.md)