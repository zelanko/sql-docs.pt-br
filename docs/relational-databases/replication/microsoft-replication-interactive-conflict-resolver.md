---
title: "Resolvedor Interativo de Conflitos de Replica&#231;&#227;o da Microsoft | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.replconflictviewer.interactiveresolver.f1"
ms.assetid: d3d4a480-782b-4b1d-b839-565c8cf6cb24
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# Resolvedor Interativo de Conflitos de Replica&#231;&#227;o da Microsoft
  O Resolvedor Interativo de Conflitos de Replicação pode ser usado para assinaturas de mesclagem sincronizadas usando o Gerenciador de Sincronização do Windows. Ele permite exibir, comparar, editar e selecionar o resultado dos conflitos de dados. A replicação também inclui o Visualizador de Conflitos, que permite exibir e modificar resultados de conflitos depois de terem sido confirmados. O Resolvedor Interativo de Conflitos permite selecionar o resultado durante a sincronização.  
  
> [!NOTE]  
>  Os conflitos que envolvem registros lógicos não são exibidos no Resolvedor Interativo. Para exibir informações sobre esses conflitos, use procedimentos armazenados de replicação. Para obter mais informações, consulte [Exibir informações de conflito para publicações de mesclagem e 40; Programação Transact-SQL de replicação e 41;](../../relational-databases/replication/view conflict information for merge publications.md).  
  
## Opções  
 **Nome da coluna**  
 O nome de todas as colunas na tabela. Uma ou mais colunas podem ter dados conflitantes. Independentemente de quais colunas estejam em conflito, toda a linha vencedora substituirá toda a linha perdedora.  
  
 **Resolução Sugerida**  
 A resolução sugerida fornecida pelo resolvedor de conflitos para o artigo.  
  
 **Publicador**  
 O valor dos dados no Publicador.  
  
 **Assinante**  
 O valor dos dados no Assinante.  
  
 **Aceitar sugestão**, **Aceitar publicador**, e **Aceitar assinante**  
 Clique para aceitar a linha que será aplicada no Publicador ou no Assinante, dependendo de quem perderá o conflito. Se o Publicador perder o conflito, todos os outros Assinantes receberão a linha vencedora da próxima vez em que sincronizarem com o Publicador.  
  
 **Resolver conflitos restantes automaticamente**  
 Resolva todos os conflitos restantes usando a resolução sugerida fornecida pelo resolvedor de conflitos para o artigo.  
  
 **Registrar em log os detalhes do conflito para referência futura**  
 Registra os detalhes do conflito em tabelas do sistema.  
  
## Consulte também  
 [Resolução de conflito interativo](../../relational-databases/replication/merge/interactive-conflict-resolution.md)   
 [Exibir e resolver conflitos de dados para publicações de mesclagem e 40; SQL Server Management Studio e 41;](../../relational-databases/replication/view and resolve data conflicts for merge publications.md)   
 [Sincronizar uma assinatura usando o Gerenciador de sincronização do Windows & #40. O Gerenciador de sincronização do Windows & 41;](../../relational-databases/replication/synchronize a subscription using windows synchronization manager.md)   
 [Detecção e resolução de conflito de replicação de mesclagem avançada ](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  