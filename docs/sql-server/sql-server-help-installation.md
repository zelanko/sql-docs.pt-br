---
title: Conteúdo da Ajuda do SQL Server e Help Viewer | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2017
ms.prod: sql
ms.technology: ''
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 51f8a08c-51d0-41d8-8bc5-1cb4d42622fb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 41b14322d3c895e687add2236c2447d93df62586
ms.sourcegitcommit: 1510d9fce125e5b13e181f8e32d6f6fbe6e7c7fe
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2019
ms.locfileid: "55771332"
---
# <a name="sql-server-offline-help-and-help-viewer"></a>Ajuda offline do SQL Server e Help Viewer

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Você pode usar o Microsoft Help Viewer para baixar e instalar os pacotes da Ajuda do SQL Server de fontes online ou do disco e exibi-los offline. O Help Viewer é instalado com o SSMS (SQL Server Management Studio) ou o VS (Visual Studio). Este artigo descreve as ferramentas que instalam o Help Viewer, como instalar o conteúdo da Ajuda offline e como exibir a Ajuda para [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)], SQL Server 2016 e SQL Server 2017.

É necessário ter acesso à Internet para baixar o conteúdo do Help Viewer. Você pode então migrar o conteúdo para um computador que não tenha acesso à Internet.

> [!NOTE]
> A Ajuda do SQL Server 2016 e do SQL Server 2017 é combinada, embora alguns tópicos se apliquem a versões individuais, quando indicado. A maioria dos tópicos se aplica a ambos.

## <a name="install-the-help-viewer"></a>Instalar o Help Viewer

Há duas versões do Help Viewer.  Cada versão dá suporte a versões diferentes do conteúdo do SQL Server.  O formato dos livros offline foi alterado ao longo do tempo e as versões mais antigas do Help Viewer não dão suporte às versões mais recentes dos livros:
- v2.x dá suporte ao SQL Server 2016 e à ajuda do SQL Server 2017. 
- v1.x dá suporte à ajuda do [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)]. O Help Viewer não dá suporte a configurações de proxy e não dá suporte ao formato ISO.


|**Ferramenta**|**Instala a versão do Help Viewer**|
|---------|---------|
|[Visual Studio 2017*](https://docs.microsoft.com/visualstudio/install/install-visual-studio?view=vs-2017) | v2.3|
|[SQL Server Management Studio 18.x](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) | v2.2|
|[SQL Server Management Studio 17.x](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) | v2.2|
|[SQL Server Data Tools para Visual Studio 2015](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt) | v2.2|
|Visual Studio 2015 | v2.2|
|SQL Server 2016 | v1. x|
|SQL Server 2014 Management Studio | v1. x|
|Versões anteriores do Visual Studio | v1. x|
| | |

\* Para instalar o Help Viewer com o Visual Studio 2017, na guia Componentes Individuais do Instalador do Visual Studio, selecione **Help Viewer** em Ferramentas de Código e, em seguida, clique em **Instalar**.

>[!NOTE]
> - O SQL Server 2016 instala o Help Viewer 1.1, que não dá suporte à Ajuda do SQL Server 2016. 
> - A instalação do SQL Server 2017 não instala o Help Viewer. O Help Viewer não está mais incluído na instalação do SQL Server.
> - O Help Viewer v2.x também pode dar suporte à Ajuda do [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)], caso o conteúdo seja instalado por meio do disco.

## <a name="use-help-viewer-v2x"></a>Usar o Help Viewer v2.x

O SSMS 17.x e o VS 2015 e 2017 usam o Help Viewer 2.x, que dá suporte à Ajuda do SQL Server 2016 e do SQL Server 2017. 

**Para baixar e instalar o conteúdo da Ajuda offline com o Help Viewer v2.x**

1. No SSMS ou VS, clique em **Adicionar e Remover Conteúdo da Ajuda** no menu Ajuda. 

   ![Adicionar e Remover Conteúdo do HelpViewer2](../sql-server/media/sql-server-help-installation/addremovecontent.png)  

   O Help Viewer é aberto na guia Gerenciar Conteúdo.  
   
2. Para instalar o último pacote de conteúdo da Ajuda, escolha **Online** em Origem da instalação.
   
   ![HelpViewer2_ManageContent_OnlineSource](../sql-server/media/sql-server-help-installation/helpviewer2-managecontent-onlinesource.png)  
   
   >[!NOTE]
   > Para instalar por meio do disco (Ajuda do SQL Server 2014), escolha **Disco** em Origem da instalação e especifique o local do disco.
   
   O caminho do repositório Local na guia Gerenciar Conteúdo mostra o local em que o conteúdo será instalado no computador local. Para alterar o local, clique em **Mover**, insira outro caminho de pasta no campo **Para** e, em seguida, clique em **OK**.
   Se a instalação da Ajuda falhar após a alteração do caminho do repositório Local, feche e reabra o Help Viewer, verifique se o novo local é exibido no caminho do repositório Local e, em seguida, tente executar a instalação novamente.

3. Clique em **Adicionar** ao lado de cada pacote de conteúdo (manual) que você deseja instalar. 
   Para instalar todo o conteúdo da Ajuda do SQL Server, adicione todos os 13 manuais em SQL Server. 
   
4. Clique em **Atualizar** no canto inferior direito. 
   O sumário da Ajuda à esquerda é atualizado automaticamente com os manuais adicionados. 
   
   ![HelpViewer2_ManageContent_AddContent](../sql-server/media/sql-server-help-installation/helpviewer2-managecontent-addcontent.png)     
   
> [!NOTE]
> Nem todos os títulos do nó superior no sumário do SQL Server correspondem exatamente aos nomes dos manuais da Ajuda baixáveis correspondentes. Os títulos do sumário são mapeados para os nomes de manuais da seguinte maneira:

(*) indica conteúdo que é da primeira versão de disponibilidade geral do conteúdo do SQL Server 2017, juntamente com conteúdo mais antigo da versão 2016. Esses livros serão removidos, pois livros separados e completos do SQL Server 2016 e 2017 contêm edições de conteúdo desde janeiro de 2019.  

| | Painel de conteúdo | Manual do SQL Server |
|-----|-----|-----|
|*|Referência de linguagem do Analysis Services | Referência de linguagem do Analysis Services (MDX)|
|*|Referência de DAX (Expressões de Análise de Dados) | Referência de DAX (Expressões de Análise de Dados)|
|*|Referência de DMX (extensões de mineração de dados) | Referência de DMX (extensões de mineração de dados)|
|*|Introdução ao aprendizado de máquina no SQL Server | Serviços do Microsoft Machine Learning|
|*|Referência do Power Query M | Referência do Power Query M|
||Documentação do SQL Server 2016 | Documentação do SQL Server 2016|
||Documentação do SQL Server 2017| Documentação do SQL Server 2017|
|*|Guias do desenvolvedor do SQL Server | Referência do SQL Server Developer|
|*|Baixar o SQL Server Management Studio | SQL Server Management Studio|
|*|Home page da programação do cliente para Microsoft SQL Server | Drivers de conexão do SQL Server|
|*|SQL Server no Linux | SQL Server no Linux|
|*|Documentação Técnica do SQL Server | Documentação técnica do SQL Server (SSIS, SSRS, mecanismo de BD, instalação)|
|*|Ferramentas e utilitários para o Banco de Dados SQL do Azure | Ferramentas do SQL Server|
|*|Referência do Transact-SQL (Mecanismo de Banco de Dados) | Referência do Transact-SQL|
|*|Referência de linguagem Xquery (SQL Server) | Referência de linguagem Xquery (SQL Server)|

> [!NOTE]
> Se o Help Viewer congelar (travar) durante a adição de conteúdo, altere a linha LastRefreshed="\<mm/dd/yyyy> 00:00:00" do Cache no arquivo %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings ou HlpViewer_VisualStudiox_en-US.settings para alguma data no futuro. Para obter mais informações sobre esse problema, confira [O Visual Studio Help Viewer congela](/visualstudio/welcome-to-visual-studio).

**Para exibir o conteúdo da Ajuda offline no SSMS com o Help Viewer v2.x**

Para exibir a Ajuda instalada no SSMS, pressione CTRL + ALT + F1 ou escolha **Adicionar ou Remover Conteúdo** no menu Ajuda, para iniciar o Help Viewer. 

   ![Adicionar e Remover Conteúdo do HelpViewer2](../sql-server/media/sql-server-help-installation/addremovecontent.png)  

O Help Viewer é aberto na guia Gerenciar Conteúdo, com o sumário da Ajuda instalada no painel esquerdo. Clique em tópicos no sumário para exibi-los no painel direito. 
> [!TIP]
> Se o painel de conteúdo não estiver visível, clique em Conteúdo na margem esquerda. Clique no ícone de pino para manter o painel de conteúdo aberto.  

   ![Help Viewer v2.x com conteúdo](../sql-server/media/sql-server-help-installation/helpviewer2-withcontentinstalled.png)

**Para exibir o conteúdo da Ajuda offline no VS com o Help Viewer v2.x**

Para exibir a Ajuda instalada no Visual Studio:
1. Aponte para **Definir Preferência da Ajuda** no menu Ajuda e escolha **Iniciar no Help Viewer**. 

   ![Definir Preferência de Exibição da Ajuda do Help Viewer no VS](../sql-server/media/sql-server-help-installation/launchviewer.png)

2. Clique em **Exibir Ajuda** no menu Ajuda para exibir o conteúdo no Help Viewer. 

   ![Exibir Ajuda](../sql-server/media/sql-server-help-installation/viewhelp.png)

   O sumário da Ajuda é mostrado à esquerda e o tópico da Ajuda selecionado, à direita. 

  
## <a name="use-help-viewer-v1x"></a>Usar o Help Viewer v1.x

As versões anteriores do SSMS e do VS usam o Help Viewer 1.x, que dá suporte à Ajuda do SQL Server 2014. 

**Para baixar e instalar o conteúdo da Ajuda offline com o Help Viewer v1.x**

Esse processo usa o Help Viewer 1.x para baixar a Ajuda do SQL Server 2014 no Centro de Download da Microsoft e instalá-la no computador.

1. Navegue para o site de download da [Documentação do Produto do Microsoft SQL Server 2014](https://www.microsoft.com/download/details.aspx?id=42557) e clique em **Baixar**.  
2. Clique em **Salvar** na caixa de mensagem para salvar o arquivo *SQLServer2014Documentation\_\*.exe* no computador.  
   
   >[!NOTE]
   >Para ambientes com restrição de firewall e proxy, salve o download em uma unidade USB ou outra mídia portátil que possa ser usada no ambiente.   
   
3. Clique duas vezes no .exe para desempacotar o arquivo de conteúdo da Ajuda e salve o arquivo em uma pasta local ou compartilhada.  
4. Abra o **Gerenciador da Biblioteca da Ajuda** iniciando o SSMS ou o VS e clicando em **Gerenciar Configurações da Ajuda** no menu Ajuda.  
5. Clique em **Instalar conteúdo do disco** e procure o diretório em que você desempacotou o arquivo de conteúdo da Ajuda.  
   
   ![HelpLibraryManager_MainPage_InstallFromDisk](../sql-server/media/sql-server-help-installation/helplibrarymanager-mainpage-installfromdisk.png)
   
   ![HelpLibraryManager_InstallContentFromDisk_dialog1](../sql-server/media/sql-server-help-installation/helplibrarymanager-installcontentfromdisk-dialog1.png)
   
   > [!IMPORTANT]
   > Para evitar a instalação de conteúdo da Ajuda local que tem apenas um sumário parcial, é necessário usar a opção **Instalar conteúdo do disco** no **Gerenciador da Biblioteca da Ajuda**.  Se você usou a opção **Instalar conteúdo online** e o Help Viewer exibe um sumário parcial, consulte esta [postagem no blog](https://blogs.msdn.microsoft.com/womeninanalytics/2016/06/21/troubleshoot-local-help-for-sql-server-2014/) para obter etapas de solução de problemas. 
   
8. Clique no arquivo HelpContentSetup.msha, clique em **Abrir** e depois clique em **Avançar**.  
9. Clique em **Adicionar** ao lado da documentação a ser instalada, depois clique em **Atualizar**.  
   
   ![HelpLibraryManager_InstallContentFromDisk_dialog2](../sql-server/media/sql-server-help-installation/helplibrarymanager-installcontentfromdisk-dialog2.png)  
   
10. Clique em **Concluir** e, em seguida, em **Sair**.

**Para exibir o conteúdo da Ajuda offline com o Help Viewer v1.x**

11. Para exibir a Ajuda instalada, abra o **Gerenciador da Biblioteca da Ajuda**, clique em **Escolher Ajuda online ou local** e, em seguida, clique em **Desejo usar a Ajuda local**.
12. Abra o Help Viewer para ver o conteúdo, clicando em **Exibir ajuda** no menu **Ajuda**. O conteúdo instalado é listado no painel esquerdo.  
   
   ![HelpViewer1_withContentInstalled_ZoomedIn](../sql-server/media/sql-server-help-installation/helpviewer1-withcontentinstalled-zoomedin.png)  
   


## <a name="view-online-help"></a>Exibir a Ajuda online

A Ajuda online sempre mostra o conteúdo mais atualizado. 

**Para exibir a Ajuda online do SQL Server no SSMS 17.x**

- Clique em **Exibir Ajuda** no menu **Ajuda**. A documentação mais recente do SQL Server 2016/2017 do [https://docs.microsoft.com/sql/https://docs.microsoft.com/sql/sql-server/sql-server-technical-documentation](https://docs.microsoft.com/sql/sql-server/sql-server-technical-documentation) pode ser exibida em um navegador. 

   ![Exibir Ajuda](../sql-server/media/sql-server-help-installation/viewhelp.png)

**Para exibir a Ajuda online do Visual Studio no Visual Studio**

1. Aponte para **Definir Preferência da Ajuda** no menu Ajuda e escolha **Iniciar no Navegador** ou **Iniciar no Help Viewer**. 
2. Clique em **Exibir Ajuda** no menu Ajuda. A última Ajuda do Visual Studio será exibida no ambiente escolhido. 

**Para exibir a Ajuda online com o Help Viewer v1.x**

1. Abra o **Gerenciador da Biblioteca da Ajuda** clicando em **Gerenciar Configurações da Ajuda** no menu Ajuda.  
2. Na caixa de diálogo Gerenciador da Biblioteca da Ajuda, clique em **Escolher Ajuda online ou local**.  
   
   ![HelpLibraryManager_MainPage_ChooseOnlineORLocal.png](../sql-server/media/sql-server-help-installation/helplibrarymanager-mainpage-chooseonlineorlocal.png.png)  
   
3. Clique em **Desejo usar a Ajuda online**, clique em **OK** e, em seguida, em **Sair**.  
   
   ![HelpLibraryManager_ChooseOnlineORLocalHelp_OnlineHelpSelected_dialog](../sql-server/media/sql-server-help-installation/helplibrarymanager-chooseonlineorlocalhelp-onlinehelpselected-dialog.png)

4. Abra o Help Viewer para ver o conteúdo, clicando em **Exibir ajuda** no menu **Ajuda**. 

## <a name="view-f1-help"></a>Exibir a Ajuda F1

Quando você pressiona F1 ou clica em **Ajuda** ou no ícone **?** em uma caixa de diálogo do SSMS ou do VS, um tópico da Ajuda online contextual é exibido no navegador ou no Help Viewer. 

**Para exibir a Ajuda F1**

1. Aponte para **Definir Preferência da Ajuda** no menu Ajuda e escolha **Iniciar no Navegador** ou **Iniciar no Help Viewer**.
2. Pressione F1 ou então clique em **Ajuda** ou em **?** nas caixas de diálogo em que essas opções estiverem disponíveis para ver tópicos online contextuais no ambiente escolhido.

> [!NOTE]
> A Ajuda F1 só funciona quando você está online. Não há nenhuma fonte offline para a Ajuda F1.

## <a name="systems-without-internet-access"></a>Sistemas sem acesso à Internet
Depois que os livros offline tiverem sido baixados em um sistema que tem acesso à Internet, você poderá usar as etapas a seguir para migrar o conteúdo para um sistema que não tem acesso à Internet.

  >[!NOTE]
  >O Software compatível com o Visualizador da Ajuda, como SQL Server Management Studio, deve ser instalado no sistema offline.

1. Abra o Visualizador da Ajuda (Ctrl + Alt + F1).
1. Selecione a documentação na qual tem interesse. Por exemplo, filtre por SQL e selecione a Documentação Técnica do SQL Server.
1. Identifique o caminho físico dos arquivos no disco, que pode ser encontrado em **Caminho do repositório local**.
1. Navegue até essa localização usando o explorador de sistema de arquivos.
    1.  A localização padrão é: `C:\Program Files (x86)\Microsoft SQL Server\140\Tools\Binn\ManagementStudio\Extensions\Application`
1. Selecione as três pastas **ContentStore**, **Incoming** e **IndexStore** e copie-as para a mesma localização no seu sistema offline. Talvez você precise usar um dispositivo de mídia intermediário, como um CD ou USB.
1. Depois que esses arquivos tiverem sido movidos, inicie o Visualizador da Ajuda no sistema offline e a documentação técnica do SQL Server estará disponível.

![physical-location-of-offline-content.png](media/sql-server-help-installation/physical-location-of-offline-content.png)

## <a name="next-steps"></a>Próximas etapas
[Microsoft Help Viewer – Visual Studio](/visualstudio/ide/microsoft-help-viewer)  

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]