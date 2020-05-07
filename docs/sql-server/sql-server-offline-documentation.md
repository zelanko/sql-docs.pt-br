---
title: Instalar versões anteriores da documentação do SQL Server offline
description: Saiba como instalar a documentação offline do SQL Server 2019, 2017, 2016, 2014 e 2012. Use o SSMS (SQL Server Management Studio) para exibir o conteúdo offline.
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
ms.assetid: 51f8a08c-51d0-41d8-8bc5-1cb4d42622fb
author: markingmyname
ms.author: maghan
ms.date: 04/20/2020
ms.openlocfilehash: 1420e18fbf335e22d44bf78d526ab35c8b1434e5
ms.sourcegitcommit: c37777216fb8b464e33cd6e2ffbedb6860971b0d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82087866"
---
# <a name="install-previous-versions-of-sql-server-documentation-to-view-offline-in-ssms"></a>Instalar versões anteriores da documentação do SQL Server para exibi-la offline no SSMS

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo descreve como baixar e exibir o conteúdo do SQL Server no [SSMS (SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md) offline. O conteúdo offline permite acessar a documentação sem estar conectado à Internet (embora seja necessário inicialmente uma conexão com a Internet para baixá-lo).

A documentação offline está disponível para várias versões anteriores do SQL Server. Embora você também possa [visualizar o conteúdo de versões anteriores online](https://docs.microsoft.com/previous-versions/sql/), uma opção offline fornece uma maneira conveniente de acessar conteúdo mais antigo.

## <a name="how-to-download-and-configure-offline-content"></a>Como baixar e configurar conteúdo offline

Você pode baixar e instalar pacotes de ajuda do SQL Server de fontes online ou do disco local. As seções a seguir explicam como carregar conteúdo offline para diferentes versões do SQL Server:

- [SQL Server 2019](#sql2019)
- [SQL Server 2017](#sql2017)
- [SQL Server 2016](#sql2016)
- [SQL Server 2014](#sql2014)
- [SQL Server 2012](#sql2012)

## <a name="sql-server-2019"></a><a id="sql2019"></a> SQL Server 2019

Siga as etapas abaixo para carregar a documentação offline do SQL Server 2019.

1. No SSMS, selecione **Adicionar e Remover o Conteúdo da Ajuda** no menu Ajuda.

   ![Adicionar e remover conteúdo do Help Viewer](../sql-server/media/sql-server-help-installation/add-remove-content.png)

   O Help Viewer é aberto na guia Gerenciar Conteúdo.

2. Para localizar o conteúdo da ajuda mais recente do SQL Server 2019, na guia **Gerenciar Conteúdo**, escolha **Online** na Origem de instalação e digite *sql server 2019* na barra de pesquisa.

   ![Pesquisa de documentação do SQL Server 2019 no Help Viewer](../sql-server/media/sql-server-help-installation/sql-2019-search.png)

   > [!Note]
   > O caminho do repositório Local na guia Gerenciar Conteúdo mostra o local em que o conteúdo será instalado no computador local. Para alterar o local, selecione **Mover**, insira um caminho de pasta diferente no campo **Para** e selecione **OK**. Se a instalação da ajuda falhar após a alteração do caminho do repositório Local, feche e abra novamente o Help Viewer. Verifique se o novo local consta no caminho do repositório Local e tente realizar a instalação novamente.

3. Para instalar o conteúdo da ajuda mais recente do SQL Server 2019, selecione **Adicionar** ao lado de cada pacote de conteúdo (manual) que você deseja instalar e selecione **Atualizar** no canto inferior direito.

   ![Atualização e adição de manuais do SQL Server 2019 no Help Viewer](../sql-server/media/sql-server-help-installation/sql-2019-add-update.png)

   > [!NOTE]
   > Se o Help Viewer congelar (travar) durante a adição de conteúdo, altere a linha LastRefreshed="\<mm/dd/yyyy> 00:00:00" do Cache no arquivo %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings ou HlpViewer_VisualStudiox_en-US.settings para alguma data no futuro. Para obter mais informações sobre esse problema, confira [O Visual Studio Help Viewer congela](/visualstudio/welcome-to-visual-studio).

4. Você pode verificar se o conteúdo do SQL Server 2019 foi carregado pesquisando por *sql server 2019* no painel de conteúdo à esquerda.

   ![Atualização automática de manuais do SQL Server 2019](../sql-server/media/sql-server-help-installation/sql-2019-content.png)

## <a name="sql-server-2017"></a><a id="sql2017"></a> SQL Server 2017

Siga as etapas abaixo para carregar a documentação offline do SQL Server 2017.

1. No SSMS, selecione **Adicionar e Remover o Conteúdo da Ajuda** no menu Ajuda.

   ![Adicionar e remover conteúdo do Help Viewer](../sql-server/media/sql-server-help-installation/add-remove-content.png)

   O Help Viewer é aberto na guia Gerenciar Conteúdo.

2. Para localizar o conteúdo da ajuda mais recente do SQL Server 2017, na guia **Gerenciar Conteúdo**, escolha **Online** na Origem de instalação e digite *sql server 2017* na barra de pesquisa.

   ![Pesquisa de manuais do SQL Server 2017 no Help Viewer](../sql-server/media/sql-server-help-installation/sql-2017-search.png)

   > [!Note]
   > O caminho do repositório Local na guia Gerenciar Conteúdo mostra o local em que o conteúdo será instalado no computador local. Para alterar o local, selecione **Mover**, insira um caminho de pasta diferente no campo **Para** e selecione **OK**. Se a instalação da ajuda falhar após a alteração do caminho do repositório Local, feche e abra novamente o Help Viewer. Verifique se o novo local consta no caminho do repositório Local e tente realizar a instalação novamente.

3. Para instalar o conteúdo da ajuda mais recente do SQL Server 2017, selecione **Adicionar** ao lado de cada pacote de conteúdo (manual) que você deseja instalar e selecione **Atualizar** no canto inferior direito.

   ![Atualização e adição de manuais do SQL Server 2017 no Help Viewer](../sql-server/media/sql-server-help-installation/sql-2017-add-update.png)

   > [!NOTE]
   > Se o Help Viewer congelar (travar) durante a adição de conteúdo, altere a linha LastRefreshed="\<mm/dd/yyyy> 00:00:00" do Cache no arquivo %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings ou HlpViewer_VisualStudiox_en-US.settings para alguma data no futuro. Para obter mais informações sobre esse problema, confira [O Visual Studio Help Viewer congela](/visualstudio/welcome-to-visual-studio).

4. Você pode verificar se o conteúdo do SQL Server 2017 foi carregado pesquisando por *sql server 2017* no painel de conteúdo à esquerda.

   ![Atualização automática de manuais do SQL Server 2017](../sql-server/media/sql-server-help-installation/sql-2017-content.png)

## <a name="sql-server-2016"></a><a id="sql2016"></a> SQL Server 2016

Siga as etapas abaixo para carregar a documentação offline do SQL Server 2016.

1. No SSMS, selecione **Adicionar e Remover o Conteúdo da Ajuda** no menu Ajuda.

   ![Adicionar e remover conteúdo do Help Viewer](../sql-server/media/sql-server-help-installation/add-remove-content.png)

   O Help Viewer é aberto na guia Gerenciar Conteúdo.

2. Para localizar o conteúdo da ajuda mais recente do SQL Server 2016, na guia **Gerenciar Conteúdo**, escolha **Online** na fonte de instalação e digite *sql server 2016* na barra de pesquisa.

   ![Pesquisa de manuais do SQL Server 2016 no Help Viewer](../sql-server/media/sql-server-help-installation/sql-2016-search.png)

   > [!Note]
   > O caminho do repositório Local na guia Gerenciar Conteúdo mostra o local em que o conteúdo será instalado no computador local. Para alterar o local, selecione **Mover**, insira um caminho de pasta diferente no campo **Para** e selecione **OK**. Se a instalação da ajuda falhar após a alteração do caminho do repositório Local, feche e abra novamente o Help Viewer. Verifique se o novo local consta no caminho do repositório Local e tente realizar a instalação novamente.

3. Para instalar o conteúdo da ajuda mais recente do SQL Server 2016, selecione **Adicionar** ao lado de cada pacote de conteúdo (manual) que você deseja instalar e selecione **Atualizar** no canto inferior direito.

   ![Atualização e adição de manuais do SQL Server 2016 no Help Viewer](../sql-server/media/sql-server-help-installation/sql-2016-add-update.png)

   > [!NOTE]
   > Se o Help Viewer congelar (travar) durante a adição de conteúdo, altere a linha LastRefreshed="\<mm/dd/yyyy> 00:00:00" do Cache no arquivo %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings ou HlpViewer_VisualStudiox_en-US.settings para alguma data no futuro. Para obter mais informações sobre esse problema, confira [O Visual Studio Help Viewer congela](/visualstudio/welcome-to-visual-studio).

4. Você pode verificar se o conteúdo do SQL Server 2016 foi carregado pesquisando por *sql server 2016* no painel de conteúdo à esquerda.

   ![Atualização automática de manuais do SQL Server 2016](../sql-server/media/sql-server-help-installation/sql-2016-content.png)

## <a name="sql-server-2014"></a><a id="sql2014"></a> SQL Server 2014

Siga as etapas abaixo para carregar a documentação offline do SQL Server 2014.

1. Baixe o conteúdo da [Documentação do produto do Microsoft SQL Server 2014 para ambientes restritos por firewall e proxy](https://www.microsoft.com/download/details.aspx?id=42557) no centro de downloads e salve-o em uma pasta.

2. Descompacte a pasta zip para visualizar o arquivo.msha.

   ![Arquivo de instalação da documentação de Ajuda do SQL Server 2014](../sql-server/media/sql-server-help-installation/sql-2014-help-content-setup-msha.png)

3. No SSMS, selecione **Adicionar e Remover o Conteúdo da Ajuda** no menu Ajuda.

   ![Adicionar e remover conteúdo do Help Viewer](../sql-server/media/sql-server-help-installation/add-remove-content.png)

   O Help Viewer é aberto na guia Gerenciar Conteúdo.

4. Para instalar o conteúdo de ajuda mais recente, escolha **Disco** em Origem da instalação e selecione as reticências (...).

   ![Gerenciar fonte de disco de conteúdo no Help Viewer](../sql-server/media/sql-server-help-installation/install-source-disk.png)

   > [!NOTE]
   > O caminho do repositório Local na guia Gerenciar Conteúdo mostra o local em que o conteúdo será alocado no computador local. Para alterar o local, selecione **Mover**, insira um caminho de pasta diferente no campo **Para** e selecione **OK**.
   Se a instalação da ajuda falhar após a alteração do caminho do repositório Local, feche e abra novamente o Help Viewer. Verifique se o novo local consta no caminho do repositório Local e tente realizar a instalação novamente.

5. Localize a pasta onde você descompactou o conteúdo. Escolha o arquivo **HelpContentSetup.msha** na pasta e selecione **Abrir**.

   ![Abrir o arquivo setup.msha do conteúdo da ajuda do SQL Server 2014](../sql-server/media/sql-server-help-installation/sql-2014-open-msha.png)

6. Digite *sql server 2014* na barra de pesquisa. Depois de ver o conteúdo de 2014 disponível, selecione **Adicionar** ao lado de cada pacote de conteúdo (manual) que você deseja instalar no Help Viewer e escolha **Atualizar**.

   ![Pesquisa de manuais do SQL Server 2014 no Help Viewer](../sql-server/media/sql-server-help-installation/sql-2014-search.png)

   ![Atualização e adição de manuais do SQL Server 2014 no Help Viewer](../sql-server/media/sql-server-help-installation/sql-2014-add-update.png)

    > [!NOTE]
    > Se o Help Viewer congelar (travar) durante a adição de conteúdo, altere a linha LastRefreshed="\<mm/dd/yyyy> 00:00:00" do Cache no arquivo %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings ou HlpViewer_VisualStudiox_en-US.settings para alguma data no futuro. Para obter mais informações sobre esse problema, confira [O Visual Studio Help Viewer congela](/visualstudio/welcome-to-visual-studio).

7. Você pode verificar se o conteúdo do SQL Server 2014 foi instalado pesquisando por *sql server 2014* no painel de conteúdo à esquerda.

   ![Manuais do SQL Server 2014 atualizados automaticamente](../sql-server/media/sql-server-help-installation/sql-2014-content.png)

## <a name="sql-server-2012"></a><a id="sql2012"></a> SQL Server 2012

Siga as etapas abaixo para carregar a documentação offline do SQL Server 2012.

1. Baixe o conteúdo da [Documentação do produto do Microsoft SQL Server 2012 para ambientes restritos por firewall e proxy](https://www.microsoft.com/download/details.aspx?id=35750) no centro de downloads e salve-o em uma pasta.

2. Descompacte a pasta zip para visualizar o arquivo.msha.

   ![Arquivo de instalação do conteúdo da Ajuda do SQL Server 2012](../sql-server/media/sql-server-help-installation/sql-2012-help-content-setup-msha.png)

3. No SSMS, selecione **Adicionar e Remover o Conteúdo da Ajuda** no menu Ajuda.

   ![Adicionar e remover conteúdo do Help Viewer](../sql-server/media/sql-server-help-installation/add-remove-content.png)

   O Help Viewer é aberto na guia Gerenciar Conteúdo.

4. Para instalar o conteúdo de ajuda mais recente, escolha **Disco** em Origem da instalação e selecione as reticências (...).

   ![Gerenciar fonte de disco de conteúdo no Help Viewer](../sql-server/media/sql-server-help-installation/install-source-disk.png)

   > [!NOTE]
   > O caminho do repositório Local na guia Gerenciar Conteúdo mostra o local em que o conteúdo será alocado no computador local. Para alterar o local, selecione **Mover**, insira um caminho de pasta diferente no campo **Para** e selecione **OK**.
   Se a instalação da ajuda falhar após a alteração do caminho do repositório Local, feche e abra novamente o Help Viewer. Verifique se o novo local consta no caminho do repositório Local e tente realizar a instalação novamente.

5. Localize a pasta onde você descompactou o conteúdo. Escolha o arquivo **HelpContentSetup.msha** na pasta e selecione **Abrir**.

   ![Abrir o arquivo setup.msha do conteúdo da ajuda do SQL Server 2012](../sql-server/media/sql-server-help-installation/sql-2012-open-msha.png)

6. Digite *sql server 2012* na barra de pesquisa. Depois de ver o conteúdo de 2012 disponível, selecione **Adicionar** ao lado de cada pacote de conteúdo (manual) que você deseja instalar no Help Viewer e escolha **Atualizar**.

   ![Pesquisa de manuais do SQL Server 2012 no Help Viewer](../sql-server/media/sql-server-help-installation/sql-2012-search.png)

   ![Atualização e adição de manuais do SQL Server 2012 no Help Viewer](../sql-server/media/sql-server-help-installation/sql-2012-add-update.png)

    > [!NOTE]
    > Se o Help Viewer congelar (travar) durante a adição de conteúdo, altere a linha LastRefreshed="\<mm/dd/yyyy> 00:00:00" do Cache no arquivo %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings ou HlpViewer_VisualStudiox_en-US.settings para alguma data no futuro. Para obter mais informações sobre esse problema, confira [O Visual Studio Help Viewer congela](/visualstudio/welcome-to-visual-studio).

7. Você pode verificar se o conteúdo do SQL Server 2012 foi carregado pesquisando por *sql server 2012* no painel de conteúdo à esquerda.

   ![Documentação do SQL Server 2012 atualizada automaticamente](../sql-server/media/sql-server-help-installation/sql-2012-content.png)

## <a name="view-offline-documentation"></a>Exibir documentação offline

Você pode exibir o conteúdo de ajuda do SQL Server usando o menu **AJUDA** na versão mais recente do [SSMS (SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md).

### <a name="view-offline-help-content-in-ssms"></a>Exibir o conteúdo da ajuda offline no SSMS

Para visualizar a ajuda instalada no SSMS, selecione **Inicializar no Help Viewer** no menu Ajuda, para iniciar o Help Viewer.

   ![Inicializar no Help Viewer](../sql-server/media/sql-server-help-installation/helpviewer-view-offline.png)  

O Help Viewer é aberto na guia Gerenciar Conteúdo, com o sumário da Ajuda instalada no painel esquerdo. Selecione os artigos no sumário para exibi-los no painel à direita.

> [!TIP]
> Se o painel de conteúdo não estiver visível, selecione Conteúdos na margem esquerda. Selecione o ícone de pino para manter o painel de conteúdo aberto.  

   ![Help Viewer com conteúdo](../sql-server/media/sql-server-help-installation/view-offline-all.png)

## <a name="life-cycle-policy"></a>Política de ciclo de vida

Confira o Ciclo de Vida do Produto da Microsoft para obter informações de compatibilidade de um produto, serviço ou tecnologia específica:

- [Política do Ciclo de Vida da Microsoft](https://support.microsoft.com/lifecycle/selectindex)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre conteúdo arquivado e sobre o Help Viewer, confira os links abaixo.

- [Um link direto para versões anteriores da documentação do SQL Server](https://docs.microsoft.com/previous-versions/sql/)
- [Microsoft Help Viewer – Visual Studio](https://docs.microsoft.com/visualstudio/help-viewer/overview)
- [Documentação do SQL Server, início](../sql-server/index.yml?view=sql-server-2016)
- [Sistema de controle de versão para documentação do SQL](../sql-server/versioning-system-monikers-ui-sql-server.md?view=sql-server-2016)