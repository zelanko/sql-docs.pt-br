---
title: rsAccessedDenied – erro do Reporting Services | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
helpviewer_keywords:
- rsAccessDenied error
ms.assetid: 2f76b1bf-96a2-4755-b76b-84e933220efc
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b7545f9aafec22f268d71f71d2b6e39a18b54b95
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47793294"
---
# <a name="rsaccesseddenied---reporting-services-error"></a>rsAccessedDenied - Erro do Reporting Services
  O erro do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] **rsAccessedDenied** ocorre quando um usuário não tem permissão para realizar uma ação. Por exemplo, o usuário não tem uma atribuição de função que o permita abrir um relatório ou ele não abriu seu navegador com as permissões necessárias.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  Modo nativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] &#124; modo do SharePoint|  
  
-   Se o erro tiver ocorrido ao acessar o servidor de relatório diretamente através de uma URL, a exceção será mapeada para um erro HTTP 401.  
  
-   Se ele tiver ocorrido ao usar o Gerenciador de Relatórios ou outra ferramenta, o erro será exibido em uma página de erro.  
  
-   Se ele tiver ocorrido durante uma operação, uma assinatura ou uma entrega agendada, o erro será exibido somente no arquivo de log do servidor de relatório.  
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|**Nome do produto**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**ID do evento**|rsAccessedDenied|  
|**Origem do evento**|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|**Componente**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|**Texto da mensagem**|As permissões concedidas ao usuário 'meudomínio\minhaConta' são insuficientes para a execução dessa operação. (rsAccessDenied) (ReportingServicesLibrary)|  
  
## <a name="user-action"></a>Ação do usuário  
 A permissão para acessar as operações e o conteúdo do servidor de relatório é concedida através de atribuições de função. Em uma nova instalação, somente administradores locais têm acesso a um servidor de relatório. Para conceder acesso a outros usuários, é necessário que um administrador local crie uma atribuição de função que especifique um usuário de domínio ou uma conta de grupo, uma ou mais funções que definem as tarefas que o usuário pode executar e um escopo (geralmente, a pasta Base ou o nó raiz da hierarquia de pastas do servidor de relatório). É possível usar o Gerenciador de Relatórios para criar as atribuições de função. Para obter mais informações, consulte "Atribuições de função" nos Manuais Online do SQL Server.  
  
 Esse erro também é causado pela administração local do servidor de relatório. Para obter mais informações, consulte [Configurar um servidor de relatório no modo nativo para a Administração Local &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Atribuições de função](../../reporting-services/security/role-assignments.md)   
 [Concedendo permissões em um servidor de relatório no modo nativo](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [Funções e permissões &#40;Reporting Services&#41;](../../reporting-services/security/roles-and-permissions-reporting-services.md)  
  
  
