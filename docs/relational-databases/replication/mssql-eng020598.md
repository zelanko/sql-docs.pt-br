---
title: "MSSQL_ENG020598 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "erro MSSQL_ENG020598"
ms.assetid: 1c3032f2-23d1-4ead-94ee-16ac4d75cd0c
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# MSSQL_ENG020598
    
## Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|20598|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|A linha não foi encontrada no Assinante ao aplicar o comando replicado.|  
  
## Explicação  
 Esse erro ocorre na replicação transacional quando o Distribution Agent tenta atualizar uma linha no Assinante, mas a linha foi excluída ou a chave primária da linha foi alterada. Por padrão, os Assinantes de publicações transacionais devem ser tratados como somente leitura, porque as alterações não são propagadas de volta para o Publicador. Para a replicação transacional, as alterações do usuário devem ser realizadas no Assinante somente se forem usadas assinaturas que podem ser atualizadas ou replicação ponto a ponto (P2P). Para obter informações sobre essas opções, consulte [assinaturas atualizáveis para replicação transacional](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md) e [replicação transacional ponto a ponto](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
## Ação do usuário  
 **Para resolver esse problema:**  
  
1.  Se a replicação deve continuar enquanto você identifica a origem do erro, especifique o parâmetro **- SkipErrors 20598** para o Distribution Agent. Isso permite que o agente ignore alterações que resultem no erro 20598, enquanto permite que outras alterações sejam replicadas.  
  
2.  Identifique quais linhas no Assinante foram excluídas ou possuem uma chave primária diferente daquela das linhas correspondentes no Publicador. Você pode usar o [utilitário tablediff](../../tools/tablediff-utility.md) para determinar quais linhas são diferentes dos bancos de dados de publicação e assinatura. Para obter informações sobre como usar esse utilitário com bancos de dados replicados, consulte [Comparar tabelas replicadas para diferenças & #40. Programação de replicação e 41;](../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md).  
  
3.  Corrija as linhas no assinante usando o **tablediff** utilitário ou outro método.  
  
4.  (Opcional) Remover o **- SkipErrors** parâmetro.  
  
## Consulte também  
 [Erros e eventos referência & #40. Replicação e 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  