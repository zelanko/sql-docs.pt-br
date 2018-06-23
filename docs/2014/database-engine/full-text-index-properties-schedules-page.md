---
title: Propriedades do índice de texto completo (página agendas) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-search
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.fulltextsearch.fulltextindexproperties.schedule.f1
ms.assetid: a828e284-097e-4854-8c49-931934eb73bf
caps.latest.revision: 15
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: e564784e5f3fcae652068dcb200a805062a5e6bf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013394"
---
# <a name="full-text-index-properties-schedules-page"></a>Propriedades do Índice de Texto Completo (página Agendas)
  Use esta página para exibir e criar agendas para executar um trabalho do SQL Server Agent que inicia uma população incremental de atualizações na tabela base do índice de texto completo. Se a tabela base ou exibição não contiver uma coluna do `timestamp` tipo de dados, uma população completa é executada.  
  
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
  
  