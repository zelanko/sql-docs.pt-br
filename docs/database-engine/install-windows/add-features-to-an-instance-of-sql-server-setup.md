---
title: Adicionar recursos a uma instância do SQL Server (Instalação)
description: Este artigo fornece um procedimento passo a passo para adicionar recursos com reconhecimento de instância a uma instância do SQL Server 2019.
ms.prod: sql
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- feature adding [SQL Server]
- " SQL Server, features"
- adding features to  SQL Server
ms.assetid: 97931fdc-d943-48dd-81b9-ae8b8d2c6dad
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: ''
ms.date: 09/07/2019
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 599f0edf2a62413aaa44ccaff191bfac034aa3d9
ms.sourcegitcommit: 863420525a1f5d5b56b311b84a6fb14e79404860
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/10/2020
ms.locfileid: "94418013"
---
# <a name="add-features-to-an-instance-of-sql-server-setup"></a>Adicionar recursos a uma instância do SQL Server (Instalação)

[!INCLUDE [ SQL Server - Windows Only](../../includes/applies-to-version/sql-windows-only.md)]

Este artigo contém um procedimento passo a passo para adicionar recursos a uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Alguns componentes ou serviços do SQL Server são específicos de uma instância do SQL Server. Eles também são conhecidos como capazes de reconhecimento de instância. Eles compartilham a mesma versão que a instância que os hospeda e são usados exclusivamente para aquela instância. Você poderá adicionar os componentes com reconhecimento de instância a uma instância do SQL Server junto com os componentes compartilhados, caso eles ainda não estejam instalados. Para obter uma lista de recursos com suporte nas diferentes edições do SQL Server, confira [Edições e recursos com suporte do SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md).

Para adicionar recursos a uma instância do SQL Server por meio do prompt de comando, confira [Instalar o SQL Server por meio do prompt de comando](./install-sql-server-from-the-command-prompt.md).

## <a name="prerequisites"></a>Pré-requisitos

Antes de continuar, examine os artigos em [Planejando uma instalação do SQL Server](../../sql-server/install/planning-a-sql-server-installation.md).

> [!NOTE]
> Para instalações locais, você deve executar a Instalação como um administrador. Se você instalar o SQL Server de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura no compartilhamento remoto.  
  
> [!NOTE]
> Quando você adicionar recursos a uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], as configurações de relatório de uso existentes serão aplicadas aos recursos recém-adicionados. Para alterar essas configurações, use a ferramenta **Relatório de Erro e Uso do SQL Server** no menu **Ferramentas de Configuração** do SQL Server.

## <a name="procedures"></a>Procedimentos

#### <a name="to-add-features-to-an-instance-of-sscurrent"></a>Para adicionar recursos a uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]

1. Insira a mídia de instalação do SQL Server. Na pasta raiz, clique duas vezes em setup.exe. Para instalar a partir de um compartilhamento de rede, navegue para a pasta raiz no compartilhamento e clique duas vezes em setup.exe. Se a caixa de diálogo Instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] for exibida, selecione **OK** para instalar os pré-requisitos e, em seguida, **Cancelar** para sair da instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  

2. O Assistente de Instalação iniciará o Centro de Instalação do SQL Server. Para adicionar um novo recurso a uma instância existente do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], selecione **Instalação** na área de navegação esquerda e depois **Nova instalação autônoma do SQL Server ou adicionar recursos a uma instalação existente**.

3. O Verificador de Configuração do Sistema executará uma operação de descoberta no computador. Para exibir os detalhes da verificação, selecione **Exibir Detalhes**. Para continuar, selecione **OK**.

4. Na página Atualizações de Produto, as atualizações de produto do SQL Server mais recentes disponíveis são exibidas. Caso você não deseje incluir as atualizações, desmarque a caixa de seleção **Incluir atualizações de produto SQL Server**. Se nenhuma atualização de produto for descoberta, a Instalação do SQL Server não exibirá esta página e avançará automaticamente para a página **Instalar Arquivos de Instalação**.

5. Na página Instalar Arquivos de Instalação, a Instalação apresenta o andamento do download, da extração e da instalação dos arquivos de Instalação. Se uma atualização para a Instalação do SQL Server for localizada e especificada para ser incluída, ela também será instalada. selecione **Instalar** para instalar arquivos de Suporte à Instalação.  

6. O Verificador de Configuração do Sistema verificará o estado do sistema do computador antes da continuação da instalação.  

7. Na página Tipo de Instalação, selecione a opção **Adicionar recursos a uma instância existente do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** e selecione a instância a ser atualizada.

8. Na página Seleção de Recursos, selecione os componentes para a instalação. Uma descrição de cada grupo de componentes é exibida no painel à direita depois que você seleciona o nome do recurso. Você pode selecionar qualquer combinação de caixas de seleção. Para obter mais informações, consulte [Edições e recursos com suporte para o SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md). Cada componente pode ser instalado somente uma vez em uma determinada instância do SQL Server. Para instalar vários componentes, você precisa instalar uma instância adicional do SQL Server.

    Os pré-requisitos dos recursos selecionados são exibidos no painel à direita. A Instalação do SQL Server instalará os pré-requisitos que ainda não estiverem instalados durante a etapa descrita posteriormente neste procedimento.

    O Verificador de Configuração do Sistema verificará o estado do sistema do computador antes da continuação da instalação. selecione **Avançar** para continuar.

9. A página Requisitos de Espaço em Disco calcula o espaço em disco necessário para os recursos especificados, e compara os requisitos com o espaço em disco disponível no computador em que a Instalação estiver sendo executada.

10. O fluxo de trabalho do restante deste artigo depende dos recursos especificados para a instalação. Talvez você não veja todas as páginas, dependendo de suas seleções.

11. Na página Configuração do Servidor – Contas de Serviço, especifique contas de logon para os serviços do SQL Server. Os serviços reais configurados nessa página dependem dos recursos selecionados para instalação.

    Você pode atribuir a mesma conta de logon a todos os serviços do SQL Server ou configurar cada conta de serviço individualmente. Você também pode especificar se os serviços serão iniciados automaticamente ou manualmente, ou se eles serão desabilitados. A Microsoft recomenda que você configure as contas de serviço individualmente para fornecer privilégios mínimos a cada serviço, nos quais os serviços do SQL Server recebem as permissões mínimas necessárias para concluir as tarefas deles. Para obter mais informações, consulte [Configuração do servidor — Contas de serviço](./install-sql-server.md) e [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).

    Para especificar a mesma conta de logon para todas as contas de serviço nessa instância do SQL Server, forneça credenciais nos campos na parte inferior da página.

    **Observação de segurança** : [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]

    Depois de concluir a especificação de informações de logon para serviços do SQL Server, selecione **Avançar**.

12. Use a guia **Configuração do Servidor – Ordenação** para especificar ordenações não padrão para o Mecanismo de Banco de Dados e o Analysis Services. Para obter mais informações, consulte [Configuração do SQL Server – Ordenação](./install-sql-server.md).

13. Use a página Configuração do Mecanismo de Banco de Dados - Provisionamento de Conta para especificar o seguinte:  

    - Modo de Segurança – Selecione Autenticação do Windows ou Autenticação de Modo Misto para sua instância do SQL Server. Se você selecionar Autenticação de Modo Misto, precisará fornecer uma senha forte para a conta interna do administrador do sistema do SQL Server.

        Depois que um dispositivo estabelecer uma conexão com êxito com o SQL Server, o mecanismo de segurança será o mesmo para Autenticação do Windows e Modo Misto. Para obter mais informações, consulte [Configuração do Mecanismo de Banco de Dados – Configuração do Servidor](./install-sql-server.md).  

    - Administradores do SQL Server – Você precisa especificar pelo menos um administrador do sistema para a instância do SQL Server. Para adicionar a conta na qual a instalação do SQL Server está sendo executada, selecione **Adicionar Usuário Atual**. Para adicionar ou remover contas da lista de administradores do sistema, selecione **Adicionar** ou **Remover** e edite a lista de usuários, grupos ou computadores que terão privilégios de administrador para a instância do SQL Server. Para obter mais informações, consulte [Configuração do Mecanismo de Banco de Dados – Configuração do Servidor](./install-sql-server.md).

    Quando concluir a edição da lista, selecione **OK**. Verifique a lista de administradores na caixa de diálogo de configuração. Quando a lista estiver completa, selecione **Avançar**.

14. Use a página Configuração do Mecanismo de Banco de Dados – Diretórios de Dados para especificar diretórios de instalação não padrão. Para instalar nos diretórios padrão, selecione **Avançar**.  

    > [!IMPORTANT]
    > Se você especificar diretórios de instalação diferentes do padrão, verifique se as pastas de instalação são exclusivas a essa instância do SQL Server. Nenhum dos diretórios nesta caixa de diálogo deve ser compartilhado com diretórios de outras instâncias do SQL Server.

    Para obter mais informações, consulte [Configuração do Mecanismo de Banco de Dados – Diretórios de dados](./install-sql-server.md).

15. Use a página Configuração do Mecanismo de Banco de Dados – FILESTREAM para habilitar o FILESTREAM na instância do SQL Server. Para obter mais informações sobre FILESTREAM, veja [Configuração do Mecanismo de Banco de Dados – Fluxo de arquivos](./install-sql-server.md). Para continuar, selecione Avançar.

16. Use a página Configuração do Analysis Services – Provisionamento de Conta para especificar o modo de servidor e os usuários ou as contas que terão permissões de administrador no Analysis Services. O modo de servidor determina quais subsistemas de memória e de armazenamento são usados no servidor. Tipos de solução diferentes são executados em modos de servidor diferentes. Se você pretende executar bancos de dados de cubo multidimensionais no servidor, escolha a opção padrão, modo de servidor Multidimensional e de Mineração de dados. Em relação às permissões de administrador, especifique pelo menos um administrador do sistema para o Analysis Services. Para adicionar a conta na qual a instalação do SQL Server está sendo executada, selecione **Adicionar Usuário Atual**. Para adicionar ou remover contas da lista de administradores do sistema, selecione **Adicionar** ou **Remover** e edite a lista de usuários, grupos ou computadores que terão privilégios de administrador para o Analysis Services. Para obter mais informações sobre permissões de modo e administrador do servidor, veja [Configuração do Analysis Services – Provisionamento de conta](./install-sql-server.md).

    Quando concluir a edição da lista, selecione **OK**. Verifique a lista de administradores na caixa de diálogo de configuração. Quando a lista estiver completa, selecione **Avançar**.

17. Use a página Configuração do Analysis Services – Diretórios de Dados para especificar diretórios de instalação não padrão. Para instalar nos diretórios padrão, selecione **Avançar**.

    > [!IMPORTANT]
    > Se você especificar diretórios de instalação diferentes do padrão, verifique se as pastas de instalação são exclusivas a essa instância do SQL Server. Nenhum dos diretórios nesta caixa de diálogo deve ser compartilhado com diretórios de outras instâncias do SQL Server.

    Para obter mais informações, veja [Configuração do Analysis Services – Diretórios de dados](./install-sql-server.md).

18. Use a página Configuração do Reporting Services para especificar o tipo de instalação do Reporting Services a ser criado. Para obter mais informações sobre os modos de configuração do Reporting Services, confira [Opções de configuração do Reporting Services &#40;SSRS&#41;](./install-sql-server.md).

19. Use a página Configuração do Distributed Replay Controller para especificar os usuários aos quais você deseja conceder permissões administrativas para o serviço Distributed Replay Controller. Usuários que têm permissões administrativas terão acesso ilimitado ao serviço Distributed Replay Controller.

    selecione o botão **Adicionar Usuário Atual** para adicionar os usuários aos quais você deseja conceder permissões de acesso para o serviço de controlador do Distributed Replay. selecione o botão **Adicionar** para adicionar permissões de acesso para o serviço de controlador do Distributed Replay. selecione o botão **Remover** para remover as permissões de acesso do serviço de controlador do Distributed Replay.

    Para continuar, selecione **Avançar**.

20. Use a página Configuração do Distributed Replay Client para especificar os usuários aos quais você deseja conceder permissões administrativas para o serviço Distributed Replay Client. Usuários que têm permissões administrativas terão acesso ilimitado ao serviço Distributed Replay Client.

    **Nome do Controlador** é um parâmetro opcional e o valor padrão é \<*blank*>. Digite o nome do controlador com o qual o computador cliente se comunicará para o serviço Distributed Replay Client. Observe o seguinte:

    - Se você já tiver configurado um controlador, digite o nome do controlador enquanto configura cada cliente.

    - Se você ainda não tiver configurado um controlador, poderá deixar o nome do controlador em branco. No entanto, digite manualmente o nome do controlador no arquivo de **configuração do cliente** .

    Especifique o **Diretório de Trabalho** para o serviço Distributed Replay Client. O diretório de trabalho padrão é \<*drive letter*>:\Arquivos de Programas\Microsoft\SQL Server\DReplayClient\WorkingDir.

    Especifique o **Diretório de Resultado** para o serviço Distributed Replay Client. O diretório de resultado padrão é \<*drive letter*>:\Arquivos de Programas\Microsoft SQL Server\DReplayClient\ResultDir.

    Para continuar, selecione **Avançar**.

21. Na página Relatório de Erro, especifique as informações que gostaria de enviar para a Microsoft para ajudar a aprimorar o SQL Server. Por padrão, as opções de relatório de erros estão habilitadas.

22. O Verificador de Configuração do Sistema executará mais um conjunto de regras para validar a configuração do computador com os recursos do SQL Server especificados.  

23. A página Pronto para Instalar mostra uma exibição de árvore das opções de instalação que foram especificadas durante a Instalação. Nesta página, a Instalação indica se o recurso Atualização de Produto está habilitado ou desabilitado e a versão da atualização final. Quando você selecionar Instalar, a Instalação do SQL Server instalará primeiro os pré-requisitos necessários aos recursos selecionados e, depois, os recursos de instalação.  

24. Durante a instalação, a página Andamento da Instalação fornece o status para que você possa monitorar o andamento da instalação conforme a Instalação prossegue.  

25. Após a instalação, a página Concluída fornece um link para o arquivo de log de resumo da instalação e outras observações importantes. Para concluir o processo de instalação do SQL Server, selecione **Fechar**.

26. Se você for instruído a reiniciar o computador, faça-o agora. É importante ler a mensagem do Assistente de Instalação ao concluir a Instalação. Para obter informações sobre os arquivos de log da Instalação, veja [Exibir e ler arquivos de log da Instalação do SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).

## <a name="next-steps"></a>Próximas etapas

Configurar sua instalação do SQL Server

- Para reduzir a área da superfície sujeita a ataques de um sistema, o SQL Server instala e ativa serviços e recursos principais de maneira seletiva. Para obter mais informações, consulte [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md).

## <a name="see-also"></a>Consulte Também
- [Exibir e ler arquivos de log da Instalação do SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)
- [Validar uma instalação do SQL Server](../../database-engine/install-windows/validate-a-sql-server-installation.md)
- [Reparar uma instalação com falha do SQL Server 2016](../../database-engine/install-windows/repair-a-failed-sql-server-installation.md)
- [Fazer Upgrade do SQL Server Usando o Assistente de Instalação &#40;Instalação&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)
- [Instalar o SQL Server do prompt de comando](./install-sql-server-from-the-command-prompt.md)
