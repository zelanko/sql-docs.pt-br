---
title: Classificar colunas | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.monitor.sortcolumns.f1
ms.assetid: 66b44b6c-10a5-4e3f-a97b-7568609c88ac
caps.latest.revision: 7
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2580942a4a0cb482b499ab556a0c0dcb7c215d40
ms.lasthandoff: 04/11/2017

---
# <a name="sort-columns"></a>Classificar Colunas
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
  
## <a name="see-also"></a>Consulte também  
 [Monitorando a Replicação](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
