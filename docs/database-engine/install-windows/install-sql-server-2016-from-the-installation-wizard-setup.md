---
title: "Instalar o SQL Server 2016 por meio do Assistente de Instala&#231;&#227;o (Instala&#231;&#227;o) | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Instalando o SQL Server, etapas"
  - "Instalação [SQL Server], etapas"
  - "SQL Server, instalando"
ms.assetid: 6ad23de1-2bab-4933-9122-c09f5565028d
caps.latest.revision: 91
ms.author: "mikeray"
manager: "jhubbard"
---
# Instalar o SQL Server 2016 por meio do Assistente de Instala&#231;&#227;o (Instala&#231;&#227;o)
  Este tópico apresenta um procedimento passo a passo sobre como instalar uma nova instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o assistente para instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O Assistente para Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece uma única árvore de recursos para instalação de todos os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que você não precise instalá-los individualmente. Para obter mais informações sobre os vários componentes que podem ser instalados, veja [Instalação do SQL Server 2016](../../database-engine/install-windows/installation-for-sql-server-2016.md).  Para obter mais informações sobre como instalar os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] individualmente, veja [Instalar o SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016.md).  

 Estes tópicos adicionais documentam outras maneiras de instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  

-   [Instalar o SQL Server 2016 do prompt de comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)  
  
-   [Instalar o SQL Server 2016 usando um arquivo de configuração](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)  
  
-   [Instalar o SQL Server 2016 usando SysPrep](../../database-engine/install-windows/install-sql-server-2016-using-sysprep.md)  
  
-   [Criar um novo cluster de failover do SQL Server &#40;Instalação&#41;](../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)  
  
-   [Atualizar para o SQL Server 2016 usando o Assistente de Instalação &#40;Instalação&#41;](../../database-engine/install-windows/upgrade-to-sql-server-2016-using-the-installation-wizard-setup.md) 

-   [Instalar edições gratuitas do SQL Server 2016 diretamente da Internet](../../database-engine/install-windows/install-sql-server-2016.md#bkmk_basicInstaller) 
  
## Pré-requisitos  
 Antes de instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], examine os tópicos em [Planejando uma instalação do SQL Server](../../sql-server/install/planning-a-sql-server-installation.md).  
  
> [!NOTE]  
>  Para instalações locais, você deve executar a Instalação como um administrador. Se você instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura e de execução no compartilhamento remoto.  
 
 ###  <a name="bkmk_ga_instalpatch"></a> Instalar o requisito de patch 

A Microsoft identificou um problema com a versão específica dos binários do Tempo de Execução Microsoft VC++ 2013 que são instalados como um pré-requisito pelo SQL Server 2016. Se essa atualização para os binários do Tempo de Execução de VC não for instalada, o SQL Server 2016 poderá apresentar problemas de estabilidade em determinados cenários. Antes de instalar o SQL Server 2016, siga as instruções em [Notas de Versão do SQL Server 2016](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) para ver se seu computador precisa de um patch para os binários de tempo de execução do VC. 
  
## Para instalar o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
1.  Insira a mídia de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Na pasta raiz, clique duas vezes em Setup.exe. Para instalar a partir de um compartilhamento de rede, localize a pasta raiz no compartilhamento e clique duas vezes em Setup.exe.  
  
2.  O Assistente de Instalação executa a Central de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para criar uma nova instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], clique em **Instalação** na área de navegação esquerda e depois em **Nova instalação autônoma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou adicionar recursos a uma instalação existente**.  
  
3.  Na página Chave do Produto, selecione uma opção para indicar se você está instalando uma edição gratuita do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou uma versão de produção do produto que tem uma chave de PID. Para obter mais informações, consulte [Edições e componentes do SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md).  
  
     Para continuar, clique em **Avançar**.  
  
4.  Na página Termos de Licença, examine o contrato de licença e, se concordar, marque a caixa de seleção **Aceito os termos da licença** e clique em **Avançar**. Para ajudar a aperfeiçoar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você também pode habilitar a opção de uso de recursos e enviar relatórios à [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
5.  Na janela Regras Globais, o procedimento de instalação avançará automaticamente para a janela Atualizações de Produto se não houver nenhum erro de regra.  
  
6.  A página atualização da [!INCLUDE[msCoName](../../includes/msconame-md.md)] será exibida em seguida se a caixa de seleção de atualização da [!INCLUDE[msCoName](../../includes/msconame-md.md)] nas configurações do Painel de Controle\Todos os itens do Painel de Controle\Windows Update\Alterar não estiver marcada. Colocar a marca na página de atualização da [!INCLUDE[msCoName](../../includes/msconame-md.md)] modificará as configurações do computador para incluir as atualizações mais recentes quando você procurar pelo Windows Update.  
  
7.  Na página Atualizações de Produto, as atualizações mais recentes de produtos disponíveis do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são exibidas. Se nenhuma atualização de produto for descoberta, a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não exibirá esta página e avançará automaticamente para a página **Instalar Arquivos de Instalação** .  
  
8.  Na página Instalar Arquivos de Instalação, a Instalação apresenta o andamento do download, da extração e da instalação dos arquivos de Instalação. Se uma atualização para a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for localizada, e for especificada para ser incluída, essa atualização também será instalada.  
  
9. Na página Função de Instalação, selecione **Instalação de Recurso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** e clique em **Avançar** para continuar para a página Seleção de Recursos.  
  
10. Na página Seleção de Recursos, selecione os componentes para a instalação. Uma descrição de cada grupo de componentes é exibida no painel **Descrição do recurso** depois que você seleciona o nome do recurso. Você pode selecionar qualquer combinação de caixas de seleção. Para obter mais informações, consulte [Edições e componentes do SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md) e [Recursos com suporte nas edições do SQL Server 2016](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md).  
  
     Os pré-requisitos dos recursos selecionados são exibidos no painel **Pré-requisitos dos recursos selecionados** . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A Instalação instalará os pré-requisitos ainda não instalados na etapa de instalação descrita posteriormente neste procedimento.  
  
     Você também pode especificar um diretório personalizado para componentes compartilhados usando o campo na parte inferior da página Seleção de Recursos. Para alterar o caminho de instalação de componentes compartilhados, atualize o nome do caminho no campo fornecido na parte inferior da caixa de diálogo ou clique em **Procurar** para ir para um diretório de instalação. O caminho de instalação padrão é [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)].  
  
     O caminho especificado para os componentes compartilhados deve ser um caminho absoluto. A pasta não deve estar compactada ou criptografada. Não há suporte para unidades mapeadas.  
  
     Se você estiver instalando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um sistema operacional de 64 bits, você verá as seguintes opções:  
  
    1.  Diretório de recursos compartilhados  
  
    2.  Diretório de recursos compartilhados (x86)  
  
     O caminho especificado para cada uma das opções anteriores deve ser diferente.  
  
11. A janela Regras de Recurso avançará automaticamente se todas as regras passarem.  
  
12. Na página Configuração da Instância, especifique se deseja instalar uma instância padrão ou uma instância nomeada. Para obter mais informações, consulte [Instance Configuration](../Topic/Instance%20Configuration.md).  
  
     **ID da Instância** — Por padrão, o nome da instância é usado como a ID da Instância. Isso é usado para identificar os diretórios de instalação e as chaves do Registro da sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esse é o caso para instâncias padrão e instâncias nomeadas. Para uma instância padrão, o nome de instância e o ID da instância seriam MSSQLSERVER. Para usar uma ID de instância não padrão, especifique um valor diferente para a caixa de texto **ID da Instância**.  
  
    > [!NOTE]  
    >  Instâncias autônomas típicas do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], com instâncias padrão ou nomeadas, não usam um valor não padrão para a caixa **ID da Instância**.  
  
     Todos os service packs e atualizações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serão aplicados a cada componente de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     **Instâncias instaladas** — A grade mostra as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que estão no computador onde a Instalação está sendo executada. Se já existir uma instância padrão instalada no computador, instale uma instância nomeada do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
     O fluxo de trabalho do restante da instalação depende dos recursos especificados para a instalação. Talvez você não veja todas as páginas, dependendo de suas seleções.  
  
13. Use a página Configuração do Servidor — Contas de Serviço para especificar contas de logon para serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Os serviços reais configurados nessa página dependem dos recursos selecionados para instalação.  
  
     Você pode atribuir a mesma conta de logon a todos os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou configurar cada conta de serviço individualmente. Você também pode especificar se os serviços serão iniciados automaticamente ou manualmente, ou se eles serão desabilitados. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que você configure contas de serviço individualmente para fornecer privilégios mínimos para cada serviço, em que os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recebem as permissões mínimas para concluir suas tarefas. Para obter mais informações, consulte [Configuração do servidor — Contas de serviço](../Topic/Server%20Configuration%20-%20Service%20Accounts.md) e [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
     Para especificar a mesma conta de logon para todas as contas de serviço nessa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], forneça credenciais nos campos na parte inferior da página.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
     Use a página Configuração do Servidor — Agrupamento para especificar agrupamentos não padrão para o [!INCLUDE[ssDE](../../includes/ssde-md.md)] e o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para obter mais informações, consulte [Configuração do SQL Server – Agrupamento](../Topic/Server%20Configuration%20-%20Collation.md).  
  
14. Use a página Configuração — Configuração do servidor do [!INCLUDE[ssDE](../../includes/ssde-md.md)] para especificar o seguinte:  
  
    -   Modo de Segurança — selecione Autenticação do Windows ou Autenticação de Modo Misto para sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se você selecionar Autenticação de Modo Misto, deverá fornecer uma senha forte para a conta interna do administrador de sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
         Depois que um dispositivo estabelecer uma conexão com êxito com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o mecanismo de segurança será o mesmo para Autenticação do Windows e Modo Misto. Para obter mais informações, consulte [Configuração do Mecanismo de Banco de Dados – Configuração do Servidor](../Topic/Database%20Engine%20Configuration%20-%20Server%20Configuration.md).  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] — Você deve especificar pelo menos um administrador de sistema para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para adicionar a conta sob a qual a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executada, clique em **Adicionar Usuário Atual**. Para adicionar ou remover contas da lista de administradores do sistema, clique em **Adicionar** ou **Remover**e edite a lista de usuários, grupos ou computadores que terão privilégios de administrador para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Use a página Configuração do [!INCLUDE[ssDE](../../includes/ssde-md.md)] - Diretórios de Dados para especificar diretórios de instalação não padrão. Para instalar nos diretórios padrão, clique em **Avançar**.  
  
    > [!IMPORTANT]  
    >  Se você especificar diretórios de instalação diferentes do padrão, assegure que as pastas de instalação sejam exclusivas a esta instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nenhum dos diretórios nesta caixa de diálogo deve ser compartilhado com diretórios de outras instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Para obter mais informações, consulte [Configuração do Mecanismo de Banco de Dados – Diretórios de dados](../Topic/Database%20Engine%20Configuration%20-%20Data%20Directories.md).  
  
     Use a página Configuração do [!INCLUDE[ssDE](../../includes/ssde-md.md)] - FILESTREAM para habilitar FILESTREAM para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Configuração do Mecanismo de Banco de Dados – Fluxo de arquivos](../Topic/Database%20Engine%20Configuration%20-%20Filestream.md).  
  
     Use a página [!INCLUDE[ssDE](../../includes/ssde-md.md)] Configuração – TempDB para configurar o tamanho do arquivo, o número de arquivos, os diretórios de instalação não padrão e as configurações de expansão de arquivo do TempDB. Para obter mais informações, veja [Configuração do Mecanismo de Banco de Dados – TempDB](../Topic/Database%20Engine%20Configuration%20-%20TempDB.md).  
  
15. Use a página Configuração do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] — Provisionamento de Conta para especificar o modo de servidor e os usuários ou contas que terão permissões de administrador do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. O modo de servidor determina quais subsistemas de memória e de armazenamento são usados no servidor. Tipos de solução diferentes são executados em modos de servidor diferentes. Se você pretende executar bancos de dados de cubo multidimensionais no servidor, escolha a opção padrão, modo de servidor Multidimensional e de Mineração de dados. Em relação a permissões de administrador, especifique pelo menos um administrador de sistema para o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para adicionar a conta na qual a Instalação do SQL Server está sendo executada, clique em **Adicionar Usuário Atual**. Para adicionar ou remover contas da lista de administradores do sistema, clique em **Adicionar** ou **Remover**e edite a lista de usuários, grupos ou computadores que terão privilégios de administrador no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para obter mais informações sobre permissões de modo e administrador do servidor, veja [Configuração do Analysis Services – Provisionamento de conta](../Topic/Analysis%20Services%20Configuration%20-%20Account%20Provisioning.md).  
  
     Ao concluir a edição da lista, clique em **OK**. Verifique a lista de administradores na caixa de diálogo de configuração. Quando a lista estiver concluída, clique em **Avançar**.  
  
     Use a página Configuração do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] — Diretórios de Dados para especificar diretórios de instalação não padrão. Para instalar nos diretórios padrão, clique em **Avançar**.  
  
    > [!IMPORTANT]  
    >  -   Ao instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se você especificar o mesmo caminho de diretório para INSTANCEDIR e SQLUSERDBDIR, SQL Server Agent e a Pesquisa de Texto Completo não iniciarão devido à falta de permissões.  
    > -   Se você especificar diretórios de instalação diferentes do padrão, assegure que as pastas de instalação sejam exclusivas a esta instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nenhum dos diretórios nesta caixa de diálogo deve ser compartilhado com diretórios de outras instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Para obter mais informações, veja [Configuração do Analysis Services – Diretórios de dados](../Topic/Analysis%20Services%20Configuration%20-%20Data%20Directories.md).  
  
16. Use a página Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para especificar o tipo de instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a ser criada. Para obter mais informações sobre os modos de configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e as opções disponíveis, veja [Opções de configuração do Reporting Services &#40;SSRS&#41;](../Topic/Reporting%20Services%20Configuration%20Options%20\(SSRS\).md).  
  
     Depois que você escolher uma opção, clique em **Avançar** para continuar.  
  
17. Use a página Configuração do Distributed Replay Controller para especificar os usuários aos quais você deseja conceder permissões administrativas para o serviço Distributed Replay Controller. Usuários que têm permissões administrativas terão acesso ilimitado ao serviço Distributed Replay Controller.  
  
     Clique no botão **Adicionar Usuário Atual** para adicionar os usuários aos quais você deseja conceder permissões de acesso para o serviço Distributed Replay Controller. Clique no botão **Adicionar** para adicionar permissões de acesso para o serviço Distributed Replay Controller. Clique no botão **Remover** para remover permissões de acesso do serviço Distributed Replay Controller.  
  
     Para continuar, clique em **Avançar**.  
  
18. Use a página Configuração do Distributed Replay Client para especificar os usuários aos quais você deseja conceder permissões administrativas para o serviço Distributed Replay Client. Usuários que têm permissões administrativas terão acesso ilimitado ao serviço Distributed Replay Client.  
  
     **Nome do Controlador** é um parâmetro opcional e o valor padrão é \<*blank*>. Digite o nome do controlador com o qual o computador cliente se comunicará para o serviço Distributed Replay Client. Observe o seguinte:  
  
    -   Se você já tiver configurado um controlador, digite o nome do controlador enquanto configura cada cliente.  
  
    -   Se você ainda não tiver configurado um controlador, poderá deixar o nome do controlador em branco. No entanto, digite manualmente o nome do controlador no arquivo de **configuração do cliente** .  
  
     Especifique o **Diretório de Trabalho** para o serviço Distributed Replay Client. O diretório de trabalho padrão é \<*letra da unidade*>:\Arquivos de Programas\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\WorkingDir\\.  
  
     Especifique o **Diretório de Resultado** para o serviço Distributed Replay Client. O diretório de resultado padrão é \<*letra da unidade*>:\Arquivos de Programas\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\ResultDir\\.  
  
     Para continuar, clique em **Avançar**.  
  
19. A página Pronto para Instalar mostra uma exibição de árvore das opções de instalação que foram especificadas durante a Instalação. Nesta página, a Instalação indica se o recurso Atualização de Produto está habilitado ou desabilitado e a versão da atualização final.  
  
     Para continuar, clique em **Instalar**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A Instalação instalará primeiro os pré-requisitos exigidos para os recursos selecionados, seguidos da instalação dos recursos.  
  
20. Durante a instalação, a página Progresso da Instalação fornece o status para que você possa monitorar o progresso da Instalação.  
  
21. Após a instalação, a página Concluída fornece um link para o arquivo de log de resumo da instalação e outras observações importantes. Para concluir o processo de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , clique em **Fechar**.  
  
22. Se você for instruído a reiniciar o computador, faça-o agora. É importante ler a mensagem do Assistente de Instalação ao concluir a Instalação. Para obter mais informações, consulte [View and Read SQL Server Setup Log Files](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
## Próximas etapas  
 Configure a nova instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para reduzir a área da superfície de um sistema vulnerável a ataques, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala e habilita seletivamente serviços e recursos essenciais. Para obter mais informações, consulte [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md).  
  
## Consulte também  
 [Validar uma instalação do SQL Server](../../database-engine/install-windows/validate-a-sql-server-installation.md)   
 [Reparar uma instalação com falha do SQL Server 2016](../../database-engine/install-windows/repair-a-failed-sql-server-2016-installation.md)   
 [Exibir e ler arquivos de log da Instalação do SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)   
 [Atualizar para o SQL Server 2016 usando o Assistente de Instalação &#40;Instalação&#41;](../../database-engine/install-windows/upgrade-to-sql-server-2016-using-the-installation-wizard-setup.md)   
 [Instalar o SQL Server 2016 do prompt de comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)  
  
  