---
title: Instalar a documentação do SQL Server para visualização offline
description: Saiba como instalar a documentação offline do SQL Server 2019, 2017, 2016, 2014 e 2012. Use o SSMS (SQL Server Management Studio) para exibir o conteúdo offline.
ms.prod: sql
ms.technology: install
ms.topic: conceptual
ms.assetid: 51f8a08c-51d0-41d8-8bc5-1cb4d42622fb
author: markingmyname
ms.author: maghan
ms.reviewer: carlrab
ms.date: 07/22/2020
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || sql-server-previousversions || >= sql-server-2016 || >= sql-server-linux-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 0d4145832aee94a1786308e21ac425081d4d2a88
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87237836"
---
# <a name="install-sql-server-documentation-to-view-offline-in-ssms"></a>Instalar a documentação do SQL Server para visualização offline em SSMS

[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

Este artigo descreve como baixar e exibir o conteúdo do SQL Server no [SSMS (SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md) offline. O conteúdo offline permite acessar a documentação sem estar conectado à Internet (embora seja necessário inicialmente uma conexão com a Internet para baixá-lo).

A documentação offline está disponível para versões do SQL Server 2012 e posteriores. Embora você possa ver o conteúdo de [versões anteriores online](https://docs.microsoft.com/previous-versions/sql/), uma opção offline fornece um modo conveniente de acessar conteúdo mais antigo.

- [SQL Server 2016 e posterior](#sql-server-2016-and-later-offline-content)
- [SQL Server 2014](#sql-server-2014-offline-content)
- [SQL Server 2012](#sql-server-2012-offline-content)

## <a name="sql-server-2016-and-later-offline-content"></a>SQL Server 2016 e conteúdo offline posterior

As etapas a seguir explicam como carregar conteúdo offline para o SQL Server 2016 e posteriores.

1. No SSMS, selecione **Adicionar e Remover o Conteúdo da Ajuda** no menu Ajuda.

   ![Adicionar e Remover Conteúdo da Ajuda](../sql-server/media/sql-server-offline-documentation/add-remove-content.png)

   O Help Viewer é aberto na guia Gerenciar Conteúdo.

2. Para localizar o conteúdo da ajuda mais recente do SQL Server 2016 e posteriores, na guia **Gerenciar Conteúdo**, escolha **Online** na origem de instalação e digite *sql server* na barra de pesquisa.

   ![Pesquisa de livros do SQL Server](../sql-server/media/sql-server-offline-documentation/sql-online-search.png)

   > [!Note]
   > O caminho do repositório Local na guia Gerenciar Conteúdo mostra o local em que o conteúdo será instalado no computador local. Para alterar o local, selecione **Mover**, insira um caminho de pasta diferente no campo **Para** e selecione **OK**. Se a instalação da ajuda falhar após a alteração do caminho do repositório Local, feche e abra novamente o Help Viewer. Verifique se o novo local consta no caminho do repositório Local e tente realizar a instalação novamente.

3. Para instalar o conteúdo da ajuda mais recente do SQL Server 2016 e posteriores, selecione **Adicionar** ao lado de cada pacote de conteúdo (manual) que você deseja instalar e selecione **Atualizar** no canto inferior direito.

   ![Adicionar e atualizar livros online do SQL Server](../sql-server/media/sql-server-offline-documentation/sql-add-update.png)

   > [!NOTE]
   > Se o Help Viewer congelar (travar) durante a adição de conteúdo, altere a linha LastRefreshed="\<mm/dd/yyyy> 00:00:00" do Cache no arquivo %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings ou HlpViewer_VisualStudiox_en-US.settings para alguma data no futuro. Para obter mais informações sobre esse problema, confira [O Visual Studio Help Viewer congela](/visualstudio/welcome-to-visual-studio).

4. Você pode verificar se o conteúdo do SQL Server 2016 e posteriores foi carregado pesquisando por *sql server 2016* no painel de conteúdo à esquerda.

   ![Atualização automática de manuais do SQL Server 2016](../sql-server/media/sql-server-offline-documentation/sql-2016-content.png)

## <a name="sql-server-2014-offline-content"></a>Conteúdo offline do SQL Server 2014

> [!IMPORTANT]
> O conteúdo Transact-SQL do SQL 2014 só está disponível offline.

As etapas a seguir explicam como carregar conteúdo offline para o SQL Server 2014.

1. Baixe o conteúdo da [Documentação do produto do Microsoft SQL Server 2014 para ambientes restritos por firewall e proxy](https://www.microsoft.com/download/details.aspx?id=42557) no centro de downloads e salve-o em uma pasta.

2. Descompacte o arquivo para ver o arquivo *.msha*.

   ![Arquivo de instalação da documentação de Ajuda do SQL Server 2014](../sql-server/media/sql-server-offline-documentation/sql-2014-help-content-setup-msha.png)

3. No SSMS, selecione **Adicionar e Remover o Conteúdo da Ajuda** no menu Ajuda.

   ![Adicionar e remover conteúdo do Help Viewer](../sql-server/media/sql-server-offline-documentation/add-remove-content.png)

   O Help Viewer é aberto na guia Gerenciar Conteúdo.

4. Para instalar o conteúdo de ajuda mais recente, escolha **Disco** em Origem da instalação e selecione as reticências (...).

   ![Gerenciar fonte de disco de conteúdo no Help Viewer](../sql-server/media/sql-server-offline-documentation/install-source-disk.png)

   > [!NOTE]
   > O caminho do repositório Local na guia Gerenciar Conteúdo mostra o local em que o conteúdo será alocado no computador local. Para alterar o local, selecione **Mover**, insira um caminho de pasta diferente no campo **Para** e selecione **OK**.
   Se a instalação da ajuda falhar após a alteração do caminho do repositório Local, feche e abra novamente o Help Viewer. Verifique se o novo local consta no caminho do repositório Local e tente realizar a instalação novamente.

5. Localize a pasta onde você descompactou o conteúdo. Escolha o arquivo **HelpContentSetup.msha** na pasta e selecione **Abrir**.

   ![Abrir o arquivo setup.msha do conteúdo da ajuda do SQL Server 2014](../sql-server/media/sql-server-offline-documentation/sql-2014-open-msha.png)

6. Digite *sql server 2014* na barra de pesquisa. Depois de ver o conteúdo de 2014 disponível, selecione **Adicionar** ao lado de cada pacote de conteúdo (manual) que você deseja instalar no Help Viewer e escolha **Atualizar**.

   ![Pesquisa de manuais do SQL Server 2014 no Help Viewer](../sql-server/media/sql-server-offline-documentation/sql-2014-search.png)

   ![Atualização e adição de manuais do SQL Server 2014 no Help Viewer](../sql-server/media/sql-server-offline-documentation/sql-2014-add-update.png)

    > [!NOTE]
    > Se o Help Viewer congelar (travar) durante a adição de conteúdo, altere a linha LastRefreshed="\<mm/dd/yyyy> 00:00:00" do Cache no arquivo %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings ou HlpViewer_VisualStudiox_en-US.settings para alguma data no futuro. Para obter mais informações sobre esse problema, confira [O Visual Studio Help Viewer congela](/visualstudio/welcome-to-visual-studio).

7. Você pode verificar se o conteúdo do SQL Server 2014 foi instalado pesquisando por *sql server 2014* no painel de conteúdo à esquerda.

   ![Manuais do SQL Server 2014 atualizados automaticamente](../sql-server/media/sql-server-offline-documentation/sql-2014-content.png)

## <a name="sql-server-2012-offline-content"></a>Conteúdo offline do SQL Server 2012

As etapas a seguir explicam como carregar conteúdo offline para o SQL Server 2012

1. Baixe o conteúdo da [Documentação do produto do Microsoft SQL Server 2012 para ambientes restritos por firewall e proxy](https://www.microsoft.com/download/details.aspx?id=35750) no centro de downloads e salve-o em uma pasta.

2. Descompacte o arquivo para ver o arquivo *.msha*.

   ![Arquivo de instalação do conteúdo da Ajuda do SQL Server 2012](../sql-server/media/sql-server-offline-documentation/sql-2012-help-content-setup-msha.png)

3. No SSMS, selecione **Adicionar e Remover o Conteúdo da Ajuda** no menu Ajuda.

   ![Adicionar e remover conteúdo do Help Viewer](../sql-server/media/sql-server-offline-documentation/add-remove-content.png)

   O Help Viewer é aberto na guia Gerenciar Conteúdo.

4. Para instalar o conteúdo de ajuda mais recente, escolha **Disco** em Origem da instalação e selecione as reticências (...).

   ![Gerenciar fonte de disco de conteúdo no Help Viewer](../sql-server/media/sql-server-offline-documentation/install-source-disk.png)

   > [!NOTE]
   > O caminho do repositório Local na guia Gerenciar Conteúdo mostra o local em que o conteúdo será alocado no computador local. Para alterar o local, selecione **Mover**, insira um caminho de pasta diferente no campo **Para** e selecione **OK**.
   Se a instalação da ajuda falhar após a alteração do caminho do repositório Local, feche e abra novamente o Help Viewer. Verifique se o novo local consta no caminho do repositório Local e tente realizar a instalação novamente.

5. Localize a pasta onde você descompactou o conteúdo. Escolha o arquivo **HelpContentSetup.msha** na pasta e selecione **Abrir**.

   ![Abrir o arquivo setup.msha do conteúdo da ajuda do SQL Server 2012](../sql-server/media/sql-server-offline-documentation/sql-2012-open-msha.png)

6. Digite *sql server 2012* na barra de pesquisa. Depois de ver o conteúdo de 2012 disponível, selecione **Adicionar** ao lado de cada pacote de conteúdo (manual) que você deseja instalar no Help Viewer e escolha **Atualizar**.

   ![Pesquisa de manuais do SQL Server 2012 no Help Viewer](../sql-server/media/sql-server-offline-documentation/sql-2012-search.png)

   ![Atualização e adição de manuais do SQL Server 2012 no Help Viewer](../sql-server/media/sql-server-offline-documentation/sql-2012-add-update.png)

    > [!NOTE]
    > Se o Help Viewer congelar (travar) durante a adição de conteúdo, altere a linha LastRefreshed="\<mm/dd/yyyy> 00:00:00" do Cache no arquivo %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings ou HlpViewer_VisualStudiox_en-US.settings para alguma data no futuro. Para obter mais informações sobre esse problema, confira [O Visual Studio Help Viewer congela](/visualstudio/welcome-to-visual-studio).

7. Você pode verificar se o conteúdo do SQL Server 2012 foi carregado pesquisando por *sql server 2012* no painel de conteúdo à esquerda.

   ![Documentação do SQL Server 2012 atualizada automaticamente](../sql-server/media/sql-server-offline-documentation/sql-2012-content.png)

## <a name="view-offline-documentation"></a>Exibir documentação offline

Você pode exibir o conteúdo de ajuda do SQL Server usando o menu **AJUDA** na versão mais recente do [SSMS (SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md).

### <a name="view-offline-help-content-in-ssms"></a>Exibir o conteúdo da ajuda offline no SSMS

Para visualizar a ajuda instalada no SSMS, selecione **Inicializar no Help Viewer** no menu Ajuda, para iniciar o Help Viewer.

   ![Inicializar no Help Viewer](../sql-server/media/sql-server-offline-documentation/helpviewer-view-offline.png)  

O Help Viewer é aberto na guia Gerenciar Conteúdo, com o sumário da Ajuda instalada no painel esquerdo. Selecione os artigos no sumário para exibi-los no painel à direita.

> [!Important]
> Se o painel de conteúdo não estiver visível, selecione Conteúdos na margem esquerda. Selecione o ícone de pino para manter o painel de conteúdo aberto.  

   ![Help Viewer com conteúdo](../sql-server/media/sql-server-offline-documentation/view-offline-all.png)

## <a name="life-cycle-policy"></a>Política de ciclo de vida

Confira o Ciclo de Vida do Produto da Microsoft para obter informações de compatibilidade de um produto, serviço ou tecnologia específica:

- [Política do Ciclo de Vida da Microsoft](https://support.microsoft.com/lifecycle/selectindex)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre conteúdo arquivado e o Help Viewer, confira os links abaixo.

- [Documentação online do SQL Server](../sql-server/index.yml?view=sql-server-2016)
- [Documentação online do SQL Server 2014](/sql/2014-toc/)
- [Versões anteriores da documentação online do SQL Server](previous-versions-sql-server.md)
- [Sistema de controle de versão para documentação do SQL](../sql-server/versioning-system-monikers-ui-sql-server.md?view=sql-server-2016)
