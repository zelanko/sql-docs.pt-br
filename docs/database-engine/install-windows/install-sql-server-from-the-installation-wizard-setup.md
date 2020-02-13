---
title: Instalar usando a interface gráfica do usuário
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- installing SQL Server, steps
- Setup [SQL Server], steps
- SQL Server, installing
ms.assetid: 6ad23de1-2bab-4933-9122-c09f5565028d
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 9dc0d760bd7fd6a89d9829fa5e883ef1ad9b59b7
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "76934198"
---
# <a name="install-sql-server-from-the-installation-wizard-setup"></a>Instalar o SQL Server por meio do Assistente de Instalação (Instalação)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo explica como instalar o SQL Server com o Assistente de Instalação. Aplica-se ao [!INCLUDE[SQLServer2016](../../includes/sssql15-md.md)] e ao [!INCLUDE[SQLServer2017](../../includes/sssqlv14-md.md)].

Este artigo apresenta um procedimento passo a passo sobre como instalar uma nova instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O Assistente de Instalação fornece uma única árvore de recursos para instalação de todos os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], para que você não precise instalá-los individualmente. Para instalar os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] individualmente, confira o tópico [Instalar o SQL Server](../../database-engine/install-windows/install-sql-server.md#individual-component-installation).  

Para ver outras maneiras de instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], confira:  

* [Instalar o SQL Server do prompt de comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)  
* [Instalar o SQL Server usando um arquivo de configuração](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)  
* [Instalar o SQL Server usando o SysPrep](../../database-engine/install-windows/install-sql-server-using-sysprep.md)  
* [Criar um novo cluster de failover do SQL Server &#40;Instalação&#41;](../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)  
* [Atualizar o SQL Server usando o Assistente de Instalação &#40;Instalação&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)

## <a name="get-the-installation-media"></a>Obtenha a mídia de instalação

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]
  
## <a name="prerequisites"></a>Prerequisites

Antes de instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], confira o tópico [Como planejar uma instalação do SQL Server](../../sql-server/install/planning-a-sql-server-installation.md).  
  
> [!NOTE]  
> Para instalações locais, você deve executar a Instalação como um administrador. Se você instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura e de execução no compartilhamento remoto.  

::: monikerRange=">=sql-server-2016 <=sql-server-2017||=sqlallproducts-allversions"

###  <a name="bkmk_ga_instalpatch"></a> Instalar o requisito de patch

A Microsoft identificou um problema com os binários de runtime do Microsoft Visual C++ 2013, que são instalados como um pré-requisito pelo SQL Server 2016 e 2017. Uma atualização está disponível para correção deste problema. Se essa atualização para os binários de runtime do Visual C++ não for instalada, o SQL Server poderá apresentar problemas de estabilidade em determinados cenários. Antes de instalar o SQL Server, siga as instruções das [Notas de versão do SQL Server](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) para ver se seu computador precisa de um patch para os binários de runtime do Visual C++. 

Isso não se aplica a [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)].

## <a name="to-install-sql-server-2016-and-2017"></a>Para instalar o SQL Server 2016 e 2017  

1. Insira a mídia de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Na pasta raiz, clique duas vezes em **Setup.exe**. Para instalar em um compartilhamento de rede, localize a pasta raiz no compartilhamento e clique duas vezes no arquivo **Setup.exe**.  
  
1. O Assistente de Instalação executa a Central de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para criar uma nova instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], selecione **Instalação**, na área de navegação esquerda, e selecione **Nova instalação autônoma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou adicionar recursos a uma instalação existente**.  

1. Na página **Chave do produto (Product Key)** , selecione uma opção para indicar se você está instalando uma edição gratuita do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou uma versão de produção que tem uma chave de PID. Para obter mais informações, consulte [Edições e recursos com suporte para o SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md).  
  
   Para continuar, selecione **Avançar**.

1. Na página dos **Termos de Licença**, examine o Contrato de Licença. Se você concordar, marque a caixa de seleção **Aceito os termos da licença** e, em seguida, selecione **Avançar**.  
    
   > [!NOTE]
   > O SQL Server transmite informações sobre sua experiência de instalação, bem como outros dados de uso e desempenho para ajudar a Microsoft a melhorar o produto. Para saber mais sobre o processamento de dados e os controles de privacidade do SQL Server, confira os tópicos [Política de privacidade](https://privacy.microsoft.com/privacystatement) e [Configurar o SQL Server para enviar comentários à Microsoft](https://docs.microsoft.com/sql/sql-server/sql-server-customer-feedback).

1. Na página **Regras Globais**, o procedimento de instalação avançará automaticamente para a página **Atualizações de Produto** se não houver nenhum erro de regra.  
  
1. A página do **Microsoft Update** será exibida em seguida se a caixa de seleção do **Microsoft Update** no **Painel de Controle** > **Todos os Itens do Painel de Controle** > **Windows Update** > **Alterar configurações** não estiver marcada. Ao marcar a caixa de seleção do **Microsoft Update**, você altera as configurações do computador para incluir as atualizações mais recentes de todos os produtos da Microsoft quando procurar atualizações do Windows.  

1. Na página **Atualizações de Produto**, nosso sistema exibe as atualizações mais recentes de produto do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] disponíveis. Se nenhuma atualização de produto for descoberta, a Instalação não exibirá essa página e avançará automaticamente para a página **Instalar Arquivos de Instalação**.  

1. Na página **Instalar Arquivos de Instalação**, a Instalação apresenta o andamento do download, da extração e da instalação dos arquivos de instalação. Se uma atualização da instalação for localizada e for especificada para ser incluída, essa atualização também será instalada. Se nenhuma atualização for encontrada, a instalação avançará automaticamente.
  
1. Na página **Regras de Instalação**, o recurso verifica possíveis problemas que podem ocorrer durante a execução da instalação. Se ocorrerem falhas, selecione um item na coluna **Status** para saber mais. Caso contrário, selecione **Avançar**.

1. Se esta for a primeira instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no computador, a página **Tipo de Instalação** será ignorada, e a instalação irá diretamente para a página **Seleção de Recursos**. Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] já estiver instalado no sistema, vá até a página **Tipo de Instalação** e escolha executar uma nova instalação ou adicionar recursos a uma instalação existente. Para continuar, selecione **Avançar**.
  
1. Na página **Seleção de Recursos**, selecione os componentes para a instalação. Por exemplo, para instalar uma nova instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)], selecione **Serviços de Mecanismo de Banco de Dados**.

    Uma descrição de cada grupo de componentes é exibida no painel **Descrição do recurso** depois que você seleciona o nome do recurso. Você pode selecionar qualquer combinação de caixas de seleção. Para saber mais, confira [Edições e componentes do SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md) e [Edições e componentes do SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md).
  
     Os pré-requisitos dos recursos selecionados são exibidos no painel **Pré-requisitos dos recursos selecionados** . A instalação instalará os pré-requisitos que não foram instalados na etapa descrita posteriormente neste procedimento.  
  
     Você pode também especificar um diretório personalizado para componentes compartilhados usando o campo na parte inferior da página **Seleção de Recursos**. Para alterar o caminho de instalação de componentes compartilhados, atualize o nome do caminho no campo fornecido, na parte inferior da caixa de diálogo, ou selecione **Procurar** para ir até um diretório de instalação. O caminho de instalação padrão é [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)].  
  
     > [!NOTE]
     > O caminho especificado para os componentes compartilhados deve ser um caminho absoluto. A pasta não deve estar compactada ou criptografada. Não há suporte para unidades mapeadas.  
  
     O SQL Server usa dois diretórios para recursos compartilhados:
  
     * Diretório de recursos compartilhados  
     * Diretório de recursos compartilhados (x86)  
  
     > [!NOTE]
     > O caminho especificado para cada uma das opções anteriores deve ser diferente.  
  
1. A página **Regras de Recurso** avançará automaticamente se todas as regras passarem.  
  
1. Na página **Configuração da Instância**, especifique se deseja instalar uma instância padrão ou uma instância nomeada. Para saber mais, veja o tópico [Configuração da instância](../../sql-server/install/instance-configuration.md#instance-configuration-page).  
  
     * **ID da Instância**: Por padrão, o nome da instância é usado como a ID da Instância. Essa ID é usada para identificar os diretórios de instalação e as chaves do Registro de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O mesmo comportamento ocorre com instâncias padrão e instâncias nomeadas. No caso de uma instância padrão, o nome da instância e a ID da Instância é MSSQLSERVER. Para usar uma ID da Instância não padrão, especifique um valor diferente na caixa de texto **ID da Instância**.  
  
       > [!NOTE]  
       > Instâncias autônomas típicas do [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)], sejam instâncias padrão ou nomeadas, não usam valores não padrão para a ID da Instância.  
  
       Todos os service packs e as atualizações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se aplicam a todos os componentes de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     * **Instâncias Instaladas**: a grade mostra todas as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que estão no computador cuja instalação está sendo executada. Se já existir uma instância padrão instalada no computador, instale uma instância nomeada do [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)].  
  
     O fluxo de trabalho do restante da instalação depende dos recursos especificados para a instalação. Talvez você não veja todas as páginas, dependendo de suas seleções. 

1. Optar pela instalação do recurso PolyBase adicionará a página **Configuração do PolyBase** à instalação do SQL Server, exibida após a página **Configuração da Instância**. O PolyBase requer o Oracle JRE 7 Update 51 (pelo menos). Se ele ainda não estiver instalado, sua instalação será bloqueada. Na página **Configuração do PolyBase**, você pode optar por usar o SQL Server como uma instância autônoma habilitada para PolyBase ou pode usar esse SQL Server como parte de um grupo de escala horizontal do PolyBase. Se optar por usar o grupo de escala horizontal, você precisará especificar um intervalo de portas com 6 portas ou mais. 


1. Use a página **Configuração do Servidor – Contas de Serviço** para especificar contas de logon para serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os serviços reais configurados nesta página dependem dos recursos selecionados para instalação. Para saber mais sobre as definições de configuração, confira [Ajuda do Assistente de Instalação](../../sql-server/install/instance-configuration.md#serverconfig).
  
     Você pode atribuir a mesma conta de logon a todos os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou configurar cada conta de serviço individualmente. Você pode, inclusive, especificar se os serviços serão iniciados automaticamente ou manualmente ou se eles serão desabilitados. Recomendamos configurar as contas de serviço individualmente para fornecer o mínimo de privilégios para cada serviço. Conceda as permissões mínimas necessárias para que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possa concluir as respectivas tarefas. Para saber mais, leia o tópico [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
     Para especificar a mesma conta de logon para todas as contas de serviço nessa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], forneça credenciais nos campos, na parte inferior da página.  
  
    > [!IMPORTANT]  
    > [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  

    > [!NOTE]
    > Do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] em diante, marque a caixa de seleção **Conceder Realizar Tarefa de Manutenção de Volume para o Serviço do Mecanismo de Banco de Dados do SQL Server** para permitir que a conta de serviço do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] use a [Inicialização Instantânea de Arquivo de Banco de Dados](../../relational-databases/databases/database-instant-file-initialization.md).
  
1. Use a página **Configuração do Servidor – Ordenação** para especificar ordenações não padrão para o [!INCLUDE[ssDE](../../includes/ssde-md.md)] e o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].    

   A configuração de instalação padrão é determinada pela localidade do SO (sistema operacional). A ordenação no nível de servidor pode ser alterada durante a instalação ou por meio da alteração da localidade do SO antes da instalação. A ordenação padrão é definida como a versão disponível mais antiga associada a cada localidade específica. Isso ocorre por motivos de compatibilidade com versões anteriores. Por isso, essa nem sempre é a ordenação recomendada. Para aproveitar ao máximo os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], altere as configurações de instalação padrão para usar ordenações do Windows. Por exemplo, para a localidade do SO **Inglês (Estados Unidos)** (página de código 1252), a ordenação padrão durante a instalação é **SQL_Latin1_General_CP1_CI_AS** e pode ser alterado para sua ordenação equivalente do Windows mais próxima, **Latin1_General_100_CI_AS_SC**.

   Para saber mais, confira [Suporte para ordenações e Unicode](../../relational-databases/collations/collation-and-unicode-support.md).  
  
1. Use a página **Configuração do Mecanismo de Banco de Dados – Configuração do Servidor** para especificar as seguintes opções:  
  
    * **Modo de segurança**: Selecione **Autenticação do Windows** ou **Autenticação de Modo Misto** para sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se você selecionar **Autenticação de Modo Misto**, forneça uma senha forte para a conta interna do administrador de sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
       Quando um dispositivo estabelecer uma conexão bem-sucedida com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o mecanismo de segurança será o mesmo para a Autenticação do Windows e a Autenticação de Modo Misto. Para saber mais, leia a página [Configuração do Mecanismo de Banco de Dados – Configuração do Servidor](../../sql-server/install/instance-configuration.md#serverconfig).
  
    * **Administradores do SQL Server**: especifique pelo menos um administrador de sistema para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para adicionar a conta sob a qual a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executada, selecione **Adicionar Usuário Atual**. Para adicionar ou remover contas da lista de administradores do sistema, selecione **Adicionar** ou **Remover** e edite a lista de usuários, grupos ou computadores que têm privilégios de administrador para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Use a página **Configuração do Mecanismo de Banco de Dados – Diretórios de Dados** para especificar diretórios de instalação não padrão. Para instalar nos diretórios padrão, selecione **Avançar**.  
  
    > [!IMPORTANT]  
    > Se você especificar diretórios de instalação não padrão, verifique se as pastas de instalação são exclusivas para essa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nenhum dos diretórios nesta caixa de diálogo deve ser compartilhado com diretórios de outras instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Para saber mais, leia a página [Configuração do Mecanismo de Banco de Dados – Diretórios de dados](../../sql-server/install/instance-configuration.md#datadir).

     Use a página **Configuração do Mecanismo de Banco de Dados – TempDB** para configurar o tamanho do arquivo, o número de arquivos, os diretórios de instalação não padrão e as configurações de ampliação de arquivo do **tempdb**. Para saber mais, veja a página [Configuração do Mecanismo de Banco de Dados – TempDB](../../sql-server/install/instance-configuration.md#tempdb). 

 
     Use a página **Configuração do Mecanismo de Banco de Dados – Fluxo de arquivos** para habilitar o fluxo de arquivos na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para saber mais, leia a página [Configuração do Mecanismo de Banco de Dados – Fluxo de arquivos](../../sql-server/install/instance-configuration.md#database-engine-configuration---filestream-page).  
  
1. Use a página **Configuração do Analysis Services – Provisionamento de Conta** para especificar o modo de servidor e os usuários ou as contas que têm permissões de administrador no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. O modo de servidor determina quais subsistemas de memória e de armazenamento são usados no servidor. Tipos de solução diferentes são executados em modos de servidor diferentes. Se você pretende executar bancos de dados de cubo multidimensionais no servidor, escolha a opção padrão do modo de servidor **Multidimensional e Mineração de Dados**.

    Especifique pelo menos um administrador de sistema para o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]:

    * Para adicionar a conta na qual a instalação do SQL Server está sendo executada, selecione **Adicionar Usuário Atual**.

    * Para adicionar ou remover contas da lista de administradores do sistema, selecione **Adicionar** ou **Remover** e edite a lista de usuários, grupos ou computadores que têm privilégios de administrador no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].

    Para saber mais sobre permissões de administrador e modo de servidor, veja a página [Configuração do Analysis Services – Provisionamento de conta](../../sql-server/install/instance-configuration.md#analysis-services-configuration---account-provisioning-page).

    Quando concluir a edição da lista, selecione **OK**. Verifique a lista de administradores na caixa de diálogo de configuração. Quando concluir a lista, selecione **Avançar**.

    Use a página **Configuração do Analysis Services – Diretórios de Dados** para especificar diretórios de instalação não padrão. Para instalar nos diretórios padrão, selecione **Avançar**.  

    > [!IMPORTANT]  
    > Se você especificar o mesmo caminho de diretório para INSTANCEDIR e SQLUSERDBDIR quando instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o SQL Server Agent e a pesquisa de texto completo não serão iniciados devido à ausência de permissões.  
    >  
    > Se você especificar diretórios de instalação não padrão, verifique se as pastas de instalação são exclusivas para essa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nenhum dos diretórios nesta caixa de diálogo deve ser compartilhado com diretórios de outras instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

    Para saber mais, veja a página [Configuração do Analysis Services – Diretórios de Dados](../../sql-server/install/instance-configuration.md#analysis-services-configuration---data-directories-page).  

1. Use a página **Configuração do Distributed Replay Controller** para especificar os usuários aos quais você deseja conceder permissões administrativas para o serviço Distributed Replay Controller. Os usuários com permissões administrativas têm acesso ilimitado ao serviço Distributed Replay Controller.  
  
     * Para conceder permissões de acesso para o serviço Distributed Replay Controller aos usuários que estão executando a Instalação do SQL Server, selecione o botão **Adicionar Usuário Atual**.

     * Para conceder permissões de acesso a outros usuários para o serviço Distributed Replay Controller, selecione o botão **Adicionar**.

     * Para remover permissões de acesso do serviço Distributed Replay Controller, selecione o botão **Remover**.

     * Para continuar, selecione **Avançar**.  
  
1. Use a página **Configuração do Distributed Replay Client** para especificar os usuários aos quais você deseja conceder permissões administrativas para o serviço Distributed Replay Client. Os usuários com permissões administrativas têm acesso ilimitado ao serviço Distributed Replay Client.  
  
     * O **nome do controlador** é opcional. O valor padrão é \<*em branco*>. Digite o nome do controlador com o qual o computador cliente se comunicará para o serviço Distributed Replay Client:  
  
       * Se já configurou um controlador, digite o respectivo nome enquanto configura cada cliente.  
  
       * Se ainda não configurou um controlador, pode deixar o nome em branco. No entanto, digite manualmente o nome do controlador no arquivo de **configuração do cliente** .  
  
     * Especifique o **Diretório de Trabalho** para o serviço Distributed Replay Client. O diretório de trabalho padrão é \<*drive letter*>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\WorkingDir\\.  
  
     * Especifique o **Diretório de Resultado** para o serviço Distributed Replay Client. O diretório de resultado padrão é \<*drive letter*>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\ResultDir\\.  
  
     * Para continuar, selecione **Avançar**.  
  
1. A página **Pronto para Instalar** mostra uma exibição de árvore das opções especificadas durante a instalação. Nesta página, a instalação indica se o recurso **Atualização de Produto** está habilitado ou desabilitado e mostra a versão final da atualização.  
  
     Para continuar, selecione **Instalar**. A instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalará primeiro os pré-requisitos exigidos para os recursos selecionados, seguidos da instalação desses recursos.  
  
1. Durante a instalação, a página **Progresso da Instalação** fornece atualizações do status para que você possa monitorar o andamento da instalação.  
  
1. Após a instalação, a página **Concluído** fornece um link para o arquivo de log de resumo da instalação e outras observações importantes.
  
    > [!IMPORTANT]
    > Não deixe de ler a mensagem do Assistente de Instalação, quando concluir a instalação. Para saber mais, veja [Exibir e ler arquivos de log da instalação do SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).

    Para concluir o processo de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], selecione **Fechar**.  
  
1. Se você for orientado a reiniciar o computador, faça isso nessa ocasião.

::: moniker-end

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions" 
## <a name="to-install-sql-server-2019"></a>Para instalar o SQL Server 2019 
  
1. Insira a mídia de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Na pasta raiz, clique duas vezes em **Setup.exe**. Para instalar em um compartilhamento de rede, localize a pasta raiz no compartilhamento e clique duas vezes no arquivo **Setup.exe**.  
  
1. O Assistente de Instalação executa a Central de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para criar uma nova instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], selecione **Instalação**, na área de navegação esquerda, e selecione **Nova instalação autônoma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou adicionar recursos a uma instalação existente**.  

1. Na página **Chave do produto (Product Key)** , selecione uma opção para indicar se você está instalando uma edição gratuita do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou uma versão de produção que tem uma chave de PID. Para obter mais informações, consulte [Edições e recursos com suporte para o SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-version-15.md).  
  
   Para continuar, selecione **Avançar**.
  
1. Na página dos **Termos de Licença**, examine o Contrato de Licença. Se você concordar, marque a caixa de seleção **Aceito os termos da licença e a [política de privacidade](https://privacy.microsoft.com/privacystatement)** e, em seguida, selecione **Avançar**.  

   > [!NOTE]
   > Se uma chave do produto (Product Key) de licença do Enterprise Server/CAL for inserida e o computador tiver mais que 20 núcleos físicos ou 40 núcleos lógicos quando o Hyper-Threading estiver habilitado, será exibido um aviso durante a instalação. Você ainda pode continuar a instalação marcando a caixa de seleção **Marque esta caixa para reconhecer esta limitação ou clique em Voltar/Cancelar para inserir uma licença do produto Enterprise Core compatível com o máximo do sistema operacional** ou clique em **Voltar** e insira uma chave de licença compatível com o número máximo de processadores do sistema operacional.

   > [!NOTE]
   > O SQL Server transmite informações sobre sua experiência de instalação, bem como outros dados de uso e desempenho para ajudar a Microsoft a melhorar o produto. Para saber mais sobre o processamento de dados e os controles de privacidade do SQL Server, confira os tópicos [Política de privacidade](https://privacy.microsoft.com/privacystatement) e [Configurar o SQL Server para enviar comentários à Microsoft](https://docs.microsoft.com/sql/sql-server/sql-server-customer-feedback).

1. Na página **Regras Globais**, o procedimento de instalação avançará automaticamente para a página **Atualizações de Produto** se não houver nenhum erro de regra.  
  
1. A página do **Microsoft Update** será exibida em seguida se a caixa de seleção do **Microsoft Update** no **Painel de Controle** > **Todos os Itens do Painel de Controle** > **Windows Update** > **Alterar configurações** não estiver marcada. Ao marcar a caixa de seleção do **Microsoft Update**, você altera as configurações do computador para incluir as atualizações mais recentes de todos os produtos da Microsoft quando procurar atualizações do Windows.  

1. Na página **Atualizações de Produto**, nosso sistema exibe as atualizações mais recentes de produto do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] disponíveis. Se nenhuma atualização de produto for descoberta, a Instalação não exibirá essa página e avançará automaticamente para a página **Instalar Arquivos de Instalação**.  

1. Na página **Instalar Arquivos de Instalação**, a Instalação apresenta o andamento do download, da extração e da instalação dos arquivos de instalação. Se uma atualização da instalação for localizada e for especificada para ser incluída, essa atualização também será instalada. Se nenhuma atualização for encontrada, a instalação avançará automaticamente.
  
1. Na página **Regras de Instalação**, o recurso verifica possíveis problemas que podem ocorrer durante a execução da instalação. Se ocorrerem falhas, selecione um item na coluna **Status** para saber mais. Caso contrário, selecione **Avançar**.

1. Se esta for a primeira instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no computador, a página **Tipo de Instalação** será ignorada, e a instalação irá diretamente para a página **Seleção de Recursos**. Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] já estiver instalado no sistema, vá até a página **Tipo de Instalação** e escolha executar uma nova instalação ou adicionar recursos a uma instalação existente. Para continuar, selecione **Avançar**.
  
1. Na página **Seleção de Recursos**, selecione os componentes para a instalação. Por exemplo, para instalar uma nova instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)], selecione **Serviços de Mecanismo de Banco de Dados**.

    Uma descrição de cada grupo de componentes é exibida no painel **Descrição do recurso** depois que você seleciona o nome do recurso. Você pode selecionar qualquer combinação de caixas de seleção. Para saber mais, confira [Edições e componentes do SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md) e [Edições e componentes do SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md).
  
     Os pré-requisitos dos recursos selecionados são exibidos no painel **Pré-requisitos dos recursos selecionados** . A instalação instalará os pré-requisitos que não foram instalados na etapa descrita posteriormente neste procedimento.  
  
     Você pode também especificar um diretório personalizado para componentes compartilhados usando o campo na parte inferior da página **Seleção de Recursos**. Para alterar o caminho de instalação de componentes compartilhados, atualize o nome do caminho no campo fornecido, na parte inferior da caixa de diálogo, ou selecione **Procurar** para ir até um diretório de instalação. O caminho de instalação padrão é [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)].  
  
     > [!NOTE]
     > O caminho especificado para os componentes compartilhados deve ser um caminho absoluto. A pasta não deve estar compactada ou criptografada. Não há suporte para unidades mapeadas.  
  
     O SQL Server usa dois diretórios para recursos compartilhados:
  
     * Diretório de recursos compartilhados  
     * Diretório de recursos compartilhados (x86)  
  
     > [!NOTE]
     > O caminho especificado para cada uma das opções anteriores deve ser diferente.  
  
1. A página **Regras de Recurso** avançará automaticamente se todas as regras passarem.  
  
1. Na página **Configuração da Instância**, especifique se deseja instalar uma instância padrão ou uma instância nomeada. Para saber mais, veja o tópico [Configuração da instância](../../sql-server/install/instance-configuration.md#instance-configuration-page).  
  
     * **ID da Instância**: Por padrão, o nome da instância é usado como a ID da Instância. Essa ID é usada para identificar os diretórios de instalação e as chaves do Registro de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O mesmo comportamento ocorre com instâncias padrão e instâncias nomeadas. No caso de uma instância padrão, o nome da instância e a ID da Instância é MSSQLSERVER. Para usar uma ID da Instância não padrão, especifique um valor diferente na caixa de texto **ID da Instância**.  
  
       > [!NOTE]  
       > Instâncias autônomas típicas do [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)], sejam instâncias padrão ou nomeadas, não usam valores não padrão para a ID da Instância.  
  
       Todos os service packs e as atualizações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se aplicam a todos os componentes de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     * **Instâncias Instaladas**: a grade mostra todas as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que estão no computador cuja instalação está sendo executada. Se já existir uma instância padrão instalada no computador, instale uma instância nomeada do [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)].  
  
     O fluxo de trabalho do restante da instalação depende dos recursos especificados para a instalação. Talvez você não veja todas as páginas, dependendo de suas seleções. 

1. Do [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] em diante, o Polybase não exige mais que o Oracle JRE 7 Update 51 (no mínimo) esteja pré-instalado no computador antes de instalar o recurso. Optar pela instalação do recurso Polybase adicionará a página **Local da Instalação do Java** à instalação do SQL Server exibida após a página **Configuração da Instância**. Na página Localização da Instalação do Java, você pode optar por instalar o Azul Zulu Open JRE incluído com a instalação do [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] ou por fornecer a localização de um JRE ou JDK diferente que já foi instalado no computador.

1. Do [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] em diante, o Java foi adicionado com Extensões de Linguagem. Optar pela instalação do recurso de Java adicionará a página **Localização de Instalação do Java** à janela de instalação do SQL Server, exibida após a página **Configuração da Instância**. Na página **Localização da Instalação do Java**, você pode optar por instalar o Azul Zulu Open JRE incluído com a instalação do [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] ou por fornecer a localização de um JRE ou JDK diferente que já foi instalado no computador.

1. Use a página **Configuração do Servidor – Contas de Serviço** para especificar contas de logon para serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os serviços reais configurados nesta página dependem dos recursos selecionados para instalação. Para saber mais sobre as definições de configuração, confira [Ajuda do Assistente de Instalação](../../sql-server/install/instance-configuration.md#serverconfig).
  
     Você pode atribuir a mesma conta de logon a todos os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou configurar cada conta de serviço individualmente. Você pode, inclusive, especificar se os serviços serão iniciados automaticamente ou manualmente ou se eles serão desabilitados. Recomendamos configurar as contas de serviço individualmente para fornecer o mínimo de privilégios para cada serviço. Conceda as permissões mínimas necessárias para que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possa concluir as respectivas tarefas. Para saber mais, leia o tópico [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
     Para especificar a mesma conta de logon para todas as contas de serviço nessa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], forneça credenciais nos campos, na parte inferior da página.  
  
    > [!IMPORTANT]  
    > [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  

    > [!NOTE]
    > Do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] em diante, marque a caixa de seleção **Conceder Realizar Tarefa de Manutenção de Volume para o Serviço do Mecanismo de Banco de Dados do SQL Server** para permitir que a conta de serviço do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] use a [Inicialização Instantânea de Arquivo de Banco de Dados](../../relational-databases/databases/database-instant-file-initialization.md).
  
     Use a página **Configuração do Servidor – Ordenação** para especificar ordenações não padrão para o [!INCLUDE[ssDE](../../includes/ssde-md.md)] e o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para saber mais, confira [Suporte para ordenações e Unicode](../../relational-databases/collations/collation-and-unicode-support.md).  
  
1. Use a página **Configuração do Mecanismo de Banco de Dados – Configuração do Servidor** para especificar as seguintes opções:  
  
    * **Modo de segurança**: Selecione **Autenticação do Windows** ou **Autenticação de Modo Misto** para sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se você selecionar **Autenticação de Modo Misto**, forneça uma senha forte para a conta interna do administrador de sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
       Quando um dispositivo estabelecer uma conexão bem-sucedida com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o mecanismo de segurança será o mesmo para a Autenticação do Windows e a Autenticação de Modo Misto. Para saber mais, leia a página [Configuração do Mecanismo de Banco de Dados – Configuração do Servidor](../../sql-server/install/instance-configuration.md#serverconfig).
  
    * **Administradores do SQL Server**: especifique pelo menos um administrador de sistema para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para adicionar a conta sob a qual a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executada, selecione **Adicionar Usuário Atual**. Para adicionar ou remover contas da lista de administradores do sistema, selecione **Adicionar** ou **Remover** e edite a lista de usuários, grupos ou computadores que têm privilégios de administrador para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Use a página **Configuração do Mecanismo de Banco de Dados – Diretórios de Dados** para especificar diretórios de instalação não padrão. Para instalar nos diretórios padrão, selecione **Avançar**.  
  
    > [!IMPORTANT]  
    > Se você especificar diretórios de instalação não padrão, verifique se as pastas de instalação são exclusivas para essa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nenhum dos diretórios nesta caixa de diálogo deve ser compartilhado com diretórios de outras instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Para saber mais, leia a página [Configuração do Mecanismo de Banco de Dados – Diretórios de dados](../../sql-server/install/instance-configuration.md#datadir).

     Use a página **Configuração do Mecanismo de Banco de Dados – TempDB** para configurar o tamanho do arquivo, o número de arquivos, os diretórios de instalação não padrão e as configurações de ampliação de arquivo do **tempdb**. Para saber mais, veja a página [Configuração do Mecanismo de Banco de Dados – TempDB](../../sql-server/install/instance-configuration.md#tempdb).

     Use a página **Configuração do [!INCLUDE[ssDE](../../includes/ssde-md.md)] – MaxDOP** para especificar o grau máximo de paralelismo. Essa configuração determina a quantidade de processadores que uma única instrução pode usar durante a execução. O valor recomendado é calculado automaticamente durante a instalação. 
     
    > [!NOTE]  
    > Esta página só está disponível na Configuração a partir do [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]. 
    
    Para saber mais, veja a [página Configuração do Mecanismo de Banco de Dados – MaxDOP](https://docs.microsoft.com/sql/sql-server/install/instance-configuration?view=sql-server-ver15#maxdop). 

     Use a página **Configuração do Mecanismo de Banco de Dados – Memória** para especificar os valores **memória mínima do servidor** e **memória máxima do servidor** que esta instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usará após a inicialização. Use os valores padrão, os valores recomendados calculados ou especifique manualmente seus próprios valores, depois de escolher a opção **Recomendado**.
     
    > [!NOTE]  
    > Esta página só está disponível na Configuração a partir do [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]. 
    
    Para saber mais, veja a [página Configuração do Mecanismo de Banco de Dados – Memória](https://docs.microsoft.com/sql/sql-server/install/instance-configuration?view=sql-server-ver15#memory). 

     Use a página **Configuração do Mecanismo de Banco de Dados – Fluxo de arquivos** para habilitar o fluxo de arquivos na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para saber mais, leia a página [Configuração do Mecanismo de Banco de Dados – Fluxo de arquivos](../../sql-server/install/instance-configuration.md#database-engine-configuration---filestream-page).  
  
1. Use a página **Configuração do Analysis Services – Provisionamento de Conta** para especificar o modo de servidor e os usuários ou as contas que têm permissões de administrador no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. O modo de servidor determina quais subsistemas de memória e de armazenamento são usados no servidor. Tipos de solução diferentes são executados em modos de servidor diferentes. Se você pretende executar bancos de dados de cubo multidimensionais no servidor, escolha a opção padrão do modo de servidor **Multidimensional e Mineração de Dados**.

    Especifique pelo menos um administrador de sistema para o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]:

    * Para adicionar a conta na qual a instalação do SQL Server está sendo executada, selecione **Adicionar Usuário Atual**.

    * Para adicionar ou remover contas da lista de administradores do sistema, selecione **Adicionar** ou **Remover** e edite a lista de usuários, grupos ou computadores que têm privilégios de administrador no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].

    Para saber mais sobre permissões de administrador e modo de servidor, veja a página [Configuração do Analysis Services – Provisionamento de conta](../../sql-server/install/instance-configuration.md#analysis-services-configuration---account-provisioning-page).

    Quando concluir a edição da lista, selecione **OK**. Verifique a lista de administradores na caixa de diálogo de configuração. Quando concluir a lista, selecione **Avançar**.

    Use a página **Configuração do Analysis Services – Diretórios de Dados** para especificar diretórios de instalação não padrão. Para instalar nos diretórios padrão, selecione **Avançar**.  

    > [!IMPORTANT]  
    > Se você especificar o mesmo caminho de diretório para INSTANCEDIR e SQLUSERDBDIR quando instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o SQL Server Agent e a pesquisa de texto completo não serão iniciados devido à ausência de permissões.  
    >  
    > Se você especificar diretórios de instalação não padrão, verifique se as pastas de instalação são exclusivas para essa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nenhum dos diretórios nesta caixa de diálogo deve ser compartilhado com diretórios de outras instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

    Para saber mais, veja a página [Configuração do Analysis Services – Diretórios de Dados](../../sql-server/install/instance-configuration.md#analysis-services-configuration---data-directories-page).  

1. Use a página **Configuração do Distributed Replay Controller** para especificar os usuários aos quais você deseja conceder permissões administrativas para o serviço Distributed Replay Controller. Os usuários com permissões administrativas têm acesso ilimitado ao serviço Distributed Replay Controller.  
  
     * Para conceder permissões de acesso para o serviço Distributed Replay Controller aos usuários que estão executando a Instalação do SQL Server, selecione o botão **Adicionar Usuário Atual**.

     * Para conceder permissões de acesso a outros usuários para o serviço Distributed Replay Controller, selecione o botão **Adicionar**.

     * Para remover permissões de acesso do serviço Distributed Replay Controller, selecione o botão **Remover**.

     * Para continuar, selecione **Avançar**.  
  
1. Use a página **Configuração do Distributed Replay Client** para especificar os usuários aos quais você deseja conceder permissões administrativas para o serviço Distributed Replay Client. Os usuários com permissões administrativas têm acesso ilimitado ao serviço Distributed Replay Client.  
  
     * O **nome do controlador** é opcional. O valor padrão é \<*em branco*>. Digite o nome do controlador com o qual o computador cliente se comunicará para o serviço Distributed Replay Client:  
  
       * Se já configurou um controlador, digite o respectivo nome enquanto configura cada cliente.  
  
       * Se ainda não configurou um controlador, pode deixar o nome em branco. No entanto, digite manualmente o nome do controlador no arquivo de **configuração do cliente** .  
  
     * Especifique o **Diretório de Trabalho** para o serviço Distributed Replay Client. O diretório de trabalho padrão é \<*drive letter*>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\WorkingDir\\.  
  
     * Especifique o **Diretório de Resultado** para o serviço Distributed Replay Client. O diretório de resultado padrão é \<*drive letter*>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\ResultDir\\.  
  
     * Para continuar, selecione **Avançar**.  
  
1. A página **Pronto para Instalar** mostra uma exibição de árvore das opções especificadas durante a instalação. Nesta página, a instalação indica se o recurso **Atualização de Produto** está habilitado ou desabilitado e mostra a versão final da atualização.  
  
     Para continuar, selecione **Instalar**. A instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalará primeiro os pré-requisitos exigidos para os recursos selecionados, seguidos da instalação desses recursos.  
  
1. Durante a instalação, a página **Progresso da Instalação** fornece atualizações do status para que você possa monitorar o andamento da instalação.  
  
1. Após a instalação, a página **Concluído** fornece um link para o arquivo de log de resumo da instalação e outras observações importantes.
  
    > [!IMPORTANT]
    > Não deixe de ler a mensagem do Assistente de Instalação, quando concluir a instalação. Para saber mais, veja [Exibir e ler arquivos de log da instalação do SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).

    Para concluir o processo de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], selecione **Fechar**.  
  
1. Se você for orientado a reiniciar o computador, faça isso nessa ocasião.

::: moniker-end

## <a name="next-steps"></a>Próximas etapas

[Configure a nova instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]](https://docs.microsoft.com/sql/database-engine/configure-windows/database-engine-instances-sql-server?view=sql-server-2017).  
  
Para reduzir a área da superfície de um sistema vulnerável a ataques, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala e habilita seletivamente serviços e recursos essenciais. Para saber mais, veja o tópico [Configuração de área da superfície](../../relational-databases/security/surface-area-configuration.md).  
  
## <a name="see-also"></a>Confira também
  
* [Validar uma instalação do SQL Server](../../database-engine/install-windows/validate-a-sql-server-installation.md)  
* [Reparar uma instalação com falha do SQL Server](../../database-engine/install-windows/repair-a-failed-sql-server-installation.md)
* [Exibir e ler arquivos de log da instalação do SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)
* [Atualizar o SQL Server usando o Assistente de Instalação &#40;Instalação&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)
* [Instalar o SQL Server do prompt de comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md) 
