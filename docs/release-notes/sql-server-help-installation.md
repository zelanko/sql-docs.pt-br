---
title: "Help Viewer e conteúdo offline para o SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 06/27/2017
ms.prod: sql-non-specified
ms.technology: server-general
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2014
- SQL Server 2016
- SQL Server 2017
ms.assetid: 51f8a08c-51d0-41d8-8bc5-1cb4d42622fb
caps.latest.revision: 8
author: sabotta
ms.author: carlasab
ms.translationtype: Human Translation
ms.sourcegitcommit: aad94f116c1a8b668c9a218b32372424897a8b4a
ms.openlocfilehash: ca52d53cf25fa0ead6abd9b870f4d8dab424d11a
ms.contentlocale: pt-br
ms.lasthandoff: 06/28/2017

---
<a id="help-viewer-and-offline-content-for-sql-server" class="xliff"></a>

# Help Viewer e conteúdo offline para o SQL Server
  
  
  
Este artigo mostra como instalar o Help Viewer e exibir a documentação do SQL Server offline. O artigo aborda a documentação do [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)], do SQL Server 2016 e do SQL Server 2017. 

<a id="install-help-viewer" class="xliff"></a>

## Instalar o Help Viewer
A tabela a seguir lista as ferramentas que instalam o Help Viewer, com base na versão do SQL Server que você está usando. Instale uma das ferramentas listadas para instalar o Help Viewer.


|**Versão do SQL Server**|**Ferramentas que instalam o Help Viewer**|**Versão do Help Viewer instalada**|
|---------|---------|---------|
|SQL Server 2017<br>SQL Server 2016     |   [Versão mais recente do SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)<br><br>[Versão mais recente do SQL Server Data Tools para Visual Studio 2015](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)<br><br>2017 do Visual Studio (*dá suporte apenas ao SQL Server 2016*)  |  v2.x       |
|SQL Server 2014    | SQL Server 2014 Management Studio<br><br>Versões do Visual Studio anteriores ao Visual Studio 2012        |  v1. x       |


> [!IMPORTANT]
> O SQL Server 2016 instala o Help Viewer 1.1 que não pode ser usado para exibir a documentação do SQL Server 2016 e 2017.
> <br>
> <br>
> O SQL Server 2017 não instala o Help Viewer.
> <br>
> <br>
> Para instalar o Help Viewer com o Visual Studio 2017, clique na guia **Componentes individuais** no programa **Instalador do Visual Studio**, clique em **Help Viewer** na categoria **Ferramentas de código** e clique em **Instalar**. 
> <br>
> <br>
> Você pode exibir a Ajuda local fo [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] usando o Help Viewer 2. x somente quando ao **Instalar o conteúdo do disco**. 


<a id="sql-server-2016-sql-server-2017-offline-content" class="xliff"></a>

## Conteúdo offline do SQL Server 2016, SQL Server 2017  
 
**Para instalar o conteúdo offline**  
1. Abra o Help Viewer iniciando o SQL Server Management Studio ou o Visual Studio e, em seguida, clicando em **Adicionar e Remover Conteúdo da Ajuda** no menu **Ajuda**.  
2. Clique na guia **Gerenciar Conteúdo**.  
3. Para instalar a Ajuda de uma origem online, clique em **Online** na área **Origem da instalação**.  
![HelpViewer2_ManageContent_OnlineSource](../release-notes/media/helpviewer2-managecontent-onlinesource.png)  
7. Clique em **Adicionar** ao lado da documentação a ser instalada, depois clique em **Atualizar**.  
![HelpViewer2_ManageContent_AddContent](../release-notes/media/helpviewer2-managecontent-addcontent.png)     
  
   >[!IMPORTANT] 
   >No SQL Server Management Studio e no Visual Studio, o aplicativo Help Viewer poderá congelar (parar de responder) durante o processo de adição da documentação. Para resolver esse problema, tente o seguinte. Para obter mais informações sobre esse problema, confira [O Visual Studio Help Viewer congela](https://msdn.microsoft.com/library/mt654096.aspx).  
   >>Abra o arquivo %LOCALAPPDATA%\Microsoft\HelpViewer2.2\HlpViewer_SSMS16_en-US.settings | HlpViewer_VisualStudio14_en-US.settings no Bloco de Notas e altere a data no código a seguir para alguma data no futuro. Esse arquivo está disponível no computador local apenas após você instalar o Visual Studio. 
   >>>Cache LastRefreshed="12/31/2017 00:00:00"  
  
    O sumário no painel esquerdo é atualizado automaticamente para incluir a documentação que você adicionou.  
![HelpViewer2_withContentInstalled](../release-notes/media/helpviewer2-withcontentinstalled.png)

1. (Opcional) A caixa **Caminho do repositório local** na guia **Gerenciar Conteúdo** mostra o local em que a documentação é instalada no computador local. Para mover a documentação para um local diferente, clique em **Mover**, insira um caminho de pasta no campo **Para** da caixa de diálogo **Mover Conteúdo** e clique em **Ok**.

   ![HelpViewer2_Move Content Dialog](../release-notes/media/helpviewer2-move-content-dialog.png)

   Depois que o conteúdo é movido, o novo local é exibido no **Caminho do repositório local**.
      
   >[!IMPORTANT]
   > Se aparecer uma mensagem indicando que a operação de movimentação falhou, feche a caixa de mensagem, feche o Help Viewer e, em seguida, abra novamente o Help Viewer. Agora, o novo local para o conteúdo deve aparecer no **Caminho do repositório local**.   
 
<a id="includesssql14mdincludessssql14-mdmd-offline-content" class="xliff"></a>

## Conteúdo offline do [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] 
 
  
**Para instalar o conteúdo offline**  
1. Navegue até o [site de download](https://www.microsoft.com/en-us/download/details.aspx?id=42557) para obter o conteúdo de Ajuda e clique em **Baixar**.  
2. Clique em **Salvar** na caixa de mensagem para salvar o arquivo SQLServer2014Documentation_*.exe em seu computador.  

 Para ambientes com restrição de firewall e proxy, salve o download em uma unidade USB ou outra mídia portátil que possa ser usada no ambiente.   

3. Clique duas vezes em .exe para descompactar o arquivo de conteúdo de Ajuda e salve o arquivo em uma pasta local ou compartilhada.  
4. Abra o **Gerenciador de Biblioteca de Ajuda** iniciando o SQL Server Management Studio ou o Visual Studio e clicando em **Gerenciar Configurações da Ajuda** no menu **Ajuda**.  
5. Clique em **Instalar conteúdo do disco** e navegue até o diretório em que você descompactou o arquivo de conteúdo de Ajuda.  
  
     Selecione Instalar conteúdo do disco  |Navegue até o arquivo de conteúdo de Ajuda   
     ---------|---------  
     ![HelpLibraryManager_MainPage_InstallFromDisk](../release-notes/media/helplibrarymanager-mainpage-installfromdisk.png)    | ![HelpLibraryManager_InstallContentFromDisk_dialog1](../release-notes/media/helplibrarymanager-installcontentfromdisk-dialog1.png)          
  
     >[!IMPORTANT]
     > Para evitar instalar conteúdo da Ajuda local que tenha apenas um sumário parcial, use a opção **Instalar conteúdo do disco** no **Gerenciador de Biblioteca de Ajuda**.  
     >>Se você usou a opção **Instalar conteúdo online** e o Help Viewer está exibindo um sumário parcial, consulte esta [postagem de blog](https://blogs.msdn.microsoft.com/womeninanalytics/2016/06/21/troubleshoot-local-help-for-sql-server-2014/) para etapas de solução de problemas. 

8. Clique no arquivo HelpContentSetup.msha, clique em **Abrir** e depois clique em **Avançar**.  
9. Clique em **Adicionar** ao lado da documentação a ser instalada, depois clique em **Atualizar**.  
  
   ![HelpLibraryManager_InstallContentFromDisk_dialog2](../release-notes/media/helplibrarymanager-installcontentfromdisk-dialog2.png)  
10. Clique em **Concluir** e clique em **Sair**.
11. Abra o **Gerenciador da Biblioteca da Ajuda** novamente, clique em **Escolher ajuda online ou local** e, em seguida, clique em **Desejo usar a ajuda local**.
12. Abra o Help Viewer para ver o conteúdo, clicando em **Exibir ajuda** no menu **Ajuda**. Você deve ver o conteúdo que você instalou listado no sumário, no painel esquerdo.  
  
    ![HelpViewer1_withContentInstalled_ZoomedIn](../release-notes/media/helpviewer1-withcontentinstalled-zoomedin.png)  
  
<a id="view-online-content-in-help-viewer" class="xliff"></a>

## Exibir conteúdo online no Help Viewer

Nao Help Viewer v2. x, você pode exibir o conteúdo online seguindo um dos procedimentos a seguir.

- No SQL Server Management Studio, clique em **Exibir Ajuda** no menu **Ajuda**. A documentação é exibida em um navegador.
![HelpViewer2_SSMS_ChooseOnlineORLocalHelp](../release-notes/media/helpviewer2-ssms-chooseonlineorlocalhelp.png)

- No Visual Studio, clique em **Definir Preferência da Ajuda** no menu **Ajuda** e clique em **Iniciar no Navegador**. Quando você clica em **Exibir Ajuda** no menu **Ajuda**, a documentação é exibida em um navegador.

![HelpViewer2_VisualStudio_ChooseOnlineORLocalHelp](../release-notes/media/helpviewer2-visualstudio-chooseonlineorlocalhelp.png)   

No Help Viewer v1.x, você pode exibir o conteúdo online, fazendo o seguinte.
1. Abra o **Gerenciador de Biblioteca de Ajuda** clicando em **Gerenciar Configurações da Ajuda** no menu **Ajuda**.  
2. Na caixa de diálogo **Gerenciador de Biblioteca de Ajuda**, clique em **Escolha ajuda online ou local**.  
  
   ![HelpLibraryManager_MainPage_ChooseOnlineORLocal.png](../release-notes/media/helplibrarymanager-mainpage-chooseonlineorlocal.png.png)  
3. Clique em **Desejo usar a ajuda online**, clique em **OK** e clique em **Sair**.  

   ![HelpLibraryManager_ChooseOnlineORLocalHelp_OnlineHelpSelected_dialog](../release-notes/media/helplibrarymanager-chooseonlineorlocalhelp-onlinehelpselected-dialog.png)

<a id="f1-help-and-other-tips" class="xliff"></a>

## Ajuda F1 e outras dicas

Quando você pressiona F1, o tópico correspondente aparece online. O tópico não pode ser exibido na Ajuda local.

Além disso, o Help Viewer não dá suporte a configurações de proxy, nem ao formato ISO. 


<a id="additional-information" class="xliff"></a>

## Informações adicionais
[Microsoft Help Viewer – Visual Studio 2015](https://msdn.microsoft.com/library/hh580782.aspx)

