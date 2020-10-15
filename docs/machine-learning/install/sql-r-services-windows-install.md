---
title: Instalar o SQL Server 2016 R Services
titleSuffix: ''
description: Saiba como instalar o SQL Server 2016 R Services no Windows. Você pode usar o R Services para executar scripts R no banco de dados.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 08/06/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: contperfq4
monikerRange: =sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 1aa6fee67871e705f915f72a178ee4d0e4c562e6
ms.sourcegitcommit: afb02c275b7c79fbd90fac4bfcfd92b00a399019
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2020
ms.locfileid: "91956758"
---
# <a name="install-sql-server-2016-r-services"></a>Instalar o SQL Server 2016 R Services

[!INCLUDE[SQL Server 2016 only](../../includes/applies-to-version/sqlserver2016-only.md)]

Saiba como instalar o SQL Server 2016 R Services no Windows. Você pode usar o R Services para executar scripts R no banco de dados.

> [!NOTE]
> No SQL Server 2017 e posterior, o R está incluído nos [Serviços de Machine Learning](../sql-server-machine-learning-services.md), juntamente com o Python. Caso você deseje obter o R e tenha o SQL Server 2017 ou posterior, confira [Instalar os Serviços de Machine Learning do SQL Server](sql-machine-learning-services-windows-install.md) para adicionar o recurso.

<a name="bkmk_prereqs"></a>

## <a name="pre-install-checklist"></a>Lista de verificação pré-instalação

+ Uma instância do mecanismo de banco de dados é necessária. Não é possível instalar apenas o R, embora você possa adicioná-lo de maneira incremental a uma instância existente.

+ Para continuidade dos negócios, há suporte para [grupos de disponibilidade Always On](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md) no R Services. Você precisa instalar o R Services e configurar pacotes em cada nó.

+ Não instale o R Services em uma FCI (Instância do Cluster de Failover) sempre ativada do SQL Server. O mecanismo de segurança usado para isolar processos do R não é compatível com um ambiente da FCI (Instância do Cluster de Failover) Always On do SQL Server.

+ Não instale o R Services em um controlador de domínio. A parte do R Services da instalação falhará.

+ Não instale **Recursos Compartilhados** > **R Server (Autônomo)** no mesmo computador que executa uma instância no banco de dados.

+ A instalação lado a lado com outras versões do R é compatível, mas não recomendada. Ela é compatível porque a instância do SQL Server usa uma cópia própria da distribuição de software livre do R. No entanto, a execução de código que usa o R no computador do SQL Server fora do SQL Server pode levar a vários problemas:

  + Você usa uma biblioteca e um executável diferentes daqueles obtidos ao executar no SQL Server, com resultados também diferentes.
  + Scripts R executados em bibliotecas externas não podem ser gerenciados pelo SQL Server, o que leva à contenção de recursos.
  
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

1. Na guia **Instalação**, selecione **Nova instalação autônoma do SQL Server ou adicionar recursos a uma instalação existente**.

    ![Instalar o R Services (no Banco de Dados)](media/2016-setup-installation-rsvcs.png "Iniciar a instalação do mecanismo de banco de dados com o R Services")

1. Na página **Seleção de Recursos**, selecione as seguintes opções:

    + Selecione **Serviços do Mecanismo de Banco de Dados**. O mecanismo de banco de dados é necessário em cada instância do que usa o aprendizado de máquina.
    + Selecione **R Services (no Banco de Dados)** . Instala o suporte para o uso no banco de dados do R.

    ![Seleção de recursos do R Services](media/2016setup-rsvcs-features.png "Selecionar esses recursos para o R Services no Banco de Dados")

    > [!IMPORTANT]
    > Não instale o R Server e o R Services ao mesmo tempo. 

1. Na página **Consentimento para Instalar o Microsoft R Open**, clique em **Aceitar**.
  
    Esse contrato de licença é necessário para baixar o Microsoft R Open, que inclui uma distribuição dos pacotes e das ferramentas base do R de software livre, junto com pacotes R avançados e provedores de conectividade da equipe de desenvolvimento do Microsoft R.
  
1. Depois que você aceitar o contrato de licença, haverá uma breve pausa enquanto o instalador é preparado. Clique em **Avançar** quando o botão ficar disponível.

1. Na página **Pronto para Instalar**, verifique se os itens a seguir estão incluídos e, em seguida, selecione **Instalar**.

    + Serviços do Mecanismo de Banco de Dados
    + R Services (no Banco de Dados)

1. Após a conclusão da instalação, se você receber instruções para reiniciar o computador, faça-o agora. É importante ler a mensagem do Assistente de Instalação ao concluir a Instalação. Para saber mais, veja [Exibir e ler arquivos de log da Instalação do SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).

## <a name="set-environment-variables"></a>Definir variáveis de ambiente

Somente para a integração de recursos do R, é necessário definir a variável de ambiente **MKL_CBWR** para [garantir a saída consistente](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) dos cálculos da Intel MKL (Math Kernel Library).

1. No Painel de Controle, clique em **Sistema e Segurança** > **Sistema** > **Configurações Avançadas do Sistema** > **Variáveis de Ambiente**.

1. Crie uma variável de usuário ou do sistema.

    + Defina o nome da variável como `MKL_CBWR`
    + Defina o valor da variável como `AUTO`

Esta etapa requer uma reinicialização do servidor. Você poderá segurar a reinicialização até que todo o trabalho de configuração seja concluído.

<a name="bkmk_enableFeature"></a>

##  <a name="enable-script-execution"></a>Habilitar a execução do script

1. Abra o [SSMS (SQL Server Management Studio)](../../ssms/download-sql-server-management-studio-ssms.md) ou o [Azure Data Studio](../../azure-data-studio/what-is.md).

1. Conecte-se à instância em que você instalou o R Services, clique em **Nova Consulta** para abrir uma janela de consulta e execute o seguinte comando:

   ```sql
   sp_configure
   ```

    O valor da propriedade `external scripts enabled`, deve ser **0** neste momento. Isso ocorre porque o recurso está desativado por padrão. Para executar scripts R, o recurso deve ser habilitado explicitamente por um administrador.

1. Para habilitar o recurso de script externo, execute a instrução a seguir:
  
    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
## <a name="restart-the-service"></a>Reinicie o serviço.

Quando a instalação for concluída, reinicie o mecanismo de banco de dados antes de passar para a próxima, habilitando a execução do script.

Reiniciar o serviço também reinicia automaticamente o serviço [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] relacionado.

Você pode reiniciar o serviço usando o comando **Reiniciar**, encontrado no clique com o botão direito do mouse, para a instância no SSMS ou usando o [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md).

## <a name="verify-installation"></a>Verifique a instalação

Use as etapas a seguir para verificar se todos os componentes usados para iniciar o script externo estão em execução.

1. No SQL Server Management Studio, abra uma nova janela de consulta e execute o seguinte comando:

    ```sql
    EXEC sp_configure 'external scripts enabled'
    ```

    O **run_value** agora deve ser definido como 1.

1. Abra o SQL Server Configuration Manager e verifique se o **serviço SQL Server Launchpad** está em execução. Você deve ter um serviço para cada instância do mecanismo de banco de dados que tem o R instalado. Para obter mais informações sobre o serviço, confira [Estrutura de extensibilidade](../concepts/extensibility-framework.md).

1. Se o Launchpad estiver em execução, você deverá conseguir executar o R simples para verificar se os runtimes de script externo podem se comunicar com o SQL Server.

    Abra uma nova janela de **Consulta** em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou no Azure Data Studio e execute um script como o seguinte:

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

Recomendamos que você aplique o service pack e a atualização cumulativa mais recentes aos componentes de machine learning e do mecanismo de banco de dados.

Em dispositivos conectados à Internet, as atualizações cumulativas são normalmente aplicadas por meio do Windows Update, mas você também pode usar as etapas abaixo para atualizações controladas. Quando você aplica a atualização do mecanismo de banco de dados, a Instalação obtém as atualizações cumulativas para as bibliotecas do R instaladas na mesma instância. 

Em servidores desconectados, são necessárias etapas adicionais. Para obter mais informações, confira [Instalar em computadores sem acesso à Internet > Aplicar atualizações cumulativas](sql-ml-component-install-without-internet-access.md#apply-cu).

1. Comece com uma instância de linha de base já instalada: Versão inicial do SQL Server 2016, SQL Server 2016 SP 1 ou SQL Server 2016 SP 2.

1. Acesse a lista de atualizações cumulativas: [Atualizações mais recentes do Microsoft SQL Server](../../database-engine/install-windows/latest-updates-for-microsoft-sql-server.md)

1. Selecione o service pack (ainda não instalado como a instância de linha de base) e a atualização cumulativa mais recentes. Um executável é baixado e extraído automaticamente.

1. Execute a instalação. Aceite os termos de licenciamento e, na página seleção de recursos, examine os recursos para os quais as atualizações cumulativas são aplicadas. Você deverá ver todos os recursos instalados para a instância atual, incluindo o R Services. A instalação baixa os arquivos CAB necessários para atualizar todos os recursos.

1. Continue com o assistente, aceitando os termos de licenciamento para a distribuição do R.

> [!NOTE]
> A CU (atualização cumulativa) 14 e posterior para o SQL Server 2016 SP2 inclui uma versão mais recente do runtime do R. Para obter mais informações, confira [Alterar a versão de runtime do idioma padrão](change-default-language-runtime-version.md).

<a name="bkmk_FollowUp"></a>

## <a name="additional-configuration"></a>Configuração adicional

Se a etapa de verificação de script externo for bem-sucedida, você poderá executar comandos do R por meio do SQL Server Management Studio, do Azure Data Studio ou de qualquer outro cliente que possa enviar instruções T-SQL ao servidor.

Se você receber um erro ao executar o comando, examine as etapas de configuração adicionais nesta seção. Talvez seja necessário realizar configurações apropriadas adicionais para o serviço ou banco de dados.

No nível da instância, a configuração adicional pode incluir:

* [Configuração de firewall para os Serviços de Machine Learning do SQL Server](../../machine-learning/security/firewall-configuration.md).
* [Habilitar protocolos de rede adicionais](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md).
* [Habilitar conexões remotas](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md).
* [Gerenciar cotas de disco](/windows/desktop/fileio/managing-disk-quotas) para evitar que scripts externos executem tarefas que esgotem o espaço em disco.

<a name="bkmk_configureAccounts"></a>
<a name="bkmk_AllowLogon"></a>

No banco de dados, talvez você precise das seguintes atualizações de configuração:

* [Conceder aos usuários permissão para os Serviços de Machine Learning do SQL Server](../../machine-learning/security/user-permission.md)
* [Adicionar SQLRUserGroup como um usuário de banco de dados](../../machine-learning/security/create-a-login-for-sqlrusergroup.md)

> [!NOTE]
> Nem todas as alterações listadas são necessárias e nenhuma pode ser necessária. Os requisitos dependem do esquema de segurança, da localização em que o SQL Server foi instalado e da maneira como você espera que os usuários se conectem ao banco de dados e executem scripts externos. Encontre mais diretrizes de instalação aqui: [Instalar os Serviços de Machine Learning do SQL Server](../install/sql-machine-learning-services-windows-install.md)

## <a name="suggested-optimizations"></a>Otimizações sugeridas

Talvez convenha também otimizar o servidor para oferecer suporte ao machine learning com R ou instalar modelos pré-treinados.

### <a name="add-more-worker-accounts"></a>Adicionar mais contas de trabalho

Se você acreditar que fará uso considerável do R ou esperar que muitos usuários executem scripts simultaneamente, aumente o número de contas de trabalho atribuídas ao serviço Launchpad. Para obter mais informações, confira a [execução simultânea da escala de scripts externos nos Serviços de Machine Learning do SQL Server](../administration/scale-concurrent-execution-external-scripts.md).

<a name="bkmk_optimize"></a>

### <a name="optimize-the-server-for-external-script-execution"></a>Otimizar o servidor para a execução de script externo

As configurações padrão da instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] destinam-se a otimizar o equilíbrio do servidor para uma variedade de serviços compatíveis com o mecanismo de banco de dados, que podem incluir processos ETL (incluir, transformar e carregar), relatórios, auditoria e aplicativos que usam os dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Portanto, nas configurações padrão, você poderá descobrir que os recursos para os recursos de machine learning são algumas vezes restritos ou limitados, especialmente em operações com uso intensivo de memória.

Para verificar se os trabalhos de machine learning são priorizados e têm os recursos apropriados, recomendamos que você use o SQL Server Resource Governor para configurar um pool de recursos externo. Talvez convenha também alterar a quantidade de memória alocada ao mecanismo de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou aumentar o número de contas executadas no serviço [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)].

- Para configurar um pool de recursos para o gerenciamento de recursos externos, confira [Criar um pool de recursos externo](../../t-sql/statements/create-external-resource-pool-transact-sql.md).
  
- Para alterar a quantidade de memória reservada para o banco de dados, confira [Opções de configuração de memória do servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md).
  
- Para alterar o número de contas do R que podem ser iniciadas pelo [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], confira [Dimensionar a execução simultânea de scripts externos nos Serviços de Machine Learning do SQL Server](../administration/scale-concurrent-execution-external-scripts.md).

Se estiver usando a Edição Standard e não tiver o Resource Governor, você poderá usar DMVs (Exibições de Gerenciamento Dinâmico) e Eventos Estendidos, assim como o monitoramento de eventos do Windows, para ajudar a gerenciar os recursos do servidor que são usados por R.

### <a name="install-additional-r-packages"></a>Instalar pacotes adicionais do R

As soluções do R que você cria para o SQL Server podem chamar funções básicas do R, funções dos pacotes proprietários instalados com o SQL Server e pacotes R de terceiros compatíveis com a versão do R de software livre instalada pelo SQL Server.

Pacotes que você desejar usar do SQL Server deverão ser instalados na biblioteca padrão usada pela instância. Caso você tenha uma instalação separada do R no computador ou tenha instalado pacotes em bibliotecas do usuário, não poderá usar esses pacotes no T-SQL.

O processo de instalação e gerenciamento de pacotes R é diferente no SQL Server 2016 e no SQL Server 2017. No SQL Server 2016, um administrador de banco de dados precisa instalar os pacotes R necessários para os usuários. No SQL Server 2017, você pode configurar grupos de usuários para compartilhar pacotes em um nível por banco de dados ou configurar funções de banco de dados para permitir que os usuários instalem seus próprios pacotes. Para obter mais informações, confira [Instalar pacotes com as ferramentas R](../package-management/install-r-packages-standard-tools.md).

## <a name="next-steps"></a>Próximas etapas

Os desenvolvedores do R podem começar com alguns exemplos simples e aprender os fundamentos de como o R funciona com o SQL Server. Para a próxima etapa, confira os links a seguir:

+ [Início Rápido: Executar o R no T-SQL](../tutorials/quickstart-r-create-script.md)
+ [Tutoriais do R para aprendizado de máquina do SQL](../tutorials/r-tutorials.md)
+ [Documentação do machine learning do SQL](../index.yml)