---
title: Itens protegíveis | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- securable items [Reporting Services]
- roles [Reporting Services], securable items
- security [Reporting Services], securable items listed
- role-based security [Reporting Services], securable items
ms.assetid: 27f58d4c-5c7b-4947-af5b-0f1fa60faf5f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 998028cafe4d08be660276a4f88f17667d919863
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63461080"
---
# <a name="securable-items"></a>Itens protegíveis
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa a segurança baseada em função para controlar o acesso a itens armazenados em um servidor de relatório. Quando você concede acesso a um servidor de relatório para um usuário, normalmente faz isso criando um par de atribuições de função:  
  
-   No nível de site  
  
-   Em Base, que é o nó raiz da hierarquia de pastas do servidor de relatório  
  
 A segurança é herdada na hierarquia de pastas do servidor de relatório. Criar atribuições de função no nível de site e na pasta Base define uma herança de permissões que se estende a todos os itens e operações de um servidor de relatório.  
  
 Para ignorar a herança de permissões, defina a segurança para itens individuais. Entre os itens que podem ser protegidos individualmente estão os seguintes:  
  
-   Pastas  
  
-   Relatórios  
  
-   Modelos de relatório  
  
-   Recursos  
  
-   Fontes de dados compartilhadas  
  
-   Conjuntos de dados compartilhados  
  
 Outras construções, como agendas e assinaturas, não são protegidas explicitamente. Agendas e assinaturas operam dentro da segurança de um relatório.  
  
## <a name="item-descriptions"></a>Descrições de itens  
 A tabela a seguir lista itens protegíveis e descreve suas características.  
  
|Item|Características|  
|----------|---------------------|  
|Pastas|A segurança de pasta se aplica à própria pasta e aos itens que ela contém. A pasta Base é o nó raiz da hierarquia de pastas. A segurança definida para essa pasta estabelece as configurações iniciais de segurança para todas as pastas, relatórios, recursos e fontes de dados compartilhadas subordinados na hierarquia de pastas. Para obter mais informações, consulte [Proteger pastas](secure-folders.md).<br /><br /> Meu Relatórios é uma pasta com finalidade especial que é protegida por uma atribuição de função baseada em uma função dedicada. Para obter mais informações, consulte [Proteger Meus Relatórios](secure-my-reports.md).|  
|Relatórios|Os relatórios e os relatórios vinculados podem ser protegidos para controlar as ações que podem ser executadas pelos usuários, como a alteração das propriedades de um relatório específico.<br /><br /> O histórico de relatórios é protegido pelo relatório que contém o histórico. Você não pode proteger instantâneos individuais no histórico de relatórios.<br /><br /> Para obter mais informações sobre a segurança de relatório, consulte [Proteger relatórios e recursos](secure-reports-and-resources.md).|  
|Modelos de relatório|Você pode especificar a atribuição de função em tudo ou em parte de um modelo de relatório. Como os modelos de relatório podem ser muito extensos, talvez seja necessário proteger os itens de modelo mapeados para dados confidenciais.|  
|Recursos|Os recursos podem ser protegidos para controlar o acesso ao próprio recurso e a suas propriedades.<br /><br /> Somente recursos autônomos podem ser protegidos como itens separados. Os recursos que são inseridos em um relatório não podem ser protegidos separadamente do relatório.<br /><br /> Para obter mais informações sobre a segurança de recursos, consulte [Proteger relatórios e recursos](secure-reports-and-resources.md).|  
|Fontes de dados compartilhadas|As fontes de dados compartilhadas podem ser protegidas para limitar o acesso ao item e a suas páginas de propriedade. Para obter mais informações, consulte [Proteger itens de fonte de dados compartilhada](secure-shared-data-source-items.md).|  
|Conjuntos de dados compartilhados|Os conjuntos de dados compartilhados podem ser protegidos para controlar as ações que podem ser executadas pelos usuários, como a exibição ou alteração da definição ou a alteração das propriedades de um conjunto de dados compartilhado específico.<br /><br /> Para obter mais informações, consulte [Proteger itens de conjunto de dados compartilhados](secure-shared-dataset-items.md).|  
  
## <a name="see-also"></a>Consulte também  
 [Concedendo permissões em um servidor de relatório no modo nativo](granting-permissions-on-a-native-mode-report-server.md)   
 [Criar, excluir ou modificar uma função &#40;Management Studio&#41;](role-definitions-create-delete-or-modify.md)   
 [Conceder acesso ao usuário a um servidor de relatório &#40;Gerenciador de Relatórios&#41;](grant-user-access-to-a-report-server.md)   
 [Modificar ou excluir uma atribuição de função &#40;Gerenciador de Relatórios&#41;](role-assignments-modify-or-delete.md)  
  
  
