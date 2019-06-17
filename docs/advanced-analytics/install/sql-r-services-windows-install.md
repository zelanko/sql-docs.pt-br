---
title: Instalação do SQL Server 2016 R Services (no banco de dados) – SQL Server Machine Learning
description: Adicione suporte a idiomas para um mecanismo de banco de dados no SQL Server 2016 R Services do Windows de programação R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/03/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: bc9762470b6e2a836c29f53ebfc3ffeadbcc381f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66454685"
---
# <a name="install-sql-server-2016-r-services"></a>Instalar o SQL Server 2016 R Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo explica como instalar e configurar **SQL Server 2016 R Services**. Se você tiver o SQL Server 2016, instale esse recurso para permitir a execução de código do R no SQL Server.

No SQL Server 2017, a integração do R é oferecida em [serviços de Machine Learning](../r/r-server-standalone.md), refletindo a adição do Python. Se você deseja integração de R e ter a mídia de instalação do SQL Server 2017, consulte [instalar o SQL Server 2017 Machine Learning Services](sql-machine-learning-services-windows-install.md) para adicionar o recurso. 

<a name="bkmk_prereqs"> </a> 

## <a name="pre-install-checklist"></a>Lista de verificação de pré-instalação

+ Uma instância do mecanismo de banco de dados é necessária. Você não pode instalar apenas R, embora você possa adicioná-lo incrementalmente a uma instância existente.

+ Para continuidade de negócios [Availabilty grupos AlwaysOn](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server) têm suporte para R Services. Você precisa instalar o R Services e configurar pacotes, em cada nó.

+ Não instale o R Services em um cluster de failover. O mecanismo de segurança usado para isolar processos do R não é compatível com um ambiente de cluster de failover do Windows Server.

+ Não instale o R Services em um controlador de domínio. A parte de serviços de R da instalação falhará.

+ Não instale **recursos compartilhados** > **R Server (autônomo)** no mesmo computador que está executando uma instância no banco de dados. 

  Instalação lado a lado com outras versões do R e Python são possíveis porque a instância do SQL Server usa suas próprias cópias das distribuições de R e Anaconda do código-fonte aberto. No entanto, a execução de código que usa o R e Python no computador do SQL Server fora do SQL Server pode levar a vários problemas:
    
  + Você usa uma biblioteca diferente e executável diferente e obter resultados diferentes, do que quando você estiver executando no SQL Server.
  + Scripts de R e Python em execução em bibliotecas externas não podem ser gerenciados pelo SQL Server, levando à contenção de recursos.
  
Se você tiver usado todas as versões anteriores do ambiente de desenvolvimento do Revolution Analytics ou os pacotes RevoScaleR ou se você instalou todas as versões de pré-lançamento do SQL Server 2016, você deve desinstalá-los. Não há suporte para que executam versões mais antigas e mais recentes do RevoScaleR e outros pacotes de proprietários. Para obter ajuda com a remoção de versões anteriores, consulte [atualização e perguntas frequentes sobre a instalação do SQL Server Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md).

> [!IMPORTANT]
> Após a conclusão da instalação, certifique-se de concluir as etapas adicionais de pós-configuração descritas neste artigo. Essas etapas incluem a habilitação do SQL Server usar scripts externos e adicionando as contas necessárias para o SQL Server executar trabalhos do R em seu nome. Alterações de configuração geralmente requerem uma reinicialização da instância ou uma reinicialização do serviço Launchpad.

## <a name="get-the-installation-media"></a>Obtenha a mídia de instalação

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

<a name="bkmk_ga_instalpatch"></a>

 ### <a name="install-patch-requirement"></a>Instalar o requisito de patch 

A Microsoft identificou um problema com a versão específica dos binários do Tempo de Execução Microsoft VC++ 2013 que são instalados como um pré-requisito pelo SQL Server. Se essa atualização para os binários do Tempo de Execução de VC não for instalada, o SQL Server poderá apresentar problemas de estabilidade em determinados cenários. Antes de instalar o SQL Server, siga as instruções em [Notas de Versão do SQL Server](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) para ver se seu computador precisa de um patch para os binários de tempo de execução do VC.  

<a name="bkmk2016top"></a>

## <a name="run-setup"></a>Executar a instalação

Para instalações locais, você deve executar a Instalação como um administrador. Se você instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura e de execução no compartilhamento remoto.

1. Inicie o Assistente de instalação do SQL Server 2016.

2. Sobre o **instalação** guia, selecione **instalação autônoma do novo SQL Server ou adicionar recursos a uma instalação existente**.
    
   ![Instalar o R Services (no banco de dados)](media/2016-setup-installation-rsvcs.png "Iniciar instalação do mecanismo de banco de dados com R Services")
   
3. Sobre o **seleção de recursos** , selecione as opções a seguir:

   - Selecione **serviços de mecanismo de banco de dados**. O mecanismo de banco de dados é necessário em cada instância que usa o aprendizado de máquina.
   - Selecione **R Services (no banco de dados)** . Instala o suporte para uso no banco de dados do R.
    
     ![Seleção de recursos de R Services](media/2016setup-rsvcs-features.png "selecione esses recursos para R Services no banco de dados")

    > [!IMPORTANT]
    > Não instale o servidor R e R Services ao mesmo tempo. Normalmente você deve instalar o R Server (autônomo) para criar um ambiente que um desenvolvedor ou cientista de dados usa para se conectar ao SQL Server e implantar soluções de R. Portanto, não é necessário instalar ambos no mesmo computador.

4.  Sobre o **consentimento para instalar o Microsoft R Open** , clique em **Accept**.
  
    Este contrato de licença é necessária para baixar o Microsoft R Open, que inclui uma distribuição de pacotes de base de R de código-fonte aberto e ferramentas, junto com pacotes de R aprimorados e provedores de conectividade da equipe de desenvolvimento do Microsoft R.
  
5. Depois que você aceitou o contrato de licença, há uma pequena pausa enquanto o instalador está preparado. Clique em **próxima** quando o botão fica disponível.

6. Sobre o **pronto para instalar** página, verifique se os itens a seguir estão incluídos e, em seguida, selecione **instalar**.

   + Serviços do Mecanismo de Banco de Dados
   + R Services (no Banco de Dados)

    Anote o local da pasta no caminho `..\Setup Bootstrap\Log` onde os arquivos de configuração são armazenados. Quando a instalação for concluída, você pode examinar os componentes instalados no arquivo de resumo.

7. Após a instalação for concluída, se você for instruído a reiniciar o computador, faça isso agora. É importante ler a mensagem do Assistente de Instalação ao concluir a Instalação. Para saber mais, veja [Exibir e ler arquivos de log da Instalação do SQL Server](https://docs.microsoft.com/sql/database-engine/install-windows/view-and-read-sql-server-setup-log-files).

## <a name="set-environment-variables"></a>Configurar variáveis de ambiente

Para R integração de recursos somente, você deve definir a **MKL_CBWR** variável de ambiente [garantir uma saída consistente](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) cálculos da Intel MKL Math Kernel Library ().

1. No painel de controle, clique em **sistema e segurança** > **sistema** > **configurações avançadas do sistema**  >   **Variáveis de ambiente**.

2. Crie uma nova variável de sistema ou usuário. 

  + Nome de variável de conjunto para `MKL_CBWR`
  + Defina o valor da variável como `AUTO`

Esta etapa requer uma reinicialização do servidor. Se você está prestes a habilitar a execução do script, você pode adiar a reinicialização até que todo o trabalho de configuração é feita.

<a name="bkmk_enableFeature"></a>

##  <a name="enable-script-execution"></a>Habilitar a execução do script

1. Abra [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. 

    > [!TIP]
    > Você pode baixar e instalar a versão apropriada nesta página: [Baixe o SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
    > 
    > Você também pode experimentar a versão de visualização da [Studio do Azure Data](../../azure-data-studio/what-is.md), que oferece suporte a tarefas administrativas e consultas no SQL Server.
  
2. Conecte-se à instância onde você instalou os serviços de Machine Learning, clique em **nova consulta** para abrir uma janela de consulta e execute o seguinte comando:

   ```sql
   sp_configure
   ```
    O valor da propriedade `external scripts enabled`, deve ser **0** neste momento. Isso ocorre porque o recurso é desativado por padrão. O recurso deve ser habilitado explicitamente por um administrador antes de executar scripts R ou Python.
     
3. Para habilitar o recurso de script externo, execute a seguinte instrução:
  
    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
## <a name="restart-the-service"></a>Reinicie o serviço.

Quando a instalação for concluída, reinicie o mecanismo de banco de dados antes de continuar para a próxima, permitindo a execução do script.

Reiniciar o serviço também automaticamente reinicia relacionado [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] service.

Você pode reiniciar o serviço usando o botão direito do mouse **reinicie** comando para a instância no SSMS ou usando o **Services** painel no painel de controle ou usando [SQL Server Configuration Manager ](../../relational-databases/sql-server-configuration-manager.md).

## <a name="verify-installation"></a>Verifique a instalação

Verificar o status de instalação da instância usando [relatórios personalizados](../r/monitor-r-services-using-custom-reports-in-management-studio.md).

Use as etapas a seguir para verificar se todos os componentes usados para iniciar o script externo estão em execução.

1. No SQL Server Management Studio, abra uma nova janela de consulta e execute o seguinte comando:
    
    ```sql
    EXEC sp_configure  'external scripts enabled'
    ```

    O **run_value** agora deve ser definido como 1.

2. Abra o **Services** painel ou o SQL Server Configuration Manager e verifique se **Launchpad do SQL Server service** está em execução. Você deve ter um serviço para cada instância do mecanismo de banco de dados que tem o R ou Python instalado. Para obter mais informações sobre o serviço, consulte [Extensibility framework](../concepts/extensibility-framework.md).

7. Se o Launchpad estiver em execução, você poderá executar R simple para verificar se os tempos de execução de scripts externos podem se comunicar com o SQL Server. 

    Abra uma nova **consulta** janela no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], e, em seguida, executar um script como o seguinte:
    
    ```sql
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    O script pode demorar um pouco enquanto executar na primeira vez que o tempo de execução do script externo é carregado. Os resultados devem ser algo parecido com isto:

    | hello |
    |----|
    | 1|

<a name="apply-cu"></a>

## <a name="apply-updates"></a>Aplicar atualizações

É recomendável que você aplique a atualização cumulativa mais recente para o mecanismo de banco de dados e componentes de aprendizado de máquina.

Em dispositivos conectados à internet, as atualizações cumulativas são geralmente aplicadas por meio do Windows Update, mas você também pode usar as etapas abaixo para atualizações de controlado. Quando você aplicar a atualização para o mecanismo de banco de dados, a instalação puxa as atualizações cumulativas para bibliotecas de R instalados na mesma instância. 

Em servidores desconectados, são necessárias etapas adicionais. Para obter mais informações, consulte [instalar em computadores sem acesso à internet > Aplicar atualizações cumulativas](sql-ml-component-install-without-internet-access.md#apply-cu).

1. Comece com uma instância de linha de base já instalada: Versão inicial do SQL Server 2016, SQL Server 2016 SP 1 ou SQL Server 2016 SP 2.

2. Vá para a lista de atualização cumulativa: [Atualizações do SQL Server 2016](https://sqlserverupdates.com/sql-server-2016-updates/)

3. Selecione a atualização cumulativa mais recente. Um executável é baixado e extraído automaticamente.

4. Execute a instalação. Aceite os termos de licenciamento e, na página de seleção de recursos, analise os recursos para os quais as atualizações cumulativas são aplicadas. Você deve ver todos os recursos instalados para a instância atual, incluindo os serviços de R. A instalação baixará os arquivos CAB necessários para atualizar todos os recursos.

5. Prossiga com o assistente, aceitando os termos de licenciamento para a distribuição de R. 

<a name="bkmk_FollowUp"></a> 

## <a name="additional-configuration"></a>Configuração adicional

Se a etapa de verificação de script externo foi bem-sucedida, você pode executar comandos de Python do SQL Server Management Studio, Visual Studio Code ou qualquer outro cliente que pode enviar instruções T-SQL para o servidor.

Se você obteve um erro ao executar o comando, examine as etapas de configuração adicionais nesta seção. Talvez seja necessário fazer configurações adicionais de apropriado para o serviço ou o banco de dados.

No nível de instância, configurações adicionais podem incluir:

* [Configuração do firewall para serviços do SQL Server Machine Learning](../../advanced-analytics/security/firewall-configuration.md)
* [Habilite os protocolos de rede adicionais](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [Habilitar conexões remotas](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [Gerenciar cotas de disco](https://docs.microsoft.com/windows/desktop/fileio/managing-disk-quotas) para evitar a execução de tarefas que esgotar o espaço em disco de scripts externos

<a name="bkmk_configureAccounts"></a>
<a name="bkmk_AllowLogon"></a>

Banco de dados, talvez você precise as atualizações de configuração a seguir:

* [Conceder aos usuários permissão para serviços do SQL Server Machine Learning](../../advanced-analytics/security/user-permission.md)
* [Adicionar SQLRUserGroup como um usuário de banco de dados](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)

> [!NOTE]
> Nem todas as alterações listadas são necessárias e nenhum pode ser necessária. Os requisitos dependem de seu esquema de segurança, onde você instalou o SQL Server e como você espera que os usuários para se conectar ao banco de dados e executar scripts externos. Dicas de solução de problemas adicionais podem ser encontradas aqui: [Perguntas frequentes sobre atualização e instalação](../r/upgrade-and-installation-faq-sql-server-r-services.md)

## <a name="suggested-optimizations"></a>Otimizações sugeridas

Agora que você tem tudo funcionando, você também poderá otimizar o servidor para oferecer suporte ao aprendizado de máquina ou modelos pré-treinados de instalação.

### <a name="add-more-worker-accounts"></a>Adicionar mais contas de trabalho

Se você achar que você pode usar o R muito ou se você espera que vários usuários executando scripts simultaneamente, você pode aumentar o número de contas de trabalho que são atribuídos ao serviço Launchpad. Para obter mais informações, consulte [modificar o pool de conta de usuário para serviços do SQL Server Machine Learning](../administration/modify-user-account-pool.md).

<a name="bkmk_optimize"></a>

### <a name="optimize-the-server-for-external-script-execution"></a>Otimizar o servidor para execução de scripts externos

As configurações padrão para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalação destinam-se para otimizar o equilíbrio entre o servidor para uma variedade de serviços que têm suporte pelo mecanismo de banco de dados, que pode incluir a extração, transformação e carregamento (ETL) de processos, relatórios, auditoria, e aplicativos que usam [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados. Portanto, sob as configurações padrão, você pode encontrar recursos de aprendizagem de máquina, às vezes, são restritos ou limitados, especialmente em operações com uso intensivo de memória.

Para garantir que os trabalhos de aprendizado de máquina são priorizados e tenham os recursos apropriados, é recomendável que você use o administrador de recursos do SQL Server para configurar um pool de recursos externos. Você também poderá alterar a quantidade de memória alocada para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mecanismo de banco de dados ou aumentar o número de contas que são executados sob o [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] service.

- Para configurar um pool de recursos para gerenciamento de recursos externos, consulte [criar um pool de recursos externos](../../t-sql/statements/create-external-resource-pool-transact-sql.md).
  
- Para alterar a quantidade de memória reservada para o banco de dados, consulte [opções de configuração de memória do servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md).
  
- Para alterar o número de contas do R que pode ser iniciado por [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], consulte [modificar o pool de conta de usuário para o machine learning](../administration/modify-user-account-pool.md).

Se você estiver usando o Standard Edition e tiver o Resource Governor, você pode usar eventos estendidos e exibições de gerenciamento dinâmico (DMVs), bem como eventos do Windows de monitoramento, para ajudar a gerenciar os recursos de servidor que são usados pelo R. Para obter mais informações, consulte [monitoramento e gerenciamento de serviços de R](../r/managing-and-monitoring-r-solutions.md).

### <a name="install-additional-r-packages"></a>Instalar pacotes R adicionais

As soluções de R que você cria para o SQL Server podem chamar funções básicas de R, funções de pacotes de proprietários instalados com o SQL Server e pacotes de R de terceiros compatível com a versão de software livre R instalado pelo SQL Server.

Pacotes que você desejar usar do SQL Server deverão ser instalados na biblioteca padrão usada pela instância. Se você tiver uma instalação separada do R no computador, ou se você tiver instalado pacotes em bibliotecas do usuário, você não poderá usar os pacotes do T-SQL.

O processo para instalar e gerenciar pacotes de R é diferente no SQL Server 2016 e SQL Server 2017. No SQL Server 2016, um administrador de banco de dados deve instalar os pacotes de R que os usuários precisam. No SQL Server 2017, você pode configurar grupos de usuários para compartilhar pacotes em um nível por banco de dados ou configurar as funções de banco de dados para permitir que os usuários instalem seus próprios pacotes. Para obter mais informações, consulte [instalar novos pacotes de R](../r/install-additional-r-packages-on-sql-server.md).

## <a name="next-steps"></a>Próximas etapas

Os desenvolvedores do R podem começar com alguns exemplos simples e aprender os fundamentos de como o R funciona com o SQL Server. Para a próxima etapa, consulte os links a seguir:

+ [Tutorial: Executar R no T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Tutorial: Análise no banco de dados para os desenvolvedores do R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Para exibir exemplos de aprendizado de máquina com base em cenários do mundo real, consulte [tutoriais de aprendizado de máquina](../tutorials/machine-learning-services-tutorials.md).