---
title: Opções do artigo para replicação transacional | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- articles [SQL Server replication], transactional replication options
- transactional replication, article options
ms.assetid: 3469b185-0ea5-4690-a71c-717230d886b6
caps.latest.revision: 29
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9be81144ab7d2653a050ce36f06bd16211a589cd
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37270512"
---
# <a name="article-options-for-transactional-replication"></a>Opções de artigo para replicação transacional
  Há vários um número de opções para artigos em publicações transacionais. Com a replicação transacional, você pode fazer o seguinte:  
  
-   Especificar como as alterações são propagadas do Publicador para os Assinantes. Para obter mais informações, consulte [Especificar como as alterações são propagadas para artigos transacionais](transactional-articles-specify-how-changes-are-propagated.md).  
  
-   Especificar que a execução de um procedimento armazenado seja replicada. Isso é útil ao replicar os resultados de procedimentos armazenados orientados a manutenção que afetam grandes quantidades de dados. Para saber mais, confira [Publishing Stored Procedure Execution in Transactional Replication](publishing-stored-procedure-execution-in-transactional-replication.md).  
  
-   Especificar opções de esquema se as restrições e os gatilhos são copiados para o Assinante. Para obter mais informações, veja [Especificar opções de esquema](../publish/specify-schema-options.md).  
  
-   Usar filtros de linha e filtros de coluna. Filtrar artigos de tabela lhe permite criar partições de dados a serem publicados. Para obter mais informações, consulte [Filter Published Data](../publish/filter-published-data.md) (Filtrar dados publicados).  
  
## <a name="see-also"></a>Consulte também  
 [Publicar dados e objetos de banco de dados](../publish/publish-data-and-database-objects.md)  
  
  
