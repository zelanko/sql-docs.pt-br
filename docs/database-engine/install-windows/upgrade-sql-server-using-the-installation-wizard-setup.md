---
title: "Fazer upgrade do SQL Server usando o Assistente de Instalação (Instalação) | Microsoft Docs"
ms.custom: 
ms.date: 07/24/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: setup-install
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- upgrading Database Engine
- Database Engine [SQL Server], upgrading
ms.assetid: cef118a5-a7ce-4bfa-8b9d-c81996284cfc
caps.latest.revision: "65"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.openlocfilehash: c2dd37cf69f59d90d1f9e271ef4c41e602d8c5e1
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="upgrade-sql-server-using-the-installation-wizard-setup"></a>Fazer upgrade do SQL Server usando o Assistente de Instalação (Instalação)
O Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece uma única árvore de recursos para a atualização in-loco de componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a última versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
>[!WARNING]  
>Quando você fizer upgrade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a instância anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será substituída e deixará de existir no computador. 
>
>Antes de atualizar, faça backup dos bancos de dados do SQL Server e de outros objetos associados à instância anterior do SQL Server.  
  
> [!CAUTION]  
> Para muitos ambientes de produção e alguns ambientes de desenvolvimento, uma nova atualização de instalação ou uma atualização sem interrupção é mais apropriada do que uma atualização in-loco.  Para obter mais informações sobre métodos de upgrade, consulte:
> * [Escolher um método de atualização do Mecanismo de Banco de Dados](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md)
> * [Atualizar o Data Quality Services](../../database-engine/install-windows/upgrade-data-quality-services.md)
> * [Atualização do Integration Services](../../integration-services/install-windows/upgrade-integration-services.md)
> * [Atualizar o Master Data Services](../../database-engine/install-windows/upgrade-master-data-services.md)
> * [Atualizar e migrar o Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)
> * [Atualizar o Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md)
> * [Fazer upgrade do Power Pivot para SharePoint](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md).  
  
## <a name="prerequisites"></a>Pré-requisitos  
Você deve executar a Instalação como um administrador. Se você instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a partir de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura e execução no compartilhamento remoto, e ser um administrador local.  
  
> [!WARNING]  
>  Lembre-se de que você não pode alterar os recursos a serem atualizados, nem adicionar recursos durante a operação de atualização. Para obter mais informações sobre como adicionar recursos a uma instância atualizada do [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] após a conclusão da operação de upgrade, consulte [Adicionar recursos a uma instância do SQL Server &#40;Instalação&#41;](../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md).  
  
 Se você estiver atualizando o [!INCLUDE[ssDE](../../includes/ssde-md.md)], examine [Planejar e testar o plano de atualização do Mecanismo de Banco de Dados](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md) e realize as seguintes tarefas, conforme apropriado para seu ambiente:  
  
-   Faça backup de todos os arquivos de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da instância a ser atualizada, para que seja possível restaurá-los se isso for necessário.  
  
-   Execute os comandos DBCC (Database Console Commands) apropriados nos bancos de dados a serem atualizados para verificar se eles se encontram em um estado consistente.  
  
-   Calcule o espaço em disco necessário para atualizar os componentes do SQL Server, além dos bancos de dados de usuários. Para obter o espaço em disco necessário para os componentes do SQL Server, consulte [Requisitos de hardware e software para a instalação do SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
-   Verifique se os bancos de dados do sistema do SQL Server existentes - mestre, modelo, msdb e tempdb - estão configurados para crescimento automático e verifique se eles têm espaço suficiente no disco rígido.  
  
-   Verifique se todos os servidores de banco de dados têm informações de logon no banco de dados mestre. Isso é importante para restaurar um banco de dados, pois as informações de logon de sistema residem em master.  
  
-   Desabilite todos os procedimentos armazenados de inicialização, pois o processo de atualização irá interromper e iniciar serviços na instância do SQL Server que está sendo atualizada. Os procedimentos armazenados processados no momento da inicialização podem bloquear o processo de atualização.  
  
-   Ao atualizar instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] onde o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é inscrito em relações de MSX/TSX, atualize os servidores de destino antes de atualizar os servidores mestres. Se você atualizar servidores mestres antes de servidores de destino, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não poderá se conectar a instâncias principais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Encerre todos os aplicativos, inclusive todos os serviços que dependam do SQL Server. A atualização poderá falhar se aplicativos locais forem conectados à instância que está sendo atualizada.  
  
-   Certifique-se que a Replicação esteja atualizada e interrompa-a.   
    Para obter etapas detalhadas para executar uma atualização sem interrupção em um ambiente replicado, consulte [Fazer upgrade de bancos de dados replicados](../../database-engine/install-windows/upgrade-replicated-databases.md).
  
## <a name="procedure"></a>Procedimento  
  
### <a name="to-upgrade-includessnoversionincludesssnoversion-mdmd"></a>Para fazer upgrade do [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)]  
  
1.  Insira a mídia de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e, na pasta raiz, clique duas vezes em Setup.exe. Para instalar a partir de um compartilhamento de rede, vá para a pasta raiz no compartilhamento e clique duas vezes em Setup.exe.  
  
2.  O Assistente de Instalação inicia o Centro de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para fazer upgrade de uma instância existente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], clique em **Instalação** na área de navegação à esquerda e, depois, em **Fazer upgrade de...** versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
3.  Na página Chave do Produto, clique em uma opção para indicar se você está atualizando uma edição gratuita do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ou se tem uma chave de PID para uma versão de produção do produto. Para obter mais informações, veja [Edições e componentes do SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md) e [Atualizações de versão e edição com suporte](../../database-engine/install-windows/supported-version-and-edition-upgrades.md).  
  
4.  Na página Termos de Licença, examine o contrato de licença e, se concordar, marque a caixa de seleção **Aceito os termos da licença** e clique em **Avançar**. Para ajudar a aperfeiçoar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você também pode habilitar a opção de uso de recursos e enviar relatórios à [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
5.  Na janela Regras Globais, o procedimento de instalação avançará automaticamente para a janela Atualizações de Produto se não houver nenhum erro de regra.  
  
6.  A página atualização da [!INCLUDE[msCoName](../../includes/msconame-md.md)] será exibida em seguida se a caixa de seleção de atualização da [!INCLUDE[msCoName](../../includes/msconame-md.md)] nas configurações do Painel de Controle\Todos os itens do Painel de Controle\Windows Update\Alterar não estiver marcada. Colocar a marca na página de atualização da [!INCLUDE[msCoName](../../includes/msconame-md.md)] modificará as configurações do computador para incluir as atualizações mais recentes quando você procurar pelo Windows Update.  
  
7.  Na página Atualizações de Produto, as atualizações mais recentes de produtos disponíveis do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são exibidas. Se você não desejar incluir as atualizações, desmarque a caixa de seleção **Incluir atualizações de produto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**. Se nenhuma atualização de produto for descoberta, a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não exibirá esta página e avançará automaticamente para a página **Instalar Arquivos de Instalação** .  
  
8.  Na página Instalar Arquivos de Instalação, a Instalação apresenta o andamento do download, da extração e da instalação dos arquivos de Instalação. Se uma atualização para a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for localizada, e for especificada para ser incluída, essa atualização também será instalada.  
  
9. Na janela Regras de Atualização, o procedimento de instalação avançará automaticamente para a janela Selecionar instância se não houver nenhum erro de regra.  
  
10. Na página Selecionar Instância, especifique a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a ser atualizada. Para atualizar as ferramentas de Gerenciamento e recursos compartilhados, selecione **Atualizar somente recursos compartilhados**.  
  
11. Na página Selecionar Recursos, os recursos a serem atualizados estarão pré-selecionados. Uma descrição de cada grupo de componentes é exibida no painel à direita depois que você seleciona o nome do recurso.  
  
     Os pré-requisitos dos recursos selecionados são exibidos no painel à direita. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A Instalação instalará os pré-requisitos ainda não instalados na etapa de instalação descrita posteriormente neste procedimento.  
  
    > [!NOTE]  
    >  Se você optou por fazer upgrade dos recursos compartilhados selecionando **\<Fazer upgrade somente de recursos compartilhados>** na página **Selecionar Instância**, todos os recursos compartilhados são pré-selecionados na página Seleção de Recursos. Todos os componentes compartilhados são atualizados ao mesmo tempo.  
  
12. Na página Configuração da Instância, especifique a ID da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     **ID da Instância** — Por padrão, o nome da instância é usado como a ID da Instância. Isso é usado para identificar os diretórios de instalação e as chaves do Registro da sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esse é o caso para instâncias padrão e instâncias nomeadas. Para uma instância padrão, o nome de instância e o ID da instância seriam MSSQLSERVER. Para usar uma ID de instância não padrão, forneça um valor para a caixa de texto **ID da Instância** .  
  
     Todos os service packs e atualizações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serão aplicados a cada componente de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     **Instâncias instaladas**  — A grade mostrará as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que estão no computador onde a Instalação está sendo executada. Se já existir uma instância padrão instalada no computador, instale uma instância nomeada do [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)].  
  
13. O fluxo de trabalho do restante deste tópico depende dos recursos especificados para a instalação. Talvez você não veja todas as páginas, dependendo de suas seleções.  
  
14. Na página Configuração do Servidor — Contas de Serviço, as contas de serviço padrão são exibidas para os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Os serviços reais configurados nessa página dependem dos recursos que estão sendo atualizados.  
  
     As informações de autenticação e de logon serão transferidas da instância anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode atribuir a mesma conta de logon a todos os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou configurar cada conta de serviço individualmente. Você também pode especificar se os serviços serão iniciados automaticamente ou manualmente, ou se eles serão desabilitados. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que você configure contas de serviço individualmente para que serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recebam as permissões mínimas que têm para concluir suas tarefas. Para obter mais informações, veja [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
     Para especificar a mesma conta de logon para todas as contas de serviço nessa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], forneça credenciais nos campos na parte inferior da página.  
  
     **Observação sobre segurança** [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
     Depois de concluir a especificação de informações de logon para serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , clique em **Avançar**.  
  
15. Na página Opções de Atualização da Pesquisa de Texto Completo, especifique as opções de atualização para os bancos de dados que estão sendo atualizados. Para obter mais informações, veja [Opções de atualização da Pesquisa de Texto Completo](http://msdn.microsoft.com/library/16c9376b-5fbb-4495-a429-06a2493849c9).  
  
16. A janela Regras de Recurso avançará automaticamente se todas as regras passarem.  
  
17. A página Pronto para Atualizar mostra uma exibição de árvore das opções de instalação que foram especificadas durante a Instalação. Para continuar, clique em **Instalar**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A Instalação instalará primeiro os pré-requisitos exigidos para os recursos selecionados, seguidos da instalação dos recursos.  
  
18. Durante a instalação, a página de progresso fornece o status para que você possa monitorar o progresso da Instalação.  
  
19. Após a instalação, a página Concluída fornece um link para o arquivo de log de resumo da instalação e outras observações importantes. Para concluir o processo de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , clique em **Fechar**.  
  
20. Se você for instruído a reiniciar o computador, faça-o agora. É importante ler a mensagem do Assistente de Instalação ao concluir a Instalação. Para obter mais informações sobre os arquivos de log da Instalação, veja [Exibir e ler arquivos de log da Instalação do SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
## <a name="next-steps"></a>Próximas etapas  
 Depois de atualizar para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], conclua as seguintes tarefas:  
  
-   **Registre os servidores** — A atualização remove as configurações do Registro da instância anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Depois de atualizar, você deve registrar os servidores novamente.  
  
-   **Atualize as estatísticas** — Para ajudar a otimizar o desempenho de consultas, é recomendável atualizar as estatísticas em todos os bancos de dados após a atualização. Use o procedimento armazenado **sp_updatestats** para atualizar as estatísticas em tabelas definidas pelo usuário nos bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Configure a nova instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** – Para reduzir a área da superfície sujeita a ataque de um sistema, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala e habilita seletivamente serviços e recursos chave. Para obter mais informações sobre a configuração da área de superfície, consulte o arquivo leiame desta versão.  
  
## <a name="see-also"></a>Consulte também  
 [Fazer upgrade do SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)   
 [Compatibilidade com versões anteriores_excluída](http://msdn.microsoft.com/library/15d9117e-e2fa-4985-99ea-66a117c1e9fd)  
  
  
