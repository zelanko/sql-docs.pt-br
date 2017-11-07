---
title: "O usuário da conexão de dados não puderam ser delegado | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: d2006df1-d244-4786-b272-49d8996cc88c
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 82b5e9a4f63aee2235972f62387367075ff4b8b9
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="the-data-connection-user-could-not-be-delegated"></a>O usuário da conexão de dados não pode ser delegado
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
  
  

