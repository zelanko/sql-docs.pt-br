---
title: Instalar o SQL Server 2016 R Services (no banco de dados)
description: Adicione o suporte à linguagem de programação R a um mecanismo de banco de dados em SQL Server 2016 R Services no Windows.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/03/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: =sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: a255b70b71f29f9cc28e4022ecfdf2741f9a838d
ms.sourcegitcommit: 2f56848ec422845ee81fb84ed321a716c677aa0e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/25/2019
ms.locfileid: "71271879"
---
# <a name="install-sql-server-2016-r-services"></a>Instalar o SQL Server R Services 2016
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo explica como instalar e configurar o **SQL Server R Services 2016**. Se você tiver SQL Server 2016, instale esse recurso para habilitar a execução do código R no SQL Server.

No SQL Server 2017, a integração do R é oferecida em [serviços de Machine Learning](../r/r-server-standalone.md), refletindo a adição do Python. Se você quiser integração com o R e tiver SQL Server mídia de instalação 2017, consulte [instalar SQL Server serviços de Machine Learning](sql-machine-learning-services-windows-install.md) para adicionar o recurso. 

<a name="bkmk_prereqs"> </a> 

## <a name="pre-install-checklist"></a>Lista de verificação de pré-instalação

+ Uma instância do mecanismo de banco de dados é necessária. Não é possível instalar apenas o R, embora você possa adicioná-lo de forma incremental a uma instância existente.

+ Para a continuidade dos negócios, [Always on os grupos de disponibilidade](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server) têm suporte para o R Services. Você precisa instalar o R Services e configurar pacotes, em cada nó.

+ Não instale o R Services em um cluster de failover. O mecanismo de segurança usado para isolar processos de R não é compatível com um ambiente de cluster de failover do Windows Server.

+ Não instale o R Services em um controlador de domínio. A parte do R Services da instalação falhará.

+ Não instale **recursos** > compartilhados do**R Server (autônomo)** no mesmo computador que executa uma instância no banco de dados. 

  A instalação lado a lado com outras versões do R e do Python é possível porque a instância de SQL Server usa suas próprias cópias das distribuições de R e Anaconda de software livre. No entanto, a execução de código que usa R e Python no SQL Server computador fora SQL Server pode levar a vários problemas:
    
  + Você usa uma biblioteca diferente e um executável diferente e obtém resultados diferentes, do que quando estiver executando o no SQL Server.
  + Scripts de R e Python executados em bibliotecas externas não podem ser gerenciados pelo SQL Server, levando à contenção de recursos.
  
Se você tiver usado qualquer versão anterior do ambiente de desenvolvimento da revolução Analytics ou dos pacotes RevoScaleR, ou se tiver instalado versões de pré-lançamento do SQL Server 2016, será necessário desinstalá-las. Não há suporte para a execução de versões mais antigas e mais recentes do RevoScaleR e outros pacotes proprietários. Para obter ajuda com a remoção de versões anteriores, consulte [perguntas frequentes sobre atualização e instalação para SQL Server serviços de Machine Learning](../r/upgrade-and-installation-faq-sql-server-r-services.md).

> [!IMPORTANT]
> Após a conclusão da instalação, certifique-se de concluir as etapas adicionais de pós-configuração descritas neste artigo. Essas etapas incluem a habilitação de SQL Server usar scripts externos e adicionar contas necessárias para SQL Server executar trabalhos de R em seu nome. As alterações de configuração geralmente exigem uma reinicialização da instância ou uma reinicialização do serviço Launchpad.

## <a name="get-the-installation-media"></a>Obtenha a mídia de instalação

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

<a name="bkmk_ga_instalpatch"></a>

 ### <a name="install-patch-requirement"></a>Instalar requisito de patch 

A Microsoft identificou um problema com a versão específica dos binários do Tempo de Execução Microsoft VC++ 2013 que são instalados como um pré-requisito pelo SQL Server. Se essa atualização para os binários do Tempo de Execução de VC não for instalada, o SQL Server poderá apresentar problemas de estabilidade em determinados cenários. Antes de instalar o SQL Server, siga as instruções em [Notas de Versão do SQL Server](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) para ver se seu computador precisa de um patch para os binários de tempo de execução do VC.  

<a name="bkmk2016top"></a>

## <a name="run-setup"></a>Executar a instalação

Para instalações locais, você deve executar a Instalação como um administrador. Se você instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura e de execução no compartilhamento remoto.

1. Inicie o assistente de instalação do SQL Server 2016.

2. Na guia **instalação** , selecione **novo SQL Server instalação autônoma ou adicionar recursos a uma instalação existente**.
    
   ![Instalar o R Services (no banco de dados)](media/2016-setup-installation-rsvcs.png "Iniciar a instalação do mecanismo de banco de dados com o R Services")
   
3. Na página **seleção de recursos** , selecione as seguintes opções:

   - Selecione **serviços de mecanismo de banco de dados**. O mecanismo de banco de dados é necessário em cada instância do que usa o aprendizado de máquina.
   - Selecione **R Services (no banco de dados)** . Instala o suporte para o uso no banco de dados do R.
    
     ![Seleção de recursos do R Services](media/2016setup-rsvcs-features.png "Selecione estes recursos para R Services no banco de dados")

    > [!IMPORTANT]
    > Não instale o R Server e o R Services ao mesmo tempo. Normalmente, você instalará o R Server (autônomo) para criar um ambiente que um cientista de dados ou desenvolvedor usa para se conectar a SQL Server e implantar soluções de R. Portanto, não é necessário instalar ambos no mesmo computador.

4.  Na página **consentimento para instalar o Microsoft R Open** , clique em **aceitar**.
  
    Este contrato de licença é necessário para baixar o Microsoft R Open, que inclui uma distribuição de pacotes e ferramentas base R de software livre, junto com pacotes de R e provedores de conectividade aprimorados da equipe de desenvolvimento do Microsoft R.
  
5. Depois de aceitar o contrato de licença, há uma breve pausa enquanto o instalador está preparado. Clique em **Avançar** quando o botão ficar disponível.

6. Na página **pronto para instalar** , verifique se os itens a seguir estão incluídos e, em seguida, selecione **instalar**.

   + Serviços do Mecanismo de Banco de Dados
   + R Services (no Banco de Dados)

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

##  <a name="enable-script-execution"></a>Habilitar execução de script

1. Abra [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. 

    > [!TIP]
    > Você pode baixar e instalar a versão apropriada desta página: [Baixe o SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
    > 
    > Você também pode experimentar a versão de visualização do [Azure Data Studio](../../azure-data-studio/what-is.md), que dá suporte a tarefas administrativas e consultas em relação a SQL Server.
  
2. Conecte-se à instância em que você instalou Serviços de Machine Learning, clique em **nova consulta** para abrir uma janela de consulta e execute o seguinte comando:

   ```sql
   sp_configure
   ```
    O valor da propriedade `external scripts enabled`, deve ser **0** neste momento. Isso ocorre porque o recurso está desativado por padrão. O recurso deve ser explicitamente habilitado por um administrador antes que você possa executar scripts R ou Python.
     
3. Para habilitar o recurso de script externo, execute a seguinte instrução:
  
    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
## <a name="restart-the-service"></a>Reinicie o serviço.

Quando a instalação for concluída, reinicie o mecanismo de banco de dados antes de continuar para o próximo, habilitando a execução do script.

Reiniciar o serviço também reinicia automaticamente o serviço relacionado [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] .

Você pode reiniciar o serviço usando o comando de reinicialização do clique com o botão direito do mouse para a instância no SSMS ou usando o painel **Serviços** no painel de controle ou usando [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md).

## <a name="verify-installation"></a>Verifique a instalação

Verifique o status da instalação da instância usando [relatórios personalizados](../r/monitor-r-services-using-custom-reports-in-management-studio.md).

Use as etapas a seguir para verificar se todos os componentes usados para iniciar o script externo estão em execução.

1. No SQL Server Management Studio, abra uma nova janela de consulta e execute o seguinte comando:
    
    ```sql
    EXEC sp_configure  'external scripts enabled'
    ```

    O **run_value** agora deve ser definido como 1.

2. Abra o painel de **Serviços** ou SQL Server Configuration Manager e verifique se o **serviço SQL Server Launchpad** está em execução. Você deve ter um serviço para cada instância do mecanismo de banco de dados que tenha o R ou Python instalado. Para obter mais informações sobre o serviço, consulte [extensibilidade Framework](../concepts/extensibility-framework.md).

7. Se o Launchpad estiver em execução, você deverá ser capaz de executar R simples para verificar se os tempos de execução de script externo podem se comunicar com SQL Server. 

    Abra uma nova janela de consulta [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]no e, em seguida, execute um script como o seguinte:
    
    ```sql
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    O script pode demorar um pouco para ser executado, na primeira vez que o tempo de execução de script externo for carregado. Os resultados devem ser algo assim:

    | hello |
    |----|
    | 1|

<a name="apply-cu"></a>

## <a name="apply-updates"></a>Aplicar atualizações

Recomendamos que você aplique a atualização cumulativa mais recente aos componentes do mecanismo de banco de dados e do Machine Learning.

Em dispositivos conectados à Internet, as atualizações cumulativas são normalmente aplicadas por meio de Windows Update, mas você também pode usar as etapas abaixo para atualizações controladas. Quando você aplica a atualização para o mecanismo de banco de dados, a instalação efetua pull das atualizações cumulativas das bibliotecas do R instaladas na mesma instância. 

Em servidores desconectados, são necessárias etapas adicionais. Para obter mais informações, consulte [instalar em computadores sem acesso à internet > aplicar atualizações cumulativas](sql-ml-component-install-without-internet-access.md#apply-cu).

1. Iniciar com uma instância de linha de base já instalada: SQL Server versão inicial 2016, SQL Server 2016 SP 1 ou SQL Server 2016 SP 2.

2. Vá para a lista de atualizações cumulativas: [Atualizações do SQL Server 2016](https://sqlserverupdates.com/sql-server-2016-updates/)

3. Selecione a atualização cumulativa mais recente. Um executável é baixado e extraído automaticamente.

4. Execute a instalação. Aceite os termos de licenciamento e, na página seleção de recursos, examine os recursos para os quais as atualizações cumulativas são aplicadas. Você deve ver todos os recursos instalados para a instância atual, incluindo o R Services. A instalação baixa os arquivos CAB necessários para atualizar todos os recursos.

5. Continue com o assistente, aceitando os termos de licenciamento para a distribuição de R. 

<a name="bkmk_FollowUp"></a> 

## <a name="additional-configuration"></a>Configuração adicional

Se a etapa de verificação de script externo tiver sido bem-sucedida, você poderá executar comandos do Python de SQL Server Management Studio, Visual Studio Code ou qualquer outro cliente que possa enviar instruções T-SQL para o servidor.

Se você recebeu um erro ao executar o comando, examine as etapas de configuração adicionais nesta seção. Talvez seja necessário fazer configurações adicionais apropriadas para o serviço ou banco de dados.

No nível da instância, a configuração adicional pode incluir:

* [Configuração de firewall para SQL Server Serviços de Machine Learning](../../advanced-analytics/security/firewall-configuration.md)
* [Habilitar protocolos de rede adicionais](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [Habilitar conexões remotas](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [Gerenciar cotas de disco](https://docs.microsoft.com/windows/desktop/fileio/managing-disk-quotas) para evitar scripts externos executando tarefas que esgotam o espaço em disco

<a name="bkmk_configureAccounts"></a>
<a name="bkmk_AllowLogon"></a>

No banco de dados, talvez você precise das seguintes atualizações de configuração:

* [Conceder aos usuários permissão para SQL Server Serviços de Machine Learning](../../advanced-analytics/security/user-permission.md)
* [Adicionar SQLRUserGroup como um usuário de banco de dados](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)

> [!NOTE]
> Nem todas as alterações listadas são necessárias, e nenhuma pode ser necessária. Os requisitos dependem do seu esquema de segurança, onde você instalou SQL Server e como você espera que os usuários se conectem ao banco de dados e executem scripts externos. Dicas de solução de problemas adicionais podem ser encontradas aqui: [Perguntas frequentes sobre atualização e instalação](../r/upgrade-and-installation-faq-sql-server-r-services.md)

## <a name="suggested-optimizations"></a>Otimizações sugeridas

Agora que tudo está funcionando, talvez você também queira otimizar o servidor para dar suporte ao aprendizado de máquina ou instalar modelos pré-treinados.

### <a name="add-more-worker-accounts"></a>Adicionar mais contas de trabalho

Se você acha que pode usar o R intensamente ou se espera que muitos usuários executem scripts simultaneamente, você pode aumentar o número de contas de trabalho atribuídas ao serviço Launchpad. Para obter mais informações, consulte [Modificar o pool de contas de usuário para SQL Server serviços de Machine Learning](../administration/modify-user-account-pool.md).

<a name="bkmk_optimize"></a>

### <a name="optimize-the-server-for-external-script-execution"></a>Otimizar o servidor para execução de script externo

As configurações padrão para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a instalação do se destinam a otimizar o equilíbrio do servidor para uma variedade de serviços com suporte no mecanismo de banco de dados, que pode incluir processos ETL (extração, transformação e carregamento), relatórios, auditoria e aplicativos que usam [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados. Portanto, sob as configurações padrão, você pode achar que os recursos para Machine Learning às vezes são restritos ou limitados, especialmente em operações com uso intensivo de memória.

Para garantir que os trabalhos do Machine Learning sejam priorizados e redirecionados adequadamente, recomendamos que você use SQL Server Resource Governor para configurar um pool de recursos externos. Talvez você também queira alterar a quantidade de memória alocada para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mecanismo de banco de dados ou aumentar o número de contas executadas [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] no serviço.

- Para configurar um pool de recursos para gerenciar recursos externos, consulte [criar um pool de recursos externos](../../t-sql/statements/create-external-resource-pool-transact-sql.md).
  
- Para alterar a quantidade de memória reservada para o banco de dados, consulte [Opções de configuração de memória do servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md).
  
- Para alterar o número de contas de R que podem ser iniciadas pelo [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], consulte [Modificar o pool de contas de usuário para aprendizado de máquina](../administration/modify-user-account-pool.md).

Se você estiver usando a Standard Edition e não tiver Resource Governor, poderá usar DMVs (exibições de gerenciamento dinâmico) e eventos estendidos, bem como o monitoramento de eventos do Windows, para ajudar a gerenciar os recursos do servidor que são usados pelo R. Para obter mais informações, consulte [monitorando e gerenciando serviços R](../r/managing-and-monitoring-r-solutions.md).

### <a name="install-additional-r-packages"></a>Instalar pacotes R adicionais

As soluções de R que você cria para SQL Server podem chamar funções básicas do R, funções dos pacotes proprietários instalados com o SQL Server e pacotes de R de terceiros compatíveis com a versão do R de software livre instalado pelo SQL Server.

Pacotes que você desejar usar do SQL Server deverão ser instalados na biblioteca padrão usada pela instância. Se você tiver uma instalação separada do R no computador ou se tiver instalado pacotes em bibliotecas de usuário, não poderá usar esses pacotes do T-SQL.

O processo de instalação e gerenciamento de pacotes R é diferente no SQL Server 2016 e SQL Server 2017. No SQL Server 2016, um administrador de banco de dados deve instalar pacotes de R que os usuários precisam. No SQL Server 2017, você pode configurar grupos de usuários para compartilhar pacotes em um nível por banco de dados ou configurar funções de banco de dados para permitir que os usuários instalem seus próprios pacotes. Para obter mais informações, consulte [instalar novos pacotes de R](../r/install-additional-r-packages-on-sql-server.md).

## <a name="next-steps"></a>Próximas etapas

Os desenvolvedores do R podem começar com alguns exemplos simples e aprender os fundamentos de como o R funciona com o SQL Server. Para a próxima etapa, confira os links a seguir:

+ [Tutorial: Executar o R no T-SQL](../tutorials/quickstart-r-create-script.md)
+ [Tutorial: Análise interna no banco de dados para desenvolvedores de R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Para exibir exemplos de aprendizado de máquina que se baseiam em cenários do mundo real, confira [Tutoriais de aprendizado de máquina](../tutorials/machine-learning-services-tutorials.md).