---
title: Instalar o SQL Server usando o SysPrep | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: install
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 11f4ed8a-aaa9-417b-bdd5-204f551c6bb6
caps.latest.revision: 29
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: craigg
ms.openlocfilehash: 3b8678535c387a6ca1117d4e2851c57632573da1
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40406574"
---
# <a name="install-sql-server-with-sysprep"></a>Instalar o SQL Server com o SysPrep

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem ser acessadas por meio da Central de Instalação. A página **Avançado** da **Central de Instalação** tem duas opções: **Preparação de imagem de uma instância autônoma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** e **Conclusão de imagem de uma instância autônoma preparada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**. As seções [Preparar](#prepare) e [Concluir](#complete) descrevem o processo de instalação em detalhes. Para obter mais informações, consulte [Considerations for Installing SQL Server Using SysPrep](../../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md). 
  
Você também pode preparar e concluir uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o prompt de comando ou um arquivo de configuração. Para obter mais informações, consulte:  
  
- [Instalar o SQL Server do prompt de comando](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)  
  
- [Instalar o SQL Server usando um arquivo de configuração](../../database-engine/install-windows/install-sql-server-using-a-configuration-file.md)  
  
## <a name="prerequisites"></a>Prerequisites  
Antes de instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], examine os artigos em [Planejando uma instalação do SQL Server](../../sql-server/install/planning-a-sql-server-installation.md). 
  
Para obter mais informações sobre as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os requisitos de hardware e software, consulte [Requisitos de hardware e software para a instalação do SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md). 
    
##  <a name="sysprep"></a> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep  
 A partir do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], o SysPrep dá suporte a instâncias clusterizadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em instalações de linha de comando. Para saber mais, consulte [O que é Sysprep?](http://msdn.microsoft.com/library/cc721940\(v=WS.10\).aspx). 
  
### <a name="to-prepare-a-includessnoversionincludesssnoversion-mdmd-failover-cluster-unattended"></a>Para preparar um cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (autônomo)  
  
1. Prepare a imagem (como discutido em [Considerações para instalação do SQL Server usando SysPrep](../../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md)) e capturar a imagem da janela com a generalização do SysPrep. O exemplo a seguir prepara a imagem:  
  
    ```  
    Setup.exe /q /ACTION=PrepareImage l /FEATURES=SQLEngine /InstanceID =<MYINST> /IACCEPTSQLSERVERLICENSETERMS  
    ```  
  
     Em seguida, execute a Generalização do Windows SysPrep. 
  
2. Implante a imagem executando o Windows SysPrep Specialize. 
  
3. Criar o cluster de failover do Windows. 
  
4. Execute o setup.exe com **/ACTION=PrepareFailoverCluster** em todos os nós. Por exemplo:  
  
    ```  
    setup.exe /q /ACTION=PrepareFailoverCluster /InstanceName=<InstanceName> /Features=SQLEngine  /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="xxxxxxxxxxx"  /IACCEPTSQLSERVERLICENSETERMS  
    ```  
  
### <a name="complete-a-includessnoversionincludesssnoversion-mdmd-failover-cluster-unattended"></a>Concluir um cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (autônomo)  
  
1. Execute setup.exe com **/ACTION=CompleteFailoverCluster** no nó que possui o grupo de armazenamento disponível:  
  
    ```  
    setup.exe /q /ACTION=CompleteFailoverCluster /InstanceName=<InstanceName>  /FAILOVERCLUSTERDISKS="<Cluster Disk Resource Name - for example, 'Disk S:'>:" /FAILOVERCLUSTERNETWORKNAME="<Insert FOI Network Name>" /FAILOVERCLUSTERIPADDRESSES="IPv4;xx.xxx.xx.xx;Cluster Network;xxx.xxx.xxx.x" /FAILOVERCLUSTERGROUP="MSSQLSERVER" /INSTALLSQLDATADIR="<Drive>:\<Path>\MSSQLSERVER" /SQLCOLLATION="SQL_Latin1_General_CP1_CS_AS" /SQLSYSADMINACCOUNTS="<DomainName\UserName>"  
    ```  
  
### <a name="adding-a-node-to-an-existing-includessnoversionincludesssnoversion-mdmd-failover-cluster-unattended"></a>Adicionando um nó a um cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] existente (autônomo)  
  
1. Implante a imagem executando o Windows SysPrep Specialize. 
  
2. Unir o cluster de failover do Windows. 
  
3. Execute setup.exe com **/ACTION=AddNode** em todos os nós:  
  
    ```  
    setup.exe /q /ACTION=AddNode /InstanceName=<InstanceName> /Features=SQLEngine  /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="xxxxxxxxxxx"  /IACCEPTSQLSERVERLICENSETERMS  
    ```  
  
##  <a name="prepare"></a> Preparar imagem  
  
### <a name="prepare-a-stand-alone-instance-of-includessnoversionincludesssnoversion-mdmd"></a>Preparar uma instância autônoma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
  
1. Insira a mídia de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Na pasta raiz, clique duas vezes em Setup.exe. Para instalar a partir de um compartilhamento de rede, localize a pasta raiz no compartilhamento e clique duas vezes em Setup.exe. 
  
2. O Assistente de Instalação executa a Central de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para preparar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], clique em **Preparação de imagem de uma instância autônoma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** na página **Avançado**. 
  
3. O Verificador de Configuração do Sistema executa uma operação de descoberta no computador. Para continuar, clique em **OK**. Você pode exibir os detalhes na tela clicando em **Mostrar Detalhes**ou como um relatório HTML clicando em **Exibir relatório detalhado**. 
  
4. Na página Atualizações de Produto, as atualizações mais recentes de produtos disponíveis do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são exibidas. Se você não desejar incluir as atualizações, desmarque a caixa de seleção **Incluir atualizações de produto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**. Se nenhuma atualização de produto for descoberta, a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não exibirá esta página e avançará automaticamente para a página **Instalar Arquivos de Instalação** . 
  
5. Na página Instalar Arquivos de Instalação, a Instalação apresenta o andamento do download, da extração e da instalação dos arquivos de Instalação. Se uma atualização para a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for localizada, e for especificada para ser incluída, essa atualização também será instalada. 
  
6. O Verificador de Configuração do Sistema verifica o estado do sistema do computador antes da continuação da instalação. Você pode exibir os detalhes na tela clicando em **Mostrar Detalhes**ou como um relatório HTML clicando em **Exibir relatório detalhado**. 
  
7. Na página **Preparar Tipo de Imagem**, selecione **Preparar uma nova instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**. 
  
     A página **Preparar Tipo de Imagem** é exibida apenas quando há uma instância preparada não configurada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no computador. Você pode querer preparar uma nova instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou adicionar os recursos do sys prep a uma instância preparada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na máquina. Para obter mais informações sobre como acrescentar recursos a uma instância preparada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consulte [Adicionar recursos a uma instância preparada](#AddFeatures). 
  
8. Na página **Termos de Licença** , leia o contrato de licença e marque a caixa de seleção para aceitar os termos e as condições da licença. Para ajudar a aperfeiçoar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você também pode habilitar a opção de uso de recursos e enviar relatórios à [!INCLUDE[msCoName](../../includes/msconame-md.md)]. 
  
9. Na página **Seleção de Recursos** , selecione os componentes para a instalação:  
  
    |||  
    |-|-|  
    |[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SysPrep|[!INCLUDE[ssDE](../../includes/ssde-md.md)]<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replicação<br /><br /> Recursos de texto completo<br /><br /> Data Quality Services<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em modo Nativo<br /><br /> [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]<br /><br /> Recursos Redistribuíveis<br /><br /> Recursos compartilhados|  
  
     Uma descrição de cada grupo de componentes é exibida no painel à direita quando você realça o nome do recurso. Você pode selecionar qualquer combinação de caixas de seleção. Para obter mais informações, consulte [Edições e recursos com suporte do SQL Server](../../sql-server/editions-and-components-of-sql-server-2017.md). 
  
     Os pré-requisitos dos recursos selecionados são exibidos no painel à direita. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A Instalação instalará os pré-requisitos ainda não instalados na etapa de instalação descrita posteriormente neste procedimento. 
  
10. Na página **Regras de Preparação de Imagem** , o Verificador de Configuração do Sistema verifica o estado do sistema do computador antes de a Instalação continuar. Você pode exibir os detalhes na tela clicando em **Mostrar Detalhes**ou como um relatório HTML clicando em **Exibir relatório detalhado**. 
  
11. Na página Configuração da Instância, especifique a ID da instância. Clique em **Avançar** para continuar. 
  
     **ID da Instância** — É usada para identificar os diretórios de instalação e as chaves do registro da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esse é o caso para instâncias padrão e instâncias nomeadas. Se a instância preparada for concluída como instância padrão durante a etapa Concluir, o nome da instância será sobrescrito como MSSQLSERVER. A ID da Instância permanecerá a mesma especificada. 
  
     **Diretório raiz da instância** — Por padrão, o diretório raiz da instância é [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]. Para especificar um diretório raiz não padrão, use o campo fornecido ou clique em **Procurar** para localizar uma pasta de instalação. O diretório especificado na etapa de preparação será usado durante a configuração na etapa Concluir. 
  
     Todos os service packs e atualizações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serão aplicados a cada componente de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
  
     **Instâncias Instaladas** — A grade mostra as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que estão no computador em que a Instalação está sendo executada. 
  
12. A página **Requisitos de Espaço em Disco** calcula o espaço em disco necessário para os recursos especificados. Em seguida, ele compara o espaço necessário com o espaço em disco disponível. 
  
13. O Verificador de Configuração do Sistema executará as regras de preparação de imagem para validar a configuração do computador com os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificados. Você pode exibir os detalhes na tela clicando em **Mostrar Detalhes**ou como um relatório HTML clicando em **Exibir relatório detalhado**. 
  
14. A página **Pronto para Preparar Imagem** mostra uma exibição de árvore das opções de instalação que foram especificadas durante a Instalação. Nesta página, a Instalação indica se o recurso Atualização de Produto está habilitado ou desabilitado e a versão da atualização final. Para continuar, clique em **Preparar**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A Instalação instalará primeiro os pré-requisitos exigidos para os recursos selecionados, seguidos da instalação dos recursos. 
  
15. Durante a instalação, a página **Progresso da Preparação de Imagem** fornece o status para que você possa monitorar o progresso da Instalação. 
  
16. Após a instalação, a página **Concluído** fornece um link para o arquivo de log de resumo da instalação e outras observações importantes. Para concluir o processo de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , clique em **Fechar**. 
  
17. Se você for instruído a reiniciar o computador, faça-o agora. É importante ler a mensagem do Assistente de Instalação ao concluir a Instalação. Para obter mais informações, consulte [View and Read SQL Server Setup Log Files](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md). 
  
18. Isto conclui a etapa de preparação. Você pode concluir a imagem ou implantar a imagem preparada conforme descrito em [Considerations for Installing SQL Server Using SysPrep](../../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md). 
  
##  <a name="complete"></a> Concluir Imagem  
  
### <a name="complete-a-prepared-instance-of-includessnoversionincludesssnoversion-mdmd"></a>Concluir uma instância preparada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
1. Se você tiver uma instância preparada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluída na imagem de seu computador, verá um atalho no Menu Iniciar. Você também pode iniciar a Central de Instalação e clicar em **Conclusão de imagem de uma instância autônoma preparada** na página **Avançado** . 
  
2. O Verificador de Configuração do Sistema executa uma operação de descoberta no computador. Para continuar, clique em **OK**. Você pode exibir os detalhes na tela clicando em **Mostrar Detalhes**ou como um relatório HTML clicando em **Exibir relatório detalhado**. 
  
3. Na página **Arquivos de Suporte à Instalação** , clique em **Instalar** para instalar os arquivos de suporte à Instalação. 
  
4. O Verificador de Configuração do Sistema verifica o estado do sistema do computador antes da continuação da instalação. Depois de concluir a verificação, clique em **Avançar** para continuar. Você pode exibir os detalhes na tela clicando em **Mostrar Detalhes**ou como um relatório HTML clicando em **Exibir relatório detalhado**. 
  
5. Na página **Chave do Produto (Product Key)** , selecione um botão de opção para indicar se você está instalando uma edição gratuita do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ou uma versão de produção do produto que tem uma chave de PID. Para obter mais informações, consulte [Edições e recursos com suporte do SQL Server](../../sql-server/editions-and-components-of-sql-server-2017.md). Se você estiver instalando a edição Evaluation, o período de avaliação de 180 dias iniciará quando você concluir esta etapa. 
  
6. Na página **Termos de Licença** , leia o contrato de licença e marque a caixa de seleção para aceitar os termos e as condições da licença. Para ajudar a aperfeiçoar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você também pode habilitar a opção de uso de recursos e enviar relatórios à [!INCLUDE[msCoName](../../includes/msconame-md.md)]. 
  
7. Na página **Selecione uma Instância Preparada** , selecione a instância preparada que você deseja concluir na caixa suspensa. Selecione a instância não configurada na lista **ID da Instância** . 
  
     **Instâncias instaladas:** Esta grade exibe todas as instâncias que incluem qualquer instância preparada nesta máquina. 
  
8. Na página **Revisão de Recurso** , você verá os recursos selecionados e os componentes incluídos na instalação durante a etapa de preparação. Se você desejar acrescentar mais recursos a sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não incluído na instância preparada, você deverá concluir esta etapa primeiro para concluir a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e, em seguida, adicione os recursos em **Adicionar Recursos** na **Central de Instalação**. 
  
    > [!NOTE]  
    >  Você pode adicionar recursos que estão disponíveis para a versão de produto que você está instalando. Para obter mais informações, consulte [Edições e recursos com suporte do SQL Server](../../sql-server/editions-and-components-of-sql-server-2017.md).  
  
9. Na página Configuração da Instância, especifique o nome da instância para a instância preparada. Esse será o nome da instância depois que você concluir a configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Clique em **Avançar** para continuar. 
  
     **ID da Instância** — É usada para identificar os diretórios de instalação e as chaves do registro da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esse é o caso para instâncias padrão e instâncias nomeadas. Se a instância preparada for concluída como instância padrão durante a etapa Concluir, o nome da instância será sobrescrito como MSSQLSERVER. A ID da Instância permanecerá a mesma especificada durante a etapa de preparação. 
  
     **Diretório raiz da instância** —O diretório especificado na etapa de preparação será usado e não poderá ser modificado nesta etapa. 
  
     Todos os service packs e atualizações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serão aplicados a cada componente de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
  
     **Instâncias instaladas** — A grade mostra as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que estão no computador onde a Instalação está sendo executada. 
  
10. O fluxo de trabalho do restante deste artigo depende dos recursos que foram selecionados durante a etapa de preparação. Talvez você não veja todas as páginas, dependendo das seleções. 
  
11. Na página **Configuração do Servidor** — Contas de Serviço, especifique contas de logon para os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Os serviços reais configurados nessa página dependem dos recursos selecionados para instalação. 
  
     Você pode atribuir a mesma conta de logon a todos os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou configurar cada conta de serviço individualmente. Você também pode especificar se os serviços serão iniciados automaticamente ou manualmente, ou se eles serão desabilitados. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que você configure contas de serviço individualmente para fornecer privilégios mínimos para cada serviço, em que os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recebem as permissões mínimas para concluir suas tarefas. Para obter mais informações, consulte [Configuração do servidor — Contas de serviço](http://msdn.microsoft.com/library/c283702d-ab20-4bfa-9272-f0c53c31cb9f) e [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md). 
  
     Para especificar a mesma conta de logon para todas as contas de serviço nessa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], forneça credenciais nos campos na parte inferior da página. 
  
     **Observação de segurança** [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
     Depois de concluir a especificação de informações de logon para serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , clique em **Avançar**. 
  
12. Use a guia **Configuração do Servidor – Agrupamento** para especificar agrupamentos não padrão para o [!INCLUDE[ssDE](../../includes/ssde-md.md)] e o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para obter mais informações, consulte [Configuração do SQL Server – Agrupamento](http://msdn.microsoft.com/library/e3986870-5be4-458b-b671-5ff12a27b022). 
  
13. Use a página Configuração – Provisionamento de Conta do [!INCLUDE[ssDE](../../includes/ssde-md.md)] para especificar o seguinte:  
  
    - Modo de Segurança — selecione Autenticação do Windows ou Autenticação de Modo Misto para sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se você selecionar Autenticação de Modo Misto, deverá fornecer uma senha forte para a conta interna do administrador de sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 
  
         Depois que um dispositivo estabelecer uma conexão com êxito com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o mecanismo de segurança será o mesmo para Autenticação do Windows e Modo Misto. Para obter mais informações, consulte [Configuração do Mecanismo de Banco de Dados – Configuração do Servidor](http://msdn.microsoft.com/library/834b26bc-49de-4033-88d5-6aa7b1609720). 
  
    - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] — Você deve especificar pelo menos um administrador de sistema para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para adicionar a conta sob a qual a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executada, clique em **Adicionar Usuário Atual**. Para adicionar ou remover contas da lista de administradores do sistema, clique em **Adicionar** ou **Remover**e edite a lista de usuários, grupos ou computadores que terão privilégios de administrador para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Configuração do Mecanismo de Banco de Dados – Configuração do Servidor](http://msdn.microsoft.com/library/834b26bc-49de-4033-88d5-6aa7b1609720). 
  
     Ao concluir a edição da lista, clique em **OK**. Verifique a lista de administradores na caixa de diálogo de configuração. Quando a lista estiver concluída, clique em **Avançar**. 
  
14. Use a página Configuração do [!INCLUDE[ssDE](../../includes/ssde-md.md)] - Diretórios de Dados para especificar diretórios de instalação não padrão. Para instalar nos diretórios padrão, clique em **Avançar**. 
  
    > [!IMPORTANT]  
    >  Se você especificar diretórios de instalação diferentes do padrão, assegure que as pastas de instalação sejam exclusivas a esta instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nenhum dos diretórios nesta caixa de diálogo deve ser compartilhado com diretórios de outras instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
  
     Para obter mais informações, consulte [Configuração do Mecanismo de Banco de Dados – Diretórios de dados](http://msdn.microsoft.com/library/9b1fa0fc-623b-479a-afc3-4f13bd850487). 
  
15. Use a página Configuração do [!INCLUDE[ssDE](../../includes/ssde-md.md)] - FILESTREAM para habilitar FILESTREAM para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Configuração do Mecanismo de Banco de Dados – Fluxo de arquivos](http://msdn.microsoft.com/library/641a10a1-ae52-4d26-8f1c-a032a4aeff02). 
  
16. Use a página Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para especificar o tipo de instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a ser criada. Para obter mais informações sobre os modos de configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], consulte [Opções de configuração do Reporting Services &#40;SSRS&#41;](http://msdn.microsoft.com/library/e4561f6c-bc7f-467e-821a-cde8e5cd7391). 
  
17. Na página **Relatório de Erros** , especifique as informações que deseja enviar à [!INCLUDE[msCoName](../../includes/msconame-md.md)] que ajudarão a aperfeiçoar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por padrão, as opções de relatório de erros estão habilitadas. 
  
18. Na página **Regras de Conclusão de Imagem** , o Verificador de Configuração do Sistema executará as regras de conclusão de imagem para validar a configuração do computador com as configurações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que você especificou. Você pode exibir os detalhes na tela clicando em **Mostrar Detalhes**ou como um relatório HTML clicando em **Exibir relatório detalhado**. 
  
19. A página **Pronto para Concluir Imagem** mostra uma exibição de árvore das opções de instalação que foram especificadas durante a Instalação. Para continuar, clique em **Instalar**. 
  
20. Durante a instalação, a página **Andamento da Imagem Completa** fornece o status para que você possa monitorar o progresso da Instalação. 
  
21. Após a instalação, a página **Concluído** fornece um link para o arquivo de log de resumo da instalação e outras observações importantes. Para concluir o processo de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , clique em **Fechar**. 
  
22. Se você for instruído a reiniciar o computador, faça-o agora. É importante ler a mensagem do Assistente de Instalação ao concluir a Instalação. Para obter mais informações, consulte [View and Read SQL Server Setup Log Files](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md). 
  
23. Essa etapa conclui a configuração da instância preparada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e você concluiu a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
  
##  <a name="AddFeatures"></a> Add Features to a Prepared Instance  
  
### <a name="add-features-to-a-prepared-instance-of-includessnoversionincludesssnoversion-mdmd"></a>Adicionar recursos a uma instância preparada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
1. Insira a mídia de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Na pasta raiz, clique duas vezes em Setup.exe. Para instalar a partir de um compartilhamento de rede, localize a pasta raiz no compartilhamento e clique duas vezes em Setup.exe. 
  
2. O Assistente de Instalação executa a Central de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para adicionar recursos a uma instância preparada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], clique em **Preparação de imagem de uma instância autônoma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** na página **Avançado**. 
  
3. O Verificador de Configuração do Sistema executa uma operação de descoberta no computador. Para continuar, clique em **OK**. Você pode exibir os detalhes na tela clicando em **Mostrar Detalhes**ou como um relatório HTML clicando em **Exibir relatório detalhado**. 
  
4. Na página Arquivos de Suporte à Instalação, clique em **Instalar** para instalar os arquivos de suporte à Instalação. 
  
5. Na página **Preparar Tipo de Imagem**, selecione a opção **Adicionar recursos a uma instância preparada existente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**. Selecione a instância preparada específica a que você deseja adicionar recursos da lista suspensa de instâncias preparadas disponíveis. 
  
6. Na página **Seleção de Recursos** , especifique os recursos que você deseja adicionar à instância preparada específica. 
  
     Os pré-requisitos dos recursos selecionados são exibidos no painel à direita. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A Instalação instalará os pré-requisitos ainda não instalados na etapa de instalação descrita posteriormente neste procedimento. 
  
7. Na página **Regras de Preparação de Imagem** , o Verificador de Configuração do Sistema verifica o estado do sistema do computador antes de a Instalação continuar. Você pode exibir os detalhes na tela clicando em **Mostrar Detalhes**ou como um relatório HTML clicando em **Exibir relatório detalhado**. 
  
8. A página Requisitos de Espaço em Disco calcula o espaço em disco necessário para os recursos especificados. Em seguida, ele compara o espaço necessário com o espaço em disco disponível. 
  
9. Na página **Regras de Preparação de Imagem** , o Verificador de Configuração do Sistema executará as regras de preparação de imagem para validar a configuração do computador com os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que você especificou. Você pode exibir os detalhes na tela clicando em **Mostrar Detalhes**ou como um relatório HTML clicando em **Exibir relatório detalhado**. 
  
10. A página **Pronto para Preparar Imagem** mostra uma exibição de árvore das opções de instalação que foram especificadas durante a Instalação. Para continuar, clique em **Instalar**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A Instalação instalará primeiro os pré-requisitos exigidos para os recursos selecionados, seguidos da instalação dos recursos. 
  
11. Durante a instalação, a página **Progresso da Preparação de Imagem** fornece o status para que você possa monitorar o progresso da Instalação. 
  
12. Após a instalação, a página **Concluído** fornece um link para o arquivo de log de resumo da instalação e outras observações importantes. Para concluir o processo de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , clique em **Fechar**. 
  
13. Se você for instruído a reiniciar o computador, faça-o agora. É importante ler a mensagem do Assistente de Instalação ao concluir a Instalação. Para obter mais informações, consulte [View and Read SQL Server Setup Log Files](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md). 
  
##  <a name="RemoveFeatures"></a> Remover recursos de uma instância preparada  
  
### <a name="removing-features-from-a-prepared-instance-of-includessnoversionincludesssnoversion-mdmd"></a>Removendo recursos de uma instância preparada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
1. Para começar o processo de desinstalação, no menu **Iniciar** , clique em **Painel de Controle** e clique duas vezes em **Programa e Recursos**. 
  
2. Clique duas vezes no componente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para desinstalar e clique em **Remover**. 
  
3. As regras de suporte à instalação são executadas para verificar a configuração do computador. Clique em **OK** para continuar. 
  
4. Na página **Selecionar Instância** , selecione a instância preparada que você deseja modificar. O nome da instância preparada será exibida como "PreparedInstanceID não configurado" onde PreparedInstanceID é a instância que você selecionou. 
  
5. Na página **Selecionar Recursos** , especifique os recursos a serem removidos da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que você especificou. Clique em **Avançar** para continuar. 
  
6. As regras de remoção são executadas para verificar se a operação pode ser concluída com êxito. 
  
7. Na página **Pronto para Desinstalar** , examine a lista de componentes e de recursos que serão desinstalados. 
  
8. A página **Progresso da Remoção** exibirá o status da operação. 
  
9. Na página **Concluir** , você pode revisar o status de conclusão da operação. Clique em **fechar** para sair do assistente de instalação. 
  
##  <a name="Uninstall"></a> Desinstalando uma instância preparada  
  
### <a name="uninstall-a-prepared-instance-of-includessnoversionincludesssnoversion-mdmd"></a>Desinstalar uma instância preparada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
1. Para começar o processo de desinstalação, no menu **Iniciar** , clique em **Painel de Controle** e clique duas vezes em **Programa e Recursos**. 
  
2. Clique duas vezes no componente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para desinstalar e clique em **Remover**. 
  
3. As regras de suporte à instalação são executadas para verificar a configuração do computador. Clique em **OK** para continuar. 
  
4. Na página **Selecionar Instância** , selecione a instância preparada que você deseja modificar. O nome da instância preparada será exibida como "PreparedInstanceID não configurado" onde PreparedInstanceID é a instância que você selecionou. 
  
5. Na página **Selecionar Recursos** , especifique os recursos a serem removidos da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que você especificou. Clique em **Avançar** para continuar. 
  
6. Na página **Regras de Remoção** , a Instalação executará regras para verificar se a operação pode ser concluída com êxito. 
  
7. Na página **Pronto para Desinstalar** , examine a lista de componentes e de recursos que serão desinstalados. 
  
8. A página **Progresso da Remoção** exibirá o status da operação. 
  
9. Na página **Concluir** , você pode revisar o status de conclusão da operação. Clique em **fechar** para sair do assistente de instalação. 
  
10. Repita as etapas de 1 a 9 até que todos os componentes do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tenham sido removidos. 
  
##  <a name="bk_Modifying_Uninstalling"></a> Modificando ou desinstalando uma instância concluída do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
 O processo para adicionar ou remover recursos ou desinstalar uma instância concluída de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é semelhante ao processo para uma instância instalada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte os artigos a seguir.  
  
- [Adicionar recursos a uma instância do SQL Server &#40;instalação&#41;](../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)  
  
- [Desinstalar uma instância existente do SQL Server &#40;instalação&#41;](../../sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md)  
  
## <a name="see-also"></a>Consulte Também  
 [O que é Windows SysPrep](http://go.microsoft.com/fwlink/?LinkId=143546)   
 [Como funciona o Windows SysPrepWork](http://go.microsoft.com/fwlink/?LinkId=143547)  
  
  
