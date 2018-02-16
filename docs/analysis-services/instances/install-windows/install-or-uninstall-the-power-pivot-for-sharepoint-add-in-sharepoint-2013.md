---
title: Instalar ou desinstalar o PowerPivot para suplemento do SharePoint (SharePoint 2013) | Microsoft Docs
ms.custom: 
ms.date: 03/20/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fe13ce8b-9369-4126-928a-9426f9119424
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7066ed9aafe287f5ed4a2bb5ed2981d27bd0e35f
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2018
---
# <a name="install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013"></a>Instalar ou Desinstalar o Power Pivot para o Suplemento SharePoint (SharePoint 2013)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] é uma coleção de componentes de servidor de aplicativos e serviços back-end que fornece acesso a dados do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] em um farm do [!INCLUDE[SPS2013](../../../includes/sps2013-md.md)] . O suplemento [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint (**spPowerpivot.msi**) é um pacote do instalador usado para instalar os componentes de servidor de aplicativos.  
  
-   O suplemento não é necessário para implantações do SharePoint 2010.  
  
-   O suplemento não é necessário em uma implantação de servidor único que inclui o SharePoint 2013 e o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no modo do SharePoint. Os componentes instalados pelo suplemento são incluídos quando você instala um servidor do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no modo do SharePoint. Para obter diagramas de implantações de exemplo com o suplemento, veja [Topologias de implantação para recursos de BI do SQL Server no SharePoint](http://msdn.microsoft.com/library/39f76bc7-94e6-4dbc-bfa5-d56f4430bb26)  
  
 **Observação:** este tópico descreve a instalação de arquivos de solução do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] e a ferramenta de configuração do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2013. Após a instalação, confira o tópico [Configurar o PowerPivot e implantar soluções &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md) para obter informações sobre a ferramenta de configuração e recursos adicionais.  
  
 Para obter informações sobre como baixar o **spPowerPivot.msi**, consulte [Microsoft® SQL Server® 2014 Power Pivot® para Microsoft SharePoint®](http://go.microsoft.com/fwlink/?LinkID=324854).  
  
##  <a name="bkmk_background"></a> Plano de fundo  
  
-   **Servidor de Aplicativos:** [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] no SharePoint 2013 inclui o uso de pastas de trabalho como uma fonte de dados, a atualização de dados agendada e o Painel de Gerenciamento do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] .  
  
     [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] é um pacote do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows Installer (**spPowerpivot.msi**) que implanta bibliotecas de cliente do Analysis Services e copia os arquivos de instalação do [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] para o computador. O instalador não implanta nem configura recursos do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] no SharePoint. Os seguintes componentes são instalados por padrão:  
  
    -   [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 2013. Esse componente inclui os scripts do PowerShell (arquivos .ps1), os pacotes de solução do SharePoint (.wsp) e a ferramenta de configuração do [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 2013 para implantar o [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] em um farm do SharePoint 2013.  
  
    -   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Provedor OLE DB para Analysis Services (MSOLAP).  
  
    -   Provedor de dados ADOMD.NET.  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   **Serviços de back-end:** se você usar o [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel para criar pastas de trabalho que contêm dados analíticos, será necessário ter Serviços do Excel configurados com um servidor BI que executa o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no modo SharePoint para acessar esses dados em um ambiente de servidor. Você pode executar a Instalação do SQL Server em um computador que tenha o SharePoint Server 2013 instalado, ou em um computador diferente que não tenha o SharePoint. O Analysis Services não tem nenhuma dependência no SharePoint.  
  
     Para obter mais informações sobre como instalar, desinstalar e configurar serviços de back-end, consulte o seguinte:  
  
    -   [Instale o Analysis Services no modo do Power Pivot.](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
    -   [Desinstalar o Power Pivot para SharePoint](../../../sql-server/install/uninstall-power-pivot-for-sharepoint.md)  
  
##  <a name="bkmk_where_to_install"></a> Onde instalar o spPowerPivot.msi?  
 Uma prática recomendada é instalar o **spPowerPivot.msi** em todos os servidores do farm do SharePoint para verificar a consistência da configuração, inclusive servidores de aplicativo e servidores Web front-end. O pacote de instalador inclui os provedores de dados do Analysis Services, bem como a ferramenta configuração do [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] . Ao instalar o **spPowerPivot.msi** , você pode personalizar a instalação excluindo componentes individuais.  
  
 **Provedores de dados:** várias tecnologias do SharePoint e do SQL Server usam os provedores de dados do Analysis Services que incluem Serviços do Excel, PerformancePoint Services e Power View. A instalação do **spPowerPivot.msi** em todos os servidores do SharePoint assegura que o conjunto completo de provedores de dados do Analysis Services e a conectividade do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] estejam consistentemente disponíveis no farm.  
  
> [!NOTE]  
>  Você deve instalar os provedores de dados do Analysis Services em um servidor do SharePoint 2013 que esteja usando o **spPowerPivot.msi**. Outros pacotes de instalador disponíveis no Feature Pack do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] não têm suporte porque esses pacotes não incluem o arquivos de suporte do SharePoint 2013 exigidos pelos provedores de dados nesse ambiente.  
  
 **Ferramenta de Configuração:** A ferramenta de configuração do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2013 é necessária somente em um dos servidores do SharePoint. No entanto, uma prática recomendada em farms de vários servidores é instalar a ferramenta de configuração em pelo menos dois servidores, para que você tem acesso à ferramenta de configuração caso um dos dois servidores esteja offline.  
  
##  <a name="bkmk_prereq"></a> Requisitos e pré-requisitos  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SharePoint Server 2013.  
  
-   O**spPowerPivot.msi** é de 64 bits somente, de acordo com os requisitos dos produtos e das tecnologias do SharePoint.  
  
-   Um servidor em [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] modo. Os Serviços do Excel usarão a instância do SQL Server Analysis Services como um servidor do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . O Analysis Services pode ser executado em um computador local ou remoto.  
  
-   **Permissões:** para instalar o [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)], o usuário atual precisará ser um administrador no computador e um grupo Administradores de Farm do SharePoint.  
  
-   Para obter mais informações sobre os requisitos e pré-requisitos do [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] , vá para [Requisitos de hardware e software para o servidor do Analysis Services no Modo do SharePoint](http://msdn.microsoft.com/library/fb86ca0a-518c-4c61-ae78-7680c57fae1f).  
  
##  <a name="bkmk_install"></a> Para instalar o Power Pivot para SharePoint  
 O pacote de instalador do **spPowerpivot.msi** dá suporte a uma interface gráfica do usuário e a um modo de linha de comando. Ambos os métodos de instalação requerem a execução do .msi com privilégios de administrador. Após a instalação, confira o tópico [Configurar o PowerPivot e implantar soluções &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md) para obter informações sobre a ferramenta de configuração e recursos adicionais.  
  
### <a name="user-interface-installation"></a>Instalação da interface do usuário  
 Para instalar o [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] com a interface gráfica do usuário, conclua as seguintes etapas:  
  
1.  Execute o **SpPowerPivot.msi**.  
  
2.  Clique em **Avançar** na página de boas-vindas.  
  
3.  Revise e aceite o contrato de licença, e clique em **Avançar**.  
  
4.  Na página **Seleção de Recursos** , todos os recursos são selecionados por padrão.  
  
5.  Clique em **Avançar**.  
  
6.  Clique em **Instalar** para concluir a instalação.  
  
### <a name="command-line-installation"></a>Instalação na linha de comando  
 Para uma instalação em linha de comando, abra um prompt de comando com permissões administrativas e execute o **spPowerPivot.msi**. Por exemplo:  
  
 `Msiexec.exe /i SpPowerPivot.msi`para obter informações sobre a ferramenta de configuração e recursos adicionais.  
  
 Para criar um log de instalação, use as opções de log MsiExec padrão. O exemplo a seguir cria o arquivo de log “Install_Log.txt” usando a opção de log detalhado “v”.  
  
```  
Msiexec.exe /i SpPowerPivot.msi /L v c:\test\Install_Log.txt  
```  
  
### <a name="quiet-command-line-installation-for-scripting"></a>Instalação silenciosa na linha de comando para scripts  
 Você pode usar a opção **/q** ou **/quiet** para uma instalação “silenciosa” que não exibirá caixas de diálogo nem avisos. A instalação silenciosa é útil quando você deseja gerar scripts da instalação do suplemento.  
  
> [!IMPORTANT]  
>  Se você usar a opção **/q** para uma instalação de linha de comando silenciosa, o contrato de licença de usuário final não será exibido. Independentemente do método de instalação, o uso deste software é controlado por um contrato de licença e você é responsável por respeitar o contrato de licença.  
  
 **Para executar uma instalação silenciosa:**  
  
1.  Abra um prompt de comando **com permissões de administrador**.  
  
2.  Execute o seguinte comando:  
  
    ```  
    Msiexec.exe /i spPowerPivot.msi /q  
    ```  
  
### <a name="command-line-installation-to-include-specific-components"></a>Instalação na linha de comando para incluir componentes específicos  
 A ferramenta de configuração do [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] não é necessária em todos os servidores do SharePoint. No entanto, é recomendável instalá-la pelo menos em dois servidores para que a ferramenta de configuração esteja disponível quando você precisar.  
  
 Quando você instala o spPowerPivot.msi, pode usar as opções de linha de comando para instalar itens específicos, como os provedores de dados, e não a ferramenta de configuração do [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] . A linha de comando a seguir é um exemplo de como instalar todos os componentes exceto a ferramenta de configuração:  
  
```  
Msiexec /i spPowerPivot.msi AGREETOLICENSE="yes" ADDLOCAL=” SQL_OLAPDM,SQL_ADOMD,SQL_AMO,SQLAS_SP_Common”  
```  
  
|Opção|Description|  
|------------|-----------------|  
|Analysis_Server_SP_addin|[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Configuração|  
|SQL_OLAPDM|MSOLAP|  
|SQL_ADOMD|Provedor ADOMD.net|  
|SQL_AMO|Provedor AMO|  
|SQLAS_SP_Common|Componentes comuns do Analysis Services para SharePoint 2013|  
  
##  <a name="bkmk_deploy_solution"></a> Implantar os Arquivos de Solução do SharePoint com a Ferramenta de Configuração do Power Pivot para SharePoint 2013  
 Três dos arquivos copiados no disco rígido pelo spPowerPivot.msi são arquivos de solução do SharePoint. O escopo de um arquivo de solução é o nível do aplicativo Web, enquanto o escopo do outros arquivos é o nível do farm. Os arquivos são os seguintes:  
  
-   `PowerPivotFarmSolution.wsp`  
  
-   `PowerPivotFarm14Solution.wsp`  
  
-   `PowerPivotWebApplicationSolution.wsp`  
  
 Os arquivos de solução do são copiados para a seguinte pasta:  
  
 `ssInstallPathTools\PowerPivotTools\SPAddinConfiguration\Resources`  
  
 Após a instalação do .msi, execute a Ferramenta de Configuração do [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] para configurar e implantar as soluções no farm do SharePoint.  
  
 **Para iniciar a ferramenta de configuração:**  
  
 Na tela inicial do Windows, digite “power” e nos resultados da pesquisa de Aplicativos, clique em **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para a Configuração do SharePoint 2013**. Observe que os resultados da pesquisa podem incluir dois links pois a instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instala ferramentas de configuração do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] separadas para o SharePoint 2010 e o SharePoint 2013. Verifique se você iniciou a ferramenta de Configuração do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2013.  
  
 ![duas ferramentas de configuração do Power Pivot](../../../analysis-services/instances/install-windows/media/as-powerpivot-configtools-bothicons.gif "two powerpivot configuratoin tools")  
  
 **Or**  
  
1.  Vá para **Iniciar**, **Todos os Programas**.  
  
2.  Clique em [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)].  
  
3.  Clique em **Ferramentas de Configuração**.  
  
4.  Clique em **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para a Configuração do SharePoint 2013**.  
  
 Para obter mais informações sobre a ferramenta de configuração, consulte [Power Pivot Configuration Tools](../../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
##  <a name="bkmk_remove_addin"></a> Desinstalar ou reparar o suplemento  
  
> [!CAUTION]  
>  Se você desinstalar o **spPowerPivot.msi** , os provedores de dados e a ferramenta de configuração serão desinstalados. A desinstalação dos provedores de dados fará com que o servidor não consiga conectar-se ao [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)].  
  
 Você pode desinstalar ou reparar o [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] usando um dos seguintes métodos:  
  
1.  **Painel de controle do Windows:** Escolha [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]**[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2013**. Clique em **Desinstalar** ou **Reparar**.  
  
2.  Execute o spPowerPivot.msi e selecione a opção **Remover** ou **Reparar** .  
  
 **Linha de Comando:** Para reparar ou desinstalar o [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2013 usando a linha de comando, abra um prompt de comando **com as permissões de administrador** e execute um dos seguintes comandos:  
  
-   Para reparar, execute o seguinte comando:  
  
    ```  
    msiexec.exe /f spPowerPivot.msi  
    ```  
  
 OU  
  
-   Para desinstalar, execute o seguinte comando:  
  
    ```  
    msiexec.exe /uninstall spPowerPivot.msi  
    ```  
  
  
