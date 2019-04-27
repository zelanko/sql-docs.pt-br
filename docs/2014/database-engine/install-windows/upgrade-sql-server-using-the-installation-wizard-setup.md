---
title: Atualizar para o SQL Server 2014 usando o Assistente de instalação (instalação) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- upgrading Database Engine
- Database Engine [SQL Server], upgrading
ms.assetid: cef118a5-a7ce-4bfa-8b9d-c81996284cfc
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8330702d8c886cc9197dcd944878c3f794780205
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62775382"
---
# <a name="upgrade-to-sql-server-2014-using-the-installation-wizard-setup"></a>Atualizar para o SQL Server 2014 usando o Assistente de Instalação (instalação)
  O Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece uma única árvore de recursos para a atualização de componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você também pode instalar o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] lado a lado com uma versão anterior, ou migrar bancos de dados existentes e parâmetros de configuração de uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e aplicá-los a uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Para obter mais informações, consulte estes tópicos:  
  
-   [Atualizações de versão e edição com suporte](supported-version-and-edition-upgrades.md)  
  
-   [Trabalhar com várias versões e instâncias do SQL Server](../../sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md)  
  
-   [Atualizar uma instância de cluster de failover do SQL Server &#40;instalação&#41;](../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md)  
  
-   [Instalar o SQL Server 2014 do Prompt de Comando](install-sql-server-from-the-command-prompt.md)  
  
-   [Usar o Assistente para Copiar Banco de Dados](../../relational-databases/databases/use-the-copy-database-wizard.md)  
  
> [!NOTE]  
>  Não há suporte para atualização de uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] em um computador executando o [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1. Para obter mais informações sobre instalações Server Core, consulte [instalar o SQL Server 2014 no Server Core](install-sql-server-on-server-core.md).  
  
## <a name="prerequisites"></a>Prerequisites  
 Você deve executar a Instalação como um administrador. Se você instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a partir de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura e execução no compartilhamento remoto, e ser um administrador local.  
  
 Antes de atualizar o [!INCLUDE[ssDE](../../includes/ssde-md.md)], revise os seguintes tópicos:  
  
-   [Atualizar para o SQL Server 2014](upgrade-sql-server.md)  
  
-   [Requisitos de hardware e software para a instalação do SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
-   [Verificar parâmetros do Verificador de Configuração do Sistema](check-parameters-for-the-system-configuration-checker.md)  
  
-   [Considerações sobre segurança para uma instalação do SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
-   [Compatibilidade com versões anteriores do Mecanismo de Banco de Dados do SQL Server](../sql-server-database-engine-backward-compatibility.md)  
  
> [!WARNING]  
>  Lembre-se de que você não pode alterar os recursos a serem atualizados, nem adicionar recursos durante a operação de atualização. Para obter mais informações sobre como adicionar recursos a uma instância atualizada do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] depois que a operação de atualização for concluída, consulte [adicionar recursos a uma instância do SQL Server 2014 &#40;instalação&#41;](add-features-to-an-instance-of-sql-server-setup.md).  
  
## <a name="procedure"></a>Procedimento  
  
#### <a name="to-upgrade-to-includesscurrentincludessscurrent-mdmd"></a>Para atualizar para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
1.  Insira a mídia de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e, na pasta raiz, clique duas vezes em Setup.exe. Para instalar a partir de um compartilhamento de rede, vá para a pasta raiz no compartilhamento e clique duas vezes em Setup.exe.  
  
2.  O Assistente de Instalação inicia o Centro de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para atualizar uma instância existente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], clique em **Instalação** na área de navegação esquerda e depois em **Atualizar do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]**.  
  
3.  Na página Chave do Produto, clique em uma opção para indicar se você está atualizando uma edição gratuita do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ou se tem uma chave de PID para uma versão de produção do produto. Para obter mais informações, consulte [edições e componentes do SQL Server 2014](../../sql-server/editions-and-components-of-sql-server-2016.md) e [Supported Version and Edition Upgrades](supported-version-and-edition-upgrades.md).  
  
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
  
     **ID da Instância** – Por padrão, o nome da instância é usado como a ID da Instância. Isso é usado para identificar os diretórios de instalação e as chaves do Registro da sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esse é o caso para instâncias padrão e instâncias nomeadas. Para uma instância padrão, o nome de instância e o ID da instância seriam MSSQLSERVER. Para usar uma ID de instância não padrão, forneça um valor para a caixa de texto **ID da Instância** .  
  
     Todos os service packs e atualizações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serão aplicados a cada componente de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     **Instâncias instaladas** – a grade mostrará as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que estão no computador em que a Instalação está sendo executada. Se já existir uma instância padrão instalada no computador, instale uma instância nomeada do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
13. O fluxo de trabalho do restante deste tópico depende dos recursos especificados para a instalação. Talvez você não veja todas as páginas, dependendo de suas seleções.  
  
14. Na página Configuração do Servidor – contas de Serviço, as contas de serviço padrão são exibidas para os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os serviços reais configurados nessa página dependem dos recursos que estão sendo atualizados.  
  
     As informações de autenticação e de logon serão transferidas da instância anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode atribuir a mesma conta de logon a todos os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou configurar cada conta de serviço individualmente. Você também pode especificar se os serviços serão iniciados automaticamente ou manualmente, ou se eles serão desabilitados. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que você configure contas de serviço individualmente para que serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recebam as permissões mínimas que têm para concluir suas tarefas. Para obter mais informações, consulte [Configurar contas de serviço e permissões do Windows](../configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
     Para especificar a mesma conta de logon para todas as contas de serviço nessa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], forneça credenciais nos campos na parte inferior da página.  
  
     **Observação sobre segurança** [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
     Depois de concluir a especificação de informações de logon para serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , clique em **Avançar**.  
  
15. Na página Opções de Atualização da Pesquisa de Texto Completo, especifique as opções de atualização para os bancos de dados que estão sendo atualizados. Para obter mais informações, veja [Opções de atualização da Pesquisa de Texto Completo](../../sql-server/install/full-text-search-upgrade-options.md).  
  
16. A janela Regras de Recurso avançará automaticamente se todas as regras passarem.  
  
17. A página Pronto para Atualizar mostra uma exibição de árvore das opções de instalação que foram especificadas durante a Instalação. Para continuar, clique em **Instalar**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A Instalação instalará primeiro os pré-requisitos exigidos para os recursos selecionados, seguidos da instalação dos recursos.  
  
18. Durante a instalação, a página de progresso fornece o status para que você possa monitorar o progresso da Instalação.  
  
19. Após a instalação, a página Concluída fornece um link para o arquivo de log de resumo da instalação e outras observações importantes. Para concluir o processo de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , clique em **Fechar**.  
  
20. Se você for instruído a reiniciar o computador, faça-o agora. É importante ler a mensagem do Assistente de Instalação ao concluir a Instalação. Para obter mais informações sobre os arquivos de log da Instalação, veja [Exibir e ler arquivos de log da Instalação do SQL Server](view-and-read-sql-server-setup-log-files.md).  
  
## <a name="next-steps"></a>Próximas etapas  
 Depois de atualizar para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], conclua as seguintes tarefas:  
  
-   **Registre os servidores** – a atualização remove as configurações do Registro da instância anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Depois de atualizar, você deve registrar os servidores novamente.  
  
-   **Atualize as estatísticas** – para ajudar a otimizar o desempenho de consultas, é recomendável atualizar as estatísticas em todos os bancos de dados após a atualização. Use o procedimento armazenado `sp_updatestats` para atualizar as estatísticas das tabelas definidas pelo usuário nos bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Configure a nova instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** – para reduzir a área da superfície sujeita a ataque de um sistema, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala e habilita seletivamente serviços e recursos chave. Para obter mais informações sobre a configuração da área de superfície, consulte o arquivo leiame desta versão.  
  
## <a name="see-also"></a>Consulte também  
 [Atualizar para o SQL Server 2014](upgrade-sql-server.md)   
 [Compatibilidade com versões anteriores](../../getting-started/backward-compatibility.md)  
  
  
