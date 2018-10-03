---
title: Versões (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- version flags [Master Data Services], about version flags
- versions [Master Data Services]
- version flags [Master Data Services]
- versions [Master Data Services], version flags
ms.assetid: 752ec96d-53d7-4160-8ed2-92e0324645f3
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 5003667b952e927454e5674538d0b40fab577aa9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48190898"
---
# <a name="versions-master-data-services"></a>Versões (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], você pode criar várias versões dos dados mestre dentro de um modelo. As versões podem ser bloqueadas enquanto você valida seus dados e confirmadas depois que os dados forem validados. Versões confirmadas formam um registro auditável de alterações. Cada versão que você cria contém todos os membros, valores de atributo, membros de hierarquia, relações de hierarquia e coleções para o modelo.  
  
## <a name="when-to-use-versions"></a>Quando usar versões  
 Use versões para:  
  
-   Manter um registro auditável de seus dados mestre conforme eles forem alterados com o passar do tempo.  
  
-   Impedir que os usuários façam alterações enquanto assegura que todos os dados sejam validados com êxito segundo as regras de negócio.  
  
-   Bloquear um modelo para uso por sistemas de assinatura.  
  
-   Testar diferentes hierarquias sem implementá-las imediatamente.  
  
> [!NOTE]  
>  Quando você altera a estrutura do seu modelo, como quando cria uma nova entidade ou atributo baseado em domínio, a alteração se aplica a todas as versões. Se você exibisse uma versão anterior do modelo, a entidade ou o atributo seria exibido, mas não existiriam dados.  
  
## <a name="version-flags"></a>Sinalizadores de versão  
 Quando uma versão estiver pronta para usuários ou para um sistema de assinatura, você poderá definir um sinalizador para identificar a versão. Esse sinalizador poderá ser movido de versão para versão conforme necessário. Os sinalizadores ajudam os usuários e sistemas de assinatura a identificar qual versão de um modelo usar.  
  
## <a name="workflow-for-version-management"></a>Fluxo de trabalho para gerenciamento de versões  
 Use o seguinte fluxo de trabalho para o gerenciamento de versões:  
  
1.  Uma versão inicial é criada automaticamente quando você cria um modelo e popula o banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] com os dados mestres de sua empresa. Com base em permissões, os usuários podem fazer alterações nessa versão conforme necessário.  
  
2.  Quando você desejar confirmar uma versão de modelo, bloqueie a versão de forma que somente os administradores de modelo possam atualizar os dados. Para obter mais informações, veja [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md). Se as notificações forem configuradas, uma notificação será enviada por email aos administradores de modelos sempre que o status da versão for alterado. Para obter mais informações, consulte [Configurar notificações por email &#40;Master Data Services&#41;](../../2014/master-data-services/configure-email-notifications-master-data-services.md).  
  
3.  Aplique regras de negócio aos dados da versão bloqueada e revise qualquer problema de validação. Se necessário, você poderá preencher informações ausentes ou reverter a transação que causou o problema. Poderá também desbloquear a versão para que os usuários façam alterações.  
  
4.  Quando todos os dados estiverem validados, confirme a versão e sinalize-a para ser usada por sistemas de assinatura. Não é possível fazer alterações em uma versão confirmada.  
  
5.  Copie a versão confirmada e notifique os usuários de que eles podem começar a trabalhar em uma nova versão do modelo.  
  
## <a name="sequential-or-simultaneous-versions"></a>Versões sequenciais ou simultâneas  
 Você pode criar versões sequenciais ou simultâneas de seu modelo.  
  
-   **Versões sequenciais.** A cada vez que você confirmar uma versão, crie uma nova cópia e dê à versão o próximo número sequencial. Por exemplo, você pode copiar a **Versão 7** do modelo e nomear a cópia como **Versão 8**.  
  
-   **Versões simultâneas.** Crie versões simultâneas do seu modelo quando desejar trabalhar em duas ou mais versões dos seus dados ao mesmo tempo. Isso é útil quando sua empresa tem reorganizações ou fusões que coincidem com o curso normal de negócio e você deseja determinar como os novos dados mestre poderiam se ajustar em suas estruturas existentes.  
  
    > [!NOTE]  
    >  Uma configuração no [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] determina se você pode ou não copiar todas as versões ou somente as confirmadas. Para criar versões simultâneas você deve configurar o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] para permitir que você copie todas as versões. Esta configuração também está disponível na tabela de Configurações do Sistema. Para obter mais informações, veja [Configurações do sistema &#40;Master Data Services&#41;](../../2014/master-data-services/system-settings-master-data-services.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Alterar o nome de uma versão existente.|[Alterar um nome de versão &#40;Master Data Services&#41;](../../2014/master-data-services/change-a-version-name-master-data-services.md)|  
|Bloquear uma versão para que apenas os administradores possam editar seus dados.|[Bloquear uma versão &#40;Master Data Services&#41;](../../2014/master-data-services/lock-a-version-master-data-services.md)|  
|Desbloquear uma versão para que os usuários possam editar seus dados.|[Desbloquear uma versão &#40;Master Data Services&#41;](../../2014/master-data-services/unlock-a-version-master-data-services.md)|  
|Confirmar uma versão depois que os dados forem validados.|[Confirmar uma versão &#40;Master Data Services&#41;](../../2014/master-data-services/commit-a-version-master-data-services.md)|  
|Criar um novo sinalizador para marcar uma versão.|[Criar um sinalizador de versão &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-version-flag-master-data-services.md)|  
|Alterar o nome de um sinalizador de versão existente.|[Alterar o nome de um sinalizador de versão &#40;Master Data Services&#41;](../../2014/master-data-services/change-a-version-flag-name-master-data-services.md)|  
|Atribuir um sinalizador existente a uma versão.|[Atribuir um sinalizador a uma versão &#40;Master Data Services&#41;](../../2014/master-data-services/assign-a-flag-to-a-version-master-data-services.md)|  
|Criar uma nova cópia de uma versão existente|[Copiar uma versão &#40;Master Data Services&#41;](../../2014/master-data-services/copy-a-version-master-data-services.md)|  
|Excluir uma versão existente.|[Excluir uma versão &#40;Master Data Services&#41;](../../2014/master-data-services/delete-a-version-master-data-services.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   [Reverter uma transação &#40;Master Data Services&#41;](../../2014/master-data-services/reverse-a-transaction-master-data-services.md)  
  
-   [Notificações &#40;Master Data Services&#41;](../../2014/master-data-services/notifications-master-data-services.md)  
  
-   [Regras de negócio &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)  
  
  
