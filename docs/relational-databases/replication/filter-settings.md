---
title: "Configurações de filtro | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.monitor.filtersettings.f1
ms.assetid: 1b401d7d-db8a-4ba1-acb1-b8dec14e3311
caps.latest.revision: "6"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 533c2c34fb3ed456052eb98e4ff07a454c842691
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="filter-settings"></a>Configurações de Filtro
  A caixa de diálogo **Configurações de Filtro** permite que você defina filtros para grades no Replication Monitor. Por exemplo, para mostrar somente as assinaturas ativas na guia **Todas as Assinaturas** , selecione **Status** na coluna **Nome da Coluna** , **Igual** na coluna **Operador** e **Ativo** na coluna **Value1** . Depois de definir um filtro com base em uma ou mais colunas, o filtro é aplicado para que a grade exiba somente o subconjunto de linhas que corresponda aos critérios do filtro.  
  
## <a name="options"></a>Opções  
 **Nome da Coluna**  
 Selecione o nome da coluna na qual você pretende aplicar o filtro. Você pode basear um filtro em uma ou mais colunas.  
  
 **Operador**  
 Selecione um operador para o filtro, como **Menor que ou Igual a**.  
  
 **Value1** e **Value2**  
 Insira ou selecione um valor para o filtro. A maioria dos operadores só exige um valor na coluna **Value1** , mas os operadores **Entre** e **Não Entre** também requerem um valor na coluna **Value2** .  
  
 **Limpar Filtro**  
 Clique neste botão para limpar todos os filtros definidos. Para remover um único filtro, selecione a linha do filtro e pressione a tela Delete.  
  
## <a name="see-also"></a>Consulte também  
 [Monitorando a Replicação](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
