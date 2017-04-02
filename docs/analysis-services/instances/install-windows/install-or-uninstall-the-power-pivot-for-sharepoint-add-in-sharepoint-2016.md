---
title: "Instalar ou desinstalar o suplemento do Power Pivot para SharePoint (SharePoint 2016) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 34dd07b8-d59d-49ce-bad0-74f40e4db0b8
caps.latest.revision: 12
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 12
---
# Instalar ou desinstalar o suplemento do Power Pivot para SharePoint (SharePoint 2016)
  [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] é uma coleção de componentes de servidor de aplicativos e serviços back-end que fornece acesso a dados do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] em um farm do [!INCLUDE[SPS2016](../../../includes/sps2016-md.md)]. O suplemento do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint (**spPowerpivot16.msi**) é um pacote de instalação usado para instalar os componentes do servidor de aplicativos.  
  
 **Observação:** este tópico descreve a instalação de arquivos de solução do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] e a ferramenta de configuração do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2016. Após a instalação, confira o tópico [Configurar o PowerPivot e implantar soluções &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md) para obter informações sobre a ferramenta de configuração e recursos adicionais.  
  
 Para obter informações sobre como baixar o **spPowerPivot16.msi**, consulte o [Microsoft® SQL Server® 2016 Power Pivot® para Microsoft SharePoint®](http://go.microsoft.com/fwlink/?LinkID=324854).  
  
 **Neste tópico:**  
  
-   [Plano de fundo](#bkmk_background)  
  
-   [Onde instalar o spPowerPivot16.msi?](#bkmk_where_to_install)  
  
-   [Requisitos e pré-requisitos](#bkmk_prereq)  
  
-   [Para instalar o Power Pivot para SharePoint](#bkmk_install)  
  
-   [Implantar os arquivos de solução do SharePoint com a ferramenta de configuração do Power Pivot para SharePoint 2016](#bkmk_deploy_solution)  
  
-   [Desinstalar ou reparar o suplemento](#bkmk_remove_addin)  
  
||  
|-|  
|**[!INCLUDE[applies](../../../includes/applies-md.md)]**  SharePoint 2016|  
  
##  <a name="bkmk_background"></a> Plano de fundo  
  
-   **Servidor de aplicativos:** [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] a funcionalidade no SharePoint 2016 inclui uso de pastas de trabalho como uma fonte de dados, atualização de dados agendada, e o Painel de gerenciamento do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] .  
  
     [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] é um pacote do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows Installer (**spPowerpivot16.msi**) que implanta bibliotecas de cliente do Analysis Services e copia os arquivos de instalação do [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] no computador. O instalador não implanta nem configura recursos do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] no SharePoint. Os seguintes componentes são instalados por padrão:  
  
    -   [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)]. Esse componente inclui scripts do PowerShell (arquivos .ps1), pacotes da solução SharePoint (.wsp), e a ferramenta de configuração do [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] para implantar o [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] em um farm do SharePoint 2016.  
  
    -   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Provedor OLE DB para Analysis Services (MSOLAP).  
  
    -   Provedor de dados ADOMD.NET.  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   **Serviços de back-end:** se você usar o [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel para criar pastas de trabalho que contêm dados analíticos, precisará dos Serviços do Excel configurados com um servidor BI que executa o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no modo [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para acessar esses dados em um ambiente de servidor. Você pode executar a Instalação do SQL Server em um computador que tenha o SharePoint Server 2016 instalado, ou em um computador diferente que não tenha software SharePoint. O Analysis Services não tem nenhuma dependência no SharePoint.  
  
     Para obter mais informações sobre como instalar, desinstalar e configurar serviços de back-end, consulte o seguinte:  
  
    -   [Instale o Analysis Services no modo do Power Pivot.](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
    -   [Desinstalar o Power Pivot para SharePoint](../../../sql-server/install/uninstall-power-pivot-for-sharepoint.md)  
  
##  <a name="bkmk_where_to_install"></a> Onde instalar o spPowerPivot16.msi?  
 Uma prática recomendada é instalar o **spPowerPivot16.msi** em todos os servidores de farm do SharePoint para verificar a consistência da configuração, inclusive servidores de aplicativo e servidores front-end da Web. O pacote de instalador inclui os provedores de dados do Analysis Services, bem como a ferramenta configuração do [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)]. Ao instalar o **spPowerPivot16.msi** , você pode personalizar a instalação excluindo componentes individuais.  
  
 **Provedores de dados:** várias tecnologias do SharePoint e do SQL Server usam os provedores de dados do Analysis Services que incluem Serviços PerformancePoint e Power View. A instalação do **spPowerPivot16.ms** em todos os servidores do SharePoint assegura que o conjunto completo de provedores de dados do Analysis Services e a conectividade do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] estejam consistentemente disponíveis no farm.  
  
> [!NOTE]  
>  Você deve instalar os provedores de dados do Analysis Services em um servidor do SharePoint 2016 que esteja usando o **spPowerPivot16.msi**. Outros pacotes de instalação disponíveis no Feature Pack do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] não têm suporte porque esses pacotes não incluem o arquivos de suporte do SharePoint 2016 exigidos pelos provedores de dados nesse ambiente.  
  
 **Ferramenta de configuração:** a ferramenta de configuração do [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] é necessária somente em um dos servidores do SharePoint. No entanto, uma prática recomendada em farms de vários servidores é instalar a ferramenta de configuração em pelo menos dois servidores, para que você tem acesso à ferramenta de configuração caso um dos dois servidores esteja offline.  
  
##  <a name="bkmk_prereq"></a> Requisitos e pré-requisitos  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SharePoint Server 2016.  
  
-   O **spPowerPivot16.msi** é de 64 bits somente, de acordo com os requisitos de produtos e tecnologias do SharePoint.  
  
-   Um servidor do [!INCLUDE[ssASCurrent](../../../includes/ssascurrent-md.md)] no modo [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . O Servidor do Office Online usará a instância do SQL Server Analysis Services como um servidor do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . O Analysis Services pode ser executado no servidor SharePoint local ou em um computador remoto. Ele não pode ser instalado no Servidor do Office Online.  
  
-   **Permissões:** para instalar o [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)], é necessário que o usuário atual seja um administrador no computador e no grupo de administradores de farm do SharePoint.  
  
-   Para obter mais informações sobre os requisitos e pré-requisitos do [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)], vá para [Requisitos de hardware e software para o servidor do Analysis Services no Modo do SharePoint](../Topic/Hardware%20and%20Software%20Requirements%20for%20Analysis%20Services%20Server%20in%20SharePoint%20Mode.md).  
  
##  <a name="bkmk_install"></a> Para instalar o Power Pivot para SharePoint  
 O pacote de instalação do **spPowerpivot16.msi** dá suporte a uma interface gráfica do usuário e a um modo de linha de comando. Ambos os métodos de instalação requerem a execução do .msi com privilégios de administrador. Após a instalação, confira o tópico [Configurar o PowerPivot e implantar soluções &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md) para obter informações sobre a ferramenta de configuração e recursos adicionais.  
  
### Instalação da interface do usuário  
 Para instalar o [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] com a interface gráfica do usuário, conclua as seguintes etapas:  
  
1.  Execute o **spPowerPivot16.msi**.  
  
2.  Selecione **Avançar** na página de boas-vindas.  
  
3.  Revise e aceite o contrato de licença, e selecione **Avançar**.  
  
4.  Na página **Seleção de Recursos** , todos os recursos são selecionados por padrão.  
  
5.  Selecione **Avançar**.  
  
6.  Selecione **Instalar** para concluir a instalação.  
  
### Instalação na linha de comando  
 Para uma instalação em linha de comando, abra um prompt de comando com permissões administrativas e execute o **spPowerPivot16.msi**. Por exemplo:  
  
 `Msiexec.exe /i spPowerPivot16.msi`.  
  
 Para criar um log de instalação, use as opções de log MsiExec padrão. O exemplo a seguir cria o arquivo de log “Install_Log.txt” usando a opção de log detalhado “v”.  
  
```  
Msiexec.exe /i spPowerPivot16.msi /L v c:\test\Install_Log.txt  
```  
  
### Instalação silenciosa na linha de comando para scripts  
 Você pode usar a opção **/q** ou **/quiet** para uma instalação “silenciosa” que não exibirá caixas de diálogo nem avisos. A instalação silenciosa é útil quando você deseja gerar scripts da instalação do suplemento.  
  
> [!IMPORTANT]  
>  Se você usar a opção **/q** para uma instalação de linha de comando silenciosa, o contrato de licença de usuário final não será exibido. Independentemente do método de instalação, o uso deste software é controlado por um contrato de licença e você é responsável por respeitar o contrato de licença.  
  
 **Para executar uma instalação silenciosa:**  
  
1.  Abra um prompt de comando **com permissões de administrador**.  
  
2.  Execute o seguinte comando:  
  
    ```  
    Msiexec.exe /i spPowerPivot16.msi /q  
    ```  
  
### Instalação na linha de comando para incluir componentes específicos  
 A ferramenta de configuração do [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] não é necessária em todos os servidores do SharePoint. No entanto, é recomendável instalá-la pelo menos em dois servidores para que a ferramenta de configuração esteja disponível quando você precisar.  
  
 Quando você instala o spPowerPivot16.msi, pode usar as opções de linha de comando para instalar itens específicos, como os provedores de dados, e não a ferramenta de configuração do [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] . A linha de comando a seguir é um exemplo de como instalar todos os componentes exceto a ferramenta de configuração:  
  
```  
Msiexec /i spPowerPivot16.msi AGREETOLICENSE="yes" ADDLOCAL=” SQL_OLAPDM,SQL_ADOMD,SQL_AMO,SQLAS_SP_Common”  
```  
  
|Opção|Descrição|  
|------------|-----------------|  
|Analysis_Server_SP_addin16|[!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] Configuração|  
|SQL_OLAPDM|Provedor OLE DB do Analysis Services para SQL Server 2016|  
|SQL_ADOMD|Provedor ADOMD.NET|  
|SQL_AMO|Provedor de AMO (Objetos de Gerenciamento de Análise) do SQL Server 2016.|  
|SQLAS_SP16_Common|Componentes comuns do Analysis Services para SharePoint 2016|  
  
##  <a name="bkmk_deploy_solution"></a> Implantar os arquivos de solução do SharePoint com a ferramenta de configuração do Power Pivot para SharePoint 2016  
 Três dos arquivos copiados no disco rígido pelo spPowerPivot16.msi são arquivos da solução SharePoint. O escopo de um arquivo de solução é o nível do aplicativo Web, enquanto o escopo do outros arquivos é o nível do farm. Os arquivos são os seguintes:  
  
-   `PowerPivot16FarmSolution.wsp`  
  
-   `PowerPivot16Farm14Solution.wsp`  
  
-   `PowerPivot16WebApplicationSolution.wsp`  
  
 Os arquivos de solução do são copiados para a seguinte pasta:  
  
 `ssInstallPathTools\PowerPivotTools\SPAddinConfiguration\Resources`  
  
 Após a instalação do .msi, execute a Ferramenta de Configuração do [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] para configurar e implantar as soluções no farm do SharePoint.  
  
 **Para iniciar a ferramenta de configuração:**  
  
 Na tela inicial do Windows, digite “Ligar/Desligar ” e nos resultados da pesquisa de aplicativos selecione **[!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] Configuração**. Observe que os resultados da pesquisa podem incluir dois links pois a instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instala ferramentas de configuração do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] separadas para o SharePoint 2013 e o SharePoint 2016. Certifique-se de iniciar a ferramenta de configuração [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] .  
  
 ![PowerPivot for SharePoint 2016 Configuration](../../../analysis-services/instances/install-windows/media/powerpivot-for-sharepoint-2016-configuration.png "PowerPivot for SharePoint 2016 Configuration")  
  
 **ou**  
  
1.  Vá para **Iniciar**, **Todos os Programas**.  
  
2.  Selecione [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)].  
  
3.  Selecione **Ferramentas de Configuração**.  
  
4.  Selecione **[!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] Configuração**.  
  
 Para obter mais informações sobre a ferramenta de configuração, consulte [Power Pivot Configuration Tools](../../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
##  <a name="bkmk_remove_addin"></a> Desinstalar ou reparar o suplemento  
  
> [!CAUTION]  
>  Se você desinstalar o **spPowerPivot16.msi** , os provedores de dados e a ferramenta de configuração serão desinstalados. A desinstalação dos provedores de dados fará com que o servidor não consiga se conectar ao [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)].  
  
 Você pode desinstalar ou reparar o [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] usando um dos seguintes métodos:  
  
1.  **Painel de controle do Windows:** selecione [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]**[!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)]**. Selecione **Desinstalar** ou **Reparar**.  
  
2.  Execute o spPowerPivot16.msi e selecione a opção **Remover** ou **Reparar** .  
  
 **Linha de Comando:** para reparar ou desinstalar o [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] usando a linha de comando, abra um prompt de comando **com permissões de administrador** e execute um dos seguintes comandos:  
  
-   Para reparar, execute o seguinte comando:  
  
    ```  
    msiexec.exe /f spPowerPivot16.msi  
    ```  
  
 OU  
  
-   Para desinstalar, execute o seguinte comando:  
  
    ```  
    msiexec.exe /uninstall spPowerPivot16.msi  
    ```  
  
  