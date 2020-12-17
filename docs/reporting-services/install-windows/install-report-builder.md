---
title: Instalar o Construtor de Relatórios | Microsoft Docs
description: O Construtor de Relatórios é um aplicativo autônomo, instalado no computador por você ou por um administrador.
ms.date: 01/31/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
ms.assetid: 6b2291bb-1d20-4d08-81cb-a16dd8e01faf
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ca0071416491700254047b43056d32fc64ed1d9d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97425119"
---
# <a name="install-report-builder"></a>Instalar o Construtor de Relatórios

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] é um aplicativo autônomo, instalado no computador por você ou por um administrador. Você pode instalá-lo do Centro de Download da Microsoft, de um servidor de relatório do [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] ou de um site do SharePoint integrado com [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  

> [!NOTE]
> Você está procurando por informações de instalação do Power BI Report Builder em vez disso? Acesse a página [Microsoft Power BI Report Builder](https://www.microsoft.com/download/details.aspx?id=58158) no Centro de Download. 

 Um administrador normalmente instala e configura o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], concede permissão para baixar o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] do portal da Web e gerencia pastas e permissões para relatórios, partes de relatório e conjuntos de dados compartilhados salvos no servidor de relatório. Para obter mais informações sobre a administração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], consulte [Servidor de relatório do Reporting Services &#40;modo nativo&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md).  
  
## <a name="install-ssrbnoversion-from--a--web-portal-or-sharepoint-library"></a>Instalar [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] de um portal da Web ou biblioteca do SharePoint 

> [!NOTE]
> A integração do Reporting Services ao SharePoint não está mais disponível após o SQL Server 2016.
  
 Você pode iniciar o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] de um portal da Web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou de um site do SharePoint integrado com [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para obter informações, veja [Iniciar o Construtor de Relatórios](../../reporting-services/report-builder/start-report-builder.md).  

::: moniker range="=sql-server-2016"
  
### <a name="sharepoint-site-integrated-with-ssrsnoversion"></a>Site do SharePoint integrado com [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]
  
 Em um site do SharePoint integrado com [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], se o menu **Novo Documento** não listar as opções **Relatório do Construtor de Relatórios**, **Modelo do Construtor de Relatórios** e **Fonte de Dados de Relatório**, seus tipos de conteúdo precisarão ser adicionados à biblioteca do SharePoint. Para obter mais informações, veja [Adicionar os tipos de conteúdo do Reporting Services à sua biblioteca do SharePoint](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md).  

::: moniker-end
 
## <a name="install-ssrbnoversion-with-microsoft-endpoint-configuration-manager"></a>Instalar o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] com o Microsoft Endpoint Configuration Manager 
  
 Um administrador também pode usar um software como o Microsoft Endpoint Configuration Manager para enviar o programa por push para o computador. Para saber como usar software específico para instalar o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)], consulte a documentação do software. Para obter mais informações, confira a [documentação do Microsoft Endpoint Configuration Manager](/configmgr/).  
  
> [!IMPORTANT]  
>  Os recursos de segurança do Windows Vista e do Windows 7 exigem permissões elevadas para executar operações de linha de comando e solicitarão permissão para executar a linha de comando. A instalação não é silenciosa. Para fazer a instalação silenciosa, é necessário executar a linha de comando como um administrador.  
  
## <a name="system-requirements"></a>Requisitos do Sistema
  
 Consulte a seção **Requisitos de Sistema** da [página de download do Construtor de Relatórios](https://go.microsoft.com/fwlink/?LinkID=734968) no Centro de Download da Microsoft.
  
##  <a name="to-install-ssrbnoversion-from-the-download-site"></a><a name="download"></a> Para instalar o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] do site de download  
  
1.  Na [página do Construtor de Relatórios do Centro de Download da Microsoft](https://go.microsoft.com/fwlink/?LinkID=734968) , clique em **Download**.  
  
2.  Depois que o download de [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] for concluído, clique em **Executar**.  
  
     Isso inicia o Assistente do SQL Server [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)].  
  
3.  Aceite os termos no contrato de licença e clique em **Avançar**.  
  
4.  Na página **Servidor de Destino Padrão** , se desejar, forneça a URL ao servidor de relatório de destino se for diferente do padrão. Clique em **Próximo**.  
  
    > [!NOTE]  
    >  Se você planeja trabalhar com o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] quando ele está conectado a um servidor de relatório, é conveniente fornecer a URL ao servidor nesse momento. Você também pode fazer isso da caixa de diálogo **Opções** em [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)].  
  
5.  Clique em **Instalar** para concluir a instalação do [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)].  
  
## <a name="to-install-ssrbnoversion-from-a-share"></a>Para instalar o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] de um compartilhamento  
  
1.  Contate o administrador para saber a localização do arquivo ReportBuilder.msi que você executa para instalar o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] no computador local.  
  
2.  Localize o arquivo ReportBuilder.msi, o pacote do Windows Installer (MSI) do [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] e clique nele.  
  
     Isso inicia o Assistente do SQL Server [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)].  
  
3.  Conclua o restante das etapas em [Para instalar o Construtor de Relatórios no site de download](#download).  
  
## <a name="to-install-ssrbnoversion-from-the-command-line"></a>Para instalar o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] da linha de comando 

 Também é possível executar uma instalação de linha de comando do [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] e fornecer argumentos para personalizar a instalação. Além dos parâmetros intrínsecos ao MSI padrão, você poderá usar os parâmetros personalizados fornecidos pelo [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]: RBINSTALLDIR e RBSERVERURL. RBINSTALLDIR especifica a pasta de instalação raiz para o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]. RBSERVERURL especifica o servidor de relatório padrão que o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] usa para salvar relatórios no servidor.  
  
 Se você quiser uma instalação completamente silenciosa, sem nenhuma interação com a interface do usuário, especifique a opção **/quiet** . Por padrão, o sinalizador de opção silenciosa suprime erros de instalação. Portanto, é recomendável incluir a opção **/l** que especifica o registro, quando você usar a opção silenciosa.   
  
1.  Na [página do Construtor de Relatórios do Centro de Download da Microsoft](https://go.microsoft.com/fwlink/?LinkID=734968), clique em **Download**.  
  
2.  Depois que o download de [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] for concluído, clique em **Salvar**.  
  
3.  No menu **Iniciar** , clique em **Executar**.  
  
4.  Na caixa **Abrir** , digite **cmd.**  
  
5.  Na janela do prompt de comando, navegue até pasta em que você salvou ReportBuilder.msi.  
  
6.  Digite um comando com o seguinte formato:  
  
     `msiexec/i ReportBuilder.msi OPTION=OptionValue [OPTION=OptionValue]`  
  
     As duas opções específicas para a instalação [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] são: RBINSTALLDIR e RBSERVERURL. Não é necessário incluir esses argumentos na linha de comando. O comando de linha de base é o seguinte:  
  
     `msiexec /i ReportBuilder3_x86.msi /quiet`  
  
7.  Para executar o comando, pressione ENTER.  
  
## <a name="set-ssrbnoversion-defaults"></a>Definir padrões de [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]  
  
-   Depois de instalar o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)], você pode definir algumas opções padrão. Clique em **Arquivo** > **Opções**.  
  
     Definir o site do SharePoint ou portal da Web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] padrão é o mais útil. Para obter mais informações, consulte [Set default options for Report Builder](../../reporting-services/report-builder/set-default-options-for-report-builder.md).  
  
-   Clique em **Construtor de Relatórios** .  
  
     Se você não conseguir ver o servidor de relatórios na lista de servidores existentes, feche a caixa de diálogo **Abrir Relatório** e clique em **Conectar** na parte inferior do [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] para conectar-se ao servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar o Construtor de Relatórios](../../reporting-services/report-builder/start-report-builder.md)   
 [Desinstalar o Construtor de Relatórios](../../reporting-services/install-windows/uninstall-report-builder.md)  
  
