---
title: O usuário da conexão de dados não puderam ser delegado | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 13f2e848b18b8097bf46f75e785e2dab6d36dd10
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="the-data-connection-user-could-not-be-delegated"></a>O usuário da conexão de dados não pode ser delegado
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Para pastas de trabalho do Excel que contenham dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , os Serviços do Excel retornarão esse erro se não conseguirem se conectar a uma instância de servidor do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no SharePoint.  
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Aplica-se a|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint|  
|Versão do Produto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|Falha de conexão ao tentar usar um provedor de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .|  
|Texto da mensagem|A conexão de dados usa a Autenticação do Windows e não foi possível delegar as credenciais de usuário. As conexões a seguir não foram atualizadas: dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]|  
  
## <a name="explanation"></a>Explicação  
 Há várias causas para essa mensagem de erro. O fator comum por trás de todas elas é que os Serviços do Excel não podem obter uma identidade do usuário do Windows válida de um token de declarações no SharePoint. No caso de pastas de trabalho do Excel que contenham dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , esse erro ocorre quando uma destas condições existe:  
  
-   O Claims para Windows Token Service não está em execução. Você pode confirmar a causa desse erro exibindo o arquivo de log do SharePoint. Se os logs do SharePoint incluírem a mensagem "Não foi possível localizar o ponto de extremidade de pipe 'net.pipe://localhost/s 4u/022694f3-9fbd-422b-b4b2-312e25dae2a2' em sua máquina local", o Claims para Windows Token Service não está em execução. Para iniciá-lo, use a Administração Central e verifique se o serviço está sendo executado no aplicativo de console de Serviços.  
  
-   Um controlador de domínio não está disponível para validar a identidade do usuário. O Claims to Windows Token Service não usa credenciais armazenadas em cache. Valida a identidade do usuário para cada conexão. Você pode confirmar a causa desse erro exibindo o arquivo de log do SharePoint. Se os logs do SharePoint incluírem a mensagem "Falha ao obter WindowsIdentity de IClaimsIdentity", não foi possível autenticar a identidade do usuário.  
  
-   Os computadores devem ser membros do mesmo domínio ou de domínios que tenham uma relação de confiança bidirecional.  
  
-   Você deve usar contas de usuário de domínio do Windows. As contas devem ter um UPN.  
  
-   A conta de serviço dos Serviços do Excel deve ter permissões do Active Directory para consultar o objeto.  
  
## <a name="user-action"></a>Ação do usuário  
 Use as instruções a seguir para verificar o status do Claims para Windows Token Service.  
  
 Para todos os outros cenários, consulte o administrador da rede.  
  
#### <a name="enable-claims-to-windows-token-service"></a>Habilitar o Claims para Windows Token Service  
  
1.  Na Administração Central, em Configurações do Sistema, clique em **Gerenciar serviços no servidor**.  
  
2.  Selecione **Claims para Windows Token Service**e clique em **Iniciar**.  
  
3.  Verifique se o serviço também está em execução no console Serviços:  
  
    1.  Em Ferramentas Administrativas, clique em Serviços.  
  
    2.  Inicie o Claims to Windows Token Service se ele ainda não estiver em execução.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar contas de serviço Power Pivot](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md)  
  
  
