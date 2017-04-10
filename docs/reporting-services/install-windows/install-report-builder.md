---
title: "Instalar o Construtor de Relat&#243;rios | Microsoft Docs"
ms.custom: ""
ms.date: "09/22/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
ms.assetid: 6b2291bb-1d20-4d08-81cb-a16dd8e01faf
caps.latest.revision: 20
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 20
---
# Instalar o Construtor de Relat&#243;rios
  [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] é um aplicativo autônomo, instalado no computador por você ou por um administrador. Você pode instalá-lo do Centro de Download da Microsoft, de um servidor de relatório do [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] ou de um site do SharePoint integrado com [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 Um administrador normalmente instala e configura o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], concede permissão baixar o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] do portal da Web e gerencia pastas e permissões para relatórios, partes de relatório e conjuntos de dados compartilhados salvos no servidor de relatório. Para obter mais informações sobre a administração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], veja [Servidor de relatório do Reporting Services &#40;Modo Nativo&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md).  
  
## Instalar [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] de um portal da Web ou biblioteca do SharePoint 
  
 Você pode iniciar o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] de um portal da web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou de um site do SharePoint integrado com [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para obter informações, veja [Iniciar o Construtor de Relatórios](../../reporting-services/report-builder/start-report-builder.md).  
  
### Site do SharePoint integrado com [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]
  
 Em um site do SharePoint integrado com [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], se o menu **Novo Documento** não listar as opções **Relatório do Construtor de Relatórios**, **Modelo do Construtor de Relatórios**e **Fonte de Dados de Relatório**, seus tipos de conteúdo precisarão ser adicionados à biblioteca do SharePoint. Para obter mais informações, veja [Adicionar os tipos de conteúdo do Reporting Services à sua biblioteca do SharePoint](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md).  
 
## Instalar o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] com o System Center Configuration Manager 
  
 Um administrador também pode usar um software como o System Center Configuration Manager para enviar o programa por push para o computador. Para saber como usar software específico para instalar o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)], consulte a documentação do software. Para obter mais informações, visite o [site do System Center Configuration Manager](https://www.microsoft.com/en-us/cloud-platform/system-center-configuration-manager).  
  
> [!IMPORTANT]  
>  Os recursos de segurança do Windows Vista e do Windows 7 exigem permissões elevadas para executar operações de linha de comando e solicitarão permissão para executar a linha de comando. A instalação não é silenciosa. Para fazer a instalação silenciosa, é necessário executar a linha de comando como um administrador.  
  
## Requisitos do sistema
  
 Consulte a seção **Requisitos de Sistema** da [página de download do Construtor de Relatórios](http://go.microsoft.com/fwlink/?LinkID=734968) no Centro de Download da Microsoft.
  
##  <a name="download"></a> Para instalar o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] do site de download  
  
1.  Na [página do Construtor de Relatórios do Centro de Download da Microsoft](http://go.microsoft.com/fwlink/?LinkID=734968) , clique em **Download**.  
  
2.  Depois que o download de [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] for concluído, clique em  **Executar**.  
  
     Isso inicia o Assistente do SQL Server [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] .  
  
3.  Aceite os termos no contrato de licença e clique em **Avançar**.  
  
4.  Na página **Servidor de Destino Padrão** , se desejar, forneça a URL ao servidor de relatório de destino se for diferente do padrão. Clique em **Avançar**.  
  
    > [!NOTE]  
    >  Se você planeja trabalhar com o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] quando estiver conectado a um servidor de relatório, será conveniente fornecer a URL ao servidor nesse momento. Você também pode fazer isso da caixa de diálogo **Opções** em [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)].  
  
5.  Clique em **Instalar** para concluir a instalação do [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)].  
  
## Para instalar [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] de um compartilhamento  
  
1.  Contate o administrador para saber a localização do arquivo ReportBuilder3.msi que você executa para instalar o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] no computador local.  
  
2.  Navegue até o arquivo ReportBuilder3.msi, o Windows Installer Package (MSI) do [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] e clique nele.  
  
     Isso inicia o Assistente do SQL Server [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] .  
  
3.  Conclua o restante das etapas em [To install Report Builder from the download site](#download).  
  
## Para instalar o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] da linha de comando 

 Também é possível executar uma instalação de linha de comando do [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] e fornecer argumentos para personalizar a instalação. Além dos parâmetros intrínsecos ao MSI padrão, você pode usar os parâmetros personalizados fornecidos pelo [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] : RBINSTALLDIR e REPORTSERVERURL. RBINSTALLDIR especifica a pasta de instalação raiz para o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]. REPORTSERVERURL especifica o servidor de relatório padrão que o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] usa para salvar relatórios no servidor.  
  
 Se você quiser uma instalação completamente silenciosa, sem nenhuma interação com a interface do usuário, especifique a opção **/quiet**. Por padrão, o sinalizador de opção silenciosa suprime erros de instalação. Portanto, é recomendável incluir a opção **/l** que especifica o registro, quando você usar a opção silenciosa.   
  
1.  Na [página do Construtor de Relatórios do Centro de Download da Microsoft](http://go.microsoft.com/fwlink/?LinkID=734968), clique em **Download**.  
  
2.  Depois que o download de [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] for concluído, clique em  **Salvar**.  
  
3.  No menu **Iniciar** , clique em **Executar**.  
  
4.  Na caixa **Abrir** , digite **cmd.**  
  
5.  Na janela do prompt de comando, navegue até pasta em que você salvou ReportBuilder3.msi.  
  
6.  Digite um comando com o seguinte formato:  
  
     `msiexec/i ReportBuilder3.msi /option [value] [/option [value]]`  
  
     As duas opções específicas para instalar o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] são: RBINSTALLDIR e REPORTSERVERURL. Não é necessário incluir esses argumentos na linha de comando. O comando de linha de base é o seguinte:  
  
     `msiexec /i ReportBuilder3_x86.msi /quiet`  
  
7.  Para executar o comando, pressione ENTER.  
  
## Definir padrões de [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]  
  
-   Depois de instalar o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)], você pode definir algumas opções padrão. Clique em **Arquivo** > **Opções**.  
  
     Definir o site do SharePoint ou portal da Web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] padrão é o mais útil. Para obter mais informações, consulte [Set default options for Report Builder](../../reporting-services/report-builder/set-default-options-for-report-builder.md).  
  
-   Clique em **Construtor de Relatórios** .  
  
     Se você não conseguir ver o servidor de relatórios na lista de servidores existentes, feche a caixa de diálogo **Abrir Relatório** e clique em **Conectar** na parte inferior do [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] para conectar-se ao servidor.  
  
## Consulte também  
 [Iniciar o Construtor de Relatórios](../../reporting-services/report-builder/start-report-builder.md)   
 [Desinstalar o Construtor de Relatórios](../../reporting-services/install-windows/uninstall-report-builder.md)  
  
  