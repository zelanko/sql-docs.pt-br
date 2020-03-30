---
title: Instalar Extensões de Linguagem do SQL Server no Windows
titleSuffix: ''
description: Saiba como instalar as Extensões de Linguagem do SQL Server no Windows.
author: dphansen
ms.author: davidph
ms.date: 11/06/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3e4f3a84e5001d7485ab590a66ee497522042824
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "73658843"
---
# <a name="install-sql-server-language-extensions-on-windows"></a>Instalar Extensões de Linguagem do SQL Server no Windows

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Saiba como instalar o componente de Extensões de Linguagem no SQL Server executando o assistente de instalação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

> [!NOTE]
> Este artigo é para instalação das Extensões de Linguagem do SQL Server no Windows. Para Linux, confira [Instalar as Extensões de Linguagem do SQL Server 2019 (Java) no Linux](https://docs.microsoft.com/sql//linux/sql-server-linux-setup-language-extensions)

<a name="prerequisites"></a> 

## <a name="pre-install-checklist"></a>Lista de verificação pré-instalação

+ A Instalação do SQL Server 2019 será necessária se você desejar instalar o suporte para Extensões de Linguagem.

+ Uma instância do mecanismo de banco de dados é necessária. Você não pode instalar apenas os recursos das Extensões de Linguagem, embora você possa adicioná-los incrementalmente a uma instância existente.

+ Para continuidade de negócios, há suporte para [grupos de disponibilidade Always On](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server) para Extensões de Linguagem. Você precisa instalar extensões de linguagem e configurar pacotes em cada nó.

+ Há suporte para a instalação de Extensões de Linguagem em um cluster de failover no SQL Server 2019.

+ Não instale Extensões de Linguagem do SQL Server em um controlador de domínio. A parte da instalação de Extensões de Linguagem falhará.

+ As Extensões de Linguagem e os [Serviços de Machine Learning](../../advanced-analytics/index.yml) são instalados por padrão em Clusters de Big Data do SQL Server. Se você usar Clusters de Big Data, não precisará seguir as etapas neste artigo. Para obter mais informações, confira [Usar Serviços de Machine Learning (Python e R) em Clusters de Big Data](../../big-data-cluster/machine-learning-services.md).

> [!IMPORTANT]
> Após a conclusão da instalação, conclua as etapas de pós-configuração descritas neste artigo. Essas etapas incluem a habilitação do SQL Server para usar código externo e a adição de contas necessárias para o SQL Server executar o código Java em seu nome. Geralmente, as alterações na configuração exigem uma reinicialização da instância ou do serviço Launchpad.

<a name="java-jre-jdk"></a>

## <a name="java-jre-or-jdk"></a>Java JRE ou JDK

No SQL Server 2019 versão Release Candidate 1, há duas maneiras de instalar e usar o Java com o SQL Server:

1. Usar o runtime do Java padrão, o Zulu Open JRE versão 11.0.3. Há suporte para este runtime e ele é incluído com a instalação do SQL Server.

1. Usar a distribuição Java de sua preferência em vez do runtime do Java padrão.

    No momento, o Java 11 é a versão com suporte no Windows. O JRE (Java Runtime Environment) é o requisito mínimo, mas o JDK (Java Development Kit) será útil se você precisar do compilador e dos pacotes de desenvolvimento Java. Como o JDK é totalmente inclusivo, se você instalar o JDK, o JRE não será necessário. No Windows, recomendamos instalar o JDK na pasta `/Program Files/` padrão, se possível. Caso contrário, será necessária uma configuração adicional para conceder permissões a executáveis. Para obter mais informações, confira a seção [conceder permissões (Windows)](#perms-nonwindows) neste documento.

    > [!NOTE]
    > Considerando que o Java é compatível com versões anteriores, as versões anteriores podem funcionar, mas a versão compatível e testada para a versão Release Candidate 1 é a Java 11.
    
## <a name="get-the-installation-media"></a>Obtenha a mídia de instalação

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

## <a name="run-setup"></a>Executar a instalação

Para instalações locais, você deve executar a Instalação como um administrador. Se você instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura e de execução no compartilhamento remoto.

1. Inicie o assistente de instalação do SQL Server 2019. 
  
2. Na guia **Instalação**, selecione **Nova instalação autônoma do SQL Server ou adicionar recursos a uma instalação existente**.

    ![Instalação do SQL Server 2019](../media/sql-install.png) 

3. Na página **Seleção de Recursos** , selecione estas opções:
  
    - **Serviços do Mecanismo de Banco de Dados**
  
        Para usar as Extensões de Linguagem com o SQL Server, você deverá instalar uma instância do mecanismo de banco de dados. Você pode usar uma instância padrão ou nomeada.
  
    - **Serviços de Machine Learning e Extensões de Linguagem**
  
        Esta opção instala o componente Extensões de Linguagem que dá suporte à execução de código Java.

        - Se você desejar instalar o runtime do Java padrão, o Zulu Open JRE 11.0.3, selecione **Serviços de Machine Learning e Extensões de Linguagem** e **Java**.

        - Se você desejar usar seu próprio runtime do Java, selecione **Serviços de Machine Learning e Extensões de Linguagem**. Não selecione Java.

        Se desejar usar R e Python, confira [Instalar Serviços de Machine Learning do SQL Server no Windows](https://docs.microsoft.com/sql/advanced-analytics/install/sql-machine-learning-services-windows-install).

    ![Opções de recurso para Extensões de Linguagem](../media/sql-install-feature-selection.png)

4. Se você escolher **Java** na etapa anterior para instalar o runtime do Java padrão, a página **Localização de Instalação do Java** será exibida.

    Selecione **Instalar o Open JRE 11.0.3 incluído nesta instalação**.

    ![Escolher a localização de instalação do Java](../media/sql-install-openjdk.png)

    > [!NOTE]
    > **Forneça a localização de uma versão diferente instalada neste computador** não é usado para Extensões de Linguagem.

5. Na página **Pronto para instalar**, verifique se essas seleções estão incluídas e selecione **Instalar**.
  
    + Serviços do Mecanismo de Banco de Dados
    + Serviços de Machine Learning e Extensões de Linguagem

    Observe a localização da pasta no caminho `..\Setup Bootstrap\Log` em que os arquivos de configuração são armazenados. Quando a instalação for concluída, você poderá examinar os componentes instalados no arquivo de Resumo.

6. Após a conclusão da instalação, se você receber instruções para reiniciar o computador, faça-o agora. É importante ler a mensagem do Assistente de Instalação ao concluir a Instalação. Para saber mais, veja [Exibir e ler arquivos de log da Instalação do SQL Server](https://docs.microsoft.com/sql/database-engine/install-windows/view-and-read-sql-server-setup-log-files).

## <a name="add-the-jre_home-variable"></a>Adicionar a variável JRE_HOME

`JRE_HOME` é uma variável de ambiente do sistema que especifica a localização do interpretador de Java. Nesta etapa, crie uma variável de ambiente do sistema para ela no Windows.

1. Localize e copie o caminho inicial do JRE.

    Por exemplo, o caminho inicial do JRE do runtime do Java padrão Zulu JRE 11.0.3 é `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Binn\AZUL-OpenJDK-JRE\`.

    Dependendo do seu caminho de instalação do SQL Server ou se você escolheu outro runtime do Java, sua localização do JDK ou JRE pode ser diferente do caminho de exemplo acima. Mesmo se você tiver um JDK instalado, geralmente você obterá uma subpasta JRE como parte dessa instalação. Portanto, aponte para a pasta do JRE nesse caso. A extensão Java tentará carregar o `jvm.dll` do caminho `%JRE_HOME%\bin\server`.

2. No Painel de Controle, abra **Sistema e Segurança**, abra **Sistema** e clique em **Propriedades Avançadas do Sistema**.

3. Clique em **Variáveis de Ambiente**.

4. Crie uma variável do sistema para `JRE_HOME` com o valor do caminho JDK/JRE (encontrado na etapa 1).

5. Reinicie [Launchpad](../concepts/extensibility-framework.md#launchpad).

    1. Abra o [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md).

    2. Em Serviços do SQL Server, clique com o botão direito do mouse no SQL Server Launchpad e selecione **Reiniciar**.

<a name="perms-nonwindows"></a>

## <a name="grant-access-to-non-default-jre-folder"></a>Permitir acesso a uma pasta JRE não padrão

Se você não instalou o Zulu Open JRE padrão incluído com o SQL Server e não instalou o JDK ou JRE em arquivos de programas, você precisa executar as etapas a seguir. Execute os comandos **icacls** em uma linha *com privilégios elevados* para permitir acesso ao **SQLRUsergroup** e às contas de serviço do SQL Server (em **ALL_APPLICATION_PACKAGES**) para acessar o JRE. Os comandos permitirão recursivamente acesso a todos os arquivos e pastas no caminho de diretório especificado.

1. Conceder permissões SQLRUserGroup

    Para uma instância nomeada, acrescente o nome da instância a SQLRUsergroup (por exemplo, `SQLRUsergroupINSTANCENAME`).

    ```cmd
    icacls "<PATH to JRE>" /grant "SQLRUsergroup":(OI)(CI)RX /T
    ```
    
    Você poderá ignorar esta etapa se tiver instalado o JDK/JRE na pasta padrão em arquivos de programas no Windows.

2. Conceder permissões AppContainer

    ```cmd
    icacls "<PATH to JRE>" /grant "ALL APPLICATION PACKAGES":(OI)(CI)RX /T
    ```
    
## <a name="enable-script-execution"></a>Habilitar a execução do script

1. Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. 

    > [!TIP]
    > Você pode baixar e instalar a versão apropriada nesta página: [Baixe o SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
    > 
    > Você também pode usar o [Azure Data Studio](../../azure-data-studio/what-is.md), que dá suporte a tarefas administrativas e consultas no SQL Server.
  
2. Conecte-se à instância em que você instalou as Extensões de Linguagem, clique em **Nova Consulta** para abrir uma janela de consulta e execute o seguinte comando:

    ```sql
    sp_configure
    ```

    O valor da propriedade `external scripts enabled`, deve ser **0** neste momento. O recurso é desativado por padrão e deve ser habilitado explicitamente por um administrador antes de poder executar o código Java.
    
3.  Para habilitar o recurso de script externo, execute a instrução a seguir:
    
    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
    
    Se você já tiver habilitado o recurso para os Serviços de Machine Learning, não execute a reconfiguração uma segunda vez para as Extensões de Linguagem. A plataforma de extensibilidade subjacente dá suporte a ambos.

## <a name="restart-the-service"></a>Reinicie o serviço.

Quando a instalação for concluída, reinicie o mecanismo de banco de dados antes de passar para a próxima, habilitando a execução do script.

Reiniciar o serviço também reinicia automaticamente o serviço SQL Server Launchpad relacionado.

Você pode reiniciar o serviço usando o clique com o botão direito do mouse no comando **Reiniciar** para a instância no SSMS ou usando o painel **Serviços** no Painel de Controle ou usando o [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md).

<a name="register_external_language"></a>

## <a name="register-external-language"></a>Registrar linguagem externa

Para cada banco de dados no qual você deseja usar extensões de linguagem, é necessário registrar a linguagem externa com [CREATE EXTERNAL LANGUAGE](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql).

O exemplo a seguir adiciona uma linguagem externa chamada Java a um banco de dados no SQL Server no Windows.

```SQL
CREATE EXTERNAL LANGUAGE Java
FROM (CONTENT = N'<path-to-zip>', FILE_NAME = 'javaextension.dll');
GO
```

Para obter mais informações, confira [CREATE EXTERNAL LANGUAGE](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql).

## <a name="verify-installation"></a>Verifique a instalação

Verifique o status de instalação ad instância nos logs de instalação.

Use as etapas a seguir para verificar se todos os componentes usados para iniciar o script externo estão em execução.

1. No SQL Server Management Studio ou o Azure Data Studio, abra uma nova janela de consulta e execute a instrução a seguir:
    
    ```sql
    EXEC sp_configure  'external scripts enabled'
    ```

    O **run_value** agora está definido como 1.
    
2. Abra o painel **Serviços** ou o SQL Server Configuration Manager e verifique se o **serviço SQL Server Launchpad** está em execução. Você deve ter um serviço para toda instância do mecanismo de banco de dados que tem extensões de linguagem instaladas. Para obter mais informações sobre o serviço, confira [Estrutura de extensibilidade](../concepts/extensibility-framework.md). 
   
## <a name="additional-configuration"></a>Configuração adicional

Se a etapa de verificação tiver sido bem-sucedida, você poderá executar o Código Java do SQL Server Management Studio, Azure Data Studio, Visual Studio Code ou de qualquer outro cliente que pode enviar instruções T-SQL para o servidor.

Se você receber um erro ao executar o comando, examine as etapas de configuração adicionais nesta seção. Talvez seja necessário realizar configurações apropriadas adicionais para o serviço ou banco de dados.

No nível da instância, a configuração adicional pode incluir:

* [Configuração de firewall para os Serviços de Machine Learning do SQL Server](../../advanced-analytics/security/firewall-configuration.md)
* [Habilitar protocolos de rede adicionais](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [Habilitar conexões remotas](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [Criar um logon para SQLRUserGroup](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)

<a name="bkmk_configureAccounts"></a> 
<a name="permissions-external-script"></a> 

No banco de dados, talvez você precise das seguintes atualizações de configuração:

* [Conceder aos usuários permissão para os Serviços de Machine Learning do SQL Server](../../advanced-analytics/security/user-permission.md)
* [Conceder aos usuários permissão para executar uma linguagem específica](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql#permissions)

> [!NOTE]
> Se a configuração adicional for necessária depende do seu esquema de segurança, em que você instalou o SQL Server e como você espera que os usuários se conectem ao banco de dados e executem scripts externos.

## <a name="suggested-optimizations"></a>Otimizações sugeridas

Agora que tudo está funcionando, talvez convenha também otimizar o servidor para dar suporte a extensões de linguagem.

### <a name="optimize-the-server-for-language-extensions"></a>Otimizar o servidor para extensões de linguagem

As configurações padrão da instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] destinam-se a otimizar o equilíbrio do servidor para uma variedade de serviços compatíveis com o mecanismo de banco de dados, que podem incluir processos ETL (incluir, transformar e carregar), relatórios, auditoria e aplicativos que usam os dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Portanto, nas configurações padrão, você pode achar que esses recursos para extensões de linguagem estão algumas vezes restritos ou limitados, especialmente em operações com uso intensivo de memória.

Para verificar se os trabalhos de extensão de linguagem são priorizados e têm os recursos apropriados, recomendamos que você use o SQL Server Resource Governor para configurar um pool de recursos externo. Talvez convenha também alterar a quantidade de memória alocada ao mecanismo de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou aumentar o número de contas executadas no serviço [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)].

- Para configurar um pool de recursos para o gerenciamento de recursos externos, confira [Criar um pool de recursos externo](../../t-sql/statements/create-external-resource-pool-transact-sql.md).
  
- Para alterar a quantidade de memória reservada para o banco de dados, confira [Opções de configuração de memória do servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md).
  
Se estiver usando a Edição Standard e não tiver o Resource Governor, você poderá usar DMVs (Exibições de Gerenciamento Dinâmico) e Eventos Estendidos, assim como o monitoramento de eventos do Windows, para ajudar a gerenciar os recursos do servidor.

## <a name="next-steps"></a>Próximas etapas

Os desenvolvedores do Java podem começar com alguns exemplos simples e aprender os fundamentos de como o Java funciona com o SQL Server. Para a próxima etapa, confira o link a seguir:

+ [Tutorial: Expressões regulares com Java](../tutorials/search-for-string-using-regular-expressions-in-java.md)
