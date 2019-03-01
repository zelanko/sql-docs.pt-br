---
title: Extensão da linguagem Java no SQL Server 2019 - serviços do SQL Server Machine Learning
description: Instalar, configurar e validar a extensão da linguagem Java em SQL Server de 2019 para sistemas Linux e Windows.
ms.prod: sql
ms.technology: machine-learning
ms.date: 02/28/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a18886ea4daff3fb87853a556b67ad0562c2efd3
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57017832"
---
# <a name="java-language-extension-in-sql-server-2019"></a>Extensão da linguagem Java no SQL Server 2019 

Na visualização de 2019 do SQL Server no Windows e Linux, você pode executar código Java personalizado [estrutura de extensibilidade](../concepts/extensibility-framework.md) como um complemento para a instância do mecanismo de banco de dados. 

A estrutura de extensibilidade é uma arquitetura para a execução de código externo: Java (começando no SQL Server 2019), [Python (a partir do SQL Server 2017)](../concepts/extension-python.md), e [R (a partir do SQL Server 2016)](../concepts/extension-r.md). Execução de código é isolada de processos do mecanismo de core, mas totalmente integrada com a execução da consulta do SQL Server. Isso significa que você pode enviar dados de qualquer consulta do SQL Server para o tempo de execução externo e consumir ou manter os resultados de volta no SQL Server.

Assim como acontece com qualquer extensão de linguagem de programação, o sistema de procedimento armazenado [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) é a interface para a execução de código previamente compilado do Java.

<a name="prerequisites"></a>

## <a name="prerequisites"></a>Prerequisites

Uma instância do SQL Server 2019 preview é necessária. Versões anteriores não têm integração Java.

Há suporte para o Java 8. O Java Runtime Environment (JRE) é o requisito mínimo, mas JDKs são úteis se você precisar que o compilador Java ou os pacotes de desenvolvimento. Porque o JDK está completa, se você instalar o JDK, JRE não é necessário.

Você pode usar sua distribuição preferencial do Java 8. Abaixo estão as duas distribuições sugeridas:

| Distribuição | Versão do Java | Sistemas operacionais | JDK | JRE |
|-|-|-|-|-|
| [Oracle Java SE](https://www.oracle.com/technetwork/java/javase/downloads/index.html) | 8 | Windows e Linux | Sim | Sim |
| [Zulu OpenJDK](https://www.azul.com/downloads/zulu/) | 8 | Windows e Linux | Sim | Não |

No Linux, o **mssql-server-extensibilidade-java** pacote instala automaticamente o JRE 8 se ele não ainda estiver instalado. Scripts de instalação também adicionam o caminho da JVM para uma variável de ambiente chamada JAVA_HOME.

No Windows, é recomendável instalar o JDK em padrão `/Program Files/` pasta se possível. Caso contrário, a configuração adicional é necessário para conceder permissões para arquivos executáveis. Para obter mais informações, consulte o [conceder permissões (Windows)](#perms-nonwindows) seção neste documento.

> [!Note]
> Considerando que é compatível com Java, versões anteriores podem funcionar, mas a versão testada e com suporte para esta versão antecipada do CTP é Java 8. 

<a name="install-on-linux"></a>

## <a name="install-on-linux"></a>Instalar no Linux

Você pode instalar o [banco de dados mecanismo e a extensão de Java juntos](../../linux/sql-server-linux-setup-machine-learning.md#install-all), ou adicionar suporte a Java em uma instância existente. Os exemplos a seguir adicionar a extensão de Java a uma instalação existente.  

```bash
# RedHat install commands
sudo yum install mssql-server-extensibility-java

# Ubuntu install commands
sudo apt-get install mssql-server-extensibility-java

# SUSE install commands
sudo zypper install mssql-server-extensibility-java
```

Quando você instala **mssql-server-extensibilidade-java**, o pacote instala automaticamente o JRE 8 se ele não ainda estiver instalado. Ele também adicionará o caminho da JVM para uma variável de ambiente chamada JAVA_HOME.

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

1. Certifique-se de que uma versão compatível do Java está instalada. Para obter mais informações, consulte o [pré-requisitos](#prerequisites).

2. [Execute a instalação](../install/sql-machine-learning-services-windows-install.md) para instalar o SQL Server de 2019.

3. Quando você chega à seleção de recursos, escolha **serviços de Machine Learning (no banco de dados)**. 

   Embora a integração do Java não vem com bibliotecas de aprendizado de máquina, essa é a opção no programa de instalação fornece a estrutura de extensibilidade. Você pode omitir o R e Python, se desejar.

4. Conclua o Assistente de instalação e, em seguida, continue com as próximas duas tarefas.

### <a name="add-the-javahome-variable"></a>Adicione a variável JAVA_HOME

JAVA_HOME é uma variável de ambiente que especifica o local do interpretador de Java. Nesta etapa, crie uma variável de ambiente do sistema para ele no Windows.

1. Localize e copie o caminho do JDK/JRE (por exemplo, `C:\Program Files\Java\jdk1.8.0_201`).

    Dependendo de sua distribuição preferencial do Java, o local do JDK ou JRE pode ser diferente do exemplo de caminho acima.

2. No painel de controle, abra **sistema e segurança**, abra **sistema**e clique em **propriedades avançadas do sistema**.

3. Clique em **variáveis de ambiente**.

4. Criar uma nova variável de sistema para `JAVA_HOME` com o valor do caminho do JDK/JRE (encontrado na etapa 1).

5. Reinicie [Launchpad](../concepts/extensibility-framework.md#launchpad).

    1. Abra [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md).

    2. Em serviços do SQL Server, o Launchpad do SQL Server com o botão direito e selecione **reiniciar**.

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

## <a name="differences-in-ctp-23"></a>Diferenças no CTP 2.3

Se você já estiver familiarizado com os serviços de aprendizado de máquina, o modelo de autorização e isolamento para extensões foi alterado nesta versão. Para obter mais informações, consulte [diferenças em uma instalação de serviços do SQL Server Machine 2019 Learning](../install/sql-machine-learning-services-ver15.md).

## <a name="limitations-in-ctp-23"></a>Limitações no CTP 2.3

* O número de valores nos buffers de entrada e saídas não pode exceder `MAX_INT (2^31-1)` , já que é o número máximo de elementos que podem ser alocados em uma matriz em Java.

* Parâmetros de saída [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) não têm suporte nesta versão.

* Transmissão usando o parâmetro de sp_execute_external_script @r_rowsPerRead não tem suporte neste CTP.

* Particionamento usando o parâmetro de sp_execute_external_script @input_data_1_partition_by_columns não tem suporte neste CTP.

<a name="create-jar"></a>

## <a name="how-to-create-a-jar-file-from-class-files"></a>Como criar um arquivo jar de arquivos de classe

Navegue até a pasta que contém o arquivo de classe e execute este comando:

```cmd
jar -cf <MyJar.jar> *.class
```

Verifique se o caminho para **jar.exe** faz parte da variável de caminho do sistema. Como alternativa, especifique o caminho completo para o jar que pode ser encontrado em /bin na pasta do JDK: `C:\Users\MyUser\Desktop\jdk1.8.0_201\bin\jar -cf <MyJar.jar> *.class`

## <a name="next-steps"></a>Próximas etapas

+ [Como chamar o Java no SQL Server](howto-call-java-from-sql.md)
+ [Exemplo de Java no SQL Server](java-first-sample.md)
+ [Tipos de dados Java e o SQL Server](java-sql-datatypes.md)