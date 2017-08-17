---
title: "Adicionar recursos a uma instância do SQL Server (instalação) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- feature adding [SQL Server]
- SQL Server, features
- adding features to SQL Server
ms.assetid: 97931fdc-d943-48dd-81b9-ae8b8d2c6dad
caps.latest.revision: 29
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b33873fa1146f797a4eada3a3dbecd6ac20ce122
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="add-features-to-an-instance-of-sql-server-setup"></a>Adicionar recursos a uma instância do SQL Server (Instalação)
  Este tópico contém um procedimento passo a passo para adicionar recursos a uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Alguns componentes ou serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são específicos de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Eles também são conhecidos como capazes de reconhecimento de instância. Eles compartilham a mesma versão que a instância que os hospeda e são usados exclusivamente para aquela instância. Você pode adicionar os componentes que reconhecem a instância a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], junto com os componentes compartilhados se eles ainda não estiverem instalados. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 Para adicionar recursos a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no prompt de comando, veja [Instalar o SQL Server 2016 por meio do Prompt de Comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Antes de continuar, examine os tópicos em [Planejando uma instalação do SQL Server](../../sql-server/install/planning-a-sql-server-installation.md).  
  
> [!NOTE]  
>  Para instalações locais, você deve executar a Instalação como um administrador. Se você instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura no compartilhamento remoto.  
  
> [!NOTE]  
>  Quando você adicionar recursos a uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], as configurações de relatório de uso existentes serão aplicadas aos recursos recém-adicionados. Para alterar essas configurações, use a ferramenta **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Relatório de Erro e Uso** do no menu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**Ferramentas de Configuração** do.  
  
## <a name="procedures"></a>Procedimentos  
  
#### <a name="to-add-features-to-an-instance-of-includesscurrentincludessscurrent-mdmd"></a>Para adicionar recursos a uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
1.  Insira a mídia de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Na pasta raiz, clique duas vezes em setup.exe. Para instalar a partir de um compartilhamento de rede, navegue para a pasta raiz no compartilhamento e clique duas vezes em setup.exe. Se a caixa de diálogo Instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] for exibida, clique em [!INCLUDE[clickOK](../../includes/clickok-md.md)] para instalar os pré-requisitos e clique em **Cancelar** para sair da instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
2.  O Assistente de Instalação iniciará o Centro de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para adicionar um novo recurso a uma instância existente do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], clique em **Instalação** na área de navegação esquerda e em **Nova instalação autônoma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou adicionar recursos a uma instalação existente**.  
  
3.  O Verificador de Configuração do Sistema executará uma operação de descoberta no computador. Para exibir os detalhes da verificação, clique em **Exibir Detalhes**. Para continuar, [!INCLUDE[clickOK](../../includes/clickok-md.md)].  
  
4.  Na página Atualizações de Produto, as atualizações mais recentes de produtos disponíveis do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são exibidas. Se você não desejar incluir as atualizações, desmarque a caixa de seleção **Incluir atualizações de produto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**. Se nenhuma atualização de produto for descoberta, a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não exibirá esta página e avançará automaticamente para a página **Instalar Arquivos de Instalação** .  
  
5.  Na página Instalar Arquivos de Instalação, a Instalação apresenta o andamento do download, da extração e da instalação dos arquivos de Instalação. Se uma atualização para a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for localizada, e for especificada para ser incluída, essa atualização também será instalada. Clique em **Instalar** para instalar arquivos de Suporte à Instalação.  
  
6.  O Verificador de Configuração do Sistema verificará o estado do sistema do computador antes da continuação da instalação.  
  
7.  Na página Tipo de Instalação, selecione a opção **Adicionar recursos a uma instância existente do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** e selecione a instância a ser atualizada.  
  
8.  Na página Seleção de Recursos, selecione os componentes para a instalação. Uma descrição de cada grupo de componentes é exibida no painel à direita depois que você seleciona o nome do recurso. Você pode selecionar qualquer combinação de caixas de seleção. Para obter mais informações, consulte [Edições e componentes do SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md). Cada componente pode ser instalado somente uma vez em uma determinada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para instalar vários componentes, você deve instalar uma instância adicional do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Os pré-requisitos dos recursos selecionados são exibidos no painel à direita. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A Instalação instalará os pré-requisitos ainda não instalados na etapa de instalação descrita posteriormente neste procedimento.  
  
     O Verificador de Configuração do Sistema verificará o estado do sistema do computador antes da continuação da instalação. Clique em **Avançar** para continuar.  
  
9. A página Requisitos de Espaço em Disco calcula o espaço em disco necessário para os recursos especificados, e compara os requisitos com o espaço em disco disponível no computador em que a Instalação estiver sendo executada.  
  
10. O fluxo de trabalho do restante deste tópico depende dos recursos especificados para a instalação. Talvez você não veja todas as páginas, dependendo de suas seleções.  
  
11. Na página Configuração do Servidor — Contas de Serviço, especifique as contas de logon para os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Os serviços reais configurados nessa página dependem dos recursos selecionados para instalação.  
  
     Você pode atribuir a mesma conta de logon a todos os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou configurar cada conta de serviço individualmente. Você também pode especificar se os serviços serão iniciados automaticamente ou manualmente, ou se eles serão desabilitados. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que você configure as contas de serviço individualmente para fornecer privilégios mínimos a cada serviço, nos quais os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recebem as permissões mínimas necessárias para concluir suas tarefas. Para obter mais informações, consulte [Configuração do servidor — Contas de serviço](http://msdn.microsoft.com/library/c283702d-ab20-4bfa-9272-f0c53c31cb9f) e [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
     Para especificar a mesma conta de logon para todas as contas de serviço nessa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], forneça credenciais nos campos na parte inferior da página.  
  
     **Observação de segurança** : [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
     Depois de concluir a especificação de informações de logon para serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , clique em **Avançar**.  
  
12. Use a guia **Configuração do Servidor – Agrupamento** para especificar agrupamentos não padrão para o [!INCLUDE[ssDE](../../includes/ssde-md.md)] e o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para obter mais informações, consulte [Configuração do SQL Server – Agrupamento](http://msdn.microsoft.com/library/e3986870-5be4-458b-b671-5ff12a27b022).  
  
13. Use a página Configuração do [!INCLUDE[ssDE](../../includes/ssde-md.md)] — Provisionamento de Conta para especificar o seguinte:  
  
    -   Modo de Segurança - Selecione Autenticação do Windows ou Autenticação de Modo Misto para sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se você selecionar Autenticação de Modo Misto, deverá fornecer uma senha forte para a conta interna do administrador de sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
         Depois que um dispositivo estabelecer uma conexão com êxito com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o mecanismo de segurança será o mesmo para Autenticação do Windows e Modo Misto. Para obter mais informações, consulte [Configuração do Mecanismo de Banco de Dados – Configuração do Servidor](http://msdn.microsoft.com/library/834b26bc-49de-4033-88d5-6aa7b1609720).  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] — Você deve especificar pelo menos um administrador de sistema para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para adicionar a conta sob a qual a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executada, clique em **Adicionar Usuário Atual**. Para adicionar ou remover contas da lista de administradores do sistema, clique em **Adicionar** ou **Remover**e edite a lista de usuários, grupos ou computadores que terão privilégios de administrador para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Configuração do Mecanismo de Banco de Dados – Configuração do Servidor](http://msdn.microsoft.com/library/834b26bc-49de-4033-88d5-6aa7b1609720).  
  
     Ao concluir a edição da lista, clique em **OK**. Verifique a lista de administradores na caixa de diálogo de configuração. Quando a lista estiver concluída, clique em **Avançar**.  
  
14. Use a página Configuração do [!INCLUDE[ssDE](../../includes/ssde-md.md)] — Diretórios de Dados para especificar diretórios de instalação não padrão. Para instalar nos diretórios padrão, clique em **Avançar**.  
  
    > [!IMPORTANT]  
    >  Se você especificar diretórios de instalação diferentes do padrão, assegure que as pastas de instalação sejam exclusivas a esta instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nenhum dos diretórios nesta caixa de diálogo deve ser compartilhado com diretórios de outras instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Para obter mais informações, consulte [Configuração do Mecanismo de Banco de Dados – Diretórios de dados](http://msdn.microsoft.com/library/9b1fa0fc-623b-479a-afc3-4f13bd850487).  
  
15. Use a página Configuração do [!INCLUDE[ssDE](../../includes/ssde-md.md)] — FILESTREAM para habilitar FILESTREAM para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações sobre FILESTREAM, veja [Configuração do Mecanismo de Banco de Dados – Fluxo de arquivos](http://msdn.microsoft.com/library/641a10a1-ae52-4d26-8f1c-a032a4aeff02). Para continuar, clique em Avançar.  
  
16. Use a página Configuração do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] — Provisionamento de Conta para especificar o modo de servidor e os usuários ou contas que terão permissões de administrador do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. O modo de servidor determina quais subsistemas de memória e de armazenamento são usados no servidor. Tipos de solução diferentes são executados em modos de servidor diferentes. Se você pretende executar bancos de dados de cubo multidimensionais no servidor, escolha a opção padrão, modo de servidor Multidimensional e de Mineração de dados. Em relação a permissões de administrador, especifique pelo menos um administrador de sistema para o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para adicionar a conta na qual a Instalação do SQL Server está sendo executada, clique em **Adicionar Usuário Atual**. Para adicionar ou remover contas da lista de administradores do sistema, clique em **Adicionar** ou **Remover**e edite a lista de usuários, grupos ou computadores que terão privilégios de administrador no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para obter mais informações sobre permissões de modo e administrador do servidor, veja [Configuração do Analysis Services – Provisionamento de conta](http://msdn.microsoft.com/library/169b1af2-6fe2-467f-8ca4-919f24c620ce).  
  
     Ao concluir a edição da lista, clique em **OK**. Verifique a lista de administradores na caixa de diálogo de configuração. Quando a lista estiver concluída, clique em **Avançar**.  
  
17. Use a página Configuração do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] — Diretórios de Dados para especificar diretórios de instalação não padrão. Para instalar nos diretórios padrão, clique em **Avançar**.  
  
    > [!IMPORTANT]  
    >  Se você especificar diretórios de instalação diferentes do padrão, assegure que as pastas de instalação sejam exclusivas a esta instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nenhum dos diretórios nesta caixa de diálogo deve ser compartilhado com diretórios de outras instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Para obter mais informações, veja [Configuração do Analysis Services – Diretórios de dados](http://msdn.microsoft.com/library/ef732855-b7af-4f40-a619-5573c1c354bb).  
  
18. Use a página Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para especificar o tipo de instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a ser criada. Para obter mais informações sobre os modos de configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], consulte [Opções de configuração do Reporting Services &#40;SSRS&#41;](http://msdn.microsoft.com/library/e4561f6c-bc7f-467e-821a-cde8e5cd7391).  
  
19. Use a página Configuração do Distributed Replay Controller para especificar os usuários aos quais você deseja conceder permissões administrativas para o serviço Distributed Replay Controller. Usuários que têm permissões administrativas terão acesso ilimitado ao serviço Distributed Replay Controller.  
  
     Clique no botão **Adicionar Usuário Atual** para adicionar os usuários aos quais você deseja conceder permissões de acesso para o serviço Distributed Replay Controller. Clique no botão **Adicionar** para adicionar permissões de acesso para o serviço Distributed Replay Controller. Clique no botão **Remover** para remover permissões de acesso do serviço Distributed Replay Controller.  
  
     Para continuar, clique em **Avançar**.  
  
20. Use a página Configuração do Distributed Replay Client para especificar os usuários aos quais você deseja conceder permissões administrativas para o serviço Distributed Replay Client. Usuários que têm permissões administrativas terão acesso ilimitado ao serviço Distributed Replay Client.  
  
     **Nome do Controlador** é um parâmetro opcional e o valor padrão é \<*blank*>. Digite o nome do controlador com o qual o computador cliente se comunicará para o serviço Distributed Replay Client. Observe o seguinte:  
  
    -   Se você já tiver configurado um controlador, digite o nome do controlador enquanto configura cada cliente.  
  
    -   Se você ainda não tiver configurado um controlador, poderá deixar o nome do controlador em branco. No entanto, digite manualmente o nome do controlador no arquivo de **configuração do cliente** .  
  
     Especifique o **Diretório de Trabalho** para o serviço Distributed Replay Client. O diretório de trabalho padrão é \<*drive letter*>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\WorkingDir\\.  
  
     Especifique o **Diretório de Resultado** para o serviço Distributed Replay Client. O diretório de resultado padrão é \<*drive letter*>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\ResultDir\\.  
  
     Para continuar, clique em **Avançar**.  
  
21. Na página Relatório de Erro, especifique as informações que gostaria de enviar para a [!INCLUDE[msCoName](../../includes/msconame-md.md)] para ajudar a melhorar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por padrão, as opções de relatório de erros estão habilitadas.  
  
22. O Verificador de Configuração do Sistema executará mais um conjunto de regras para validar a configuração do computador com os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificados.  
  
23. A página Pronto para Instalar mostra uma exibição de árvore das opções de instalação que foram especificadas durante a Instalação. Nesta página, a Instalação indica se o recurso Atualização de Produto está habilitado ou desabilitado e a versão da atualização final. Quando você clicar em Instalar, a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalará primeiro os pré-requisitos necessários aos recursos selecionados e, depois, os recursos de instalação.  
  
24. Durante a instalação, a página Andamento da Instalação fornece o status para que você possa monitorar o andamento da instalação conforme a Instalação prossegue.  
  
25. Após a instalação, a página Concluída fornece um link para o arquivo de log de resumo da instalação e outras observações importantes. Para concluir o processo de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , clique em **Fechar**.  
  
26. Se você for instruído a reiniciar o computador, faça-o agora. É importante ler a mensagem do Assistente de Instalação ao concluir a Instalação. Para obter informações sobre os arquivos de log da Instalação, veja [Exibir e ler arquivos de log da Instalação do SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
## <a name="next-steps"></a>Próximas etapas  
 Configure a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Para reduzir a área da superfície sujeita a ataques de um sistema, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala e ativa serviços e recursos principais de maneira seletiva. Para obter mais informações, consulte [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e ler arquivos de log da Instalação do SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)   
 [Validar uma instalação do SQL Server](../../database-engine/install-windows/validate-a-sql-server-installation.md)   
 [Reparar uma instalação com falha do SQL Server 2016](../../database-engine/install-windows/repair-a-failed-sql-server-installation.md)   
 [Atualizar para o SQL Server 2016 usando o Assistente de Instalação &#40;Instalação&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)   
 [Instalar o SQL Server 2016 do prompt de comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)  
  
  

