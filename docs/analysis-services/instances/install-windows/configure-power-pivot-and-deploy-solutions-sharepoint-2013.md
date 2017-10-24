---
title: "Configurar o PowerPivot e implantar soluções (SharePoint 2013) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- power-view
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6401fd92-f43b-450e-8298-12db644c25bc
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 901098e2a656d178932b9b706b70d559bef4f215
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="configure-power-pivot-and-deploy-solutions-sharepoint-2013"></a>Configurar o PowerPivot e implantar soluções (SharePoint 2013)
  Estes tópicos descrevem a implantação e a configuração de aprimoramentos de camada intermediária aos recursos do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] no [!INCLUDE[SPS2013](../../../includes/sps2013-md.md)] , incluindo a Galeria [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] , a atualização de dados agendada, o Painel de Gerenciamento e os provedores de dados. Execute **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para configuração do SharePoint 2013** para concluir o seguinte:  
  
-   Implantar os arquivos de solução do SharePoint.  
  
-   Criar um aplicativo de serviço [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] .  
  
-   Configurar um Aplicativo dos Serviços do Excel para usar um servidor do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no modo do SharePoint. Para obter informações sobre serviços de back-end e sobre como instalar um [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Server no modo do SharePoint, veja [Instalar o Analysis Services no modo do Power Pivot](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md).  
  
 Para obter informações sobre como instalar a ferramenta de Configuração do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2013, consulte [Instalar ou desinstalar o suplemento do Power Pivot para SharePoint &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)  
  
 Este tópico contém as seguintes seções:  
  
 [Executar a configuração do Power Pivot para SharePoint 2013](#bkmk_run_configuration_tool)  
  
 [Verificar a configuração do Power Pivot](#bkmk_verify_powerpivot)  
  
 [Solucionar problemas](#bkmk_troubleshoot_issues)  
  
||  
|-|  
|**[!INCLUDE[applies](../../../includes/applies-md.md)]**  SharePoint 2013|  
  
##  <a name="bkmk_run_configuration_tool"></a> Executar a configuração do Power Pivot para SharePoint 2013  
 **Observação:** o assistente para instalação do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] instala duas ferramentas de configuração diferentes para [!INCLUDE[ssGeminiLong](../../../includes/ssgeminilong-md.md)]. Cada um deles oferece suporte a uma versão diferente do SharePoint.  
  
|Nome|Descrição|  
|----------|-----------------|  
|[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para configuração do SharePoint 2013|SharePoint 2013|  
|[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Ferramenta de Configuração|SharePoint 2010 com SharePoint 2010 Service Pack 1 (SP1)|  
  
 **Observação:** para concluir as etapas a seguir, você deve ser um administrador de farm. Se uma mensagem de erro semelhante à seguinte for exibida:  
  
-   “O usuário não é um administrador de farm. Corrija as falhas de validação e tente novamente.”  
  
 Faça logon como a conta que instalou o SharePoint ou configure a conta de instalação como administrador primário do site da Administração Central do SharePoint.  
  
1.  No menu **Iniciar** , clique em **Todos os Programas**em [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)], em **Ferramentas de Configuração**e clique em **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Configuração do SharePoint 2013**. As ferramentas só serão listadas quando o [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint estiver instalada no servidor local.  
  
2.  Clique em **Configurar ou Reparar o [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint** e clique em **OK**.  
  
3.  A ferramenta executa uma validação para verificar o estado atual do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] e quais etapas são necessárias para concluir a configuração. Expanda a janela para o tamanho total. Você verá uma barra de botões na parte inferior da janela que inclui os comandos **Validar**, **Executar**e **Sair** .  
  
4.  Na guia **Parâmetros** :  
  
    1.  **Nome de Usuário da Conta Padrão**: insira uma conta de usuário de domínio para a conta padrão. Essa conta será usada para provisionar serviços, inclusive o pool de aplicativos do serviço [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . Não especifique uma conta interna, como Serviço de Rede ou Sistema Local. A ferramenta bloqueia configurações que especificam contas internas.  
  
    2.  **Servidor de Banco de Dados**: você pode usar qualquer mecanismo de Banco de Dados do SQL Server com suporte para farm do SharePoint.  
  
    3.  **Frase Secreta**: insira um frase secreta. Se você estiver criando um novo farm do SharePoint, a frase secreta será usada sempre que você adicionar um servidor ou aplicativo ao farm do SharePoint. Se o farm já existir, insira a frase secreta que permite adicionar um aplicativo de servidor ao farm.  
  
    4.  **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Servidor para Serviços do Excel**: digite o nome de um servidor de modo do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] SharePoint. Em uma implantação de servidor único, ele será o servidor de banco de dados. `[ServerName]\powerpivot`  
  
    5.  Clique em **Criar Coleção de Sites** na janela esquerda. Observe a **URL do Site** para poder referenciá-la em etapas posteriores. Se o servidor do SharePoint ainda não estiver configurado, o assistente de configuração usa como padrão o aplicativo Web e as URLs da coleção de sites da raiz de `http://[ServerName]`. Para alterar os padrões, analise as seguintes páginas na janela esquerda: **Criar Aplicativo Web Padrão** e **Implantar Solução de Aplicativo Web**  
  
5.  Opcionalmente, revise os valores de entrada restantes usados para concluir cada ação. Clique em cada ação na janela esquerda para exibir e revisar os detalhes da ação. Para obter mais informações sobre cada um, consulte a seção “Valores de entrada usados para configurar o servidor” em [Configurar ou reparar o PowerPivot para SharePoint 2010 (Ferramenta de Configuração do Power Pivot)](http://msdn.microsoft.com/en-us/d61f49c5-efaa-4455-98f2-8c293fa50046) neste tópico.  
  
6.  Opcionalmente, remova as ações que você não deseja processar neste momento. Por exemplo, se desejar configurar o Serviço de Repositório Seguro, clique em **Configurar Serviço de Repositório Seguro**e desmarque a caixa de seleção **Inclua esta ação na lista de tarefas**.  
  
7.  Clique em **Validar** para verificar se a ferramenta tem informações suficientes para processar as ações na lista. Se você encontrar erros de validação, clique nos avisos no painel esquerdo para ver os detalhes do erro de validação. Corrija os erros de validação e clique em **Validar** novamente.  
  
8.  Clique em **Executar** para processar todas as ações na lista de tarefas. Observe que **Executar** fica disponível depois que você valida as ações. Se **Executar** não estiver habilitado, clique em **Validar** primeiro.  
  
 Para obter mais informações, consulte [Configurar ou reparar o PowerPivot para SharePoint 2010 (Ferramenta de Configuração do Power Pivot)](http://msdn.microsoft.com/en-us/d61f49c5-efaa-4455-98f2-8c293fa50046)  
  
##  <a name="bkmk_verify_powerpivot"></a> Verificar a configuração do Power Pivot  
 **Serviços:**  
  
1.  Na Administração Central, em Configurações do Sistema, clique em **Gerenciar serviços no servidor**.  
  
2.  Verifique se o **SQL Server Analysis Services** e o **Serviço de Sistema do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] SQL Server** foram iniciados.  
  
 **Recurso do farm:**  
  
1.  Na Administração Central, em Configurações do Sistema, clique em **Gerenciar recursos de farm**.  
  
2.  Verifique se **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Recurso de Integração** está **Ativo**.  
  
 **Recurso da coleção de sites:**  
  
1.  Navegue até a URL do site que foi criada pela ferramenta de configuração.  
  
     Clique em **configurações**![configurações SharePoint](../../../analysis-services/media/as-sharepoint2013-settings-gear.gif "configurações SharePoint")e, em seguida, clique em **configurações do Site**.  
  
     Clique em **Recursos do Conjunto de Sites**.  
  
2.  Verifique se a **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Integração de Recursos para Coleções de Sites** está **Ativa**.  
  
 **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] :**  
  
1.  Na Administração Central, no **Gerenciamento de Aplicativo**, clique em **Gerenciar aplicativos de serviço**.  
  
2.  Verifique se o status do aplicativo de serviço é **iniciado**. O nome padrão é **Aplicativo de Serviço [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Padrão**.  
  
     Clique no nome do aplicativo de serviços para abrir o Painel de Gerenciamento do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para o aplicativo de serviço aberto. No primeiro uso, o painel demora alguns minutos para carregar.  
  
 Para saber mais, confira [Verify a Power Pivot for SharePoint Installation](../../../analysis-services/instances/install-windows/verify-a-power-pivot-for-sharepoint-installation.md).  
  
##  <a name="bkmk_troubleshoot_issues"></a> Solucionar problemas  
 Para ajudar a solucionar problemas, é uma boa ideia verificar se o log de diagnóstico está habilitado.  
  
1.  Na Administração Central do SharePoint, clique em **Monitoramento** e clique em **Configurar coleta de dados de integridade e uso**.  
  
2.  Verifique se **Habilitar coleta de dados de uso** está selecionado.  
  
3.  Verifique se os eventos a seguir estão selecionados:  
  
    -   Definição de campos de uso da telemetria Educação  
  
    -   [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Conexões  
  
    -   [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Uso de Dados de Carregamento  
  
    -   [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Uso de Consulta  
  
    -   [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Uso de Dados de Descarregamento  
  
4.  Verifique se **Habilitar coleta de dados de integridade** está selecionado.  
  
5.  Clique em **OK**.  
  
 Para obter mais informações sobre como solucionar problemas de atualização de dados, consulte [Solução de problemas de atualização de dados do PowerPivot](http://social.technet.microsoft.com/wiki/contents/articles/3870.troubleshooting-powerpivot-data-refresh.aspx) (http://social.technet.microsoft.com/wiki/contents/articles/3870.troubleshooting-powerpivot-data-refresh.aspx).  
  
 Para obter mais informações sobre a ferramenta de configuração, consulte [Power Pivot Configuration Tools](../../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
  

