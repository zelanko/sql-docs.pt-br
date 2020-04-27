---
title: 'A conexão de dados usa a Autenticação do Windows e não foi possível delegar as credenciais de usuário. As seguintes conexões não foram atualizadas: dados PowerPivot | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d2006df1-d244-4786-b272-49d8996cc88c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0b11e1510213aefa98c6bf2c0c779cebaeed85e5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66071028"
---
# <a name="the-data-connection-uses-windows-authentication-and-user-credentials-could-not-be-delegated-the-following-connections-failed-to-refresh-powerpivot-data"></a>A conexão de dados usa a Autenticação do Windows e não foi possível delegar as credenciais de usuário. As conexões a seguir não foram atualizadas: Dados PowerPivot
  Para pastas de trabalho do Excel que contenham dados PowerPivot, os Serviços do Excel retornarão este erro se não conseguirem conectar-se a uma instância de servidor do PowerPivot no SharePoint.  
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Aplica-se a|PowerPivot para SharePoint|  
|Versão do produto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|Falha de conexão ao tentar usar um provedor de dados PowerPivot.|  
|Texto da mensagem|A conexão de dados usa a Autenticação do Windows e não foi possível delegar as credenciais de usuário. As conexões a seguir não foram atualizadas: Dados PowerPivot|  
  
## <a name="explanation"></a>Explicação  
 Há várias causas para essa mensagem de erro. O fator comum por trás de todas elas é que os Serviços do Excel não podem obter uma identidade do usuário do Windows válida de um token de declarações no SharePoint. No caso de pastas de trabalho do Excel que contenham dados PowerPivot, esse erro ocorre quando uma destas condições existe:  
  
-   O Claims para Windows Token Service não está em execução. Você pode confirmar a causa desse erro exibindo o arquivo de log do SharePoint. Se os logs do SharePoint incluírem a mensagem "Não foi possível localizar o ponto de extremidade de pipe 'net.pipe://localhost/s 4u/022694f3-9fbd-422b-b4b2-312e25dae2a2' em sua máquina local", o Claims para Windows Token Service não está em execução. Para iniciá-lo, use a Administração Central e verifique se o serviço está sendo executado no aplicativo de console de Serviços.  
  
-   Um controlador de domínio não está disponível para validar a identidade do usuário. O Claims to Windows Token Service não usa credenciais armazenadas em cache. Valida a identidade do usuário para cada conexão. Você pode confirmar a causa desse erro exibindo o arquivo de log do SharePoint. Se os logs do SharePoint incluírem a mensagem "Falha ao obter WindowsIdentity de IClaimsIdentity", não foi possível autenticar a identidade do usuário.  
  
-   Os computadores devem ser membros do mesmo domínio ou de domínios que tenham uma relação de confiança bidirecional.  
  
-   Você deve usar contas de usuário de domínio do Windows. As contas devem ter um UPN.  
  
-   A conta de serviço dos Serviços do Excel deve ter permissões do Active Directory para consultar o objeto.  
  
## <a name="user-action"></a>Ação do usuário  
 Use as instruções a seguir para verificar o status do Claims para Windows Token Service.  
  
 Para todos os outros cenários, consulte o administrador da rede.  
  
#### <a name="enable-claims-to-windows-token-service"></a>Habilitar o Claims para Windows Token Service  
  
1.  Na administração central, em configurações do sistema, clique em **gerenciar serviços no servidor**.  
  
2.  Selecione **Claims para Windows Token Service**e clique em **Iniciar**.  
  
3.  Verifique se o serviço também está em execução no console Serviços:  
  
    1.  Em Ferramentas Administrativas, clique em Serviços.  
  
    2.  Inicie o Claims to Windows Token Service se ele ainda não estiver em execução.  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar contas de serviço PowerPivot](configure-power-pivot-service-accounts.md)  
  
  
