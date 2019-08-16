---
title: Configurar o PowerPivot e implantar soluções (SharePoint 2013) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 6401fd92-f43b-450e-8298-12db644c25bc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6d835269f77e563b94c89c3a68c5c82844edc773
ms.sourcegitcommit: f5807ced6df55dfa78ccf402217551a7a3b44764
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69493976"
---
# <a name="configure-powerpivot-and-deploy-solutions-sharepoint-2013"></a>Configurar o PowerPivot e implantar soluções (SharePoint 2013)
  Estes tópicos descrevem a implantação e a configuração de aprimoramentos de camada intermediária aos recursos do PowerPivot no [!INCLUDE[SPS2013](../../../includes/sps2013-md.md)], incluindo a Galeria PowerPivot, a atualização de dados agendada, o Painel de Gerenciamento e os provedores de dados. Execute a ferramenta de **Configuração do PowerPivot para SharePoint 2013** para concluir o seguinte:  
  
-   Implantar os arquivos de solução do SharePoint.  
  
-   Criar um aplicativo de serviço PowerPivot.  
  
-   Configurar um Aplicativo dos Serviços do Excel para usar um servidor do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no modo do SharePoint. Para obter informações sobre os serviços de back [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -end e instalar um servidor no modo do SharePoint, consulte [instalação do PowerPivot para SharePoint 2013](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode).  
  
 Para obter informações sobre como instalar a ferramenta de configuração do PowerPivot para SharePoint 2013, consulte [instalar ou desinstalar o &#40;suplemento PowerPivot para SharePoint&#41; SharePoint 2013](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013)  
  
 Esse tópico contém as seguintes seções:  
  
 [Executar configuração do PowerPivot para SharePoint 2013](#bkmk_run_configuration_tool)  
  
 [Verificar a configuração do PowerPivot](#bkmk_verify_powerpivot)  
  
 [Solucionar problemas](#bkmk_troubleshoot_issues)  
  
##  <a name="bkmk_run_configuration_tool"></a>Executar configuração do PowerPivot para SharePoint 2013  
 **Observação:** O [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] assistente de instalação instala duas ferramentas de configuração [!INCLUDE[ssGeminiLong](../../../includes/ssgeminilong-md.md)]diferentes para o. Cada um deles oferece suporte a uma versão diferente do SharePoint.  
  
|Nome|Descrição|  
|----------|-----------------|  
|Configuração do PowerPivot para SharePoint 2013|SharePoint 2013|  
|Ferramenta de Configuração do PowerPivot|SharePoint 2010 com SharePoint 2010 Service Pack 1 (SP1)|  
  
 **Observação:** Para concluir as etapas a seguir, você deve ser um administrador do farm. Se uma mensagem de erro semelhante à seguinte for exibida:  
  
-   "O usuário não é um administrador de farm. Corrija as falhas de validação e tente novamente."  
  
 Faça logon como a conta que instalou o SharePoint ou configure a conta de instalação como administrador primário do site da Administração Central do SharePoint.  
  
1.  No menu **Iniciar** , clique em **Todos os Programas**, em [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)], em **Ferramentas de Configuração**e em **Configuração do PowerPivot para SharePoint 2013**. Toold só será listada quando o PowerPivot para SharePoint estiver instalado no servidor local.  
  
2.  Clique em **Configurar ou Reparar o PowerPivot para SharePoint** e clique em **OK**.  
  
3.  A ferramenta executa uma validação para verificar o estado atual do PowerPivot e quais etapas são necessárias para concluir a configuração. Expanda a janela para o tamanho total. Você verá uma barra de botões na parte inferior da janela que inclui os comandos **Validar**, **Executar**e **Sair** .  
  
4.  Na guia **Parâmetros** :  
  
    1.  **Nome de usuário da conta padrão**: Insira uma conta de usuário de domínio para a conta padrão. Essa conta será usada para provisionar serviços, inclusive o pool de aplicativos do serviço PowerPivot. Não especifique uma conta interna, como Serviço de Rede ou Sistema Local. A ferramenta bloqueia configurações que especificam contas internas.  
  
    2.  **Servidor de banco de dados**: Você pode usar SQL Server mecanismo de banco de dados com suporte para o farm do SharePoint.  
  
    3.  **Senha**: Insira uma frase secreta. Se você estiver criando um novo farm do SharePoint, a frase secreta será usada sempre que você adicionar um servidor ou aplicativo ao farm do SharePoint. Se o farm já existir, insira a frase secreta que permite adicionar um aplicativo de servidor ao farm.  
  
    4.  **Servidor do PowerPivot para serviços do Excel**: Digite o nome de um [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] servidor de modo do SharePoint. Em uma implantação de servidor único, ele será o servidor de banco de dados. `[ServerName]\powerpivot`  
  
    5.  Clique em **Criar Coleção de Sites** na janela esquerda. Observe a **URL do Site** para poder referenciá-la em etapas posteriores. Se o servidor do SharePoint ainda não estiver configurado, o assistente de configuração usa como padrão o aplicativo Web e as URLs da coleção de sites da raiz de `http://[ServerName]`. Para modificar os padrões, examine as seguintes páginas na janela esquerda: **Criar aplicativo Web padrão** e **implantar solução de aplicativo Web**  
  
5.  Opcionalmente, revise os valores de entrada restantes usados para concluir cada ação. Clique em cada ação na janela esquerda para exibir e revisar os detalhes da ação. Para obter mais informações sobre cada um, consulte a seção "valores de entrada usados para configurar o servidor em [Configurar ou reparar &#40;PowerPivot para SharePoint a ferramenta&#41; de configuração do PowerPivot 2010](../../configure-repair-powerpivot-sharepoint-2010.md) neste tópico.  
  
6.  Opcionalmente, remova as ações que você não deseja processar neste momento. Por exemplo, se desejar configurar o Serviço de Repositório Seguro, clique em **Configurar Serviço de Repositório Seguro**e desmarque a caixa de seleção **Inclua esta ação na lista de tarefas**.  
  
7.  Clique em **Validar** para verificar se a ferramenta tem informações suficientes para processar as ações na lista. Se você encontrar erros de validação, clique nos avisos no painel esquerdo para ver os detalhes do erro de validação. Corrija os erros de validação e clique em **Validar** novamente.  
  
8.  Clique em **Executar** para processar todas as ações na lista de tarefas. Observe que **Executar** fica disponível depois que você valida as ações. Se **Executar** não estiver habilitado, clique em **Validar** primeiro.  
  
 Para obter mais informações, consulte [Configurar ou reparar PowerPivot para SharePoint &#40;ferramenta&#41; de configuração do PowerPivot 2010](../../configure-repair-powerpivot-sharepoint-2010.md)  
  
##  <a name="bkmk_verify_powerpivot"></a>Verificar a configuração do PowerPivot  
 **Serviços:**  
  
1.  Na Administração Central, em Configurações do Sistema, clique em **Gerenciar serviços no servidor**.  
  
2.  Verifique se o **SQL Server Analysis Services** e o **Serviço de Sistema PowerPivot do SQL Server** foram iniciados.  
  
 **Recurso do farm:**  
  
1.  Na Administração Central, em Configurações do Sistema, clique em **Gerenciar recursos de farm**.  
  
2.  Verifique se **Recurso de Integração com o PowerPivot** está **Ativo**.  
  
 **Recurso da coleção de sites:**  
  
1.  Navegue até a URL do site que foi criada pela ferramenta de configuração.  
  
     Clique em **configurações**configurações![do SharePoint]configurações(https://docs.microsoft.com/analysis-services/analysis-services/media/as-sharepoint2013-settings-gear.gif "do SharePoint")e clique em **configurações do site**.  
  
     Clique em **Recursos do Conjunto de Sites**.  
  
2.  Verifique se a **Integração de recursos do PowerPivot para coleções de sites** está **Ativa**.  
  
 **Aplicativo de serviço PowerPivot:**  
  
1.  Na Administração Central, no **Gerenciamento de Aplicativo**, clique em **Gerenciar aplicativos de serviço**.  
  
2.  Verifique se o status do aplicativo de serviço é **iniciado**. O nome padrão é **Aplicativo de Serviço PowerPivot Padrão**.  
  
     Clique no nome do aplicativo de serviços para abrir o Painel de Gerenciamento PowerPivot para o aplicativo aberto. No primeiro uso, o painel demora alguns minutos para carregar.  
  
 Para obter mais informações, consulte [Verify a PowerPivot for SharePoint Installation](https://docs.microsoft.com/analysis-services/instances/install-windows/verify-a-power-pivot-for-sharepoint-installation).  
  
##  <a name="bkmk_troubleshoot_issues"></a> Solucionar problemas  
 Para ajudar a solucionar problemas, é uma boa ideia verificar se o log de diagnóstico está habilitado.  
  
1.  Na Administração Central do SharePoint, clique em **Monitoramento** e clique em **Configurar coleta de dados de integridade e uso**.  
  
2.  Verifique se **Habilitar coleta de dados de uso** está selecionado.  
  
3.  Verifique se os eventos a seguir estão selecionados:  
  
    -   Definição de campos de uso da telemetria Educação  
  
    -   Conexões do PowerPivot  
  
    -   Uso de Dados de Carregamento do PowerPivot  
  
    -   Uso de Consulta do PowerPivot  
  
    -   Uso de Dados de Descarregamentos do PowerPivot  
  
4.  Verifique se **Habilitar coleta de dados de integridade** está selecionado.  
  
5.  Clique em **OK**.  
  
 Para obter mais informações sobre a atualização de dados de solução de problemas, consulte solução https://social.technet.microsoft.com/wiki/contents/articles/3870.troubleshooting-powerpivot-data-refresh.aspx) de problemas de atualização de [dados PowerPivot](https://social.technet.microsoft.com/wiki/contents/articles/3870.troubleshooting-powerpivot-data-refresh.aspx) (.  
  
 Para obter mais informações sobre a ferramenta de configuração, consulte [PowerPivot Configuration Tools](../../power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
  
