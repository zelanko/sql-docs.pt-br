---
title: "Notas de versão do SQL Server 2012 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: sql-non-specified
ms.technology: server-general
ms.custom: 
ms.date: 01/31/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Release Notes, SQL Server
ms.assetid: 9ccb390a-67a9-4593-85ea-2b4c41c4620f
caps.latest.revision: "21"
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e7adc5d4b4fdcf8886b2c8d08bce8de90d9b3eb1
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="sql-server-2012-release-notes"></a>Notas de Versão do SQL Server 2012
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)] Este documento de Notas de Versão descreve problemas conhecidos sobre os quais você deve ler antes de instalar ou solucionar problemas do Microsoft SQL Server 2012 ([clique aqui para baixá-lo](http://go.microsoft.com/fwlink/?LinkId=238647)). Este documento de Notas de versão está disponível somente online, não em mídia de instalação, e é atualizado periodicamente.  
  
Para obter informações sobre como iniciar e instalar o SQL Server 2012, consulte o Leiame do SQL Server 2012. O documento Leiame está disponível na mídia de instalação e na página de download [Leiame](http://download.microsoft.com/download/3/B/D/3BD9DD65-D3E3-43C3-BB50-0ED850A82AD5/ENU/Readme.htm) . Você também pode encontrar mais informações em [Manuais Online do SQL Server](http://go.microsoft.com/fwlink/?LinkId=190948) e nos [Fóruns do SQL Server](http://go.microsoft.com/fwlink/?LinkId=213599).  
  
## <a name="Install"></a>1.0 Antes da instalação  
Antes de instalar o [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], considere as seguintes informações.  
  
### <a name="11-rules-documentation-for-sql-server-2012-setup"></a>1.1 Documentação de regras para a instalação do SQL Server 2012  
**Problema:** a Instalação do SQL Server valida a configuração do computador antes de a operação de Instalação ser concluída. As várias regras que são executadas durante a operação de Instalação do SQL Server são capturadas usando o relatório do SCC (Verificador de Configuração do Sistema). A documentação sobre essas regras de instalação não está mais disponível na biblioteca do MSDN.  
  
**Solução alternativa:** você pode consultar o relatório de verificação da configuração do sistema para saber mais sobre essas regras de instalação. A verificação da configuração do sistema gera um relatório que contém uma breve descrição de cada regra executada, bem como o status de execução. O relatório de verificação da configuração do sistema está localizado em %programfiles%\Microsoft SQL Server\110\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.  
  
### <a name="12-adding-a-local-user-account-for-the-distributed-replay-controller-service-might-terminate-setup-unexpectedly"></a>1.2 Adicionar uma conta de usuário local para o serviço Distributed Replay Controller pode terminar a instalação de forma inesperada  
**Problema:** na página do **Distributed Replay Controller** da instalação do SQL Server, ao tentar adicionar uma conta de usuário local para o serviço Distributed Replay Controller, a instalação será terminada de maneira inesperada com uma mensagem de erro “Falha da instalação do SQL Server”.  
  
**Solução alternativa:** durante a instalação do SQL, não adicione contas de usuário local pelas opções “Adicionar Usuário Atual” ou “Adicionar”. Após a instalação, adicione uma conta de usuário local manualmente usando as seguintes etapas:  
  
1.  Interrompa o serviço SQL Server Distributed Replay Controller  
  
2.  No computador controlador em que o serviço controlador está instalado, no prompt de comando, digite dcomcnfg.  
  
3.  Na janela Serviços de Componente, navegue até **Raiz do Console** -> **Serviços de Componente** -> **Computadores** -> **Meu Computador** -> **Dconfig** ->**DReplayController**.  
  
4.  Clique com o botão direito do mouse em **DReplayController**e clique em **Propriedades**.  
  
5.  Na janela **Propriedades do DReplayController** , na guia **Segurança** , clique em **Editar** na seção **Permissões de Inicialização e Ativação** .  
  
6.  Conceda à conta de usuário local permissões **Ativação Local e Remota** e clique em **OK**.  
  
7.  Na seção Permissões de Acesso, clique em **Editar** e conceda à conta de usuário local permissões **Acesso Local e Remoto** e clique em **OK**.  
  
8.  Clique em **OK** para fechar a janela **Propriedades do DReplayController** .  
  
9. No computador controlador, adicione a conta de usuário local ao grupo **Usuários COM Distribuídos** .  
  
10. Inicie o serviço controlador SQL Server Distributed Replay.  
  
### <a name="13-sql-server-setup-might-fail-while-trying-to-start-the-sql-server-browser-service"></a>1.3 A Instalação do SQL Server pode falhar ao tentar iniciar o serviço SQL Server Browser  
**Problema:** a Instalação do SQL Server pode falhar ao tentar iniciar o serviço SQL Server Browser, com erros semelhantes aos seguintes:  
  
<pre>The following error has occurred:  
Service 'SQLBrowser' start request failed. Click 'Retry' to retry the failed action, or click 'Cancel' to cancel this action and continue setup.</pre>  
  
ou  
  
<pre>The following error has occurred:  
SQL Server Browser configuration for feature 'SQL_Browser_Redist_SqlBrowser_Cpu32' was cancelled by user after a previous installation failure. The last attempted step: Starting the SQL Server Browser service 'SQLBrowser', and waiting for up to '900' seconds for the process to complete.</pre>  
  
**Solução alternativa:** isso pode acontecer quando há falha no SQL Server Engine ou Analysis Services. Para corrigir esse problema, consulte os logs de instalação do SQL Server e solucione as falhas do SQL Server Engine e Analysis Services. Para obter mais informações, consulte Exibir e ler arquivos de log da Instalação do SQL Server. Para saber mais, veja [View and Read SQL Server Setup Log Files](http://msdn.microsoft.com/library/ms143702(SQL.110).aspx).  
  
### <a name="14-sql-server-2008-2008-r2-analysis-services-failover-cluster-upgrade-to-sql-server-2012-might-fail-after-renaming-the-network-name"></a>1.4 Pode haver falha na atualização do Cluster de failover do SQL Server 2008, 2008 R2 Analysis Services para SQL Server 2012 depois de renomear o nome da rede  
**Problema:** depois de alterar o nome de rede de uma instância do cluster de failover de um Microsoft SQL Server 2008, ou 2008 R2 Analysis Services usando a ferramenta Administrador de Cluster do Windows, a operação de atualização poderá falhar.  
  
**Solução alternativa:** para resolver esse problema, atualize a entrada ClusterName do Registro seguindo as instruções na seção de resolução desse [artigo da Base de Dados de Conhecimento](http://support.microsoft.com/kb/955784).  
  
### <a name="15-installing-sql-server-2012-on-windows-server-2008-r2-server-core-service-pack-1"></a>1.5 Instalando o SQL Server 2012 no Windows Server 2008 R2 Server Core Service Pack 1  
Você pode instalar o SQL Server no Windows Server 2008 R2 Server Core SP1 com as seguintes limitações:  
  
-   O Microsoft SQL Server 2012 não tem suporte para a instalação por meio do assistente de instalação no sistema operacional Server Core. Quando você instala no Server Core, a Instalação do SQL Server dá suporte ao modo silencioso completo usando o parâmetro /Q ou o modo Silencioso Simples usando o parâmetro /QS.  
  
-   Não há suporte para atualização de uma versão anterior do SQL Server para o Microsoft SQL Server 2012 em um computador executando o Windows Server 2008 R2 Server Core SP1.  
  
-   Não há suporte para a instalação de uma versão de 32 bits do Microsoft SQL Server 2012 em um computador executando o Windows Server 2008 R2 Server Core SP1.  
  
-   Não é possível instalar o Microsoft SQL Server 2012 lado a lado com versões anteriores do SQL Server em um computador executando o Windows Server 2008 R2 Server Core SP1.  
  
-   Nem todos os recursos do SQL Server 2012 têm suporte no sistema operacional Server Core. Para saber mais sobre os recursos com suporte e sobre a instalação do SQL Server 2012 no Server Core, veja [Instalar o SQL Server 2012 no Server Core](http://msdn.microsoft.com/library/hh231669(SQL.110).aspx).  
  
### <a name="16-semantic-search-requires-you-to-install-an-additional-dependency"></a>1.6 A pesquisa semântica requer que você instale uma dependência adicional  
**Problema:** a Pesquisa Semântica Estatística tem um pré-requisito adicional, o banco de dados de estatísticas semânticas de idiomas, que não é instalado pelo programa de Instalação do SQL Server.  
  
**Solução alternativa:** para configurar o banco de dados de estatísticas semânticas de idioma como um pré-requisito para a indexação semântica, realize as seguintes tarefas:  
  
1.  Localize e execute o pacote do Windows Installer denominado SemanticLanguageDatabase.msi na mídia de instalação do SQL Server para extrair o banco de dados. Para o SQL Server 2012 Express, baixe o banco de dados de estatísticas semânticas de idioma do [Centro de Download da Microsoft](https://www.microsoft.com/download/details.aspx?id=35582) (http://go.microsoft.com/fwlink/?LinkId=221787) e execute o pacote do Windows Installer.  
  
2.  Mova o banco de dados para uma pasta de dados apropriada. Se você deixar o banco de dados no local padrão, deverá alterar as permissões antes de anexá-lo com êxito.  
  
3.  Anexe o banco de dados extraído.  
  
4.  Para registrar o banco de dados, chame o procedimento armazenado **sp_fulltext_semantic_register_language_statistics_db** e forneça o nome que você atribuiu ao banco de dados quando o anexou.  
  
Se essas tarefas não forem executadas, você verá a seguinte mensagem de erro ao tentar criar um índice semântico:  
  
<pre>Msg 41209, Level 16, State 3, Line 1  
A semantic language statistics database is not registered. Full-text indexes using 'STATISTICAL_SEMANTICS' cannot be created or populated.</pre>  
  
### <a name="17-installation-prerequisite-handling-during-sql-server-2012-setup"></a>1.7 Manipulação de pré-requisitos de instalação durante a instalação do SQL Server 2012  
Os tópicos a seguir descrevem o comportamento de instalação de itens de pré-requisito durante a Instalação do SQL Server 2012:  
  
-   Somente há suporte para a instalação do SQL Server 2012 no Windows 7 SP1 ou no Windows Server 2008 R2 SP1. No entanto, a Instalação não bloqueia a instalação do SQL Server 2012 no Windows 7 ou no Windows Server 2008 R2.  
  
-   O .NET Framework 3.5 SP1 é um requisito do SQL Server 2012 quando você seleciona Mecanismo de Banco de Dados, Replicação, Master Data Services, Reporting Services, DQS (Data Quality Services) ou SQL Server Management Studio e a estrutura não é mais instalada pela Instalação do SQL Server.  
  
    -   Se você executar a Instalação em um computador com o sistema operacional Windows Vista SP2 ou Windows Server 2008 SP2 e não tiver o .NET Framework 3.5 SP1 instalado, a Instalação do SQL Server exigirá o download e a instalação do .NET Framework 3.5 SP1 antes que seja possível continuar com a instalação do SQL Server. É possível baixar o .NET Framework 3.5 SP1 no Windows Update ou diretamente [aqui](https://www.microsoft.com/download/details.aspx?id=25150). Para evitar interrupção durante a Instalação do SQL Server, baixe e instale o .NET Framework 3.5 SP1 antes de executar a Instalação do SQL Server.  
  
    -   Se você executar a Instalação em um computador com o sistema operacional Windows 7 SP1 ou Windows Server 2008 R2 SP1, deverá habilitar o .NET Framework 3.5 SP1 antes de instalar o SQL Server 2012.  
  
        **Use um dos métodos a seguir para habilitar o .NET Framework 3.5 SP1 no Windows Server 2008 R2 SP1:**  
  
        Método 1: use o Gerenciador do Servidor  
  
        1.  No Gerenciador do Servidor, clique em **Adicionar Recursos** para exibir uma lista de recursos possíveis.  
  
        2.  Na interface **Selecionar Recursos** , expanda a entrada **Recursos do .NET Framework 3.5.1** .  
  
        3.  Depois que você expandir **Recursos do .NET Framework 3.5.1**, verá duas caixas de seleção. Uma é para o .NET Framework 3.5.1 e a outra é para a Ativação de WCF. Selecione **.NET Framework 3.5.1**e clique em **Avançar**. Você não pode instalar os Recursos do .NET Framework 3.5.1 a menos que os serviços de função e os recursos necessários também estejam instalados.  
  
        4.  Em **Confirmar Seleções de Instalação**, analise as seleções e clique em Instalar.  
  
        5.  Depois que o processo de instalação for concluído, clique em **Fechar**.  
  
        Método 2: use o Windows PowerShell  
  
        1.  Clique em **Iniciar** | **Todos os Programas** | **Acessórios**.  
  
        2.  Expanda o **Windows PowerShell**, clique com o botão direito em **Windows PowerShell**e clique em **Executar como administrador**. Clique em **Sim** na caixa de diálogo **Controle de Conta de Usuário** .  
  
        3.  No prompt de comando do PowerShell, digite os seguintes comandos e pressione ENTER depois de cada comando:  
  
            ```  
            Import-Module ServerManager  
            Add-WindowsFeature as-net-framework  
            ```  
  
        **Use o seguinte método para habilitar o .NET Framework 3.5 SP1 no Windows 7 SP1:**  
  
        1.  Clique em **Iniciar** | **Painel de Controle** | **Programas**e em **Ativar ou desativar recursos do Windows**. Se você for solicitado a fornecer uma senha de administrador ou confirmação, digite a senha ou forneça confirmação.  
  
        2.  Para habilitar o **Microsoft .NET Framework 3.5.1**, marque a caixa de seleção ao lado do nome do recurso. Para desativar um recurso do Windows, desmarque a caixa de seleção.  
  
        3.  Clique em **OK**.  
  
        **Use o Gerenciamento e Manutenção de Imagens de Implantação (DISM.exe) para habilitar o .NET Framework 3.5 SP1:**  
  
        Você também pode habilitar o .NET Framework 3.5 SP1 usando o Gerenciamento e Manutenção de Imagens de Implantação (DISM.exe). Para saber mais sobre como habilitar os recursos do Windows online, veja [Habilitar ou desabilitar os recursos do Windows online](http://technet.microsoft.com/library/dd744582(WS.10).aspx). Veja a seguir as instruções para habilitar o .NET Framework 3.5 SP1:  
  
        1.  No prompt de comando, digite o comando a seguir para listar todos os recursos disponíveis no sistema operacional.  
  
            ```  
            sm /online /Get-Features  
            ```  
  
        2.  Opcional: no prompt de comando, digite o comando a seguir para listar as informações sobre o recurso específico no qual você está interessado.  
  
            ```  
            Dism /online /Get-FeatureInfo /FeatureName:NetFx3  
            ```  
  
        3.  Digite o comando a seguir para habilitar o Microsoft .NET Framework 3.5.1.  
  
            ```  
            Dism /online /Enable-Feature /FeatureName:NetFx3  
            ```  
  
-   O .NET Framework 4 é um requisito do SQL Server 2012. A Instalação do SQL Server instala o .NET Framework 4 durante a etapa de instalação de recurso.  
  
    O SQL Server 2012 Express não instala o .NET Framework 4 ao instalar no sistema operacional Windows Server 2008 R2 SP1 Server Core. Ao instalar o SQL Server 2012 Express (somente banco de dados), o .NET Framework 4 não é necessário se o .NET Framework 3.5 SP1 estiver presente. Quando o .NET Framework 3.5 SP1 não estiver presente ou quando estiver instalando o SQL Server 2012 Management Studio Express, o SQL Server 2012 Express with Tools, ou SQL Server 2012 Express with Advanced Services, você deverá instalar o .NET Framework 4 antes de instalar o SQL Server2012 Express em um sistema operacional Windows Server 2008 R2 SP1 Server Core.  
  
-   Para assegurar que o componente Visual Studio seja instalado corretamente, o SQL Server exigirá que você instale uma atualização. O SQL Server Setup verifica a presença dessa atualização e requer o download e a instalação da atualização antes de continuar com a instalação do SQL Server. Para evitar a interrupção durante a Instalação do SQL Server, você pode baixar e instalar a atualização conforme descrito abaixo, antes de executar a Instalação do SQL Server (ou pode instalar todas as atualizações para o .NET Framework 3.5 SP1 disponíveis no Windows Update):  
  
    -   Se você instalar o SQL Server 2012 em um computador com o sistema operacional Windows Vista SP2 ou Windows Server 2008 SP2, poderá obter a atualização necessária [aqui](http://support.microsoft.com/?kbid=956250).  
  
    -   Se você instalar o SQL Server 2012 em um computador com o sistema operacional Windows 7 SP1 ou Windows Server 2008 R2 SP1, essa atualização já estará instalada no computador.  
  
-   O Windows PowerShell 2.0 é um pré-requisito para a instalação de componentes do Mecanismo de Banco de Dados do SQL Server 2012 e do SQL Server Management Studio, mas o Windows PowerShell não é mais instalado pela Instalação do SQL Server. Se a instalação relatar que o PowerShell 2.0 não está presente no seu computador, você poderá habilitá-lo seguindo as instruções da página [Estrutura de gerenciamento do Windows](http://support.microsoft.com/kb/968929) . Como você obtém o Windows PowerShell 2.0 depende do sistema operacional em execução:  
  
    -   Windows Server 2008 – Windows PowerShell 1.0 é um recurso e pode ser adicionado. As versões do Windows PowerShell 2.0 são baixadas e instaladas (efetivamente como uma correção de sistema operacional).  
  
    -   Windows 7/Windows Server 2008 R2 – Windows PowerShell 2.0 são instalados por padrão.  
  
-   Se você pretende usar os recursos do SQL Server 2012 em um ambiente do SharePoint, a atualização cumulativa de agosto do SharePoint Server 2010 Service Pack 1 (SP1) e do SharePoint será necessária. Você deve instalar o SP1, a [atualização cumulativa de agosto do SharePoint](http://blogs.technet.com/b/stefan_gossner/archive/2010/09/02/august-2010-cumulative-update-for-sharepoint-has-been-released.aspx), e corrigir completamente o farm de servidores antes de adicionar os recursos do SQL Server 2012 ao farm. Esse requisito se aplica aos seguintes recursos do SQL Server 2012: uso de uma instância do Mecanismo de banco de dados como o servidor de banco de dados do farm, configuração do PowerPivot para SharePoint ou implantação do Reporting Services no modo do SharePoint.  
  
### <a name="18-supported-operating-systems-for-sql-server-2012"></a>1.8 Sistemas operacionais com suporte para o SQL Server 2012  
Há suporte para o SQL Server 2012 nos sistemas operacionais Windows Vista SP2, Windows Server 2008 SP2, Windows 2008 R2 SP1 e Windows 7 SP1.  
  
### <a name="19-sync-framework-is-not-included-in-the-installation-package"></a>1.9 O Sync Framework não está incluído no pacote de instalação  
**Problema:** o Sync Framework não está incluído no pacote de instalação do SQL Server 2012.  
  
**Solução alternativa:** baixe a versão apropriada do Sync Framework [desta página do Centro de Download da Microsoft](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=23217).  
  
### <a name="110-if-visual-studio-2010-service-pack-1-is-uninstalled-the-sql-server-2012-instance-must-be-repaired-to-restore-certain-components"></a>1.10 Se o Visual Studio 2010 Service Pack 1 for desinstalado, a instância do SQL Server 2012 deverá ser reparada para restaurar determinados componentes  
**Problema:** a instalação do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] depende de alguns componentes do Visual Studio 2010 Service Pack 1. Se você desinstalar o Service Pack 1, alguns dos componentes compartilhados serão rebaixados para suas versões originais, e alguns outros componentes serão completamente removidos do computador.  
  
**Solução alternativa:** repare a instância do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] da mídia original ou do local de instalação da rede.  
  
1.  Inicie o programa de instalação do SQL Server (setup.exe) na mídia de instalação do SQL Server.  
  
2.  Depois da verificação dos pré-requisitos e do sistema, o programa de Instalação exibirá a página **Central de Instalação do SQL Server** .  
  
3.  Clique em **Manutenção** na área de navegação à esquerda e clique em **Reparar** para iniciar a operação de reparo. Se a Central de Instalação foi iniciada usando o menu **Iniciar** , você precisará fornecer o local da mídia de instalação neste momento.  
  
4.  A regra de suporte à Instalação e as rotinas de arquivos serão executadas para garantir que o sistema tenha os pré-requisitos instalados e que o computador seja aprovado nas regras de validação da Instalação. Clique em **OK** ou em **Instalar** para continuar.  
  
5.  Na página **Selecionar Instância** , selecione a instância a ser reparada e clique em **Avançar** para continuar.  
  
6.  As regras de reparo são executadas para validar a operação. Para continuar, clique em **Avançar**.  
  
7.  A página **Pronto para Reparar** indica que a operação está pronta para continuar. Para continuar, clique em **Reparar**.  
  
8.  A página de **Progresso do Reparo** mostra o status da operação de reparo. A página **Concluído** indica que a operação foi concluída.  
  
Para saber mais sobre como reparar uma instância do SQL Server, veja [Reparar uma instalação com falha do SQL Server 2012](http://msdn.microsoft.com/library/cc646006(SQL.110).aspx).  
  
### <a name="111-an-instance-of-sql-server-2012-might-fail-after-an-os-upgrade"></a>1.11 Uma instância do SQL Server 2012 poderá falhar após uma atualização do sistema operacional  
**Problema:** uma instância do SQL Server 2012 pode falhar com o seguinte erro após você atualizar o sistema operacional do Windows Vista para o Windows 7 SP1.  
  
`Setup has detected that the .NET Framework version 4 needs to be repaired. Do not restart your computer until Setup is complete.`  
  
**Solução alternativa:**repare sua instalação do .NET Framework 4 depois de atualizar seu sistema operacional. Para saber mais, veja [Como reparar uma instalação existente do .NET Framework](http://support.microsoft.com/kb/306160).  
  
### <a name="112-sql-server-edition-upgrade-requires-a-restart"></a>1.12 A atualização da edição do SQL Server exige reiniciar o computador  
**Problema**: quando você faz a atualização de edição de uma instância do SQL Server 2012, algumas das funcionalidades associadas com a nova edição podem não ser ativadas imediatamente.  
  
**Solução alternativa**: reinicie o computador depois da atualização de edição de uma instância do SQL Server 2012. Para saber mais sobre as atualizações com suporte no SQL Server 2012, veja [Versão com suporte e atualizações de edição](http://msdn.microsoft.com/library/ms143393.aspx).  
  
### <a name="113-database-with-read-only-filegroup-or-files-cannot-be-upgraded"></a>1.13 O banco de dados com grupo de arquivos ou arquivos somente leitura não pode ser atualizado  
**Problema**: você não poderá atualizar um banco de dados anexando ou restaurando um banco de dados do backup se o banco de dados ou seus arquivos/grupos de arquivos estiverem definidos como somente leitura.  O erro 3415 retorna.  Esse problema também se aplica ao realizar uma atualização no local de uma instância do SQL Server. Ou seja, você tenta substituir uma instância existente do SQL Server instalando o SQL Server 2012 e um ou mais bancos de dados existentes é definido como somente leitura.  
  
**Solução alternativa:** antes de atualizar, verifique se o banco de dados e seus arquivos/grupos de arquivos estão definidos como leitura-gravação.  
  
### <a name="114-reinstalling-an-instance-of-sql-server-failover-custer-fails-if-you-use-the-same-ip-address"></a>1.14 Reinstalar uma instância do cluster de failover do SQL Server falhará se você usar o mesmo endereço IP  
**Problema:** se você especificar um endereço IP incorreto durante uma instalação da instância do cluster de failover do SQL Server, a instalação falhará. Depois que você desinstalar a instância com falha, e se tentar reinstalar a instância do cluster de failover do SQL Server com o mesmo nome de instância e o endereço de IP correto, a instalação falhará. A falha ocorre devido ao grupo de recursos duplicado por trás da instalação anterior.  
  
**Solução alternativa:** para resolver esse problema, use um nome de instância diferente durante a reinstalação, ou exclua manualmente o grupo de recursos antes de reinstalar. Para obter mais informações, consulte [Adicionar ou remover nós em um cluster de failover do SQL Server](http://msdn.microsoft.com/library/ms191545).  
  
![horizontal_bar](media/horizontal-bar.png "horizontal_bar")  
  
## <a name="AS"></a>2.0 Analysis Services  
  
### <a name="21-sql-editor-and-as-editor-cannot-connect-to-their-respective-server-instances-in-the-same-ssms-instance"></a>2.1 Não foi possível para o editor SQL e o editor do AS se conectarem às suas instâncias de servidor respectivas na mesma instância do SSMS  
**Problema:** não é possível conectar a um servidor do Analysis Services usando o editor do MDX/DMX quando o editor SQL já estiver conectado.  
  
Ao usar o SQL Server Management Studio 2012 (SSMS), se um arquivo .sql estiver aberto no editor e estiver conectado a uma instância do SQL Server, um arquivo do MDX ou DMX, quando aberto na mesma instância do SSMS, não poderá se conectar a uma instância de servidor do AS. Da mesma forma, se um arquivo MDX ou DMX já estiver aberto no editor no SSMS e estiver conectado a uma instância de servidor do AS, um arquivo .sql, quando aberto na mesma instância do SSMS, não poderá se conectar a uma instância do SQL Server.  
  
**Solução alternativa**: use uma das opções a seguir para resolver este problema.  
  
-   Inicie outra instância do SSMS para abrir o arquivo MDX/DMX.  
  
-   Desconecte o editor SQL e conecte o editor do MDX/DMX a um servidor do AS.  
  
### <a name="22-cannot-create-or-open-tabular-projects-when-builtinadministrators-group-name-cannot-be-resolved"></a>2.2 Não é possível criar ou abrir projetos tabulares quando o nome de grupo BUILTIN\Administrators não pode ser resolvido  
**Problema:** você deve ser um administrador em um servidor de banco de dados do local de trabalho antes de poder criar ou abrir projetos tabulares. Um usuário pode ser adicionado ao grupo de administradores de servidor por meio da adição do nome de usuário ou nome do grupo. Se você for membro do grupo BUILTIN\Administrator, não poderá criar ou editar arquivos BIM files, a menos que o servidor de banco de dados do local de trabalho tenha sido unido ao domínio do qual foi originalmente provisionado. Se você abrir ou criar o arquivo BIM, ele falhará com a seguinte mensagem de erro:  
  
`"The BIM file cannot be opened. The server connected to is not valid. Reason: You are not an administrator of server [server name]."`  
  
**Soluções alternativas:**  
  
-   Una novamente o servidor de banco de dados do local de trabalho e o computador do SQL Server Data Tools (SSDT) ao domínio.  
  
-   Se o servidor de banco de dados do local de trabalho e/ou os computadores SSDT não forem ser unidos no domínio o tempo todo, adicione nomes de usuários individuais, em vez do grupo BUILTIN\Administrators como administradores no servidor de banco de dados do local de trabalho.  
  
### <a name="23-ssis-components-for-as-tabular-models-do-not-work-as-expected"></a>2.3 Os componentes do SSIS para modelos tabulares do AS não funcionam como esperado  
Os componentes do SSIS (SQL Server Integration Services) para o AS (Analysis Services) não funcionam como esperado para modelos tabulares. Veja a seguir os problemas conhecidos que podem ocorrer quando você tenta gravar um pacote do SSIS para funcionar com modelos tabulares.  
  
**Problema:** o Gerenciador de Conexões do AS não pode usar um modelo tabular na mesma solução que uma fonte de dados.  
  
**Solução alternativa:** você deve se conectar explicitamente ao servidor do AS antes de configurar a Tarefa de Processamento do AS ou a Tarefa Executar DDL do AS.  
  
Há problemas com a Tarefa de Processamento do AS quando você trabalha com modelos tabulares:  
  
**Problema:** em vez de bancos de dados, tabelas e partições, você verá cubos, grupos de medidas e dimensões. Essa é uma limitação da tarefa.  
  
**Solução alternativa:** você ainda pode processar seu modelo de tabela usando a estrutura de cubo/grupo de medidas/dimensão.  
  
**Problema:** algumas opções de processamento com suporte do AS em execução no modo tabular não são expostas na Tarefa de Processamento do AS, como Processar Desfragmentação.  
  
**Solução alternativa:** use a tarefa Executar DDL do Analysis Services, em vez de executar um script XMLA que contenha o comando ProcessDefrag.  
  
**Problema:** algumas opções de configuração na ferramenta não são aplicáveis. Por exemplo, "Objetos relacionados ao processo" não devem ser usados durante o processamento de partições e a opção de configuração "Processamento Paralelo" contém uma mensagem de erro inválido dizendo que não há suporte para o processamento paralelo no SKU padrão.  
  
**Solução alternativa:** não há  
  
![horizontal_bar](media/horizontal-bar.png "horizontal_bar")  
  
## <a name="BOL"></a>3.0 Manuais Online  
  
### <a name="31-help-viewer-for-sql-server-crashes-in-environments-configured-to-run-only-ipv6"></a>3.1 O Visualizador da Ajuda do SQL Server falha nos ambientes configurados para executar apenas IPv6  
**Problema**: se o seu ambiente estiver configurado para executar apenas IPv6, o Visualizador da Ajuda do SQL Server 2012 falhará e você verá a seguinte mensagem de erro:  
  
`HelpLibAgent.exe has stopped working.`  
  
> [!IMPORTANT]  
> Isso se aplica a todos os ambientes em execução somente com o IPv6 habilitado. Ambientes com IPv4 habilitado (e IPv4 com IPv6) não são afetados.  
  
**Solução alternativa**: para evitar esse problema, habilite o IPv4 ou use as etapas a seguir para adicionar uma entrada ao Registro e crie uma ACL para habilitar o Visualizador da Ajuda para IPv6:  
  
1.  Crie uma chave de Registro com o nome “IPv6” e um valor de “1 (DWORD(32 bit))” em HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Help\v1.0.  
  
2.  Defina as ACLs de segurança da porta para IPv6 executando o seguinte de uma janela CMD do admin:  
  
    ```  
    netsh http add urlacl url=http://[::1]:47873/help/ sddl=D:(A;;GX;;;WD)  
    ```  
  
![horizontal_bar](media/horizontal-bar.png "horizontal_bar")  
  
## <a name="DQS"></a>4.0 Data Quality Services  
  
### <a name="41-dqs-not-supported-in-a-cluster"></a>4.1 O DQS não tem suporte em um cluster  
**Problema:** não há suporte para o DQS em uma instalação de cluster do SQL Server. Se você estiver instalando uma instância de cluster do SQL Server, não deverá marcar as caixas de seleção **Data Quality Services** e **Cliente Data Quality** na página de **Seleção de Recursos** . Se estas caixas de seleção estiverem marcadas durante a instalação da instância de cluster (e você concluir a instalação do Data Quality Server executando o arquivo DQSInstaller.exe), o DQS será instalado neste nó, mas não estará disponível em nós adicionais quando você adicionar mais nós ao cluster e, consequentemente, não funcionará em nós adicionais.  
  
**Solução alternativa:** instale a atualização cumulativa 1 do SQL Server 2012 para resolver este problema. Para obter instruções, veja [http://support.microsoft.com/kb/2674817](http://support.microsoft.com/kb/2674817).  
  
### <a name="42-to-reinstall-data-quality-server-delete-the-dqs-objects-after-uninstalling-data-quality-server"></a>4.2 Para reinstalar o Data Quality Server, exclua os objetos DQS depois de desinstalar o Data Quality Server  
**Problema:** se você desinstalar o servidor Data Quality Server, os objetos DQS (bancos de dados DQS, logons DQS e um procedimento armazenado DQS) não serão excluídos da instância do SQL Server.  
  
**Solução alternativa:** para reinstalar o Data Quality Server no mesmo computador e na mesma instância do SQL Server, você deverá excluir manualmente os objetos DQS da instância do SQL Server. Além disso, você também deve excluir os arquivos de bancos de dados DQS (DQS_MAIN, DQS_PROJECTS, and DQS_STAGING_DATA) da pasta C:\Program Files\Microsoft SQL Server\MSSQL11.<SQL_Server_Instance>\MSSQL\DATA no computador, antes de reinstalar o Data Quality Server. Caso contrário, a instalação do Data Quality Server falhará. Mova os arquivos de banco de dados, em vez de excluí-los, se você quiser preservar dados, como bases de dados de conhecimentos ou projetos de qualidade de dados. Para saber mais sobre como remover objetos DQS após a conclusão do processo de desinstalação, veja [Remover objetos do Data Quality Server](http://msdn.microsoft.com/library/hh231667.aspx).  
  
### <a name="43-indication-of-a-terminated-knowledge-discovery-or-interactive-cleansing-activity-is-delayed"></a>4.3 A indicação de uma descoberta de conhecimento terminada ou atividade de limpeza interativa está atrasada  
**Problema:** se um administrador terminar uma atividade na tela Monitoramento de Atividades, um usuário interativo que estiver executando a atividade de descoberta de conhecimento, gerenciamento de domínio ou limpeza interativa não receberá nenhuma indicação de que sua atividade terminou, até executar a operação seguinte.  
  
**Solução alternativa:** não há  
  
### <a name="44-a-cancel-operation-discards-work-from-multiple-activities"></a>4.4 Uma operação de cancelamento descarta o trabalho de várias atividades  
**Problema:** se você clicar em **Cancelar** para uma atividade de descoberta de conhecimento ou gerenciamento de domínio em execução, e outras atividades tiverem sido concluídas antes sem que uma operação de publicação fosse realizada durante a execução da atividade, o trabalho de todas as atividades executadas desde a última publicação será descartado, não apenas o atual.  
  
**Solução alternativa:** para evitar isso, publique o trabalho que deve persistir na base de dados de conhecimento antes de iniciar uma nova atividade.  
  
### <a name="45-controls-do-not-scale-properly-on-large-font-sizes"></a>4.5 Os controles não são dimensionados corretamente em tamanhos de fontes grandes  
**Problema:** se você alterar o tamanho do texto para “Maior – 150%” (no Windows Server 2008 ou Windows 7) ou alterar a configuração de DPI Personalizada para 200% (no Windows 7), os botões **Cancelar** e **Criar** na página **Nova Base de Dados de Conhecimento** não ficarão acessíveis.  
  
**Solução alternativa:**para resolver o problema, defina a tela para um tamanho menor.  
  
### <a name="46-screen-resolution-of-800x600-is-not-supported"></a>4.6 Não há suporte para a resolução de tela de 800 x 600  
**Problema:** o aplicativo cliente Data Quality não será exibido corretamente se a resolução da tela estiver definida como 800 x 600.  
  
**Solução alternativa:** para resolver o problema, defina a resolução da tela com um valor mais alto.  
  
### <a name="47-map-bigint-column-in-the-source-data-to-a-decimal-domain-to-prevent-data-loss"></a>4.7 Mapear coluna Bigint na fonte de dados para um domínio decimal para evitar a perda de dados  
**Problema:** se uma coluna na sua fonte de dados for do tipo de dados **bigint** você deverá mapear essa coluna para um domínio do tipo de dados **decimal** , em vez do tipo de dados **integer** no DQS. Isso ocorre porque o tipo de dados **decimal** representa um intervalo maior de valores, em vez do tipo de dados **int** e, portanto, pode conter valores maiores.  
  
### <a name="48-nvarcharmax-and-varcharmax-data-types-are-not-supported-in-the-dqs-cleansing-component-in-integration-services"></a>4.8 Os tipos de dados NVARCHAR(MAX) e VARCHAR(MAX) não têm suporte no Componente de Limpeza DQS no Integration Services  
**Problema:** as colunas de dados dos tipos de dados **NVARCHAR(MAX)** e **VARCHAR(MAX)** não têm suporte no componente de Limpeza DQS no Integration Services. Dessa forma, essas colunas de dados estão indisponíveis para mapeamento na guia Mapeamento do Editor de Transformação de Limpeza DQS e, portanto, não pode ser limpo.  
  
**Solução alternativa:** antes de processar essas colunas de dados usando o componente de limpeza DQS, você deve convertê-las para tipo de dados **DT_STR** ou **DT_WSTR** usando a transformação de Conversão de Dados.  
  
### <a name="49-the-item-to-run-dqsinstallerexe-on-the-start-menu-is-overwritten-on-new-sql-server-instance-installation"></a>4.9 O item para executar o DQSInstaller.exe no menu Iniciar é substituído na nova instalação da instância do SQL Server  
**Problema:** se você escolher instalar o Data Quality Services em uma instância do SQL Server, um item será criado no menu **Iniciar** no grupo de programas **Data Quality Services** chamado **Instalador do Data Quality Server** depois que você concluir a instalação do SQL Server. No entanto, se você instalar diversas instâncias do SQL Server no mesmo computador, existirá ainda um único item do **Instalador do Data Quality Server** no menu **Iniciar** . Clicar neste item executa o arquivo DQSInstaller.exe na instância instalada mais recente do SQL Server.  
  
### <a name="410-activity-monitoring-displays-incorrect-status-for-failed-integration-services-cleansing-activities"></a>4.10 O monitoramento de atividade exibe status incorreto para atividades de limpeza do Integration Services com falha  
A tela Monitoramento de Atividade exibe **Êxito** incorretamente mesmo para atividades de limpeza do Integration Services com falha na coluna **Status atual** .  
  
### <a name="411-schema-name-is-not-displayed-as-part-of-tableview-name"></a>4.11 O nome do esquema não é exibido como parte do Nome da Tabela/Exibição  
Ao selecionar uma fonte de dados do SQL Server em qualquer uma das atividades DQS durante o estágio de mapeamento no cliente Data Quality, a lista de tabelas e exibições será exibida sem o nome do esquema. Portanto, se houver diversas tabelas/exibições com o mesmo nome, mas esquemas diferentes, elas podem ser distinguidas somente pela visualização de dados, ou selecionando-as e, em seguida, observando os campos disponíveis para mapear.  
  
### <a name="412-issue-with-cleansing-output-and-export-if-data-source-is-mapped-to-a-composite-domain-containing-a-child-domain-of-date-type"></a>4.12 Problema com a saída de limpeza e exportação se a fonte de dados for mapeada para um domínio composto contendo um domínio filho de tipo de data  
Em um projeto de qualidade de dados de limpeza, se você tiver mapeado um campo em seus dados de origem com um domínio composto que tenha um domínio filho do tipo de dados de data, a saída do domínio filho no resultado de limpeza terá formato de data incorreto e haverá falha na operação de exportação para banco de dados.  
  
### <a name="413-error-when-mapping-to-an-excel-sheet-that-contains-a--semicolon-in-its-name"></a>4.13 Erro ao mapear para uma planilha do Excel que contém um ; (ponto e vírgula) no nome  
**Problema:** na página **Mapear** de qualquer atividade DQS no cliente Data Quality, se você mapear para a folha do Excel da origem que contém um ; (ponto-e-vírgula) no nome, uma mensagem de exceção sem tratamento será exibida quando você clicar em **Avançar** na página **Mapear** .  
  
**Solução alternativa:** remova o ; (ponto-e-vírgula) do nome da planilha no arquivo Excel que contém os dados de origem a serem mapeados e tente novamente.  
  
### <a name="414-issue-with-date-or-datetime-values-in-unmapped-source-fields-in-excel-during-cleansing-and-matching"></a>4.14 Problema com valores Date ou DateTime em campos de origem não mapeados no Excel durante a limpeza e a correspondência  
**Problema**: se seus dados de origem forem o Excel e você não tiver mapeado os campos de origem que contêm valores de tipo de dados **Date** ou **DateTime** , o seguinte ocorrerá durante as atividades de limpeza e correspondência:  
  
-   Os valores **Date** não mapeados são exibidos e exportados no formato aaaammdd.  
  
-   O valor de hora é perdido para os valores **DateTime** não mapeados, e eles são exibidos e exportados no formato aaaammdd.  
  
**Solução alternativa:** você pode exibir os valores do campo não mapeado no painel inferior direito na página **Gerenciar e exibir resultados** na atividade de limpeza e na página **Correspondência** na atividade de correspondência.  
  
### <a name="415-cannot-import-domain-values-from-an-excel-file-xls-containing-more-than-255-columns-of-data"></a>4.15 Não é possível importar valores de domínio de um arquivo do Excel (.xls) contendo mais de 255 colunas de dados  
**Solução alternativa:** se você importar valores para um domínio de um arquivo do Excel 97-2003 (.xls) que contém mais de 255 colunas de dados, uma mensagem de exceção será exibida e ocorrerá falha na importação.  
  
**Solução alternativa:** para corrigir esse problema, faça o seguinte:  
  
-   Salve o arquivo .xls como .xlsx e importe os valores de um arquivo .xlsx para um domínio.  
  
-   Remova os dados em todas as colunas além da coluna 255 no arquivo .xls, salve o arquivo e, em seguida, importe os valores do arquivo para um domínio.  
  
### <a name="416-activity-monitoring-feature-is-unavailable-for-roles-other-than-dqsadministrator"></a>4.16 O recurso Monitoramento de Atividades está indisponível para funções diferentes de dqs_administrator  
O recurso de monitoramento de atividade está disponível somente para os usuários que têm a função de dqs_administrator Se sua conta de usuário tiver a função dqs_kb_editor ou dqs_kb_operator, o recurso Monitoramento de Atividades estará indisponível no aplicativo cliente Data Quality.  
  
### <a name="417-error-on-opening-a-knowledge-base-in-the-recent-knowledge-base-list-for-domain-management"></a>4.17 Erro ao abrir a base de dados de conhecimento na lista da base de dados de conhecimento recente para o gerenciamento de domínio  
Problema: você pode receber o seguinte erro se abrir a base de dados de conhecimento na lista **Base de Dados de Conhecimento Recente** para a atividade de gerenciamento de domínio na tela inicial do cliente Data Quality:  
  
`"A configuration with name 'RecentList:KB:<domain>\<username>' already exists in the database."`  
  
Isso ocorre por causa da diferença na maneira como o DQS compara cadeias de caracteres no banco de dados do SQL Server e no C#. A comparação de cadeia de caracteres no banco de dados do SQL Server não faz distinção de maiúsculas e minúsculas embora faça distinção no C#.  
  
Vamos ilustrar isso com um exemplo. Considere um usuário, Domínio\usuário1. O usuário faz logon no computador do cliente Data Quality usando a conta "usuário1" e trabalha em uma base de dados de conhecimento. O DQS armazena a base de dados de conhecimento recente para cada usuário como um registro na tabela A_CONFIGURATION no banco de dados DQS_MAIN. Nesse caso, o registro será armazenado com o seguinte nome: RecentList:KB:Domínio\usuário1. Posteriormente, o usuário faz logon no computador do cliente Data Quality como “Usuário1” (observe o U maiúsculo) e tenta abrir a base de dados de conhecimento na lista **Base de Dados de Conhecimento Recente** para a atividade de gerenciamento de domínio. O código subjacente no DQS comparará as duas cadeias de caracteres, RecentList:KB:DOMÍNIO\usuário1 e DOMÍNIO\Usuário1 e, considerando a comparação de cadeia de caracteres com distinção de maiúsculas e minúsculas no C#, as cadeias de caracteres não corresponderão e, portanto, o DQS tentará inserir um novo registro para o usuário (Usuário1) na tabela A_CONFIGURATION no banco de dados DQS_MAIN. No entanto, devido à comparação de cadeia de caracteres com distinção de maiúsculas e minúsculas no banco de dados SQL, a cadeia de caracteres já existe na tabela A_CONFIGURATION no banco de dados DQS_MAIN e a operação de inserção falhará.  
  
**Solução alternativa:** para corrigir esse problema, faça o seguinte:  
  
-   Verifique se existem entradas duplicadas executando a instrução a seguir:  
  
    ```  
    SELECT * FROM DQS_MAIN.dbo.A_CONFIGURATION WHERE NAME like 'RecentList%'  
    ```  
  
    Em seguida, você pode executar a seguinte instrução para excluir o relatório somente para o usuário afetado alterando o valor na cláusula WHERE para corresponder ao domínio e ao nome de usuário afetado.  
  
    ```  
    DELETE DQS_MAIN.dbo.A_Configuration WHERE NAME LIKE 'RecentList%<domain>\<username>'  
    ```  
  
    Como alternativa, você pode remover todos os itens recentes para todos os usuários no DQS:  
  
    ```  
    DELETE DQS_MAIN.dbo.A_Configuration WHERE NAME LIKE 'RecentList%'  
    ```  
  
-   Use a mesma política de maiúsculas e minúsculas que da última vez para especificar sua conta de usuário enquanto faz logon no computador do cliente Data Quality.  
  
> [!NOTE]  
> Para evitar esse problema, use políticas consistentes de maiúsculas e minúsculas para especificar sua conta de usuário enquanto faz logon no computador do cliente Data Quality.  
  
![horizontal_bar](media/horizontal-bar.png "horizontal_bar")  
  
## <a name="DE"></a>5.0 Mecanismo de banco de dados  
  
### <a name="51-use-of-distributed-replay-controller-and-distributed-replay-client-features"></a>5.1 Uso do controlador Distributed Replay e recursos de cliente Distributed Replay.  
**Problema:** o controlador Distributed Replay e os recursos de cliente Distributed Replay são disponibilizados no SKU do Server Core do Windows Server 2008, do Windows Server 2008 R2 e do Windows Server 7, embora esses dois recursos não tenham suporte no SKU do Server Core.  
  
**Solução alternativa:** não instale nem use esses dois recursos no SKU do Server Core do Windows Server 2008, do Windows Server 2008 R2 e do Windows Server 7.  
  
### <a name="52-sql-server-management-studio-depends-on-visual-studio-2010-sp1"></a>5.2 O SQL Server Management Studio depende do Visual Studio 2010 SP1  
**Problema**: o SQL Server 2012 Management Studio depende do Visual Studio 2010 SP1 para funcionar corretamente. Desinstalar o Visual Studio 2010 SP1 pode causar perda de funcionalidade no SQL Server Management Studio e deixará o Management Studio em um estado sem suporte. Os seguintes problemas podem ser vistos nesse caso:  
  
-   Parâmetros de linha de comando para ssms.exe não funcionarão corretamente.  
  
-   As informações da Ajuda exibidas ao tentar executar o ssms.exe com a opção /? estarão incorretas.  
  
-   Para cada arquivo aberto clicando duas vezes nele no Windows Explorer, uma nova instância do SSMS será lançada para abrir o arquivo.  
  
-   As consultas não podem ser depuradas no modo de usuário normal.  
  
**Solução alternativa**: instale o Visual Studio 2010 SP1 novamente e reinicie o Management Studio.  
  
### <a name="53-x64-operating-systems-require-64-bit-powershell-20"></a>5.3 Os sistemas operacionais x64 exigem o PowerShell 2.0 de 64 bits  
**Problema:** não há suporte para instalações de 32 bits do Windows PowerShell Extensions para SQL Server para instâncias do SQL Server 2012 em sistemas operacionais de 64 bits.  
  
**Soluções alternativas:**  
  
-   Instale o SQL Server 2012 de 64 bits com as Ferramentas de Gerenciamento de 64 bits e o Windows PowerShell Extensions para SQL Server de 64 bits.  
  
-   Ou importe o módulo SQLPS de um prompt do Windows PowerShell 2.0 de 32 bits.  
  
### <a name="54-an-error-might-occur-when-navigating-in-the-generate-script-wizard"></a>5.4 Um erro pode ocorrer ao navegar no Assistente Gerar Scripts  
**Problema:** após gerar um script no Assistente Gerar Scripts, clicando em **Salvar ou Publicar Scripts**, e depois clicar em **Escolher Opções** ou **Definir Opções de Script**, clicar em **Salvar ou Publicar Scripts** novamente pode resultar no erro a seguir:  
  
<a name="prean-exception-occurred-while-executing-a-transact-sql-statement-or-batch-microsoftsqlserverconnectioninfo"></a><pre>An exception occurred while executing a Transact-SQL statement or batch. (Microsoft.SqlServer.ConnectionInfo)  
------------------------------  
INFORMAÇÕES ADICIONAIS:  
Nome de objeto 'sys.federations' inválido. (Microsoft SQL Server, Error: 208)</pre>  
  
**Solução alternativa:** feche e reabra o Assistente de geração de scripts.  
  
### <a name="55-new-maintenance-plan-layout-not-compatible-with-earlier-sql-server-tools"></a>5.5 O novo layout do plano de manutenção não é compatível com as ferramentas do SQL Server anteriores  
**Problema:** quando as ferramentas de gerenciamento do SQL Server 2012 são usadas para modificar um plano de manutenção existente criado em uma versão anterior das ferramentas de gerenciamento do SQL Server (SQL Server 2008 R2, SQL Server 2008 ou SQL Server 2005), o plano de manutenção é salvo em um novo formato. As versões anteriores das ferramentas de gerenciamento do SQL Server não dão suporte a esse formato novo.  
  
**Solução alternativa:**não há  
  
### <a name="56-intellisense-has-limitations-when-logged-in-to-a-contained-database"></a>5.6 O Intellisense tem limitações quando conectado a um banco de dados independente  
Problema: o Intellisense no SQL Server Management Studio (SSMS) e no SQL Server Data Tools (SSDT) não funciona conforme o esperado quando usuários independentes estão conectados a bancos de dados independentes. O comportamento a seguir é visto nesses casos:  
  
1.  Sublinhar para objetos inválidos não é exibido.  
  
2.  A lista de preenchimento automático não é exibida.  
  
3.  A ajuda para dica de ferramenta para funções internas não funciona.  
  
**Solução alternativa:**não há  
  
### <a name="57-alwayson-availability-groups"></a>5.7 Grupos de disponibilidade AlwaysOn  
Antes de tentar criar um grupo de disponibilidade, veja [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn (SQL Server)](http://go.microsoft.com/?linkid=9753168) nos Manuais Online. Para obter uma introdução aos Grupos de Disponibilidade AlwaysOn, veja [Grupos de Disponibilidade AlwaysOn (SQL Server)](http://go.microsoft.com/?linkid=9753166)nos Manuais Online.  
  
#### <a name="571-client-connectivity-for-alwayson-availability-groups"></a>5.7.1 Conectividade de cliente para grupos de disponibilidade AlwaysOn  
**Atualizado em:** 13 de agosto de 2012  
  
Esta seção descreve o suporte de driver para Grupos de Disponibilidade AlwaysOn e soluções alternativas para drivers sem suporte.  
  
**Suporte de driver**  
  
A tabela a seguir resume o suporte de driver para Grupos de Disponibilidade AlwaysOn:  
  
|Driver|Failover de várias sub-redes|Tentativa de aplicativo|Roteamento somente leitura|Failover de várias sub-redes: failover mais rápido de ponto de extremidade de sub-rede simples|Failover de várias sub-redes: resolução de instância nomeada para instâncias clusterizadas SQL|  
|----------|--------------------------|----------------------|----------------------|------------------------------------------------------------------|---------------------------------------------------------------------------------|  
|SQL Native Client 11.0 ODBC|Sim|Sim|Sim|Sim|Sim|  
|SQL Native Client 11.0 OLEDB|Não|Sim|Sim|Não|Não|  
|ADO .NET com .NET Framework 4.0 com patch de conectividade**\&#42;**|Sim|Sim|Sim|Sim|Sim|  
|ADO .NET com .NET Framework 3.5 SP1 com patch de conectividade **\&#42;\&#42;**|Sim|Sim|Sim|Sim|Sim|  
|Microsoft JDBC driver 4.0 para SQL Server|Sim|Sim|Sim|Sim|Sim|  
  
**\&#42;** Baixe o patch de conectividade para ADO .NET com .NET Framework 4.0: [http://support.microsoft.com/kb/2600211](http://support.microsoft.com/kb/2600211).  
  
**\&#42;\&#42;** Baixe o patch de conectividade para ADO .NET com .NET Framework 3.5 SP1: [http://support.microsoft.com/kb/2654347](http://support.microsoft.com/kb/2654347).  
  
**Palavra-chave MultiSubnetFailover e recursos associados**  
  
MultiSubnetFailover é uma nova palavra-chave da cadeia de conexão usada para habilitar failover mais rápido com os Grupos de disponibilidade AlwaysOn e Instâncias de cluster de failover AlwaysOn no SQL Server 2012. Os três seguintes sub-recursos estarão habilitados quando o MultiSubnetFailover=True for definido na cadeia de conexão:  
  
-   Um failover de várias sub-redes mais rápido para um ouvinte de várias sub-redes para um Grupo de Disponibilidade AlwaysOn ou instâncias de cluster de failover.  
  
    -   A resolução de instância nomeada para uma instância de cluster de failover AlwaysOn de várias sub-redes.  
  
-   Um failover de sub-rede única mais rápido para um ouvinte de sub-rede única para um Grupo de Disponibilidade AlwaysOn ou instâncias de cluster de failover.  
  
    -   Esse recurso é usado ao conectar-se a um ouvinte que tem um IP único em uma única sub-rede. Isso realiza tentativas de conexão de TCP mais agressivas para acelerar os failovers de sub-rede única.  
  
-   A resolução de instância nomeada para uma instância de cluster de failover AlwaysOn de várias sub-redes.  
  
    -   Isso é para adicionar o suporte à resolução de instância nomeada para uma instância de cluster de failover AlwaysOn com diversos pontos de extremidade de sub-rede.  
  
**Não há suporte para MultiSubnetFailover=True pelo .NET Framework 3.5 ou OLEDB**  
  
**Problema:** se seu Grupo de Disponibilidade ou Instância de Cluster de Failover tiver um nome de ouvinte (conhecido como o nome da rede ou o Ponto de Acesso para Cliente no Gerenciador de Cluster do WSFC) que dependa dos diversos endereços IP de diferentes sub-redes, e você estiver usando o ADO .NET com .NET Framework 3.5SP1 ou SQL Native Client 11.0 OLEDB, possivelmente 50% das suas solicitações de conexão de cliente para o ouvinte do grupo de disponibilidade atingirão um tempo limite de conexão.  
  
**Soluções alternativas:** é recomendável que você execute uma das tarefas a seguir.  
  
-   Se você não tiver a permissão para manipular recursos de cluster, altere o tempo limite da conexão para 30 segundos (esse valor resulta em um período de tempo limite TCP de 20 segundos mais um buffer de 10 segundos).  
  
    **Prós**: se ocorrer um failover de sub-rede cruzado, o tempo de recuperação do cliente será rápido.  
  
    **Contras**: metade das conexões de cliente demorarão mais de 20 segundos.  
  
-   Se você tiver permissão para manipular os recursos de cluster, a abordagem mais recomendada é definir o nome de rede do ouvinte do grupo de disponibilidade como **RegisterAllProvidersIP**=0. Para obter mais informações, consulte "Exemplo de script PowerShell para desabilitar RegisterAllProvidersIP e reduzir o TTL", posteriormente nesta seção.  
  
    **Prós:** você não precisa aumentar o valor de tempo limite de conexão de cliente.  
  
    **Contras:** se um failover de sub-rede cruzado ocorrer, o tempo de recuperação do cliente poderá ser de 15 minutos ou mais, dependendo da configuração de HostRecordTTL e da configuração da agenda de replicação DNS/AD entre sites.  
  
**Exemplo de script PowerShell para desabilitar RegisterAllProvidersIP e reduzir o TTL**  
  
O exemplo a seguir de script PowerShell demonstra como desabilitar `RegisterAllProvidersIP` e reduzir o TTL. Substitua `yourListenerName` pelo nome do ouvinte que você está alterando.  
  
```  
Import-Module FailoverClusters  
Get-ClusterResource yourListenerName|Set-ClusterParameter RegisterAllProvidersIP 0  
Get-ClusterResource yourListenerName|Set-ClusterParameter HostRecordTTL 300  
```  
  
#### <a name="572-upgrading-from-ctp3-with-availability-group-configured-is-not-supported"></a>5.7.2 Atualizar do CTP3 com um grupo de disponibilidade configurado não tem suporte  
Descarte o grupo de disponibilidade e recrie-o antes de atualizar. Isso é devido a uma limitação no build CTP3. Os builds futuros não terão essa restrição.  
  
#### <a name="573-side-by-side-installation-of-ctp3-with-later-versions-is-not-supported-if-you-have-an-availability-group-configured-in-your-instance"></a>5.7.3 A instalação lado a lado do CTP3 com versões posteriores não terá suporte se você tiver um grupo de disponibilidade configurado em sua instância  
Isso é devido a uma limitação no build CTP3. Os builds futuros não terão essa restrição.  
  
#### <a name="574-side-by-side-installation-of-ctp3-with-later-versions-of-failover-cluster-instances-is-not-supported"></a>5.7.4 A instalação lado a lado do CTP3 com versões posteriores de instâncias de cluster de failover não tem suporte.  
Isso é devido a uma limitação no build CTP3. Os builds futuros não terão essa restrição. Para atualizar instâncias de cluster de failover do CTP3, atualize todas as instâncias em um nó ao mesmo tempo.  
  
#### <a name="575--timeouts-may-occur-when-using-multi-ips-in-the-same-subnet-with-alwayson"></a>5.7.5 Tempo limite pode ocorrer ao usar diversos IPs na mesma sub-rede com AlwaysOn  
**Problema:** ao usar diversos IPs na mesma sub-rede com AlwaysOn, os clientes podem observar um tempo limite. Isso ocorre se o IP no topo da lista está incorreto.  
  
**Solução alternativa:** use 'multisubnetfailover = true' na cadeia de conexão.  
  
#### <a name="576-failure-to-create-new-availability-group-listeners-because-of-active-directory-quotas"></a>5.7.6 Falha ao criar novos ouvintes de grupo de disponibilidade devido a cotas do Active Directory  
**Problema:** pode haver falha na criação de um novo ouvinte de grupo de disponibilidade porque você atingiu uma cota do Active Directory para a conta da máquina do nó de cluster participante. Para saber mais, veja [Como solucionar problemas da conta do serviço de cluster quando ela modifica objetos de computador](http://support.microsoft.com/kb/307532) e [Cotas do Active Directory](http://technet.microsoft.com/library/cc904295(WS.10).aspx).  
  
#### <a name="577-netbios-conflicts-because-availability-group-listener-names-use-an-identical-15-character-prefix"></a>5.7.7 Conflitos de NetBIOS porque os nomes dos ouvintes de grupo de disponibilidade usam um prefixo de 15 caracteres idênticos  
Se você tiver dois clusters do WSFC que sejam controlados pelo mesmo Active Directory e tentar criar ouvintes de grupo de disponibilidade nos dois clusters usando nomes com mais de 15 caracteres e um prefixo idêntico de 15 caracteres, você obterá um erro relatando que o recurso Nome de Rede virtual não pôde ser colocado online. Para saber mais sobre regras da nomenclatura de prefixos para nomes DNS, veja [Atribuindo nomes de domínio](http://technet.microsoft.com/library/cc731265(WS.10).aspx)  
  
![horizontal_bar](media/horizontal-bar.png "horizontal_bar")  
  
## <a name="IS"></a>6.0 Integration Services  
  
### <a name="61-the-change-data-capture-service-for-oracle-and-the-change-data-capture-designer-console-for-oracle"></a>6.1 Serviço Change Data Capture para Oracle e Change Data Capture Designer Console para Oracle  
O Serviço CDC para Oracle é um Serviço do Windows que examina os logs de transação do Oracle e capturam alterações a tabelas de interesse do Oracle em tabelas de alteração do SQL Server. O CDC Designer Console é usado para desenvolver e manter Instâncias Oracle CDC. O CDC Designer Console é um snap-in do Console de Gerenciamento Microsoft (MMC) que contém os seguintes elementos:  
  
#### <a name="611-install-the-cdc-service-for-oracle-and-the-cdc-designer-for-oracle"></a>6.1.1 Instalar o Serviço CDC para Oracle e o CDC Designer para Oracle  
**Problema:** o Serviço CDC e CDC Designer não são instalados pela instalação do SQL Server. Você deve instalar manualmente o Serviço CDC Service ou CDD Designer em um computador que atenda aos requisitos e pré-requisitos de acordo com os arquivos atualizados da Ajuda.  
  
**Solução alternativa:** para instalar o Serviço CDC para Oracle, execute manualmente AttunityOracleCdcService.msi a partir da mídia de instalação do SQL Server. Para instalar o CDC Designer Console, execute manualmente o arquivo AttunityOracleCdcDesigner.msi da mídia de instalação do SQL Server.  Os pacotes de instalação para x86 e x64 estão localizados em . \Tools\AttunityCDCOracle\ na mídia de instalação do SQL Server.  
  
#### <a name="612-f1-help-functionality-points-to-incorrect-documentation-files"></a>6.1.2 A funcionalidade de Ajuda F1 aponta para arquivos de documentação incorretos  
**Problema:** você não pode acessar a documentação da Ajuda correta usando a lista suspensa da Ajuda F1 ou clicando na "?" nos Consoles da Attunity. Esses métodos apontam para arquivos chm incorretos.  
  
**Solução alternativa:** os arquivos chm corretos são instalados quando o Serviço CDC para Oracle e o CDC Designer for Oracle estão instalados. Para exibir o conteúdo da Ajuda correto, inicie os arquivos chm diretamente a partir deste local: `%Program Files%\Change Data Capture for Oracle by Attunity\*.chm`.  
  
![horizontal_bar](media/horizontal-bar.png "horizontal_bar")  
  
## <a name="MDS"></a>7.0 Master Data Services  
  
### <a name="71-fixing-an-mds-installation-in-a-cluster"></a>7.1 Corrigindo uma instalação do MDS em um cluster  
**Problema:** se você instalar uma instância clusterizada da versão do RTM do SQL Server 2012 com a caixa de seleção **Master Data Services** marcada, o MDS estará instalado em um único nó, mas não estará disponível e não funcionará em nós adicionais que você adiciona ao cluster.  
  
**Solução alternativa**: para resolver esse problema, você deverá instalar a versão cumulativa 1 do SQL Server 2012 (CU1), realizando as seguintes etapas:  
  
1.  Certifique-se de que não haja nenhuma instalação do SQL/MDS.  
  
2.  Baixe o SQL Server 2012 CU1 para um diretório local.  
  
3.  Instale o SQL Server 2012 com o recurso MDS no nó de cluster primário e, em seguida, instale o SQL Server 2012 com o recurso MDS em qualquer um dos nós de cluster adicionais.  
  
Para saber mais sobre os problemas e informações sobre como realizar as etapas acima, veja [http://support.microsoft.com/kb/2683467](http://support.microsoft.com/kb/2683467).  
  
### <a name="72-microsoft-silverlight-5-required"></a>7.2 Microsoft Silverlight 5 obrigatório  
Para trabalhar no aplicativo Web do Master Data Manager o Silverlight 5.0 deverá estar instalado no computador cliente. Se você não tiver a versão exigida do Silverlight, será solicitado a instalá-la quando navegar até uma área do aplicativo Web que a exige. Você pode instalar o Silverlight 5 em [http://go.microsoft.com/fwlink/?LinkId=243096](http://go.microsoft.com/fwlink/?LinkId=243096).  
  
![horizontal_bar](media/horizontal-bar.png "horizontal_bar")  
  
## <a name="RS"></a>8.0 Reporting Services  
  
### <a name="81-reporting-services-connectivity-to-sql-server-pdw-requires-updated-drivers"></a>8.1 A conectividade do Reporting Services para SQL Server PDW exige drivers atualizados  
A conectividade do SQL Server 2012 Reporting Services para a Atualização 2 e superior do Aplicativo Microsoft SQL Server PDW exige uma atualização para os drivers de conectividade do PDW. Para obter mais informações, os clientes do SQL Server PDW devem entrar em contato com o suporte da Microsoft.  
  
![horizontal_bar](media/horizontal-bar.png "horizontal_bar")  
  
## <a name="SI"></a>9.0 StreamInsight  
O SQL Server 2012 inclui StreamInsight 2.0. O StreamInsight 2.0 exige uma licença do Microsoft SQL Server 2012 e o .NET Framework 4.0. Ele inclui vários aperfeiçoamentos feitos e algumas correções de bugs. Para saber mais, veja as [Notas de versão do Microsoft StreamInsight 2.0](http://social.technet.microsoft.com/wiki/contents/articles/6539.aspx). Para baixar o StreamInsight 2.0 separadamente, visite a [Página de download do Microsoft StreamInsight 2.0](http://go.microsoft.com/fwlink/?LinkId=241593) no Centro de Download da Microsoft.  
  
![horizontal_bar](media/horizontal-bar.png "horizontal_bar")  
  
## <a name="UA"></a>10.0 Supervisor de Atualização  
  
### <a name="101-link-to-install-upgrade-advisor-is-not-enabled-on-chinese-hk-operating-systems"></a>10.1 O link para instalação do Supervisor de Atualização não está habilitado nos sistemas operacionais em chinês (HK)  
Problema: quando você tentar instalar o Supervisor de Atualização em qualquer versão com suporte dos sistemas operacionais Windows em Chinês (Hong Kong), talvez descubra que o link para instalação desse item não está habilitado.  
  
**Solução alternativa**: localize o arquivo **SQLUA.msi** na sua mídia do SQL Server 2012 em `\1028_CHT_LP\x64\redist\Upgrade Advisor` ou em `\1028_CHT_LP\x86\redist\Upgrade Advisor`, dependendo da arquitetura do seu sistema operacional.  
  
![horizontal_bar](media/horizontal-bar.png "horizontal_bar")  
  
