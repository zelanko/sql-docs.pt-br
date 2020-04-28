---
title: Ferramentas de Configuração do PowerPivot | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: f934c51d-01fe-4e67-971d-cd87d7d7ee51
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 299b40b92b3d2f8c5559a5e10e511f80ab5a5bc9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78175655"
---
# <a name="powerpivot-configuration-tools"></a>PowerPivot Configuration Tools
  Configure, repare ou remova um [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] com o ferramentas de configuração do PowerPivot.

 O Assistente de Configuração do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] instala a Ferramenta de Configuração do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint 2010, bem como a Ferramenta de Configuração do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint 2013. Este tópico descreve o uso geral das duas ferramentas e as diferenças entre elas.

 **[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2013 | SharePoint 2010

 **Neste tópico:**

-   [Requisitos para usar as ferramentas de configuração](#bkmk_requirements)

-   [Duas versões da ferramenta de configuração](#bkmk_twoversions)

-   [Visão geral do uso de uma ferramenta de configuração do PowerPivot](#bkmk_overview)

-   [Iniciar uma das ferramentas de configuração do PowerPivot](#bmkm_start_tool)

##  <a name="requirements-for-using-the-configuration-tools"></a><a name="bkmk_requirements"></a>Requisitos para usar o Ferramentas de Configuração

-   Você deve ser um administrador de farm.

-   Você deve ser um administrador de servidor na instância do Analysis Services (somente SharePoint 2010).

-   Você deve estar db_owner no banco de dados de configuração do farm.

-   Não há requisitos de porta TCP/IP para usar as ferramentas de configuração. Portanto, não é preciso configurar o firewall para acomodar as ferramentas de configuração. A ferramenta configuração espera que os aplicativos Web e serviços compartilhados estejam disponíveis como parte da plataforma SharePoint. Pode ser necessário configurar o firewall para o servidor [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Para obter mais informações, consulte [Configure the Windows Firewall to Allow Analysis Services Access](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).

##  <a name="two-versions-of-the-configuration-tool"></a><a name="bkmk_twoversions"></a>Duas versões da ferramenta de configuração
 O Assistente de Configuração do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] instala a Ferramenta de Configuração do PowerPivot para SharePoint 2010, bem como a Ferramenta de Configuração do PowerPivot para SharePoint 2013.

 As ferramentas podem ser usada apenas com uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ou [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]. Não use-as com instalações do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] .

|Nome|Versão com suporte do SharePoint|Configuração detalhada|
|----------|-------------------------------------|----------------------------|
|Configuração do PowerPivot para SharePoint 2013|SharePoint 2013|[Configurar ou reparar a ferramenta de configuração do PowerPivot para SharePoint 2013 &#40;o PowerPivot&#41;](configure-or-repair-power-pivot-for-sharepoint-2013.md)|
|Ferramenta de Configuração do PowerPivot|SharePoint 2010 com SharePoint 2010|[Configurar ou reparar a ferramenta de configuração do PowerPivot para SharePoint 2010 &#40;o PowerPivot&#41;](../configure-repair-powerpivot-sharepoint-2010.md)|

###  <a name="how-the-two-configuration-tools-are-different"></a><a name="bkmk_sum_differences_betweentools"></a>Como os dois Ferramentas de Configuração são diferentes
 As duas versões da ferramenta de configuração são semelhantes, mas há diferenças nas etapas de configuração executadas pelas duas ferramentas. As diferenças se devem a alterações entre o SharePoint 2010 e o SharePoint 2013, mas também a diferenças na arquitetura entre a versão do SQL Server 2012 SP1 do PowerPivot para SharePoint e as versões anteriores do PowerPivot para SharePoint.

 A tabela a seguir descreve recursos novos e modificados na ferramenta de **Configuração do PowerPivot para SharePoint 2013** . A tabela também descreve recursos da **Ferramenta de Configuração do PowerPivot** que não estão na Ferramenta de Configuração do PowerPivot para SharePoint 2013. As linhas da tabela estão na mesma ordem que as guias nas ferramentas de configuração.

|Configuração do PowerPivot para SharePoint 2013|Ferramenta de Configuração do PowerPivot|
|--------------------------------------------------|-----------------------------------|
|A página principal tem uma nova opção para **Servidor do PowerPivot para Serviços do Excel**. A opção dá suporte à nova arquitetura com o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] executado fora do farm do SharePoint. Você configura Serviços do Excel para usar um ou mais servidores do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em execução no modo do SharePoint.<br /><br /> ![Servidor do PowerPivot na nova ferramenta de configuração](../media/as-powerpivot-configtool-differences-new-mainpage.gif "Servidor do PowerPivot na nova ferramenta de configuração")||
||A ferramenta 2010 inclui a SQL Server Analysis Services de registro de página **(PowerPivot) no servidor local** para configurar uma instância [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]local do. Essa página não faz parte da ferramenta 2013 porque não há instância local do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].<br /><br /> ![Conta de serviço AS na antiga ferramenta de configuração](../media/as-powerpivot-configtool-differences-old-register-as-localserver.gif "Conta de serviço AS na antiga ferramenta de configuração")|
||A página **Criar Aplicativo de Serviço PowerPivot** tem uma opção adicional de **Atualizar pastas de trabalho para habilitar atualização de dados**. Essa opção não está disponível na ferramenta 2013.<br /><br /> ![atualizar pastas de trabalho na antiga ferramenta de configuração](../media/as-powerpivot-configtool-differences-old-uprgadeworkbooks.gif "atualizar pastas de trabalho na antiga ferramenta de configuração")|
|A ferramenta 2013 tem uma nova página **Configurar Servidores PowerPivot**. Essa página dá suporte à nova arquitetura do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] executado fora do farm do SharePoint. Por padrão, o nome do servidor que foi digitado na página principal na caixa de texto **Servidor do PowerPivot para Serviços do Excel**também será listado em **Configurar Servidores PowerPivot**.<br /><br /> ![Registrar servidores do PowerPivot na nova ferramenta de configuração](../media/as-powerpivot-configtool-differences-new-powerpivot-servers.gif "Registrar servidores do PowerPivot na nova ferramenta de configuração")||
|A ferramenta 2013 tem uma nova página **Registrar o Suplemento PowerPivot como Rastreador de Uso de Serviços do Excel**. Os Serviços do Excel no SharePoint 2010 não rastreiam dados de uso do PowerPivot.||
||A ferramenta 2010 inclui a página **Adicionar MSOLAP.5 como um provedor confiável** para registrar MSOLAP de modo que os Serviços do Excel no SharePoint 2010 possam carregar modelos do PowerPivot. Essa página não faz parte da ferramenta 2013. Os Serviços do Excel para SharePoint 2013 não usam o provedor MSOLAP para carregar modelos.|

##  <a name="overview-of-using-a-powerpivot-configuration-tool"></a><a name="bkmk_overview"></a>Visão geral do uso de uma ferramenta de configuração do PowerPivot
 Quando você inicia uma das Ferramentas de Configuração do PowerPivot, a ferramenta avalia a instalação existente para determinar quais operações são aplicáveis. Em uma nova instalação, apenas a tarefa de configuração está disponível. Depois que o servidor estiver configurado, a tarefa de remoção será exibida. Se você tiver iniciado com uma instância do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] , a atualização também será habilitada na lista de tarefas disponíveis.

 Se não estiver familiarizado com a Administração Central ou o Windows PowerShell, você poderá executar a ferramenta de configuração como uma alternativa para concluir uma instalação do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] .

 Além disso, a ferramenta pode detectar se o farm está configurado ou se recursos necessários estão ausentes. Se os arquivos de programa do SharePoint estiverem instalados, mas o farm não estiver configurado, a ferramenta fornecerá ações para configurar o farm e a instalação do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] .

 Você pode examinar a guia **Script** para saber e compreender como configurar o PowerPivot e o SharePoint usando o Windows PowerShell. Para saber mais, consulte o seguinte:

-   [Configuração do PowerPivot usando o Windows PowerShell](power-pivot-configuration-using-windows-powershell.md)

-   [Referência do PowerShell para PowerPivot para SharePoint](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint)

> [!NOTE]
>  A ferramenta não configura o Reporting Services. Se estiver adicionando o Reporting Services a seu ambiente do SharePoint, você precisará instalar e configurar o Reporting Services separadamente. Para saber mais, consulte o seguinte:
> 
>  -   [Instale o Reporting Services modo do SharePoint para sharepoint 2013](../../sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md).
> -   [Instale o Reporting Services modo do SharePoint para sharepoint 2010](../../sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md).

##  <a name="start-one-of-the-powerpivot-configuration-tools"></a><a name="bmkm_start_tool"></a>Iniciar uma das Ferramentas de Configuração do PowerPivot

1.  Na tela **Iniciar** , digite`powerpivot`

     Na tela **Iniciar** , digite `powerpivot` ou no menu **Iniciar** , clique em **todos os programas**, clique [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]em **ferramentas de configuração**e, em seguida, clique em um dos seguintes:

    -   **Ferramenta de configuração do PowerPivot**.

    -   **OU**

    -   **Configuração do PowerPivot para SharePoint 2013**.

     ![duas ferramentas de configuração do PowerPivot](../media/as-powerpivot-configtools-bothicons.gif "duas ferramentas de configuração do PowerPivot")

     **Observação:** As ferramentas estão disponíveis apenas quando o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] é instalado no servidor local.

2.  Na inicialização, as ferramentas de configuração verificam o status de sua instalação e fornecem tarefas que são válidas para a instalação.

3.  Dependendo do estado atual da instalação, uma ou mais destas tarefas podem ser executadas:

    1.  Clique em **Configurar ou reparar PowerPivot para SharePoint** para concluir as tarefas pós-instalação ou para reparar uma instalação.

    2.  Clique em **Remover Recursos, Serviços, Aplicativos e Soluções** para remover recursos e soluções do farm.

    3.  Clique em **Atualizar Recursos, Serviços, Aplicativos e Soluções** para atualizar recursos e soluções que foram instaladas usando uma versão anterior do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)].

     Por exemplo, a imagem mostra a página de inicialização da ferramenta de configuração do PowerPivot para o SharePoint 2013.

     ![Ferramenta de configuração do PowerPivot para SharePoint 2013](../media/ssas-powerpivot-configtool-4-sharepoint2013-choosemode.gif "Ferramenta de configuração do PowerPivot para SharePoint 2013")

 Cada tarefa é composta de ações individuais que abordam algum aspecto da configuração do servidor. Por exemplo, a tarefa de configuração inclui ações para implantar soluções, criar um aplicativo de serviço PowerPivot, ativar recursos e configurar a atualização de dados. A lista de ações variará de acordo com o estado atual da instalação. Se uma ação não for necessária, a ferramenta a excluirá da lista de tarefas.

 Quando você clica em Executar, a ferramenta processa todas as ações em modo de lote. Embora cada ação apareça como um item separado na lista de tarefas, todas as ações incluídas na tarefa são processadas em conjunto. Apenas as ações aprovadas em uma verificação de validação são processadas. Você pode precisar adicionar ou alterar alguns dos valores de entrada para ser aprovado para verificação de validação.

## <a name="related-content"></a>Conteúdo relacionado
 [Upgrade PowerPivot for SharePoint](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md) Descreve o fluxo de trabalho que atualiza uma instalação existente que já está em um farm.

 [Uninstall PowerPivot for SharePoint](../../sql-server/install/uninstall-power-pivot-for-sharepoint.md) Descreve o fluxo de trabalho que remove serviços, soluções e páginas de aplicativos do PowerPivot para SharePoint de um farm.

 [Configuração do PowerPivot usando o Windows PowerShell](power-pivot-configuration-using-windows-powershell.md)

 [Administração e configuração de servidor do PowerPivot na Administração Central](power-pivot-server-administration-and-configuration-in-central-administration.md)


