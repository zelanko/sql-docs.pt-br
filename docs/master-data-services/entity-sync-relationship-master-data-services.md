---
title: "Relação de Sincronização de Entidade (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bd627a2d-dc64-47e9-9a71-2d0ad04b4962
caps.latest.revision: 6
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 9abf874d3e813639f16e36b1ccc92cf178996f3a
ms.contentlocale: pt-br
ms.lasthandoff: 09/07/2017

---
# <a name="entity-sync-relationship-master-data-services"></a>Relacionamento de Sincronização de Entidade (Master Data Services)
  A sincronização de entidade é uma sincronização unidirecional e repetível entre versões da entidade. Ela o habilita a compartilhar dados de entidade entre diferentes modelos. Você pode manter uma única fonte de verdade em um modelo e reutilizar esses dados mestres em outros modelos. Por exemplo, você pode armazenar dados de estados dos EUA em entidade de um modelo e reutilizar esses dados em outros modelos.  
  
 Com a sincronização de entidade, você também pode fazer uma cópia única dos dados.  
  
 Todos os membros folha com atributos de arquivo e de forma livre da entidade de origem são sincronizados com a entidade de destino durante a execução da sincronização. Isso cria, exclui e modifica o esquema de entidade e os membros.  
  
 Após o estabelecimento de uma relação de sincronização, a entidade de destino pode ser modificada somente pelo processo de sincronização. Uma relação de sincronização pode ser removida a qualquer momento para tornar editável a entidade de destino.  
  
## <a name="see-also"></a>Consulte também  
 [Criar e executar uma relação de sincronização de entidade &#40;Master Data Services&#41;](../master-data-services/create-and-execute-an-entity-sync-relationship-master-data-services.md)   
 [Editar e excluir uma relação de sincronização de entidade &#40;Master Data Services&#41;](../master-data-services/edit-and-delete-an-entity-sync-relationship-master-data-services.md)  
  
  
