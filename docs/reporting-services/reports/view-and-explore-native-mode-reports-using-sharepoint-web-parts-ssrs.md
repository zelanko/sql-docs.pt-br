---
title: "Exibir e explorar os relatórios de modo nativo usando Web Parts do SharePoint (SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: dee8ee42-156b-43b6-b202-02dfb9404284
caps.latest.revision: 9
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 507cac75588632cfd89f5275ee7038a49b8cdfc5
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---

# <a name="view-and-explore-native-mode-reports-using-sharepoint-web-parts-ssrs"></a>View and Explore Native Mode Reports Using SharePoint Web Parts (SSRS)

> [!IMPORTANT]  
>  SQL Server Reporting Services não oferece mais suporte usando o modo nativo (RSWebParts.cab) web parts para acessar conteúdo do servidor de relatório em um site do SharePoint de um servidor de relatório do modo nativo. Use um [Web Part do Visualizador de Relatórios em um site do SharePoint](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md) .  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] oferece várias Web Parts que funcionam com versões específicas de um servidor de relatório e em modos de implantação específicos.  
  
-   **Modo nativo:** para acessar o conteúdo do servidor de relatório em um site do SharePoint a partir de um servidor de relatório em modo nativo, use as Web Parts do Navegador de Relatórios e Visualizador de Relatórios do SharePoint 2.0 que estão incluídas no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. As instruções para instalação e uso de Web Parts 2.0 são fornecidas neste tópico.  
  
-   **Modo do SharePoint:** se você quiser acessar um servidor de relatório executado em modo do SharePoint, use as Web Parts instaladas pelo Suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para produtos do SharePoint. Para obter mais informações sobre o suplemento, veja [Onde encontrar o suplemento Reporting Services para produtos do SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).  
  
> [!NOTE]  
>  A Web Part do visualizador de relatórios para modo nativo (SPViewer.dwp) é uma Web Part diferente de um (ReportViewer.dwp) instalado pelo Suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para produtos do SharePoint. As Web Parts têm esquemas e implementações diferentes, mas ambos podem ser instalados no mesmo farm do SharePoint. Visualmente, você pode distinguir as duas Web Parts pela seguinte característica: a Web Part do Visualizador de Relatórios que é instalada por meio do suplemento tem um menu **Ações** na barra de ferramentas.  
  
 Para obter mais informações sobre modos do servidor de relatório, veja [Servidor de relatório do Reporting Services](../../reporting-services/report-server-sharepoint/reporting-services-report-server.md).  
  
 Neste tópico:  
  
-   [Sobre o Navegador de Relatórios e o Visualizador de Relatórios](#bkmk_aboutwebparts)  
  
-   [Requisitos para usar as Web Parts](#bkmk_requirements)  
  
-   [Instalando Web Parts](#bkmk_installingwebparts)  
  
-   [Adicionar e configurar Web Parts](#bkmk_configurewebparts)  
  
##  <a name="bkmk_aboutwebparts"></a> Sobre o Navegador de Relatórios e o Visualizador de Relatórios  
 O Navegador de Relatórios e o Visualizador de Relatórios são Web Parts do SharePoint 2.0 que foram introduzidos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2000 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Service Pack 2 (SP2) e continuam disponíveis nas versões atuais.  
  
 As Web Parts oferecem um meio de visualizar os relatórios e explorar a hierarquia de pastas do servidor de relatório em um site do SharePoint.  
  
 Observe que a personalização das Web Parts não tem suporte. As Web Parts destinam-se ao uso no estado em que estão, e não devem ser estendidas nem modificadas.  
  
-   O**Navegador de Relatórios** (SPExplorer.dwp) conecta-se ao Gerenciador de Relatórios no computador do servidor de relatório. Você pode navegar nos relatórios disponíveis em um servidor de relatórios e pode assinar relatórios individuais. Se o Construtor de Relatórios estiver habilitado e você tiver permissões suficientes, você poderá iniciar o Construtor de Relatórios a partir da Web Part do Navegador de Relatórios.  
  
     O Navegador de Relatórios exibe os conteúdos de uma pasta que usa uma página no Gerenciador de Relatórios. O acesso aos itens individuais e às pastas em toda a hierarquia de pastas do servidor de relatórios é controlado por meio de atribuições de função no servidor de relatórios. Ao selecionar um relatório, uma janela de navegador nova é exibida. O Visualizador HTML no servidor de relatório exibe o relatório e oferece a barra de ferramentas do relatório, não a Web Part do Visualizador de Relatórios. Se desejar personalizar as definições da barra de ferramentas, lembre-se de especificar os parâmetro de acesso da URL no servidor de relatório. Para obter instruções, consulte [Referência de parâmetro de acesso de URL](../../reporting-services/url-access-parameter-reference.md).  
  
-   O**Visualizador de Relatórios** (SPViewer.dwp) exibe um relatório e oferece uma barra de ferramentas que você pode usar para navegar pelas páginas, procurar por conteúdo ou exportar o relatório. Você pode adicionar a Web Part do Visualizador de Relatórios a uma página de Web Part para mostrar sempre um relatório específico naquela página ou **você pode conectá-lo ao Navegador de Relatórios** para exibir relatórios que são abertos através dessa Web Part.  
  
##  <a name="bkmk_requirements"></a> Requisitos para usar as Web Parts  
 Os requisitos para usar as Web Parts do Visualizador de Relatórios e do Navegador de Relatórios incluem o seguinte:  
  
-   As versões com suporte de produtos de SharePoint e tecnologias são:  
  
    -   [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 3.0 and [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007.  
  
    -   [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] e [!INCLUDE[SPS2010](../../includes/sps2010-md.md)].  
  
-   A versão de servidor de relatórios do modo Nativo deve ser [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou posterior.  
  
-   É necessário que o servidor de relatórios esteja sendo executado no modo nativo. Você **não** pode usar as Web Parts do Visualizador de Relatórios e do Navegador de Relatórios para se conectar a ou exibir relatórios em um servidor de relatório executado no modo do SharePoint.  
  
-   O Gerenciador de Relatórios deve estar instalado.  
  
 As Web Parts do Visualizador de Relatórios e do Navegador de Relatórios são distribuídas através de um arquivo de gabinete (.cab) que é incluído com o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Instruções para a instalação, configuração e uso de Web Parts são fornecidas nas seguintes seções deste tópico.  
  
##  <a name="bkmk_installingwebparts"></a> Instalando Web Parts  
 As Web Parts são entregues a um servidor do SharePoint como um arquivo de gabinete (.cab). Execute a ferramenta Stsadm.exe do SharePoint no arquivo .cab a partir da linha de comando para instalar Web Parts. Para saber mais sobre a ferramenta e a implantação de Web Parts, consulte sua documentação de SharePoint.  
  
#### <a name="install-web-parts-using-powershell"></a>Instalar as Web Parts usando o PowerShell  
  
1.  Copie o **RSWebParts.cab** em uma pasta no servidor SharePoint. Você pode copiar o mesmo em qualquer pasta do servidor SharePoint, e excluí-lo posteriormente após instalar Web Parts. Por padrão no SQL Server 2014 Reporting Services e anteriores, instala o arquivo RSWebParts.cab na pasta a seguir:  
  
    ```  
    C:\Program Files (x86)\Microsoft SQL Server\110\Tools\Reporting Services\SharePoint  
    ```  
  
2.  No computador que tem a instalação do produto do SharePoint, abra o **Shell de Gerenciamento do SharePoint 2010** com **privilégios administrativos**.  
  
3.  Execute o seguinte comando do PowerShell:  
  
    ```  
    Install-SPWebPartPack -LiteralPath "C:\Program Files (x86)\Microsoft SQL Server\110\Tools\Reporting Services\SharePoint\RSWebParts.cab" -GlobalInstall  
    ```  
  
4.  Você deve ver uma mensagem semelhante à seguinte, indicando que a Web Part foi implantada."  
  
    > Nome               Id da solução                                            Implantado  
  
    > ----                    ----------                                              -------\-  
  
    > rswebparts.cab    00000000-0000-0000-0000-000000000000     True  
  
     Para obter mais informações sobre como usar o PowerShell, consulte [Install-SPWebPartPack (http://technet.microsoft.com/library/ff607840.aspx)](http://technet.microsoft.com/library/ff607840.aspx).  
  
#### <a name="install-web-parts-using-stsadmexe"></a>Instale as Web Parts usando STSADM.exe  
  
1.  Copie o arquivo **RSWebParts.cab** para o mesmo local no servidor do SharePoint como descrito na seção do PowerShell deste documento.  
  
2.  No computador que tiver a instalação do produto ou tecnologia SharePoint, abra uma janela Prompt de Comando com privilégios administrativos e navegue para a pasta que contém a ferramenta **Stsadm.exe** . O caminho padrão para [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] é o seguinte:  
  
    > C:\Arquivos de Programas\Common Files\Microsoft Shared\Web Server Extensions\14\BIN.  
  
3.  Execute O Stsadm.exe no .cab, usando a seguinte sintaxe:  
  
    ```  
    STSADM.EXE -o addwppack -filename "C:\Program Files (x86)\Microsoft SQL Server\110\Tools\Reporting Services\SharePoint\RSWebParts.cab" -globalinstall  
    ```  
  
4.  Você deve ver uma mensagem de "Operação concluída com êxito".  
  
     A especificação de `-globalinstall` adiciona as Web Parts ao GAC (cache de assembly global). Esta etapa será necessária se você quiser conectar as Web Parts.  
  
##  <a name="bkmk_configurewebparts"></a> Adicionar e configurar Web Parts  
 Após ter instalado as Web Parts, você pode adicioná-las a uma ou mais página da Web em um site do SharePoint. Você deve ter permissão para criar sites da Web e adicionar o conteúdo.  
  
 O procedimento a seguir adicionará Web Parts a uma página e, em seguida, conectará o Navegador de Relatórios e o Visualizador de Relatórios para que, quando você clicar em um relatório no Navegador de Relatórios, ele será exibido dentro do Visualizador de Relatórios.  
  
#### <a name="add-report-viewer"></a>Adicionar Visualizador de Relatórios  
  
1.  Em Ações do Site, clique em **Editar Página**.  
  
2.  Em uma zona na página, clique em **Adicionar uma Web Part**.  
  
3.  Na caixa de diálogo **Adicionar Web Parts** , role até a categoria **Diversos** .  
  
4.  Selecione **Visualizador de Relatórios**.  
  
    > [!WARNING]  
    >  Não selecione **Visualizador de Relatórios do SQL Server Reporting Services** no qual a Web Part está registrada quando você instala o Suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para produtos do SharePoint, e é usado para executar um servidor de relatório em modo do SharePoint. Não pode ser usado para exibir relatórios em um servidor de relatório de modo nativo.  
  
5.  Clique em **Adicionar**.  
  
6.  Enquanto a página estiver em modo de edição, clique em **Editar Web Part** na Web Part do Visualizador de Relatórios.  
  
7.  Na **URL do Gerenciador de Relatórios**, digite uma URL para uma instância do Gerenciador de Relatórios associada ao servidor de relatório de modo nativo que deseja acessar. Por padrão, uma URL do Gerenciador de relatórios tem a seguinte sintaxe: **http://\<servername > / reports**.  
  
8.  Em **Caminho do Relatório**, especifique uma barra invertida, seguida pelo caminho da pasta e o nome do relatório. **Not** inclua o nome do servidor nem o diretório virtual do Gerenciador de Relatórios. Por exemplo, para abrir o relatório de Vendas de Empresa na pasta do Aventure Works, especifique **/Adventure Works/Vendas da Empresa**. Veja a seguir outro exemplo no qual o relatório 'Produtos' está na pasta raiz **/Produtos**no servidor de relatório.  
  
9. Clique em **OK**.  
  
#### <a name="add-report-explorer-and-connect-to-report-viewer"></a>Adicionar o Navegador de Relatórios e conectar ao Visualizador de Relatórios  
  
1.  Em outra zona da página, clique em **Adicionar uma Web Part** e, na pasta diversos, clique em **Navegador de Relatórios** e clique em **Adicionar**.  
  
2.  No menu de contexto de Web Part do Navegador de Relatórios, clique em **Editar Web Part**.  
  
3.  Na **URL do Gerenciador de Relatórios**, digite uma URL para uma instância do Gerenciador de Relatórios associada ao servidor de relatório de modo nativo que deseja acessar.  
  
4.  Opcionalmente, defina o **Caminho Inicial**. O caminho inicial é uma pasta na hierarquia de pastas do servidor de relatório. Você pode especificar um caminho inicial se deseja que a página padrão seja uma pasta bem-adiante na hierarquia das pastas. O caminho deve começar com uma barra invertida. Você deve especificar um caminho completo que se inicia com o nó raiz da hierarquia de pastas do servidor de relatórios, mas não inclui o nome do servidor nem o diretório virtual do Gerenciador de Relatórios. Por exemplo, para abrir uma pasta chamada Adventure Works logo abaixo do nó raiz, especifique **/Adventure Works** no Caminho Inicial.  
  
5.  Clique em **OK**.  
  
6.  O Navegador de Relatórios mostrará uma lista de itens de relatórios no servidor de relatório. Por padrão, se você clicar no nome de um relatório, abrirá o relatório em uma nova janela. Conclua as seguintes etapas se quiser conectar o Navegador de Relatórios ao Visualizador de Relatórios para que, quando você clicar em um nome de relatório no Navegador de Relatórios, ele seja exibido dentro do Visualizador de Relatórios.  
  
    1.  No menu de contexto do Navegador de Relatórios, clique em **Conexões**.  
  
    2.  Clique em **Mostrar relatório em**.  
  
    3.  Clique em **Visualizador de Relatórios**.  

Mais perguntas? [Tente fazer o fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
