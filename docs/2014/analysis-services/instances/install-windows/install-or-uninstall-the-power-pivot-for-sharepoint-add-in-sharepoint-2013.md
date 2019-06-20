---
title: Instalar ou desinstalar o PowerPivot para suplemento SharePoint (SharePoint 2013) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: fe13ce8b-9369-4126-928a-9426f9119424
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b1fb1e718f8b2ab0257651ff47674d293a9e6a95
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66079881"
---
# <a name="install-or-uninstall-the-powerpivot-for-sharepoint-add-in-sharepoint-2013"></a>Instalar ou desinstalar o suplemento do PowerPivot para SharePoint (SharePoint 2013)
  [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] é uma coleção de componentes de servidor de aplicativos e serviços back-end que fornece acesso a dados do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] em um farm do [!INCLUDE[SPS2013](../../../includes/sps2013-md.md)] . O suplemento [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint (**spPowerpivot.msi**) é um pacote do instalador usado para instalar os componentes de servidor de aplicativos.  
  
-   O suplemento não é necessário para implantações do SharePoint 2010.  
  
-   O suplemento não é necessário em uma implantação de servidor único que inclui o SharePoint 2013 e o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no modo do SharePoint. Os componentes instalados pelo suplemento são incluídos quando você instala um servidor do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no modo do SharePoint. Para obter diagramas das implantações de exemplo com o suplemento, consulte [topologias de implantação para recursos de BI do SQL Server no SharePoint](../../../sql-server/install/deployment-topologies-for-sql-server-bi-features-in-sharepoint.md).  
  
 **Observação:** Este tópico descreve a instalação do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] arquivos de solução e [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para a ferramenta de configuração do SharePoint 2013. Após a instalação, consulte o tópico a seguir para obter informações sobre a ferramenta de configuração e recursos adicionais, [configurar o PowerPivot e implantar soluções &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md).  
  
 Para obter informações sobre como baixar o **spPowerPivot.msi**, consulte [Microsoft® SQL Server® 2014 PowerPivot® para Microsoft SharePoint®](https://go.microsoft.com/fwlink/?LinkID=324854).  
  
 **Neste tópico:**  
  
-   [Plano de fundo](#bkmk_background)  
  
-   [Onde instalar o spPowerPivot.msi?](#bkmk_where_to_install)  
  
-   [Requisitos e pré-requisitos](#bkmk_prereq)  
  
-   [Para instalar o PowerPivot para SharePoint](#bkmk_install)  
  
-   [Implantar os arquivos de solução do SharePoint com o PowerPivot para a ferramenta de configuração do SharePoint 2013](#bkmk_deploy_solution)  
  
-   [Desinstalar ou reparar o suplemento](#bkmk_remove_addin)  
  
##  <a name="bkmk_background"></a> Plano de fundo  
  
-   **Servidor de Aplicativos:** [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] no SharePoint 2013 inclui o uso de pastas de trabalho como uma fonte de dados, a atualização de dados agendada e o Painel de Gerenciamento do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] .  
  
     [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] é um pacote do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows Installer (**spPowerpivot.msi**) que implanta bibliotecas de cliente do Analysis Services e copia os arquivos de instalação do [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] para o computador. O instalador não implanta nem configura recursos do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] no SharePoint. Os seguintes componentes são instalados por padrão:  
  
    -   [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 2013. Esse componente inclui os scripts do PowerShell (arquivos .ps1), os pacotes de solução do SharePoint (.wsp) e a ferramenta de configuração do [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 2013 para implantar o [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] em um farm do SharePoint 2013.  
  
    -   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Provedor OLE DB para Analysis Services (MSOLAP).  
  
    -   Provedor de dados ADOMD.NET.  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   **Serviços de back-end:** Se você usar [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel para criar pastas de trabalho que contêm dados analíticos, você deve ter configurado com um servidor BI que executa os serviços do Excel [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no modo do SharePoint para acessar os dados em um ambiente de servidor. Você pode executar a Instalação do SQL Server em um computador que tenha o SharePoint Server 2013 instalado, ou em um computador diferente que não tenha o SharePoint. O Analysis Services não tem nenhuma dependência no SharePoint.  
  
     Para obter mais informações sobre como instalar, desinstalar e configurar serviços de back-end, consulte o seguinte:  
  
    -   [Instalação do PowerPivot para SharePoint 2013](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
    -   [Desinstalar o PowerPivot para SharePoint](../../../sql-server/install/uninstall-power-pivot-for-sharepoint.md)  
  
##  <a name="bkmk_where_to_install"></a> Onde instalar o spPowerPivot.msi?  
 Uma prática recomendada é instalar o **spPowerPivot.msi** em todos os servidores do farm do SharePoint para verificar a consistência da configuração, inclusive servidores de aplicativo e servidores Web front-end. O pacote de instalador inclui os provedores de dados do Analysis Services, bem como a ferramenta configuração do [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] . Ao instalar o **spPowerPivot.msi** , você pode personalizar a instalação excluindo componentes individuais.  
  
 **Provedores de dados:** Várias tecnologias do SharePoint e SQL Server usam provedores de dados do Analysis Services, incluindo os serviços do Excel, os Serviços PerformancePoint e Power View. A instalação do **spPowerPivot.msi** em todos os servidores do SharePoint assegura que o conjunto completo de provedores de dados do Analysis Services e a conectividade do PowerPivot estejam consistentemente disponíveis no farm.  
  
> [!NOTE]  
>  Você deve instalar os provedores de dados do Analysis Services em um servidor do SharePoint 2013 que esteja usando o **spPowerPivot.msi**. Outros pacotes de instalador disponíveis no Feature Pack do [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] não têm suporte porque esses pacotes não incluem o arquivos de suporte do SharePoint 2013 exigidos pelos provedores de dados nesse ambiente.  
  
 **Ferramenta de configuração:** O PowerPivot para SharePoint 2013 ferramenta de configuração é necessária somente em um dos servidores do SharePoint. No entanto, uma prática recomendada em farms de vários servidores é instalar a ferramenta de configuração em pelo menos dois servidores, para que você tem acesso à ferramenta de configuração caso um dos dois servidores esteja offline.  
  
##  <a name="bkmk_prereq"></a> Requisitos e pré-requisitos  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SharePoint Server 2013.  
  
-   O**spPowerPivot.msi** é de 64 bits somente, de acordo com os requisitos dos produtos e das tecnologias do SharePoint.  
  
-   Um servidor do [!INCLUDE[ssASCurrent](../../../includes/ssascurrent-md.md)] no modo do PowerPivot. Os Serviços do Excel usarão a instância do SQL Server Analysis Services como um servidor do PowerPivot. O Analysis Services pode ser executado em um computador local ou remoto.  
  
-   **Permissões:** Para instalar o [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)], o usuário atual deve ser um administrador no computador e um grupo de administradores de Farm do SharePoint.  
  
-   Para obter mais informações sobre [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] requisitos e pré-requisitos, vá para [requisitos de Hardware e Software para servidor do Analysis Services no modo do SharePoint &#40;SQL Server 2014&#41;](../../../sql-server/install/hardware-software-requirements-analysis-services-server-sharepoint-mode.md).  
  
##  <a name="bkmk_install"></a> Para instalar o PowerPivot para SharePoint  
 O pacote de instalador do **spPowerpivot.msi** dá suporte a uma interface gráfica do usuário e a um modo de linha de comando. Ambos os métodos de instalação requerem a execução do .msi com privilégios de administrador. Após a instalação, consulte o tópico a seguir para obter informações sobre a ferramenta de configuração e recursos adicionais, [configurar o PowerPivot e implantar soluções &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md).  
  
### <a name="user-interface-installation"></a>Instalação da interface do usuário  
 Para instalar o [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] com a interface gráfica do usuário, conclua as seguintes etapas:  
  
1.  Execute o **SpPowerPivot.msi**.  
  
2.  Clique em **Avançar** na página de boas-vindas.  
  
3.  Revise e aceite o contrato de licença, e clique em **Avançar**.  
  
4.  Na página **Seleção de Recursos** , todos os recursos são selecionados por padrão.  
  
5.  Clique em **Avançar**.  
  
6.  Clique em **Instalar** para concluir a instalação.  
  
### <a name="command-line-installation"></a>Instalação na linha de comando  
 Para uma instalação em linha de comando, abra um prompt de comando com permissões administrativas e execute o **spPowerPivot.msi**. Por exemplo:  
  
 `Msiexec.exe /i SpPowerPivot.msi`para obter informações sobre a ferramenta de configuração e recursos adicionais.  
  
 Para criar um log de instalação, use as opções de log MsiExec padrão. O exemplo a seguir cria o arquivo de log "Install_log" usando a opção de registro em log detalhado "v".  
  
```  
Msiexec.exe /i SpPowerPivot.msi /L v c:\test\Install_Log.txt  
```  
  
### <a name="quiet-command-line-installation-for-scripting"></a>Instalação silenciosa na linha de comando para scripts  
 Você pode usar a opção **/q** ou **/quiet** para uma instalação "silenciosa" que não exibirá caixas de diálogo nem avisos. A instalação silenciosa é útil quando você deseja gerar scripts da instalação do suplemento.  
  
> [!IMPORTANT]  
>  Se você usar a opção **/q** para uma instalação de linha de comando silenciosa, o contrato de licença de usuário final não será exibido. Independentemente do método de instalação, o uso deste software é controlado por um contrato de licença e você é responsável por respeitar o contrato de licença.  
  
 **Para executar uma instalação silenciosa:**  
  
1.  Abra um prompt de comando **com permissões de administrador**.  
  
2.  Execute o seguinte comando:  
  
    ```  
    Msiexec.exe /i spPowerPivot.msi /q  
    ```  
  
### <a name="command-line-installation-to-include-specific-components"></a>Instalação na linha de comando para incluir componentes específicos  
 A ferramenta de configuração do [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] não é necessária em todos os servidores do SharePoint. No entanto, é recomendável instalá-la pelo menos em dois servidores para que a ferramenta de configuração esteja disponível quando você precisar.  
  
 Quando você instala o spPowerPivot.msi, pode usar as opções de linha de comando para instalar itens específicos, como os provedores de dados, e não a ferramenta de configuração do [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] . A linha de comando a seguir é um exemplo de como instalar todos os componentes exceto a ferramenta de configuração:  
  
```  
Msiexec /i spPowerPivot.msi AGREETOLICENSE="yes" ADDLOCAL=" SQL_OLAPDM,SQL_ADOMD,SQL_AMO,SQLAS_SP_Common"  
```  
  
|Opção|Descrição|  
|------------|-----------------|  
|Analysis_Server_SP_addin|Configuração do PowerPivot|  
|SQL_OLAPDM|MSOLAP|  
|SQL_ADOMD|Provedor ADOMD.net|  
|SQL_AMO|Provedor AMO|  
|SQLAS_SP_Common|Componentes comuns do Analysis Services para SharePoint 2013|  
  
##  <a name="bkmk_deploy_solution"></a> Implantar os arquivos de solução do SharePoint com o PowerPivot para a ferramenta de configuração do SharePoint 2013  
 Três dos arquivos copiados no disco rígido pelo spPowerPivot.msi são arquivos de solução do SharePoint. O escopo de um arquivo de solução é o nível do aplicativo Web, enquanto o escopo do outros arquivos é o nível do farm. Os arquivos são os seguintes:  
  
-   `PowerPivotFarmSolution.wsp`  
  
-   `PowerPivotFarm14Solution.wsp`  
  
-   `PowerPivotWebApplicationSolution.wsp`  
  
 Os arquivos de solução do são copiados para a seguinte pasta:  
  
 `C:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools\SPAddinConfiguration\Resources`  
  
 Após a instalação do .msi, execute a Ferramenta de Configuração do [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] para configurar e implantar as soluções no farm do SharePoint.  
  
 **Para iniciar a ferramenta de configuração:**  
  
 No menu Iniciar do Windows do tela, digite "power" e nos resultados da pesquisa de aplicativos, clique em **PowerPivot para SharePoint 2013**. Observe que os resultados da pesquisa podem incluir dois links pois a instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instala ferramentas de configuração do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] separadas para o SharePoint 2010 e o SharePoint 2013. Verifique se você iniciou a ferramenta de Configuração do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2013.  
  
 ![duas ferramentas de configuração do powerpivot](../../../analysis-services/media/as-powerpivot-configtools-bothicons.gif "duas ferramentas de configuração do powerpivot")  
  
 **Or**  
  
1.  Vá para **Iniciar**, **Todos os Programas**.  
  
2.  Clique em **Microsoft SQL Server 2014**.  
  
3.  Clique em **Ferramentas de Configuração**.  
  
4.  Clique em **Configuração do PowerPivot para SharePoint 2013**.  
  
 Para obter mais informações sobre a ferramenta de configuração, consulte [PowerPivot Configuration Tools](../../power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
##  <a name="bkmk_remove_addin"></a> Desinstalar ou reparar o suplemento  
  
> [!CAUTION]  
>  Se você desinstalar o **spPowerPivot.msi** , os provedores de dados e a ferramenta de configuração serão desinstalados. A desinstalação dos provedores de dados fará com que o servidor não consiga se conectar ao PowerPivot.  
  
 Você pode desinstalar ou reparar o [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] usando um dos seguintes métodos:  
  
1.  **Painel de controle do Windows:** Selecione **Microsoft SQL Server 2012 PowerPivot para SharePoint 2013**. Clique em **Desinstalar** ou **Reparar**.  
  
2.  Execute o spPowerPivot.msi e selecione a opção **Remover** ou **Reparar** .  
  
 **Linha de comando:** Para reparar ou desinstalar o PowerPivot para SharePoint 2013 usando a linha de comando, abra um prompt de comando **com permissões de administrador** e execute um dos seguintes comandos:  
  
-   Para reparar, execute o seguinte comando:  
  
    ```  
    msiexec.exe /f spPowerPivot.msi  
    ```  
  
 OU  
  
-   Para desinstalar, execute o seguinte comando:  
  
    ```  
    msiexec.exe /uninstall spPowerPivot.msi  
    ```  
  
  
