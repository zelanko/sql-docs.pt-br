---
title: Instalar o SQL Server 2016 R Services (no banco de dados)
description: Adicione o suporte à linguagem de programação R a um mecanismo de banco de dados no SQL Server 2016 R Services no Windows.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/06/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: =sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 6fcb4245d4efff00002dea9b490312792e0d83d6
ms.sourcegitcommit: b4ad3182aa99f9cbfd15f4c3f910317d6128a2e5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2019
ms.locfileid: "73706999"
---
# <a name="install-sql-server-2016-r-services"></a>Instalar o SQL Server 2016 R Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo explica como instalar e configurar o **SQL Server 2016 R Services**. Caso você tenha o SQL Server 2016, instale esse recurso para habilitar a execução do código R no SQL Server.

No SQL Server 2017, a integração do R é oferecida nos [Serviços de Machine Learning](../r/r-server-standalone.md), refletindo a adição do Python. Caso você deseje obter a integração ao R e tenha a mídia de instalação do SQL Server 2017, confira [Instalar os Serviços de Machine Learning do SQL Server](sql-machine-learning-services-windows-install.md) para adicionar o recurso. 

<a name="bkmk_prereqs"> </a> 

## <a name="pre-install-checklist"></a>Lista de verificação pré-instalação

+ Uma instância do mecanismo de banco de dados é necessária. Não é possível instalar apenas o R, embora você possa adicioná-lo de maneira incremental a uma instância existente.

+ Para continuidade dos negócios, há suporte para [grupos de disponibilidade Always On](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server) no R Services. Você precisa instalar o R Services e configurar pacotes em cada nó.

+ Não instale o R Services em um cluster de failover. O mecanismo de segurança usado para isolar processos do R não é compatível com um ambiente de cluster de failover do Windows Server.

+ Não instale o R Services em um controlador de domínio. A parte do R Services da instalação falhará.

+ Não instale **Recursos Compartilhados** > **R Server (Autônomo)** no mesmo computador que executa uma instância no banco de dados. 

  A instalação lado a lado com outras versões do R e do Python é possível porque a Instância do SQL Server usa as próprias cópias das distribuições de software livre do R e do Anaconda. No entanto, a execução de código que usa o R e o Python no computador do SQL Server fora do SQL Server pode levar a vários problemas:
    
  + Você usa uma biblioteca e um executável diferentes daqueles obtidos ao executar no SQL Server, com resultados também diferentes.
  + Scripts de R e Python executados em bibliotecas externas não podem ser gerenciados pelo SQL Server, o que leva à contenção de recursos.
  
Caso você tenha instalado versões anteriores do ambiente de desenvolvimento da Revolution Analytics ou dos pacotes do RevoScaleR ou caso tenha instalado versões de pré-lançamento do SQL Server 2016, desinstale-as. Não há suporte para a execução de versões mais antigas e mais recentes do RevoScaleR e de outros pacotes proprietários. Para obter ajuda com a remoção de versões anteriores, confira [Perguntas frequentes sobre atualização e instalação dos Serviços de Machine Learning do SQL Server](../r/upgrade-and-installation-faq-sql-server-r-services.md).

> [!IMPORTANT]
> Após a conclusão da instalação, conclua as etapas de pós-configuração adicionais descritas neste artigo. Essas etapas incluem a habilitação do SQL Server para usar scripts externos e a adição de contas necessárias para o SQL Server executar trabalhos do R em seu nome. Geralmente, as alterações na configuração exigem uma reinicialização da instância ou do serviço Launchpad.

## <a name="get-the-installation-media"></a>Obtenha a mídia de instalação

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

<a name="bkmk_ga_instalpatch"></a>

 ### <a name="install-patch-requirement"></a>Instalar o requisito de patch 

A Microsoft identificou um problema com a versão específica dos binários do Runtime Microsoft VC++ 2013 que são instalados como um pré-requisito pelo SQL Server. Se essa atualização para os binários do Runtime de VC não for instalada, o SQL Server poderá apresentar problemas de estabilidade em determinados cenários. Antes de instalar o SQL Server, siga as instruções em [Notas de Versão do SQL Server](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) para ver se seu computador precisa de um patch para os binários de runtime do VC.  

<a name="bkmk2016top"></a>

## <a name="run-setup"></a>Executar a instalação

Para instalações locais, você deve executar a Instalação como um administrador. Se você instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura e de execução no compartilhamento remoto.

1. Inicie o assistente de instalação do SQL Server 2016.

2. Na guia **Instalação**, selecione **Nova instalação autônoma do SQL Server ou adicionar recursos a uma instalação existente**.
    
   ![Instalar o R Services (no Banco de Dados)](media/2016-setup-installation-rsvcs.png "Iniciar a instalação do mecanismo de banco de dados com o R Services")
   
3. Na página **Seleção de Recursos**, selecione as seguintes opções:

   - Selecione **Serviços do Mecanismo de Banco de Dados**. O mecanismo de banco de dados é necessário em cada instância do que usa o aprendizado de máquina.
   - Selecione **R Services (no Banco de Dados)** . Instala o suporte para o uso no banco de dados do R.
    
     ![Seleção de recursos do R Services](media/2016setup-rsvcs-features.png "Selecionar esses recursos para o R Services no Banco de Dados")

    > [!IMPORTANT]
    > Não instale o R Server e o R Services ao mesmo tempo. Normalmente, você instalará o R Server (Autônomo) para criar um ambiente que será usado por um cientista de dados ou um desenvolvedor para se conectar ao SQL Server e implantar soluções do R. Portanto, não é necessário instalar ambos no mesmo computador.

4.  Na página **Consentimento para Instalar o Microsoft R Open**, clique em **Aceitar**.
  
    Esse contrato de licença é necessário para baixar o Microsoft R Open, que inclui uma distribuição dos pacotes e das ferramentas base do R de software livre, junto com pacotes R avançados e provedores de conectividade da equipe de desenvolvimento do Microsoft R.
  
5. Depois que você aceitar o contrato de licença, haverá uma breve pausa enquanto o instalador é preparado. Clique em **Avançar** quando o botão ficar disponível.

6. Na página **Pronto para Instalar**, verifique se os itens a seguir estão incluídos e, em seguida, selecione **Instalar**.

   + Serviços do Mecanismo de Banco de Dados
   + R Services (no Banco de Dados)

    Observe a localização da pasta no caminho `..\Setup Bootstrap\Log` em que os arquivos de configuração são armazenados. Quando a instalação for concluída, você poderá examinar os componentes instalados no arquivo de Resumo.

7. Após a conclusão da instalação, se você receber instruções para reiniciar o computador, faça-o agora. É importante ler a mensagem do Assistente de Instalação ao concluir a Instalação. Para saber mais, veja [Exibir e ler arquivos de log da Instalação do SQL Server](https://docs.microsoft.com/sql/database-engine/install-windows/view-and-read-sql-server-setup-log-files).

## <a name="set-environment-variables"></a>Definir variáveis de ambiente

Somente para a integração de recursos do R, é necessário definir a variável de ambiente **MKL_CBWR** para [garantir a saída consistente](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) dos cálculos da Intel MKL (Math Kernel Library).

1. No Painel de Controle, clique em **Sistema e Segurança** > **Sistema** > **Configurações Avançadas do Sistema** > **Variáveis de Ambiente**.

2. Crie uma variável de usuário ou do sistema. 

  + Defina o nome da variável como `MKL_CBWR`
  + Defina o valor da variável como `AUTO`

Esta etapa requer uma reinicialização do servidor. Se estiver prestes a habilitar a execução de script, você poderá manter a reinicialização até que todo o trabalho de configuração seja concluído.

<a name="bkmk_enableFeature"></a>

##  <a name="enable-script-execution"></a>Habilitar a execução do script

1. Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. 

    > [!TIP]
    > Você pode baixar e instalar a versão apropriada nesta página: [Baixe o SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
    > 
    > Você também pode usar o [Azure Data Studio](../../azure-data-studio/what-is.md), que dá suporte a tarefas administrativas e consultas no SQL Server.
  
2. Conecte-se à instância em que você instalou os Serviços de Machine Learning, clique em **Nova Consulta** para abrir uma janela de consulta e execute o seguinte comando:

   ```sql
   sp_configure
   ```
    O valor da propriedade `external scripts enabled`, deve ser **0** neste momento. Isso ocorre porque o recurso está desativado por padrão. O recurso precisa ser habilitado explicitamente por um administrador antes que seja possível executar scripts R ou Python.
     
3. Para habilitar o recurso de script externo, execute a instrução a seguir:
  
    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
## <a name="restart-the-service"></a>Reinicie o serviço.

Quando a instalação for concluída, reinicie o mecanismo de banco de dados antes de passar para a próxima, habilitando a execução do script.

Reiniciar o serviço também reinicia automaticamente o serviço [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] relacionado.

Você pode reiniciar o serviço usando o clique com o botão direito do mouse no comando **Reiniciar** para a instância no SSMS ou usando o painel **Serviços** no Painel de Controle ou usando o [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md).

## <a name="verify-installation"></a>Verifique a instalação

Verifique o status da instalação da instância usando [relatórios personalizados](../r/monitor-r-services-using-custom-reports-in-management-studio.md).

Use as etapas a seguir para verificar se todos os componentes usados para iniciar o script externo estão em execução.

1. No SQL Server Management Studio, abra uma nova janela de consulta e execute o seguinte comando:
    
    ```sql
    EXEC sp_configure  'external scripts enabled'
    ```

    O **run_value** agora deve ser definido como 1.

2. Abra o painel **Serviços** ou o SQL Server Configuration Manager e verifique se o **serviço SQL Server Launchpad** está em execução. Você deve ter um serviço para toda instância do mecanismo de banco de dados que tem o R ou o Python instalados. Para obter mais informações sobre o serviço, confira [Estrutura de extensibilidade](../concepts/extensibility-framework.md).

7. Se o Launchpad estiver em execução, você deverá conseguir executar o R simples para verificar se os runtimes de script externo podem se comunicar com o SQL Server. 

    Abra uma nova janela **Consulta** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e, em seguida, execute um script como o seguinte:
    
    ```sql
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    Na primeira vez que o runtime de script externo for carregado, o script poderá demorar um pouco para ser executado. Os resultados devem ser semelhantes a estes:

    | hello |
    |----|
    | 1|

<a name="apply-cu"></a>

## <a name="apply-updates"></a>Aplicar atualizações

Recomendamos que você aplique a atualização cumulativa mais recente aos componentes do mecanismo de banco de dados e de aprendizado de máquina.

Em dispositivos conectados à Internet, as atualizações cumulativas são normalmente aplicadas por meio do Windows Update, mas você também pode usar as etapas abaixo para atualizações controladas. Quando você aplica a atualização do mecanismo de banco de dados, a Instalação obtém as atualizações cumulativas para as bibliotecas do R instaladas na mesma instância. 

Em servidores desconectados, são necessárias etapas adicionais. Para obter mais informações, confira [Instalar em computadores sem acesso à Internet > Aplicar atualizações cumulativas](sql-ml-component-install-without-internet-access.md#apply-cu).

1. Comece com uma instância de linha de base já instalada: Versão inicial do SQL Server 2016, SQL Server 2016 SP 1 ou SQL Server 2016 SP 2.

2. Acesse a lista de atualizações cumulativas: [Atualizações do SQL Server 2016](https://sqlserverupdates.com/sql-server-2016-updates/)

3. Selecione a atualização cumulativa mais recente. Um executável é baixado e extraído automaticamente.

4. Execute a instalação. Aceite os termos de licenciamento e, na página seleção de recursos, examine os recursos para os quais as atualizações cumulativas são aplicadas. Você deverá ver todos os recursos instalados para a instância atual, incluindo o R Services. A instalação baixa os arquivos CAB necessários para atualizar todos os recursos.

5. Continue com o assistente, aceitando os termos de licenciamento para a distribuição do R. 

<a name="bkmk_FollowUp"></a> 

## <a name="additional-configuration"></a>Configuração adicional

Se a etapa de verificação de script externo for bem-sucedida, você poderá executar comandos do Python por meio do SQL Server Management Studio, do Azure Data Studio ou de qualquer outro cliente que possa enviar instruções T-SQL ao servidor.

Se você receber um erro ao executar o comando, examine as etapas de configuração adicionais nesta seção. Talvez seja necessário realizar configurações apropriadas adicionais para o serviço ou banco de dados.

No nível da instância, a configuração adicional pode incluir:

* [Configuração de firewall para os Serviços de Machine Learning do SQL Server](../../advanced-analytics/security/firewall-configuration.md)
* [Habilitar protocolos de rede adicionais](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [Habilitar conexões remotas](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [Gerenciar cotas de disco](https://docs.microsoft.com/windows/desktop/fileio/managing-disk-quotas) para evitar que scripts externos executem tarefas que esgotam o espaço em disco

<a name="bkmk_configureAccounts"></a>
<a name="bkmk_AllowLogon"></a>

No banco de dados, talvez você precise das seguintes atualizações de configuração:

* [Conceder aos usuários permissão para os Serviços de Machine Learning do SQL Server](../../advanced-analytics/security/user-permission.md)
* [Adicionar SQLRUserGroup como um usuário de banco de dados](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)

> [!NOTE]
> Nem todas as alterações listadas são necessárias e nenhuma pode ser necessária. Os requisitos dependem do esquema de segurança, da localização em que o SQL Server foi instalado e da maneira como você espera que os usuários se conectem ao banco de dados e executem scripts externos. Encontre mais dicas de solução de problemas aqui: [Perguntas frequentes sobre atualização e instalação](../r/upgrade-and-installation-faq-sql-server-r-services.md)

## <a name="suggested-optimizations"></a>Otimizações sugeridas

Agora que tudo está funcionando, talvez convenha também otimizar o servidor para oferecer suporte a aprendizado de máquina ou então instalar modelos pré-treinados.

### <a name="add-more-worker-accounts"></a>Adicionar mais contas de trabalho

Se você acreditar que fará uso considerável do R ou esperar que muitos usuários executem scripts simultaneamente, aumente o número de contas de trabalho atribuídas ao serviço Launchpad. Para obter mais informações, confira [Modificar o pool de contas de usuário dos Serviços de Machine Learning do SQL Server](../administration/modify-user-account-pool.md).

<a name="bkmk_optimize"></a>

### <a name="optimize-the-server-for-external-script-execution"></a>Otimizar o servidor para a execução de script externo

As configurações padrão da instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] destinam-se a otimizar o equilíbrio do servidor para uma variedade de serviços compatíveis com o mecanismo de banco de dados, que podem incluir processos ETL (incluir, transformar e carregar), relatórios, auditoria e aplicativos que usam os dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Portanto, nas configurações padrão, você poderá descobrir que os recursos para os recursos de machine learning são algumas vezes restritos ou limitados, especialmente em operações com uso intensivo de memória.

Para verificar se os trabalhos de machine learning são priorizados e têm os recursos apropriados, recomendamos que você use o SQL Server Resource Governor para configurar um pool de recursos externo. Talvez convenha também alterar a quantidade de memória alocada ao mecanismo de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou aumentar o número de contas executadas no serviço [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)].

- Para configurar um pool de recursos para o gerenciamento de recursos externos, confira [Criar um pool de recursos externo](../../t-sql/statements/create-external-resource-pool-transact-sql.md).
  
- Para alterar a quantidade de memória reservada para o banco de dados, confira [Opções de configuração de memória do servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md).
  
- Para alterar o número de contas do R que podem ser iniciadas pelo [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], confira [Modificar o pool de contas de usuário para o aprendizado de máquina](../administration/modify-user-account-pool.md).

Caso você esteja usando a Edição Standard e não tenha o Resource Governor, use DMVs (exibições de gerenciamento dinâmico) e Eventos Estendidos, bem como o monitoramento de eventos do Windows, para ajudar a gerenciar recursos do servidor usados pelo R. Para obter mais informações, confira [Monitoramento e gerenciamento do R Services](../r/managing-and-monitoring-r-solutions.md).

### <a name="install-additional-r-packages"></a>Instalar pacotes adicionais do R

As soluções do R que você cria para o SQL Server podem chamar funções básicas do R, funções dos pacotes proprietários instalados com o SQL Server e pacotes R de terceiros compatíveis com a versão do R de software livre instalada pelo SQL Server.

Pacotes que você desejar usar do SQL Server deverão ser instalados na biblioteca padrão usada pela instância. Caso você tenha uma instalação separada do R no computador ou tenha instalado pacotes em bibliotecas do usuário, não poderá usar esses pacotes no T-SQL.

O processo de instalação e gerenciamento de pacotes R é diferente no SQL Server 2016 e no SQL Server 2017. No SQL Server 2016, um administrador de banco de dados precisa instalar os pacotes R necessários para os usuários. No SQL Server 2017, você pode configurar grupos de usuários para compartilhar pacotes em um nível por banco de dados ou configurar funções de banco de dados para permitir que os usuários instalem seus próprios pacotes. Para obter mais informações, confira [Instalar novos pacotes do R](../r/install-additional-r-packages-on-sql-server.md).

## <a name="next-steps"></a>Próximas etapas

Os desenvolvedores do R podem começar com alguns exemplos simples e aprender os fundamentos de como o R funciona com o SQL Server. Para a próxima etapa, confira os links a seguir:

+ [Tutorial: Executar o R no T-SQL](../tutorials/quickstart-r-create-script.md)
+ [Tutorial: Análise interna no banco de dados para desenvolvedores de R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Para exibir exemplos de aprendizado de máquina que se baseiam em cenários do mundo real, confira [Tutoriais de aprendizado de máquina](../tutorials/machine-learning-services-tutorials.md).