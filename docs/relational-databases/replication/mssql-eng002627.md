---
title: MSSQL_ENG002627 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG002627 error
ms.assetid: 7f4136ac-3784-4a41-a98c-8a02308e4883
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 2c1939933c87ffe9519b0ca0656c83a02d952ec5
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68766555"
---
# <a name="mssqleng002627"></a>MSSQL_ENG002627
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|2627|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico|N/A|  
|Texto da mensagem|Violação da restrição %ls '%.*ls'. Não é possível inserir uma chave duplicada no objeto '%.\*ls'.|  
  
## <a name="explanation"></a>Explicação  
 Esse é um erro geral que pode ocorrer independentemente de um banco de dados ser ou não replicado. Nos bancos de dados replicados, esse erro geralmente ocorre porque as chaves primárias não foram gerenciadas corretamente na topologia. Em um ambiente distribuído, é essencial garantir que o mesmo valor não seja inserido em uma coluna de chave primária ou qualquer outra coluna exclusiva em mais de um nó. As causas possíveis podem ser:  
  
-   Inserções e atualizações em uma linha estão acontecendo em mais de um nó. A replicação de mesclagem e as assinaturas atualizáveis para replicação transacional oferecem detecção e resolução de conflitos, mas ainda é melhor inserir ou atualizar uma determinada linha apenas em um nó. O ponto a ponto transacional não oferece detecção e resolução de conflitos. Ele exige que as inserções e as atualizações sejam particionadas.  
  
-   Uma linha foi inserida em um Assinante que deveria ser somente leitura. Assinantes de publicações de instantâneo devem ser tratados como somente leitura, do mesmo modo que Assinantes de publicações transacionais, exceto se forem usadas assinaturas atualizáveis ou replicação transacional ponto a ponto.  
  
-   Uma tabela com uma coluna de identidade está sendo usada, mas a coluna não é gerenciada apropriadamente.  
  
## <a name="user-action"></a>Ação do usuário  
 A ação necessária depende do motivo que levou à ocorrência do erro:  
  
-   Inserções e atualizações em uma linha estão acontecendo em mais de um nó.  
  
     Independentemente do tipo de replicação usado, recomendamos o particionamento das atualizações e inserções sempre que possível para reduzir o processamento necessário para a detecção e a resolução de conflitos. Para a replicação transacional ponto a ponto, é necessário o particionamento de inserções e atualizações. Para obter mais informações, consulte [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
-   Uma linha foi inserida em um Assinante que deveria ser somente leitura.  
  
     Não insira ou atualize linhas no Assinante, exceto se estiver usando a replicação de mesclagem, a replicação transacional com assinaturas atualizáveis ou a replicação transacional ponto a ponto.  
  
-   Uma tabela com uma coluna de identidade está sendo usada, mas a coluna não é gerenciada apropriadamente.  
  
     Para replicação de mesclagem e replicação transacional com assinaturas atualizáveis, as colunas de identidade devem ser gerenciadas automaticamente por replicação. Para replicação transacional ponto a ponto, elas devem ser gerenciadas manualmente. Para obter mais informações, consulte [Replicar colunas de identidade](../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de erros e eventos &#40;Replicação&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Replicação de mesclagem](../../relational-databases/replication/merge/merge-replication.md)   
 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [Assinaturas atualizáveis para replicação transacional](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
