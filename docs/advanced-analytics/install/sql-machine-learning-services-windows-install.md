---
title: Instalar SQL Server Serviços de Machine Learning (Python, R) no Windows
titleSuffix: ''
description: Este artigo explica como instalar SQL Server Serviços de Machine Learning no Windows. Você pode usar Serviços de Machine Learning para executar scripts do Python e do R no banco de dados.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/20/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 28e4681808348df97e61709745e9b59e0a44d3be
ms.sourcegitcommit: 632ff55084339f054d5934a81c63c77a93ede4ce
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69634562"
---
# <a name="install-sql-server-machine-learning-services-on-windows"></a>Instalar SQL Server Serviços de Machine Learning no Windows

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo explica como instalar SQL Server Serviços de Machine Learning no Windows. Você pode usar Serviços de Machine Learning para executar scripts do Python e do R no banco de dados.

## <a name="bkmk_prereqs"></a> Lista de verificação de pré-instalação

+ SQL Server a instalação do 2017 (ou superior) for necessária se você quiser instalar o Serviços de Machine Learning com suporte a linguagem R ou Python. Se, em vez disso, você tiver SQL Server mídia de instalação 2016, poderá instalar [SQL Server R Services (no banco de dados)](sql-r-services-windows-install.md) para obter suporte à linguagem R.

+ Uma instância do mecanismo de banco de dados é necessária. Você não pode instalar apenas os recursos do R ou do Python, embora possa adicioná-los incrementalmente a uma instância existente.

+ Para a continuidade dos negócios, [Always on grupos de disponibilidade](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server) têm suporte para serviços de Machine Learning. Você precisa instalar Serviços de Machine Learning e configurar pacotes, em cada nó.

+ *Não há suporte para* a instalação do serviços de Machine Learning em um cluster de failover no SQL Server 2017. No entanto, *há suporte para* o SQL Server 2019. 
 
+ Não instale Serviços de Machine Learning em um controlador de domínio. A parte Serviços de Machine Learning da instalação falhará.

+ Não instale **recursos** > compartilhados**Machine Learning Server (autônomo)** no mesmo computador que executa uma instância no banco de dados. Um servidor autônomo competirá pelos mesmos recursos, submineração do desempenho de ambas as instalações.

+ Há suporte para a instalação lado a lado com outras versões do R e Python, mas não recomendadas. Há suporte porque a instância do SQL Server usa suas próprias cópias das distribuições de R e Anaconda de código aberto. Mas não é recomendável porque a execução de código que usa R e Python no computador SQL Server fora SQL Server pode levar a vários problemas:
    
  + Você usa uma biblioteca diferente e um executável diferente e obtém resultados diferentes, do que quando estiver executando o no SQL Server.
  + Scripts de R e Python executados em bibliotecas externas não podem ser gerenciados pelo SQL Server, levando à contenção de recursos.
  
> [!IMPORTANT]
> Após a conclusão da instalação, certifique-se de concluir as etapas de pós-configuração descritas neste artigo. Essas etapas incluem a habilitação de SQL Server usar scripts externos e adicionar contas necessárias para SQL Server executar trabalhos de R e Python em seu nome. As alterações de configuração geralmente exigem uma reinicialização da instância ou uma reinicialização do serviço Launchpad.

## <a name="get-the-installation-media"></a>Obtenha a mídia de instalação

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

## <a name="run-setup"></a>Executar a instalação

Para instalações locais, você deve executar a Instalação como um administrador. Se você instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura e de execução no compartilhamento remoto.

1. Inicie o assistente de instalação do SQL Server 2017. 
  
2. Na guia **instalação** , selecione **novo SQL Server instalação autônoma ou adicionar recursos a uma instalação existente**.

   ![Nova SQL Server instalação autônoma](media/2017setup-installation-page-mlsvcs.PNG)
   
3. Na página **Seleção de Recursos** , selecione estas opções:
  
    -   **Serviços do Mecanismo de Banco de Dados**
  
         Para usar o R e o Python com o SQL Server, você deve instalar uma instância do mecanismo de banco de dados. Você pode usar uma instância padrão ou nomeada.
  
    -   **Serviços de Machine Learning (no banco de dados)**
  
         Esta opção instala os serviços de banco de dados que dão suporte à execução de script R e Python.

    -   **R**

        Marque esta opção para adicionar os pacotes do Microsoft R, o intérprete e o R de software livre. 

    -   **Python**

        Marque esta opção para adicionar os pacotes python da Microsoft, o executável Python 3,5 e selecione bibliotecas na distribuição Anaconda.
        
        ![Opções de recurso para R e Python](media/2017setup-features-page-mls-rpy.png "Opções de configuração para Python")

        > [!NOTE]
        > 
        > Não selecione a opção para **Machine Learning Server (autônomo)** . A opção de instalar Machine Learning Server em **recursos compartilhados** destina-se ao uso em um computador separado.

4. Na página **consentimento para instalar o R** , selecione **aceitar**. Este contrato de licença aborda o Microsoft R Open, que inclui uma distribuição de pacotes e ferramentas de base do R de software livre, juntamente com pacotes e provedores de conectividade aprimorados da equipe de desenvolvimento da Microsoft.

5. Na página **consentimento para instalar o Python** , selecione **aceitar**. O contrato de licenciamento de software livre do Python também abrange Anaconda e ferramentas relacionadas, além de algumas novas bibliotecas do Python da equipe de desenvolvimento da Microsoft.
     
     ![Contrato para a licença do Python](media/2017setup-python-license.png "Contrato de licença para Python")
  
    > [!NOTE]
    >  Se o computador que você está usando não tiver acesso à Internet, você poderá pausar a instalação neste ponto para baixar os instaladores separadamente. Para obter mais informações, consulte [instalar componentes do Machine Learning sem acesso à Internet](../install/sql-ml-component-install-without-internet-access.md).
  
     Selecione **aceitar**, aguarde até que o botão **Avançar** fique ativo e, em seguida, selecione **Avançar**.
  
6. Na página **pronto para instalar** , verifique se essas seleções estão incluídas e selecione **instalar**.
  
    + Serviços do Mecanismo de Banco de Dados
    + Serviços de Machine Learning (No Banco de Dados)
    + R ou Python, ou ambos

    Observação do local da pasta no caminho `..\Setup Bootstrap\Log` onde os arquivos de configuração são armazenados. Quando a instalação for concluída, você poderá examinar os componentes instalados no arquivo de resumo.

7. Após a conclusão da instalação, se você for instruído a reiniciar o computador, faça isso agora. É importante ler a mensagem do Assistente de Instalação ao concluir a Instalação. Para saber mais, veja [Exibir e ler arquivos de log da Instalação do SQL Server](https://docs.microsoft.com/sql/database-engine/install-windows/view-and-read-sql-server-setup-log-files).

## <a name="set-environment-variables"></a>Definir variáveis de ambiente

Somente para a integração de recursos do R, você deve definir a variável de ambiente **MKL_CBWR** para [garantir a saída consistente](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) dos cálculos da Intel Math Kernel Library (MKL).

1. No painel de controle, clique em sistema e**sistema** >  **de segurança** > **configurações** > avançadas do sistema**variáveis de ambiente**.

2. Crie uma nova variável de usuário ou de sistema. 

  + Definir nome da variável como`MKL_CBWR`
  + Defina o valor da variável como`AUTO`

Esta etapa requer uma reinicialização do servidor. Se você estiver prestes a habilitar a execução de script, poderá manter a reinicialização até que todo o trabalho de configuração seja concluído.

<a name="bkmk_enableFeature"></a>

## <a name="enable-script-execution"></a>Habilitar execução de script

1. Abra [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. 

    > [!TIP]
    > Você pode baixar e instalar a versão apropriada desta página: [Baixe o SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
    > 
    > Você também pode usar [Azure Data Studio](../../azure-data-studio/what-is.md), que oferece suporte a tarefas administrativas e consultas em relação a SQL Server.
  
2. Conecte-se à instância em que você instalou Serviços de Machine Learning, clique em **nova consulta** para abrir uma janela de consulta e execute o seguinte comando:

    ```sql
    sp_configure
    ```

    O valor da propriedade `external scripts enabled`, deve ser **0** neste momento. Isso ocorre porque o recurso está desativado por padrão. O recurso deve ser explicitamente habilitado por um administrador antes que você possa executar scripts R ou Python.
    
3.  Para habilitar o recurso de script externo, execute a seguinte instrução:
    
    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
    
    Se você já tiver habilitado o recurso para a linguagem R, não execute reconfigure uma segunda vez para o Python. A plataforma de extensibilidade subjacente dá suporte a ambos os idiomas.

## <a name="restart-the-service"></a>Reinicie o serviço.

Quando a instalação for concluída, reinicie o mecanismo de banco de dados antes de continuar para o próximo, habilitando a execução do script.

Reiniciar o serviço também reinicia automaticamente o serviço relacionado [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] .

Você pode reiniciar o serviço usando o comando de reinicialização do clique com o botão direito do mouse para a instância no SSMS ou usando o painel **Serviços** no painel de controle ou usando [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md).

## <a name="verify-installation"></a>Verifique a instalação

Verifique o status da instalação da instância em [relatórios personalizados](../r/monitor-r-services-using-custom-reports-in-management-studio.md) ou logs de instalação.

Use as etapas a seguir para verificar se todos os componentes usados para iniciar o script externo estão em execução.

1. No SQL Server Management Studio, abra uma nova janela de consulta e execute o seguinte comando:
    
    ```sql
    EXEC sp_configure  'external scripts enabled'
    ```

    O **run_value** agora deve ser definido como 1.
    
2. Abra o painel de **Serviços** ou SQL Server Configuration Manager e verifique se o **serviço SQL Server Launchpad** está em execução. Você deve ter um serviço para cada instância do mecanismo de banco de dados que tenha o R ou Python instalado. Para obter mais informações sobre o serviço, consulte [extensibilidade Framework](../concepts/extensibility-framework.md). 
   
3. Se o Launchpad estiver em execução, você deverá ser capaz de executar scripts R e Python simples para verificar se os tempos de execução de script externo podem se comunicar com SQL Server.

   Abra uma nova janela de consulta [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]no e, em seguida, execute um script como o seguinte:
    
    + Para R
    
    ```sql
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    + Para Python
    
    ```sql
    EXEC sp_execute_external_script  @language =N'Python',
    @script=N'
    OutputDataSet = InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    **Resultados**

    O script pode demorar um pouco para ser executado, na primeira vez que o tempo de execução de script externo for carregado. Os resultados devem ser algo assim:

    | hello |
    |----|
    | 1|

> [!NOTE]
> Colunas ou cabeçalhos usados no script Python não são retornados por design. Para adicionar nomes de coluna para a saída, você deve especificar o esquema para o conjunto de dados de retorno. Faça isso usando o parâmetro WITH RESULTs do procedimento armazenado, nomeando as colunas e especificando o tipo de dados SQL.
> 
> Por exemplo, você pode adicionar a seguinte linha para gerar um nome de coluna arbitrário:`WITH RESULT SETS ((Col1 AS int))`

<a name="apply-cu"></a>

## <a name="apply-updates"></a>Aplicar atualizações

Recomendamos que você aplique a atualização cumulativa mais recente aos componentes do mecanismo de banco de dados e do Machine Learning.

Em dispositivos conectados à Internet, as atualizações cumulativas são normalmente aplicadas por meio de Windows Update, mas você também pode usar as etapas abaixo para atualizações controladas. Quando você aplica a atualização para o mecanismo de banco de dados, a instalação obtém atualizações cumulativas para quaisquer recursos de R ou Python que você instalou na mesma instância. 

Em servidores desconectados, são necessárias etapas adicionais. Para obter mais informações, consulte [instalar em computadores sem acesso à internet > aplicar atualizações cumulativas](sql-ml-component-install-without-internet-access.md#apply-cu).

1. Iniciar com uma instância de linha de base já instalada: Versão inicial do SQL Server 2017

2. Vá para a lista de atualizações cumulativas: [Atualizações do SQL Server 2017](https://sqlserverupdates.com/sql-server-2017-updates/)

3. Selecione a atualização cumulativa mais recente. Um executável é baixado e extraído automaticamente.

4. Execute a instalação. Aceite os termos de licenciamento e, na página seleção de recursos, examine os recursos para os quais as atualizações cumulativas são aplicadas. Você deve ver todos os recursos instalados para a instância atual, incluindo os recursos do Machine Learning. A instalação baixa os arquivos CAB necessários para atualizar todos os recursos.

  ![Resumo dos recursos instalados](media/cumulative-update-feature-selection.png)

5. Continue com o assistente, aceitando os termos de licenciamento para distribuições de R e Python. 

## <a name="additional-configuration"></a>Configuração adicional

Se a etapa de verificação de script externo tiver sido bem-sucedida, você poderá executar comandos R ou Python de SQL Server Management Studio, Visual Studio Code ou qualquer outro cliente que possa enviar instruções T-SQL para o servidor.

Se você recebeu um erro ao executar o comando, examine as etapas de configuração adicionais nesta seção. Talvez seja necessário fazer configurações adicionais apropriadas para o serviço ou banco de dados.

No nível da instância, a configuração adicional pode incluir:

* [Configuração de firewall para SQL Server Serviços de Machine Learning](../../advanced-analytics/security/firewall-configuration.md)
* [Habilitar protocolos de rede adicionais](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [Habilitar conexões remotas](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [Criar um logon para SQLRUserGroup](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)
* [Gerenciar cotas de disco](https://docs.microsoft.com/windows/desktop/fileio/managing-disk-quotas) para evitar scripts externos executando tarefas que esgotam o espaço em disco

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
No SQL Server 2019 no Windows, o mecanismo de isolamento foi alterado. Isso afeta o **SQLRUserGroup**, as regras de firewall, a permissão de arquivo e a autenticação implícita. Para obter mais informações, consulte [isolamento de alterações para serviços de Machine Learning](sql-server-machine-learning-services-2019.md).
::: moniker-end

<a name="bkmk_configureAccounts"></a> 
<a name="permissions-external-script"></a> 

No banco de dados, talvez você precise das seguintes atualizações de configuração:

* [Conceder aos usuários permissão para SQL Server Serviços de Machine Learning](../../advanced-analytics/security/user-permission.md)

> [!NOTE]
> Se a configuração adicional é necessária depende do esquema de segurança, onde você instalou SQL Server e como você espera que os usuários se conectem ao banco de dados e executem scripts externos.

## <a name="suggested-optimizations"></a>Otimizações sugeridas

Agora que tudo está funcionando, talvez você também queira otimizar o servidor para dar suporte ao aprendizado de máquina ou instalar modelos pré-treinados.

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
### <a name="add-more-worker-accounts"></a>Adicionar mais contas de trabalho

Se você espera que muitos usuários executem scripts simultaneamente, você pode aumentar o número de contas de trabalho que são atribuídas ao serviço Launchpad. Para obter mais informações, consulte [Modificar o pool de contas de usuário para SQL Server serviços de Machine Learning](../administration/modify-user-account-pool.md).
::: moniker-end

### <a name="optimize-the-server-for-script-execution"></a>Otimizar o servidor para execução de script

As configurações padrão para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a instalação do se destinam a otimizar o equilíbrio do servidor para uma variedade de serviços com suporte no mecanismo de banco de dados, que pode incluir processos ETL (extração, transformação e carregamento), relatórios, auditoria e aplicativos que usam [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados. Portanto, sob as configurações padrão, você pode achar que os recursos para Machine Learning às vezes são restritos ou limitados, especialmente em operações com uso intensivo de memória.

Para garantir que os trabalhos do Machine Learning sejam priorizados e redirecionados adequadamente, recomendamos que você use SQL Server Resource Governor para configurar um pool de recursos externos. Talvez você também queira alterar a quantidade de memória alocada para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mecanismo de banco de dados ou aumentar o número de contas executadas [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] no serviço.

- Para configurar um pool de recursos para gerenciar recursos externos, consulte [criar um pool de recursos externos](../../t-sql/statements/create-external-resource-pool-transact-sql.md).
  
- Para alterar a quantidade de memória reservada para o banco de dados, consulte [Opções de configuração de memória do servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md).
  
- Para alterar o número de contas de R que podem ser iniciadas pelo [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], consulte [Modificar o pool de contas de usuário para aprendizado de máquina](../administration/modify-user-account-pool.md).

Se você estiver usando a Standard Edition e não tiver Resource Governor, poderá usar DMVs (exibições de gerenciamento dinâmico) e eventos estendidos, bem como o monitoramento de eventos do Windows, para ajudar a gerenciar os recursos do servidor. Para obter mais informações, consulte [monitorando e gerenciando o R Services](../r/managing-and-monitoring-r-solutions.md) e [monitorando e gerenciando serviços Python](../python/managing-and-monitoring-python-solutions.md).

### <a name="install-additional-r-packages"></a>Instalar pacotes R adicionais

As soluções de R que você cria para SQL Server podem chamar funções básicas do R, funções dos pacotes proprietários instalados com o SQL Server e pacotes de R de terceiros compatíveis com a versão do R de software livre instalado pelo SQL Server.

Pacotes que você desejar usar do SQL Server deverão ser instalados na biblioteca padrão usada pela instância. Se você tiver uma instalação separada do R no computador ou se tiver instalado pacotes em bibliotecas de usuário, não poderá usar esses pacotes do T-SQL.

Para instalar e gerenciar pacotes do R, você pode configurar grupos de usuários para compartilhar pacotes em um nível por banco de dados ou configurar funções de banco de dados para permitir que os usuários instalem seus próprios pacotes. Para obter mais informações, consulte [instalar novos pacotes R no SQL Server](../r/install-additional-r-packages-on-sql-server.md).

## <a name="next-steps"></a>Próximas etapas

Os desenvolvedores do R podem começar com alguns exemplos simples e aprender os fundamentos de como o R funciona com o SQL Server. Para a próxima etapa, confira os links a seguir:

+ [Tutorial: Executar o R no T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Tutorial: Análise interna no banco de dados para desenvolvedores de R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Os desenvolvedores do Python podem aprender a usar o Python com o SQL Server seguindo estes tutoriais:

+ [Tutorial: Executar o Python no T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Tutorial: Análise interna no banco de dados para desenvolvedores de Python](../tutorials/sqldev-in-database-python-for-sql-developers.md)

Para exibir exemplos de aprendizado de máquina que se baseiam em cenários do mundo real, confira [Tutoriais de aprendizado de máquina](../tutorials/machine-learning-services-tutorials.md).
