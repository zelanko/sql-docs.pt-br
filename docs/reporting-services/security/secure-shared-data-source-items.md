---
title: Proteger itens de fonte de dados compartilhada | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: security
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- shared data sources [Reporting Services]
- data sources [Reporting Services], shared
- security [Reporting Services], data sources
ms.assetid: 7299e498-0a1a-4821-a22a-5199bb773ce0
caps.latest.revision: 35
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: baf66967f54222bb28ebf04dd2fda9b51e90d3c3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="secure-shared-data-source-items"></a>Proteger itens de fontes de dados compartilhadas
  Você pode definir a segurança em um item fonte de dados compartilhada para habilitar ou desabilitar o acesso a ele.  
  
 Um usuário que tem acesso mínimo a uma fonte de dados compartilhada (por exemplo, o acesso concedido através da função **Navegador** ) pode exibir a lista de relatórios que usam o item, contanto que o usuário também tenha autorização para exibir os relatórios propriamente ditos.  
  
 Um usuário que tem acesso adicional (como o acesso concedido pela função **Gerenciador de Conteúdo** ) pode exibir e definir propriedades para a fonte de dados compartilhada.  
  
 Para definir a segurança, crie uma atribuição de função que especifique a conta de usuário ou grupo que tem acesso à fonte de dados compartilhada. Os usuários que têm acesso a um item fonte de dados compartilhada podem alterar seu nome, descrição, cadeia de conexão ou informações de credenciais.  
  
## <a name="tasks-and-access-to-items"></a>Tarefas e acesso a itens  
 Ao criar atribuições de função, use uma função que tem estas tarefas para atribuir permissões apropriadas aos usuários e grupos.  
  
|Selecione esta tarefa|Para conceder permissão aos usuários para|  
|----------------------|---------------------------------|  
|Exibir fontes de dados|Exibir o item fonte de dados compartilhada na hierarquia de pastas. Sem essa tarefa, o item não pode ser visto pelos usuários e eles talvez não saibam que a fonte de dados está disponível.|  
|Gerenciar fontes de dados|Exibir as propriedades que especificam o nome, a descrição e as informações de conexão. Essa tarefa também é usada para exibir um item fonte de dados compartilhada na hierarquia de pastas. Se você escolher essa tarefa, poderá omitir a tarefa “Exibir fontes de dados”.|  
|Definir segurança em itens|Criar e modificar atribuições de função que controlam o acesso à fonte de dados compartilhada. Essa tarefa deve ser usada com as tarefas “Exibir fonte de dados” ou “Gerenciar fontes de dados”. Se não for, não terá nenhum efeito porque o usuário não pode selecionar o item.|  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciar fontes de dados de relatório](../../reporting-services/report-data/manage-report-data-sources.md)   
 [Proteger pastas](../../reporting-services/security/secure-folders.md)   
 [Proteger relatórios e recursos](../../reporting-services/security/secure-reports-and-resources.md)   
 [Concedendo permissões em um servidor de relatório no modo nativo](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [Armazenar credenciais em uma fonte de dados do Reporting Services](../../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md)  
  
  
