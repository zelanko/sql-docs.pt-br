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
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2019
ms.locfileid: "69493976"
---
# <a name="configure-powerpivot-and-deploy-solutions-sharepoint-2013"></a>Configurar o PowerPivot e implantar soluções (SharePoint 2013)
  Este tópico descreve a implantação e a configuração de aprimoramentos de camada intermediária para os recursos do PowerPivot no [!INCLUDE[SPS2013](../../../includes/sps2013-md.md)], incluindo a galeria do PowerPivot, atualização de dados de agendamento, painel de gerenciamento e provedores de dados. Execute a ferramenta de **Configuração do PowerPivot para SharePoint 2013** para concluir o seguinte:  
  
-   Implantar arquivos de solução do SharePoint.  
  
-   Crie um aplicativo de serviço PowerPivot.  
  
-   Configurar um Aplicativo dos Serviços do Excel para usar um servidor do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no modo do SharePoint. Para obter informações sobre os serviços de back-end e instalar um servidor [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no modo do SharePoint, consulte [instalação do PowerPivot para SharePoint 2013](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode).  
  
 Para obter informações sobre como instalar a ferramenta de configuração do PowerPivot para SharePoint 2013, consulte [instalar ou desinstalar o &#40;suplemento PowerPivot para SharePoint&#41; SharePoint 2013](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013)  
  
 Este tópico contém as seguintes seções:  
  
 [Executar configuração do PowerPivot para SharePoint 2013](#bkmk_run_configuration_tool)  
  
 [Verificar a configuração do PowerPivot](#bkmk_verify_powerpivot)  
  
 [Solucionar problemas](#bkmk_troubleshoot_issues)  
  
##  <a name="bkmk_run_configuration_tool"></a>Executar configuração do PowerPivot para SharePoint 2013  
 **Observação:** O assistente de instalação do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] instala duas ferramentas de configuração diferentes para [!INCLUDE[ssGeminiLong](../../../includes/ssgeminilong-md.md)]. Cada um deles dá suporte a uma versão diferente do SharePoint.  
  
|Nomes|Description|  
|----------|-----------------|  
|Configuração do PowerPivot para SharePoint 2013|SharePoint 2013|  
|Ferramenta de Configuração do PowerPivot|SharePoint 2010 com SharePoint 2010 Service Pack 1 (SP1)|  
  
 **Observação:** Para concluir as etapas a seguir, você deve ser um administrador do farm. Se você vir uma mensagem de erro semelhante à seguinte:  
  
-   "O usuário não é um administrador de farm. Resolva as falhas de validação e tente novamente. "  
  
 Faça logon como a conta que instalou o SharePoint ou configure a conta de instalação como o administrador primário do site de administração central do SharePoint.  
  
1.  No menu **Iniciar** , clique em **todos os programas**e, em seguida, clique em [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)], clique em **ferramentas de configuração**e, em seguida, clique em **configuração do PowerPivot para SharePoint 2013**. A ferramenta é listada somente quando o PowerPivot para SharePoint está instalado no servidor local.  
  
2.  Clique em **Configurar ou reparar PowerPivot para SharePoint** e clique em **OK**.  
  
3.  A ferramenta executa a validação para verificar o estado atual do PowerPivot e quais etapas são necessárias para concluir a configuração. Expanda a janela para tamanho total. Você deve ver uma barra de botões na parte inferior da janela que inclui comandos de **validação**, **execução**e **saída** .  
  
4.  Na guia **parâmetros** :  
  
    1.  Nome de usuário da **conta padrão**: Insira uma conta de domínio da conta padrão. Essa conta será usada para provisionar serviços, inclusive o pool de aplicativos do serviço PowerPivot. Não especifique uma conta interna, como serviço de rede ou sistema local. A ferramenta bloqueia as configurações que especificam contas internas.  
  
    2.  **Servidor de banco de dados**: você pode usar SQL Server mecanismo de banco de dados com suporte para o farm do SharePoint.  
  
    3.  **Senha**: Insira uma frase secreta. Se você estiver criando um novo farm do SharePoint, a frase secreta será usada sempre que você adicionar um servidor ou aplicativo ao farm do SharePoint. Se o farm já existir, insira a frase secreta que permite adicionar um aplicativo de servidor ao farm.  
  
    4.  **Servidor do PowerPivot para Serviços do Excel**: digite o nome de um servidor de modo do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] SharePoint. Em uma implantação de servidor único, ele é o mesmo que o servidor de banco de dados. `[ServerName]\powerpivot`  
  
    5.  Clique em **criar coleção de sites** na janela à esquerda. Observe a **URL do site** para que você possa referenciá-la em etapas posteriores. Se o servidor do SharePoint ainda não estiver configurado, o assistente de configuração padronizará o aplicativo Web e as URLs do conjunto de sites para a raiz de `http://[ServerName]`. Para modificar os padrões, examine as seguintes páginas na janela esquerda: **criar aplicativo Web padrão** e **implantar solução de aplicativo Web**  
  
5.  Opcionalmente, examine os valores de entrada restantes usados para concluir cada ação. Clique em cada ação na janela à esquerda para ver e revisar os detalhes da ação. Para obter mais informações sobre cada um, consulte a seção "valores de entrada usados para configurar o servidor em [Configurar ou reparar &#40;PowerPivot para SharePoint a ferramenta&#41; de configuração do PowerPivot 2010](../../configure-repair-powerpivot-sharepoint-2010.md) neste tópico.  
  
6.  Opcionalmente, remova as ações que você não deseja processar neste momento. Por exemplo, se você quiser configurar o Serviço de Repositório Seguro mais tarde, clique em **configurar serviço de repositório seguro**e desmarque a caixa de seleção **incluir esta ação na lista de tarefas**.  
  
7.  Clique em **validar** para verificar se a ferramenta tem informações suficientes para processar as ações na lista. Se você vir erros de validação, clique nos avisos no painel esquerdo para ver os detalhes do erro de validação. Corrija os erros de validação e clique em **validar** novamente.  
  
8.  Clique em **executar** para processar todas as ações na lista de tarefas. Observe que a **execução** fica disponível depois que você valida as ações. Se a **execução** não estiver habilitada, clique em **validar** primeiro.  
  
 Para obter mais informações, consulte [Configurar ou reparar PowerPivot para SharePoint &#40;ferramenta&#41; de configuração do PowerPivot 2010](../../configure-repair-powerpivot-sharepoint-2010.md)  
  
##  <a name="bkmk_verify_powerpivot"></a>Verificar a configuração do PowerPivot  
 **Serviços**  
  
1.  Na administração central, em configurações do sistema, clique em **gerenciar serviços no servidor**.  
  
2.  Verifique se as Serviço de Sistema PowerPivot de **SQL Server Analysis Services** e **SQL Server** foram iniciadas.  
  
 **Recurso de farm:**  
  
1.  Na administração central, em configurações do sistema, clique em **gerenciar recursos do farm**.  
  
2.  Verifique se o **recurso de integração do PowerPivot** está **ativo**.  
  
 **Recurso de conjunto de sites:**  
  
1.  Navegue até a URL do site que foi criada pela ferramenta de configuração do.  
  
     Clique em **configurações**![configurações do SharePoint](https://docs.microsoft.com/analysis-services/analysis-services/media/as-sharepoint2013-settings-gear.gif "Configurações do SharePoint")e clique em **configurações do site**.  
  
     Clique em **recursos do conjunto de sites**.  
  
2.  Verifique se a **integração de recursos do PowerPivot para coleções de sites** está **ativa**.  
  
 **Aplicativo de serviço PowerPivot:**  
  
1.  Na administração central, no **Gerenciamento de aplicativos**, clique em **gerenciar aplicativos de serviço**.  
  
2.  Verifique se o status do aplicativo de serviço é **iniciado**. O nome padrão é **aplicativo de serviço PowerPivot padrão**.  
  
     Clique no nome do aplicativo de serviços para abrir o painel de gerenciamento PowerPivot para o aplicativo de serviço ser aberto. Na primeira utilização, o painel leva vários minutos para ser carregado.  
  
 Para obter mais informações, consulte [verificar uma instalação de PowerPivot para SharePoint](https://docs.microsoft.com/analysis-services/instances/install-windows/verify-a-power-pivot-for-sharepoint-installation).  
  
##  <a name="bkmk_troubleshoot_issues"></a>Solucionar problemas  
 Para ajudar a solucionar problemas, é uma boa ideia verificar se o log de diagnóstico está habilitado.  
  
1.  Na administração central do SharePoint, clique em **monitoramento** e, em seguida, clique em **Configurar coleta de dados de integridade e uso**.  
  
2.  Verifique se **habilitar coleta de dados de uso** está selecionado.  
  
3.  Verifique se os seguintes eventos estão selecionados:  
  
    -   Definição de campos de uso para telemetria de educação  
  
    -   Conexões do PowerPivot  
  
    -   Uso de dados de carregamento do PowerPivot  
  
    -   Uso de consulta do PowerPivot  
  
    -   Uso de dados de descarregamento do PowerPivot  
  
4.  Verifique se **habilitar coleta de dados de integridade** está selecionado.  
  
5.  Clique em **OK**.  
  
 Para obter mais informações sobre a atualização de dados de solução de problemas, consulte [solução de problemas de atualização de dados PowerPivot](https://social.technet.microsoft.com/wiki/contents/articles/3870.troubleshooting-powerpivot-data-refresh.aspx) (https://social.technet.microsoft.com/wiki/contents/articles/3870.troubleshooting-powerpivot-data-refresh.aspx).  
  
 Para obter mais informações sobre a ferramenta de configuração, consulte [PowerPivot Configuration Tools](../../power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
  
