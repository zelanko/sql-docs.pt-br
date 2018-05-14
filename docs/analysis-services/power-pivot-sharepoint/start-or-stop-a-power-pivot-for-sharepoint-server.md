---
title: Iniciar ou parar um PowerPivot para SharePoint Server | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4b53cc7730f962d790ebdb9a0373bf98e9bf32bf
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="start-or-stop-a-power-pivot-for-sharepoint-server"></a>Iniciar ou parar um Power Pivot para SharePoint Server
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] O Serviço de Sistema e uma instância do [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] funcionam em conjunto no mesmo servidor de aplicativos local para dar suporte à solicitação coordenada e ao processamento de dados em um farm do SharePoint.  
  
 Este tópico contém as seguintes seções:  
  
 [Dependências de serviço](#dependencies)  
  
 [Iniciar ou parar os serviços](#startstop)  
  
 [Efeitos da interrupção de um servidor do Power Pivot](#effects)  
  
##  <a name="dependencies"></a> Dependências de serviço  
 O Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] tem uma dependência na instância de servidor do Analysis Services local que é instalada com ele no mesmo servidor físico. Se você parar o Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , também terá que parar manualmente a instância de servidor do Analysis Services local. Se um serviço estiver em execução sem o outro, você verá erros de alocação na solicitação de processamento de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 O servidor do Analysis Services só deverá ser executado por si só se você estiver diagnosticando ou soluciona um problema. Em todos os outros casos, o servidor requer que o Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] seja executado localmente no mesmo servidor.  
  
##  <a name="startstop"></a> Iniciar ou parar os serviços  
 Sempre use a Administração Central para iniciar ou parar o Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ou a instância de servidor do Analysis Services. A Administração Central permite iniciar ou parar os serviços na mesma página. Além disso, a Administração Central usa um trabalho de timer chamado **Um ou mais serviços foram iniciados ou interrompidos** para reiniciar serviços que devem estar em execução. Se você parar o Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ou o Analysis Services usando uma ferramenta que não seja do SharePoint, os serviços serão reiniciados quando o trabalho do temporizador for executado.  
  
 Iniciar e parar serviços são ações que se aplicam a uma instância de serviço física. Se você tiver servidores adicionais do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint no farm, os outros servidores dentro do farm continuarão aceitando solicitações de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 Você não pode iniciar ou parar todos os serviços físicos simultaneamente pelo farm. Você deve selecionar cada servidor e depois iniciar ou parar um serviço específico.  
  
 Você não pode iniciar, pausar ou parar um Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para um aplicativo Web específico, mas você pode remover um serviço da lista de conexões padrão para torná-lo não disponível. Para obter mais informações, consulte [Conectar um aplicativo de serviço do Power Pivot a um aplicativo Web do SharePoint na Administração Central](../../analysis-services/power-pivot-sharepoint/connect-power-pivot-service-app-to-sharepoint-web-app-in-ca.md).  
  
1.  Na Administração Central, em **Configurações do Sistema**, clique em **Gerenciar serviços no servidor**.  
  
2.  Na parte superior da página, em Servidor, clique na seta para baixo e, em seguida, em **Alterar Servidor**.  
  
3.  Selecione o servidor do SharePoint que tem o Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ou instância do [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] que você deseja iniciar ou parar.  
  
4.  Selecione o serviço e clique na ação. Lembre-se de iniciar ou parar os serviços como um par. Se você iniciar ou parar o Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , não se esqueça de iniciar ou parar a instância de servidor do Analysis Services executada no mesmo computador.  
  
##  <a name="effects"></a> Efeitos da interrupção de um servidor do Power Pivot  
 A tabela a seguir descreve os efeitos de parar o Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e o serviço Analysis Services em um servidor do SharePoint.  
  
|Efeito em|Description|  
|---------------|-----------------|  
|Consultas existentes|As consultas que estão em andamento em um servidor do Analysis Services pararão imediatamente. O usuário receberá o erro de dados não localizados ou conexão da fonte de dados não localizada.|  
|Trabalhos de atualização de dados existentes em processamento no momento|Os trabalhos que estão em andamento em um servidor do Analysis Services atual pararão imediatamente. A atualização de dados falhará e um erro será registrado no histórico da atualização de dados.<br /><br /> É possível exibir o status de trabalhos atuais antes de parar o serviço, usando-se a página Verificar status do trabalho na Administração Central do SharePoint.<br /><br /> Embora seja impossível saber quais trabalhos estão em processamento no momento, não há como exibir a própria fila para verificar se outros trabalhos estão prestes a começar.|  
|Solicitações de atualização de dados existentes na fila|As solicitações de atualização de dados agendadas permanecerão na fila de processamento durante um ciclo completo da agenda (quer dizer, permanecem na fila até a próxima hora de início). Se o Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] não for reiniciado até lá, a solicitação de atualização de dados será removida e um erro será registrado.|  
|Novas solicitações para consultas ou atualização de dados|Se você estiver parando somente o servidor [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint no farm, novas solicitações para dados [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] não serão manipuladas e uma solicitação de dados resultará em um erro de dados não encontrados.<br /><br /> Se você tiver servidores do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint adicionais, a solicitação irá para um dos servidores disponíveis.|  
|Dados de uso|Não serão coletados dados de uso enquanto os serviços estiverem parados.|  
  
## <a name="see-also"></a>Consulte também  
 [Configurar contas de serviço Power Pivot](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md)  
  
  
