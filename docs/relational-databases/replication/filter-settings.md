---
title: "Configura&#231;&#245;es de Filtro | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.monitor.filtersettings.f1"
ms.assetid: 1b401d7d-db8a-4ba1-acb1-b8dec14e3311
caps.latest.revision: 6
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 6
---
# Configura&#231;&#245;es de Filtro
  O **configurações de filtro** caixa de diálogo permite que você defina filtros para grades no Replication Monitor. Por exemplo, para mostrar somente as assinaturas que estão ativas no **todas as assinaturas** Selecione **Status** do **nome de coluna** coluna, **é igual a** do **operador** coluna, e **Active** do **Value1** coluna. Depois de definir um filtro com base em uma ou mais colunas, o filtro é aplicado para que a grade exiba somente o subconjunto de linhas que corresponda aos critérios do filtro.  
  
## Opções  
 **Nome da coluna**  
 Selecione o nome da coluna na qual você pretende aplicar o filtro. Você pode basear um filtro em uma ou mais colunas.  
  
 **Operador**  
 Selecione um operador para o filtro, como **menor ou igual a**.  
  
 **Value1** e **valor2**  
 Insira ou selecione um valor para o filtro. A maioria dos operadores só exige um valor no **Value1** coluna, mas a **entre** e **não entre** operadores também exige um valor no **Value2** coluna.  
  
 **Limpar Filtro**  
 Clique neste botão para limpar todos os filtros definidos. Para remover um único filtro, selecione a linha do filtro e pressione a tela Delete.  
  
## Consulte também  
 [Replicação de monitoramento](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  