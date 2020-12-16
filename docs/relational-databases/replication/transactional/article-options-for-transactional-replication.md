---
description: Opções de artigo para replicação transacional
title: Opções do artigo para replicação transacional | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- articles [SQL Server replication], transactional replication options
- transactional replication, article options
ms.assetid: 3469b185-0ea5-4690-a71c-717230d886b6
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 1905b18ba3e32e80d53482d097683e0c8fa9e671
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97463137"
---
# <a name="article-options-for-transactional-replication"></a>Opções de artigo para replicação transacional
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  Há vários um número de opções para artigos em publicações transacionais. Com a replicação transacional, você pode fazer o seguinte:  
  
-   Especificar como as alterações são propagadas do Publicador para os Assinantes. Para obter mais informações, consulte [Especificar como as alterações são propagadas para artigos transacionais](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
-   Especificar que a execução de um procedimento armazenado seja replicada. Isso é útil ao replicar os resultados de procedimentos armazenados orientados a manutenção que afetam grandes quantidades de dados. Para obter mais informações, consulte [Publicando execução de procedimento armazenado em replicação transacional](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md).  
  
-   Especificar opções de esquema se as restrições e os gatilhos são copiados para o Assinante. Para obter mais informações, veja [Especificar opções de esquema](../../../relational-databases/replication/publish/specify-schema-options.md).  
  
-   Usar filtros de linha e filtros de coluna. Filtrar artigos de tabela lhe permite criar partições de dados a serem publicados. Para obter mais informações, consulte [Filter Published Data](../../../relational-databases/replication/publish/filter-published-data.md) (Filtrar dados publicados).  
  
## <a name="see-also"></a>Consulte Também  
 [Publicar dados e objetos de banco de dados](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
