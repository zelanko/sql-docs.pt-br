---
title: Classificar colunas | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.sortcolumns.f1
ms.assetid: 66b44b6c-10a5-4e3f-a97b-7568609c88ac
caps.latest.revision: 7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b699d8e81d79bd9364aaaa3efd892a2b28788988
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sort-columns"></a>Classificar Colunas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  A caixa de diálogo **Classificar Colunas** permite classificar grades no Replication Monitor com base em uma ou mais colunas. (Você também pode classificar uma única coluna clicando no cabeçalho de coluna na grade do Replication Monitor.) Por exemplo, para classificar assinaturas na guia **Todas as Assinaturas** com base no status e no tipo de conexão, siga estas etapas:  
  
1.  Na primeira linha da grade, selecione **Status** na coluna **Nome da Coluna** e um valor na coluna **Ordem de Classificação**  
  
2.  Na segunda linha da grade, selecione **Tipo de Conexão** na coluna **Nome da Coluna** e um valor na coluna **Ordem de Classificação**  
  
## <a name="options"></a>Opções  
 **Nome da Coluna**  
 O nome da coluna na qual você quer classificar. Você pode classificar em uma ou mais colunas. Você não pode classificar as colunas **Desempenho Médio Atual** ou **Pior Desempenho Atual** na guia **Publicações** por causa da forma pela qual essas colunas são calculadas.  
  
 **Ordem de Classificação**  
 Especifique um valor **Crescente** ou **Decrescente**.  
  
 **Limpar Tudo**  
 Remove todas as linhas da grade de classificação. Para remover uma única linha, selecione a linha e pressione a tecla Delete.  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorando a Replicação](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
