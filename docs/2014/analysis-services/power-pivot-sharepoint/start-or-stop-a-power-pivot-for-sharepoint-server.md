---
title: Iniciar ou parar um servidor de PowerPivot para SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: e38e6366-9f20-4db0-b2a8-da7d5adf00eb
author: minewiskan
ms.author: owend
ms.openlocfilehash: 237f4dfaa615718f7fa4301b8d64cab0c45600b0
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547758"
---
# <a name="start-or-stop-a-powerpivot-for-sharepoint-server"></a>Iniciar ou parar um PowerPivot para SharePoint Server
  O Serviço de Sistema do PowerPivot e uma instância do [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] funcionam em conjunto no mesmo servidor de aplicativo local para dar suporte à solicitação coordenada e ao processamento de dados em um farm do SharePoint.  
  
 Este tópico contém as seguintes seções:  
  
 [Dependências de serviço](#dependencies)  
  
 [Iniciar ou parar os serviços](#startstop)  
  
 [Efeitos da interrupção de um servidor do PowerPivot](#effects)  
  
##  <a name="service-dependencies"></a><a name="dependencies"></a>Dependências de serviço  
 O Serviço de Sistema do PowerPivot tem uma dependência na instância de servidor do Analysis Services local que é instalada com ele no mesmo servidor físico. Se você parar o Serviço de Sistema do PowerPivot, também terá que parar manualmente a instância de servidor do Analysis Services local. Se um serviço estiver em execução sem o outro, você verá erros de alocação na solicitação de processamento de dados PowerPivot.  
  
 O servidor do Analysis Services só deverá ser executado por si só se você estiver diagnosticando ou soluciona um problema. Em todos os outros casos, o servidor requer que o Serviço de Sistema do PowerPivot seja executado localmente no mesmo servidor.  
  
##  <a name="start-or-stop-the-services"></a><a name="startstop"></a>Iniciar ou parar os serviços  
 Sempre use a Administração Central para iniciar ou parar o Serviço de Sistema do PowerPivot ou a instância de servidor do Analysis Services. A Administração Central permite iniciar ou parar os serviços na mesma página. Além disso, a Administração Central usa um trabalho de timer chamado **Um ou mais serviços foram iniciados ou interrompidos** para reiniciar serviços que devem estar em execução. Se você parar o Serviço de Sistema do PowerPivot ou os Analysis Services usando uma ferramenta que não seja do SharePoint, os serviços serão reiniciados quando o trabalho de timer for executado.  
  
 Iniciar e parar serviços são ações que se aplicam a uma instância de serviço física. Se você tiver servidores adicionais do PowerPivot para SharePoint no farm, os outros servidores dentro do farm continuarão aceitando solicitações de dados PowerPivot.  
  
 Você não pode iniciar ou parar todos os serviços físicos simultaneamente pelo farm. Você deve selecionar cada servidor e depois iniciar ou parar um serviço específico.  
  
 Você não pode iniciar, pausar ou parar um Serviço de Sistema do PowerPivot para um aplicativo Web específico, mas você pode remover um serviço da lista de conexões padrão para torná-lo não disponível. Para obter mais informações, consulte [conectar um aplicativo de serviço PowerPivot a um aplicativo Web do SharePoint na administração central](connect-power-pivot-service-app-to-sharepoint-web-app-in-ca.md).  
  
1.  Na Administração Central, em **Configurações do Sistema**, clique em **Gerenciar serviços no servidor**.  
  
2.  Na parte superior da página, em Servidor, clique na seta para baixo e, em seguida, em **Alterar Servidor**.  
  
3.  Selecione o servidor do SharePoint que tem o Serviço de Sistema do PowerPivot ou instância do [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] que você deseja iniciar ou parar.  
  
4.  Selecione o serviço e clique na ação. Lembre-se de iniciar ou parar os serviços como um par. Se você iniciar ou parar o Serviço de Sistema do PowerPivot, não se esqueça de iniciar ou parar a instância de servidor do Analysis Services executada no mesmo computador.  
  
##  <a name="effects-of-stopping-a-powerpivot-server"></a><a name="effects"></a>Efeitos da interrupção de um servidor PowerPivot  
 A tabela a seguir descreve os efeitos de parar o Serviço de Sistema do PowerPivot e o serviço Analysis Services em um servidor do SharePoint.  
  
|Efeito em|Description|  
|---------------|-----------------|  
|Consultas existentes|As consultas que estão em andamento em um servidor do Analysis Services pararão imediatamente. O usuário receberá o erro de dados não localizados ou conexão da fonte de dados não localizada.|  
|Trabalhos de atualização de dados existentes em processamento no momento|Os trabalhos que estão em andamento em um servidor do Analysis Services atual pararão imediatamente. A atualização de dados falhará e um erro será registrado no histórico da atualização de dados.<br /><br /> É possível exibir o status de trabalhos atuais antes de parar o serviço, usando-se a página Verificar status do trabalho na Administração Central do SharePoint.<br /><br /> Embora seja impossível saber quais trabalhos estão em processamento no momento, não há como exibir a própria fila para verificar se outros trabalhos estão prestes a começar.|  
|Solicitações de atualização de dados existentes na fila|As solicitações de atualização de dados agendadas permanecerão na fila de processamento durante um ciclo completo da agenda (quer dizer, permanecem na fila até a próxima hora de início). Se o Serviço de Sistema do PowerPivot não for reiniciado até lá, a solicitação de atualização de dados será removida e um erro será registrado.|  
|Novas solicitações para consultas ou atualização de dados|Se você estiver parando somente o servidor do PowerPivot para SharePoint no farm, novas solicitações para dados PowerPivot não serão manipuladas e uma solicitação de dados resultará em um erro de dados não encontrados.<br /><br /> Se você tiver servidores do PowerPivot para SharePoint adicionais, a solicitação irá para um dos servidores disponíveis.|  
|Dados de uso|Não serão coletados dados de uso enquanto os serviços estiverem parados.|  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar contas de serviço PowerPivot](configure-power-pivot-service-accounts.md)  
  
  
