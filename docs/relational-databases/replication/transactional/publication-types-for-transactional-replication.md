---
title: Tipos de publicação para a replicação transacional | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, publications
ms.assetid: ad66aa34-3e37-401e-a6a1-fc1514eb6d50
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e17764a7a2d47ccbf9d2f35575818eb2efdf8dce
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47749354"
---
# <a name="publication-types-for-transactional-replication"></a>Tipos de publicação para Replicação Transacional
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  A Replicação Transacional oferece três tipos de publicação:  
  
|Tipo de Publicação|Descrição|  
|----------------------|-----------------|  
|Publicação Transacional padrão|Apropriada para topologias em que todos os dados do Assinante são do modo somente leitura (a replicação transacional não impõe isto no Assinante).<br /><br /> As publicações transacionais padrão são criadas por padrão ao usar Transact-SQL ou RMO (Replication Management Objects). Ao usar o Assistente para Nova Publicação, elas são criadas selecionando **Publicação Transacional** na página **Tipo de Publicação** .<br /><br /> Para obter mais informações sobre como criar publicações, veja [Publicar dados e objetos de banco de dados](../../../relational-databases/replication/publish/publish-data-and-database-objects.md).|  
|Publicação Transacional em uma topologia ponto a ponto|As características deste tipo de publicação são:<br /><br /> -Cada local tem dados idênticos e atua como um Publicador e Assinante.<br /><br /> -A mesma linha pode ser alterada apenas em um local de cada vez.<br /><br /> -Esta topologia é melhor adequada para ambientes de servidor que requerem alta disponibilidade e escalabilidade de leitura.<br /><br /> <br /><br /> Para obter mais informações, consulte [Peer-to-Peer Transactional Replication](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).|  
  
## <a name="see-also"></a>Consulte Também  
 [Replicação transacional](../../../relational-databases/replication/transactional/transactional-replication.md)  
  
  
