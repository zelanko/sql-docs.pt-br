---
title: Propriedades do índice de texto completo (página agendas) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: search
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.fulltextindexproperties.schedule.f1
ms.assetid: a828e284-097e-4854-8c49-931934eb73bf
caps.latest.revision: 15
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 83eeb3ca9ea1f2e22f3d2dadf8089b8ba510c951
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37306226"
---
# <a name="full-text-index-properties-schedules-page"></a>Propriedades do Índice de Texto Completo (página Agendas)
  Use esta página para exibir e criar agendas para executar um trabalho do SQL Server Agent que inicia uma população incremental de atualizações na tabela base do índice de texto completo. Se a tabela base ou exibição não contiver uma coluna do `timestamp` de tipo de dados, uma população completa é executada.  
  
 **Para exibir ou alterar as propriedades de um índice de texto completo**  
  
-   [Administrar índices de texto completo](../relational-databases/indexes/indexes.md)  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **Agendas**  
 Lista cada população incremental agendada, se houver, na tabela base para o índice de texto completo.  
  
 **Nome**  
 Exibe o nome de cada população agendada.  
  
 **Tipo de população**  
 Exibe o tipo de cada população agendada.  
  
 **Enabled**  
 Indica se a população agendada está habilitada ou desabilitada atualmente.  
  
 **Descrição**  
 Exibe a descrição especificada quando a agenda foi criada.  
  
 **Nova**  
 Clique para criar uma nova agenda para popular o índice de texto completo.  
  
## <a name="see-also"></a>Consulte também  
 [Use o Assistente para indexação de texto completo](../relational-databases/search/use-the-full-text-indexing-wizard.md)   
 [Popular índices de texto completo](../relational-databases/search/populate-full-text-indexes.md)  
  
  
