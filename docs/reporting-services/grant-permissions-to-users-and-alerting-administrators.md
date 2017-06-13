---
title: "Conceder permissões a usuários e administradores de alerta | Microsoft Docs"
ms.custom: 
ms.date: 05/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 166808e1-ada7-48d2-bda8-8f7c017fb3aa
caps.latest.revision: 11
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 91700c92ed7f96e00ba05d7ee9ca96590d0a4837
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="grant-permissions-to-users-and-alerting-administrators"></a>Conceder permissões a usuários e administradores de alerta

[!INCLUDE[ssrs-appliesto-sql2016-xpreview](../includes/ssrs-appliesto-sql2016-xpreview.md)][!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

Para que os usuários e os administradores de alerta possam criar, editar, excluir e exibir alertas de dados, eles devem receber permissões do SharePoint. Não há nenhuma permissão especial a ser usada com o recurso de alerta de dados do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Você usa as permissões internas do SharePoint.

> [!NOTE]
> Integração do Reporting Services com o SharePoint não está mais disponível após o SQL Server 2016.

**Operadores de informações**— As permissões devem incluir as permissões Criar Alerta e Exibir Itens do SharePoint. Os níveis de permissão internos do SharePoint denominados Design, Colaborar, Ler e Apenas Exibir incluem as permissões Criar Alerta e Exibir Itens do SharePoint. Você também pode criar um nível de permissão personalizado com as permissões necessárias dar suporte a usuários que criam, editam, executam e exibem alertas de dados.

**Administradores de alerta**—As permissões devem incluir a permissão Gerenciar Alerta do SharePoint. Por padrão, apenas o nível de permissão Controle Completo inclui essa permissão para sites criados com o modelo de Site de Equipe. Se você usar outros modelos de sites, visualizará listas diferentes de grupos padrão do SharePoint. Você pode adicionar a permissão Gerenciar Alerta a um dos níveis de permissão internos ou criar um nível de permissão personalizado com a permissão necessária para dar suporte a administradores de alerta que exibem e excluem alertas de dados.

Para obter mais informações sobre as permissões do SharePoint, consulte [Permissões de usuários e níveis de permissão (SharePoint Server 2010)](http://technet.microsoft.com/library/cc721640.aspx).

## <a name="grant-permissions"></a>Conceder permissões
  
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

[Definir permissões para itens do Servidor de Relatório em um site do SharePoint &#40;Reporting Services no modo integrado do SharePoint&#41;](../reporting-services/security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)   
[Alertas de dados do Reporting Services](../reporting-services/reporting-services-data-alerts.md)  

Mais perguntas? [Tente fazer o fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
