---
title: Relação de Sincronização de Entidade
description: A sincronização de entidade é uma sincronização unidirecional e reproduzível entre as versões de entidade, o que permite que você compartilhe dados de entidade entre modelos de Master Data Services.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: bd627a2d-dc64-47e9-9a71-2d0ad04b4962
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: a8072ca35b1676a5bace4fe60f70e7cfdbc0778b
ms.sourcegitcommit: 7d6eb09588ff3477cf39a8fd507d537a603bc60d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/16/2020
ms.locfileid: "84796291"
---
# <a name="entity-sync-relationship-master-data-services"></a>Relacionamento de Sincronização de Entidade (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  A sincronização de entidade é uma sincronização unidirecional e repetível entre versões da entidade. Ela o habilita a compartilhar dados de entidade entre diferentes modelos. Você pode manter uma única fonte de verdade em um modelo e reutilizar esses dados mestres em outros modelos. Por exemplo, você pode armazenar dados de estados dos EUA em entidade de um modelo e reutilizar esses dados em outros modelos.  
  
 Com a sincronização de entidade, você também pode fazer uma cópia única dos dados.  
  
 Todos os membros folha com atributos de arquivo e de forma livre da entidade de origem são sincronizados com a entidade de destino durante a execução da sincronização. Isso cria, exclui e modifica o esquema de entidade e os membros.  
  
 Após o estabelecimento de uma relação de sincronização, a entidade de destino pode ser modificada somente pelo processo de sincronização. Uma relação de sincronização pode ser removida a qualquer momento para tornar editável a entidade de destino.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar e executar uma relação de sincronização de entidade &#40;Master Data Services&#41;](../master-data-services/create-and-execute-an-entity-sync-relationship-master-data-services.md)   
 [Editar e excluir uma relação de sincronização de entidade &#40;Master Data Services&#41;](../master-data-services/edit-and-delete-an-entity-sync-relationship-master-data-services.md)  
  
  
