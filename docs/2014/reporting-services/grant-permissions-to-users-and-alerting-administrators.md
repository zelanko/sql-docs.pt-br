---
title: Conceder permissões a usuários e administradores de alerta | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 166808e1-ada7-48d2-bda8-8f7c017fb3aa
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 53349b7a4536c6f757b65a60bbd5a82691f9969e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48082296"
---
# <a name="grant-permissions-to-users-and-alerting-administrators"></a>Conceder permissões a usuários e administradores de alerta
  Para que os usuários e os administradores de alerta possam criar, editar, excluir e exibir alertas de dados, eles devem receber permissões do SharePoint. Não há nenhuma permissão especial a ser usada com o recurso de alerta de dados do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Você usa as permissões internas do SharePoint.  
  
 **Operadores de informações**— As permissões devem incluir as permissões Criar Alerta e Exibir Itens do SharePoint. Os níveis de permissão internos do SharePoint denominados Design, Colaborar, Ler e Apenas Exibir incluem as permissões Criar Alerta e Exibir Itens do SharePoint. Você também pode criar um nível de permissão personalizado com as permissões necessárias dar suporte a usuários que criam, editam, executam e exibem alertas de dados.  
  
 **Administradores de alerta**—As permissões devem incluir a permissão Gerenciar Alerta do SharePoint. Por padrão, apenas o nível de permissão Controle Completo inclui essa permissão para sites criados com o modelo de Site de Equipe. Se você usar outros modelos de sites, visualizará listas diferentes de grupos padrão do SharePoint. Você pode adicionar a permissão Gerenciar Alerta a um dos níveis de permissão internos ou criar um nível de permissão personalizado com a permissão necessária para dar suporte a administradores de alerta que exibem e excluem alertas de dados.  
  
 Para obter mais informações sobre as permissões do SharePoint, consulte [Permissões de usuários e níveis de permissão (SharePoint Server 2010)](http://technet.microsoft.com/library/cc721640.aspx).  
  
### <a name="to-grant-permissions"></a>Para conceder permissões  
  
1.  Vá para o site do SharePoint ao qual você deseja conceder permissões.  
  
2.  Na barra de ferramentas, clique em **Ações do Site** e clique em **Permissões do Site**.  
  
     Se você não vir essa opção, você não terá permissão suficiente para conceder permissões a outras pessoas.  
  
3.  Clique em **Conceder Permissões**.  
  
4.  Em **Usuários/Grupos**, digite os nomes dos usuários, os nomes dos grupos ou os endereços de email aos quais você quer conceder permissão.  
  
5.  Selecione a opção **Adicionar usuários a um grupo do SharePoint** ou **Conceder permissão a usuários diretamente** . Dependendo se você selecionou **Adicionar usuários a um grupo do SharePoint** ou **Conceder permissões aos usuários diretamente** , siga em destes procedimentos:  
  
    -   Se você tiver selecionado **Adicionar usuários a um grupo do SharePoint**, selecione um nível de permissão na lista suspensa.  
  
    -   Se você tiver selecionado **Conceder permissões a usuários diretamente**, selecione um nível de permissão.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Definir permissões para itens do servidor de relatório em um Site do SharePoint &#40;modo integrado do Reporting Services no SharePoint&#41;](security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)   
 [Alertas de dados do Reporting Services](../ssms/agent/alerts.md)  
  
  
