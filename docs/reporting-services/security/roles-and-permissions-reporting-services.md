---
title: "Funções e permissões (Reporting Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- access controls [Reporting Services]
- permissions [Reporting Services], about permissions
- security [Reporting Services], identity and access control
- authentication [Reporting Services]
- permissions [Reporting Services]
- security [Reporting Services], role-based
- identity [Reporting Services]
ms.assetid: eea655fe-43ed-418d-8233-b288a8f4daa4
caps.latest.revision: 18
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ea2b4cba953b6622811b80c7f6c60838ce0a6f91
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="roles-and-permissions-reporting-services"></a>Funções e permissões (Reporting Services)
  O Reporting Services fornece um subsistema de autenticação e modelo de autorização com base na função. Os modelos de autenticação e autorização variam, dependendo se o servidor de relatório é executado no modo nativo ou no modo do SharePoint. Se o servidor de relatório fizer parte de uma implantação do SharePoint, as permissões do SharePoint determinarão quem tem acesso ao servidor de relatório.  
  
## <a name="identity-and-access-control-for-native-mode"></a>Controle de identidade e acesso para o modo nativo  
 A autenticação padrão se baseia na Autenticação e na segurança integrada do Windows. Você pode alterar as configurações de autenticação para permitir que o servidor de relatório responda a solicitações de autenticação diferentes, ou mesmo substitua os recursos de segurança padrão por uma extensão de autenticação personalizada fornecida por você.  
  
 A autorização se baseia em funções que você atribui a um princípio. Cada função consiste em um conjunto de tarefas relacionadas compostas, por sua vez, por operações relacionadas. Por exemplo, a tarefa **Gerenciar relatórios** concede acesso às seguintes operações de servidor de relatório: exibir relatórios, adicionar relatório, atualizar relatório, excluir relatório, agendar relatório e atualizar propriedades de relatório.  
  
## <a name="identity-and-access-control-for-sharepoint-mode"></a>Controle de identidade e acesso no modo do SharePoint  
 No modo integrado do SharePoint, a autenticação e a autorização são manipuladas no site do SharePoint, antes da chegada das solicitações ao servidor de relatório. De acordo com o modo como você configura a autenticação, as solicitações de um site do SharePoint contêm um token de segurança ou um nome de usuário confiável. As permissões que você define para usuários e grupos do SharePoint autorizam o acesso aos itens do servidor de relatório colocados nas bibliotecas do SharePoint.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Concedendo permissões em um servidor de relatório do modo nativo](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
 Descreve o modelo de autorização com base em funções que fornece acesso a conteúdo e operações.  
  
 [Concedendo permissões em itens de servidor de relatório em um Site do SharePoint](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
 Explica como grupos, níveis de permissão e permissões do SharePoint são usados para controlar o acesso a um servidor de relatório.  
  
## <a name="see-also"></a>Consulte também  
 [Autenticação com o servidor de relatório](../../reporting-services/security/authentication-with-the-report-server.md)   
 [Concedendo permissões em um servidor de relatório do modo nativo](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  

