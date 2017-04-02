---
title: "Definir Filtros | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.replconflictviewer.definefilters.f1"
helpviewer_keywords: 
  - "caixa de diálogo Definir Filtros"
ms.assetid: 1fa71d22-ce5a-4aae-ba05-4d755842aeac
caps.latest.revision: 18
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 18
---
# Definir Filtros
  A caixa de diálogo **Definir Filtros** permite que você defina filtros que são aplicados em conflitos de dados para consultar um subconjunto dos conflitos na grade. Para definir um filtro, escolha um operador do **operador** lista suspensa caixa e, em seguida, insira um valor. Por exemplo, para mostrar somente conflitos nos quais o perdedor de conflito é servidor **ReplTest1**, selecione **igual a** do **operador** lista suspensa caixa e digite **ReplTest1** na primeira **valor** coluna.  
  
## Opções  
 **Operador**  
 Selecione um operador para o filtro, como **menor ou igual a**.  
  
 **Valor**  
 Insira um valor para o filtro. A maioria dos operadores só exige um valor na primeira coluna **Valor** , mas os operadores **Entre** e **Não Entre** requerem um valor em ambas as coluna **Valor** .  
  
 **Liberada**  
 Clique nesse botão para limpar todos os filtros anteriormente definidos.  
  
## Consulte também  
 [Visualizador de conflitos de replicação da Microsoft & #40. Replicação de mesclagem e 41;](../../relational-databases/replication/microsoft-replication-conflict-viewer-merge-replication.md)   
 [Visualizador de conflitos de replicação da Microsoft & #40. Replicação transacional e 41;](../../relational-databases/replication/microsoft-replication-conflict-viewer-transactional-replication.md)  
  
  