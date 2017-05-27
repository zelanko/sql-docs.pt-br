---
title: Help Viewer para o SQL Server | Microsoft Docs
ms.custom: 
ms.date: 02/15/2017
ms.prod: sql-non-specified
ms.technology: server-general
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2014
- SQL Server 2016
ms.assetid: 51f8a08c-51d0-41d8-8bc5-1cb4d42622fb
caps.latest.revision: 8
author: sabotta
ms.author: carlasab
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: fc2435ccea3b01328c3c4623e62fbf12ee53e400
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="help-viewer-for-sql-server"></a>Help Viewer para o SQL Server
  
  
  
Este artigo explica como instalar a Ajuda local e como exibir a Ajuda online e a local. O artigo aborda o Microsoft Help Viewer 1.1 e 2.2 e a documentação do [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] e do [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]. 

>[!IMPORTANT]
>O Visualizador da Ajuda não dá suporte a configurações de proxy e não dá suporte ao formato ISO.  

>**F1 e Ajuda**
>>Quando você pressiona F1, o tópico correspondente aparece online. O tópico não pode ser exibido na Ajuda local.

## <a name="includesscurrentmdincludessscurrent-mdmd-and-help-viewer-22"></a>[!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] e Help Viewer 2.2  
O Help Viewer 2.2 está disponível no [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] Management Studio desde a Visualização de abril de 2016 (13.0.12500.29) e no Visual Studio 2015.  

> [![Baixar o SSMS](../release-notes/media/download.png)](https://msdn.microsoft.com/library/mt238290.aspx) **[Baixar a última versão do SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)**  

**Para instalar a Ajuda local para usar com o Help Viewer 2.2**  
1. Abra o Help Viewer 2.2 iniciando o SQL Server Management Studio ou o Visual Studio e clicando em **Adicionar e Remover Conteúdo da Ajuda**, no menu **Ajuda**.  
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
  
**Para exibir a Ajuda local ou a Ajuda online do SQL Server Management Studio**  
* Para exibir a Ajuda local, clique em **Adicionar e Remover Conteúdo da Ajuda** no menu **Ajuda** e clique na guia **Início do Help Viewer** para ver a documentação.  
    >[!NOTE]
    >O texto **Início do Help Viewer** é alterado com base no tópico no qual você clicou no sumário.   
* Para exibir a Ajuda online, clique em **Exibir Ajuda** no menu **Ajuda**. A documentação é exibida em um navegador.  
![HelpViewer2_SSMS_ChooseOnlineORLocalHelp](../release-notes/media/helpviewer2-ssms-chooseonlineorlocalhelp.png)  
  
  
**Para exibir a Ajuda local ou a Ajuda online no Visual Studio**  
* Clique em **Definir Preferência da Ajuda** no menu **Ajuda** e siga um dos procedimentos a seguir.  
   * Clique em **Iniciar no Navegador** para exibir a Ajuda online. Quando você clica em **Exibir Ajuda** no menu **Ajuda**, a documentação é exibida em um navegador.  
   * Clique em **Iniciar no Help Viewer** para exibir a Ajuda local. Quando você clica em **Exibir Ajuda** no menu **Ajuda**, a documentação é exibida no Help Viewer.  
     
     ![HelpViewer2_VisualStudio_ChooseOnlineORLocalHelp](../release-notes/media/helpviewer2-visualstudio-chooseonlineorlocalhelp.png)  
  
  
## <a name="includesssql14mdincludessssql14-mdmd-and-help-viewer-11"></a>[!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] e Help Viewer 1.1  
 O Help Viewer 1.1 está disponível em [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] Management Studio e versões do Visual Studio anteriores ao Visual Studio 2012.   
 
>[!NOTE]
> Você também pode exibir a Ajuda local para [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] usando o Help Viewer 2.2 somente quando você **instalar conteúdo do disco**. O Help Viewer 2.2 está disponível no [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] Management Studio desde a Visualização de abril de 2016 (13.0.12500.29) e no Visual Studio 2015. 
   
**Para instalar a Ajuda local para usar com o Help Viewer 1.1**  
1. Navegue até o [site de download](https://www.microsoft.com/en-us/download/details.aspx?id=42557) para obter o conteúdo de Ajuda e clique em **Baixar**.  
2. Clique em **Salvar** na caixa de mensagem para salvar o arquivo SQLServer2014Documentation_*.exe em seu computador.  
   >[!NOTE]
   >Para ambientes com restrição de firewall e proxy, salve o download em uma unidade USB ou outra mídia portátil que possa ser usada no ambiente.   
3. Clique duas vezes em .exe para descompactar o arquivo de conteúdo de Ajuda e salve o arquivo em uma pasta local ou compartilhada.  
4. Abra o **Gerenciador de Biblioteca de Ajuda** iniciando o SQL Server Management Studio ou o Visual Studio e clicando em **Gerenciar Configurações da Ajuda** no menu **Ajuda**.  
7. Clique em **Instalar conteúdo do disco** e navegue até o diretório em que você descompactou o arquivo de conteúdo de Ajuda.  
  
Selecione Instalar conteúdo do disco  |Navegue até o arquivo de conteúdo de Ajuda   
---------|---------  
![HelpLibraryManager_MainPage_InstallFromDisk](../release-notes/media/helplibrarymanager-mainpage-installfromdisk.png)    | ![HelpLibraryManager_InstallContentFromDisk_dialog1](../release-notes/media/helplibrarymanager-installcontentfromdisk-dialog1.png)          
  
>[!IMPORTANT]
> Para evitar instalar conteúdo da Ajuda local que tenha apenas um sumário parcial, use a opção **Instalar conteúdo do disco** no **Gerenciador de Biblioteca de Ajuda**.  
>>Se você usou a opção **Instalar conteúdo online** e o Help Viewer está exibindo um sumário parcial, consulte esta [postagem de blog](https://blogs.msdn.microsoft.com/womeninanalytics/2016/06/21/troubleshoot-local-help-for-sql-server-2014/) para etapas de solução de problemas. 

8. Clique no arquivo HelpContentSetup.msha, clique em **Abrir** e depois clique em **Avançar**.  
9. Clique em **Adicionar** ao lado da documentação a ser instalada, depois clique em **Atualizar**.  
  
   ![HelpLibraryManager_InstallContentFromDisk_dialog2](../release-notes/media/helplibrarymanager-installcontentfromdisk-dialog2.png)  
10. Clique em **Concluir**, clique em **Sair** e, em seguida, abra o Help Viewer para ver o conteúdo clicando em **Exibir Ajuda** no menu **Ajuda**. Você deve ver o conteúdo que você instalou listado no sumário, no painel esquerdo.  
  
    ![HelpViewer1_withContentInstalled_ZoomedIn](../release-notes/media/helpviewer1-withcontentinstalled-zoomedin.png)  
  
**Para exibir a Ajuda local ou a Ajuda online**  
1. Abra o **Gerenciador de Biblioteca de Ajuda** clicando em **Gerenciar Configurações da Ajuda** no menu **Ajuda**.  
2. Na caixa de diálogo **Gerenciador de Biblioteca de Ajuda**, clique em **Escolha ajuda online ou local**.  
  
   ![HelpLibraryManager_MainPage_ChooseOnlineORLocal.png](../release-notes/media/helplibrarymanager-mainpage-chooseonlineorlocal.png.png)  
3. Realize uma das ações a seguir e, depois disso, clique em **OK** e em seguida em **Sair**.  
   * Clique em **Desejo usar a ajuda online**  
   * Clique em **Desejo usar a ajuda local**.  
  
   ![HelpLibraryManager_ChooseOnlineORLocalHelp_OnlineHelpSelected_dialog](../release-notes/media/helplibrarymanager-chooseonlineorlocalhelp-onlinehelpselected-dialog.png)  
  
Se você optar por usar a Ajuda online, quando você clicar em **Exibir Ajuda** no menu **Ajuda**, o navegador abrirá e exibirá o artigo [Manuais Online do SQL Server 2014](https://msdn.microsoft.com/library/ms130214(v=sql.120).aspx) no MSDN. Se você optar por usar a Ajuda local, quando você clicar em **Exibir Ajuda**, o Help Viewer será iniciado.  

## <a name="additional-information"></a>Informações adicionais
[Microsoft Help Viewer – Visual Studio 2015](https://msdn.microsoft.com/library/hh580782.aspx)

