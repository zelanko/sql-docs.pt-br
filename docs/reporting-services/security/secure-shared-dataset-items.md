---
title: Proteger itens de conjuntos de dados compartilhados | Microsoft Docs
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
ms.assetid: 08e6d8b5-d88c-4ed2-9c05-55c757e00014
caps.latest.revision: "6"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 40a9f5257e09cf35129c0f11d89675fdeb285c94
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="secure-shared-dataset-items"></a>Proteger itens de conjuntos de dados compartilhados
  Em um servidor de relatório, itens de conjuntos de dados compartilhados podem ser usados por vários relatórios. Você pode proteger conjuntos de dados compartilhados para controlar o grau de acesso concedido aos usuários. Por padrão, apenas usuários que são membros do grupo interno **Administradores** podem exibir conjuntos de dados compartilhados, modificar propriedades, habilitar o cache, criar planos de atualização do cache e excluir os itens. Todos os outros usuários devem ter atribuições de função criadas para eles que permitam acesso a um conjunto de dados compartilhado.  
  
 Para definir a segurança, crie uma atribuição de função que especifique qual conta de usuário ou grupo tem acesso ao conjunto de dados compartilhado.  
  
## <a name="role-based-access-to-shared-datasets"></a>Acesso baseado em função para conjuntos de dados compartilhados  
 Para conceder acesso a conjuntos de dados compartilhados, você pode permitir que os usuários herdem as atribuições de função existentes de uma pasta pai ou criem uma nova atribuição de função no próprio item.  
  
 As atribuições de função padrão que permitem adicionar, excluir, editar propriedades de item e exibir relatórios e conjuntos de dados compartilhados relacionados para conjuntos de dados são Gerenciador de Conteúdo, Meus Relatórios e Publicador. Para editar uma definição de conjunto de dados compartilhado, use as atribuições de função padrão Construtor de Relatórios ou Gerenciador de Conteúdo.  
  
 Como as atribuições de função normalmente são herdadas de um nó pai, uma pasta que tem a tarefa **Exibir relatórios** habilitada transmite essa permissão para os conjuntos de dados compartilhados e relatórios da pasta.  
  
 Para fornecer mais controle sobre conjuntos de dados compartilhados e os resultados das respectivas consultas, configure a segurança em nível de item no item do conjunto de dados compartilhado ou salve conjuntos de dados compartilhados em uma pasta e configure a segurança em nível de item na pasta.  
  
## <a name="shared-dataset-parameters"></a>Parâmetros de conjunto de dados compartilhado  
 Parâmetros de conjunto de dados compartilhado não podem ser usados para restringir dados para usuários específicos. O propósito dos parâmetros de conjunto de dados compartilhado é fornecer uma maneira de especificar quais dados incluir quando o conjunto de dados compartilhado é processado. No servidor de relatório, você não pode proteger os valores de um parâmetro de conjunto de dados compartilhado.  
  
 Na definição do conjunto de dados compartilhado, você pode marcar parâmetros como somente leitura e especificar valores padrão. Parâmetros marcados como somente leitura não podem ser substituídos no servidor. Por exemplo, em um plano de atualização de cache de um conjunto de dados compartilhado, você não pode especificar valores para parâmetros somente leitura. Se os parâmetros de conjunto de dados compartilhado incluírem expressões que fazem referência à coleção global Usuário ou tiverem qualquer outra dependência de usuário, você não poderá criar um plano de atualização de cache para o conjunto de dados compartilhado.  
  
## <a name="tasks-access-to-items-and-default-roles"></a>Tarefas, acesso a itens e funções padrão  
 Conjuntos de dados compartilhados seguem o mesmo modelo de segurança de relatórios. Para fornecer permissão para ações específicas a um usuário, escolha uma função que inclua a tarefa correspondente que inclua essas permissões. A tabela a seguir lista as tarefas e as ações que elas incluem.  
  
|Selecione esta tarefa|Para conceder permissão aos usuários para|Funções padrão que incluem a tarefa|  
|----------------------|---------------------------------|-----------------------------------------|  
|Exibir relatórios|Exibir o item do conjunto de dados compartilhado na hierarquia de pastas. Sem essa tarefa, o item não estará visível para os usuários e eles talvez não percebam que o conjunto de dados está disponível.|Navegador<br /><br /> Gerenciador de Conteúdo<br /><br /> Construtor de Relatórios<br /><br /> Meus Relatórios|  
|Gerenciar relatórios|Exibir as propriedades que especificam o nome, a descrição e as informações de conexão. Essa tarefa também é usada para exibir um item de conjunto de dados compartilhado na hierarquia de pastas. Se você escolher essa tarefa, poderá omitir a tarefa "Exibir relatórios".|Gerenciador de Conteúdo<br /><br /> Publicador<br /><br /> Meus Relatórios|  
|Relatórios de consumo|Exibir a definição do conjunto de dados compartilhado.|Gerenciador de Conteúdo<br /><br /> Construtor de Relatórios|  
|Definir segurança em itens|Criar e modificar atribuições de função que controlam o acesso ao conjunto de dados compartilhado. Essa tarefa deve ser usada com as tarefas "Exibir relatórios" ou "Gerenciar relatórios". Se não for, não terá nenhum efeito porque o usuário não pode selecionar o item.|Gerenciador de Conteúdo|  
  
 Para obter mais informações, consulte [Tarefas em nível de item](../../reporting-services/security/tasks-and-permissions-item-level-tasks.md) e [Funções predefinidas](../../reporting-services/security/role-definitions-predefined-roles.md).  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar conjuntos de dados compartilhados](../../reporting-services/report-data/manage-shared-datasets.md)   
 [Proteger pastas](../../reporting-services/security/secure-folders.md)   
 [Proteger relatórios e recursos](../../reporting-services/security/secure-reports-and-resources.md)   
 [Concedendo permissões em um servidor de relatório no modo nativo](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [Conceder permissões em um servidor de relatório no Modo Nativo](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
