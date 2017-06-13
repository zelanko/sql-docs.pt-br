---
title: "Tarefas e permissões | Microsoft Docs"
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
- permissions [Reporting Services], tasks
- role-based security [Reporting Services], permissions
- security [Reporting Services], tasks
- security [Reporting Services], permissions
- role-based security [Reporting Services], tasks
- predefined tasks [Reporting Services]
- tasks [Reporting Services]
ms.assetid: d7ff90b5-b976-4270-b9ad-9d7b801d8263
caps.latest.revision: 40
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c1e2822182d644b90aa419986f75a6fdc6fd3296
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="tasks-and-permissions"></a>Tarefas e permissões
  No [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], *tarefas* são ações que um usuário ou administrador podem executar. Tarefas são predefinidas. Não é possível criar tarefas personalizadas ou modificar aquelas fornecidas de programaticamente ou através de uma ferramenta. Há vinte e cinco tarefas no total. Essas tarefas incluem o conjunto inteiro de operações disponível em segurança com base em função. Alguns exemplos de tarefas são "Exibir relatórios", "Administrar relatórios", e "Administrar propriedades de servidor de relatório".  
  
 Cada tarefa consiste em um conjunto de permissões, que também são predefinidas. Por exemplo, a tarefa "Administrar pastas" contém permissões para criar e excluir pastas e exibir e atualizar propriedades de pasta. São documentadas permissões para cada tarefa para fornecer uma descrição mais exata de cada tarefa. Não é possível interagir diretamente com permissões ou especificá-las em atribuições de função. São concedidas permissões aos usuários indiretamente através das tarefas incluídas em definições de função.  
  
 Tarefas podem ser realizadas somente se fizerem parte de uma função incluída em uma atribuição de função. Portanto, se a tarefa Exibir Modelos não estiver incluída em uma função, ou se essa função não estiver incluída em uma atribuição de função, os usuários não poderão exibir modelos de relatório. O diagrama a seguir ilustra como as permissões são combinadas em tarefas e como tarefas são combinadas em funções que podem ser usadas para atribuições de função específicas.  
  
 ![Diagrama de permissões e tarefas](../../reporting-services/security/media/report-securityobjects.gif "Permissions and task diagram")  
Diagrama de permissões e tarefas  
  
## <a name="system-and-item-level-tasks"></a>Tarefas de nível de item e sistema  
 As tarefas podem ser divididas em duas categorias: nível de sistema e nível de item. Uma função só pode incluir tarefas de uma única categoria. A tabela a seguir descreve cada categoria de tarefas.  
  
|Categoria|Description|  
|--------------|-----------------|  
|[Tarefas em nível de item](../../reporting-services/security/tasks-and-permissions-item-level-tasks.md)|Ações executadas em itens gerenciados por um servidor de relatório, como pastas, relatórios, modelos de relatório e recursos.<br /><br /> Tarefas de nível de item entram no escopo do namespace da pasta de servidor de relatório. Todos os itens acessados pelas pastas em um servidor de relatório ou através de URL protegidos por atribuições de função que incluem tarefas de nível de item.|  
|[Tarefas de nível de sistema](../../reporting-services/security/tasks-and-permissions-system-level-tasks.md)|Ações executadas no nível de sistema, como tarefas de gerenciamento ou agendas compartilhadas que podem ser usadas com vários itens. Tarefas de nível de Sistema entram no escopo fora do namespace de pasta de servidor de relatório.|  
  
## <a name="see-also"></a>Consulte também  
 [Definições de função](../../reporting-services/security/role-definitions.md)   
 [Funções predefinidas](../../reporting-services/security/role-definitions-predefined-roles.md)   
 [Concedendo permissões em um servidor de relatório no modo nativo](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
