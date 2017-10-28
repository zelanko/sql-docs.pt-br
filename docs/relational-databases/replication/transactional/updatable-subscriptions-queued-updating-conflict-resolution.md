---
title: "Resolução e detecção de conflitos de atualização na fila | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- conflict resolution [SQL Server replication], queued updating subscriptions
- viewing queued updating conflicts
- conflict resolution [SQL Server replication]
- queued updating subscriptions [SQL Server replication]
- articles [SQL Server replication], conflict resolution
ms.assetid: 084ac587-25e7-4bd0-a385-556bbe07d02f
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 666ad0200e8429c470772fc68110d14a7809d12a
ms.contentlocale: pt-br
ms.lasthandoff: 07/31/2017

---
# <a name="updatable-subscriptions---queued-updating-conflict-resolution"></a>Assinaturas atualizáveis – Resolução de conflitos com atualização em fila
  Como as assinaturas de atualização em fila permitem modificações nos mesmos dados em vários locais, pode haver conflitos quando os dados forem sincronizados no Publicador. A replicação detecta todos os conflitos quando alterações são sincronizadas com o Publicador, resolvendo-os por meio da política de resolução selecionada durante a criação da publicação. Podem ocorrer os seguintes conflitos:  
  
-   Conflitos de atualização e inserção. Esse conflito acontece quando os mesmos dados são alterados em dois locais. Uma alteração vence e a outra perde.  
  
-   Conflitos de exclusão. Esses conflitos ocorrem quando a mesma linha é excluída em um local e alterada em outro.  
  
 A detecção e resolução de conflitos pode ser um processo demorado e que utiliza muitos recursos. No entanto, é o que há de melhor para reduzir os conflitos no aplicativo, por criar partições de dados, de modo que os vários Assinantes modifiquem diferentes subconjuntos de dados.  
  
## <a name="detecting-conflicts"></a>Conflitos de detecção  
 Ao criar uma publicação e ativar atualizações em fila, a replicação adiciona uma coluna **uniqueidentifier** (**msrepl_tran_version**) com o padrão de **newid()** à tabela subjacente. Quando os dados publicados são alterados tanto no Publicador quando no Assinante, a linha recebe um GUID (Globally Unique Identifier) para indicar que existe uma nova versão de linha. O Queue Reader Agent usa essa coluna durante a sincronização para determinar se há um conflito.  
  
 Uma transação em uma fila mantém os valores de versão de linha antigos e novos. Quando a transação é aplicada ao Publicador, os GUIDs da transação e o GUID da publicação são comparados. Se um GUID antigo, armazenado na transação, corresponder ao GUID da publicação,a publicação é atualizada e a linha é atribuída ao novo GUID que foi gerado pelo Assinante. Pela atualização da publicação com o GUID da transação, obtêm-se versões de linha correspondentes na publicação e na transação.  
  
 Se um GUID antigo, armazenado na transação, não corresponder ao GUID da publicação, será detectado um conflito. O novo GUID da publicação indica que há duas versões de linhas diferentes: uma na transação sendo submetida ao Assinante e uma mais nova que existe no Assinante. Nesse caso, outro Assinante ou o Publicador atualizou a mesma linha da publicação antes de a transação de Assinante ser sincronizada.  
  
 Diferentemente da replicação de mesclagem, o uso da coluna GUID não é destinado à identificação a própria linha, mas para verificar se a linha foi alterada.  
  
## <a name="resolving-conflicts"></a>Conflitos de resolução  
 Quando uma publicação é criada usando-se a atualização em fila, um resolvedor de conflitos é utilizado caso algum conflito seja detectado. O resolvedor de conflitos governa o modo pelo qual o Queue Reader Agent controla as diferentes versões da mesma linha, encontradas durante a sincronização. É possível alterar a política de resolução de conflitos após a criação da publicação, desde que não haja assinaturas para a publicação. As opções do resolvedor de conflitos são as seguintes:  
  
-   Publicador vence (padrão)  
  
-   O Publicador vence e a assinatura é reinicializada  
  
-   Assinante vence  
  
 Os conflitos são registrados e exibidos com o Visualizador de Conflitos.  
  
 **Para definir a política de resolução de conflitos de atualização em fila**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: [Definir opções de resolução de conflitos de atualização na fila &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/set-queued-updating-conflict-resolution-options-sql-server-management-studio.md)  
  
-   Programação Transact-SQL de replicação: [Habilitar atualização de assinaturas para publicações transacionais](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
 **Para exibir conflitos de dados**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: [Exibir conflitos de dados em publicações transacionais &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)  
  
### <a name="publisher-wins"></a>Publicador vence  
 Quando a resolução de conflito é definida como Publicador vence, a consistência transacional é mantida, com base nos dados do Publicador. A transação conflitante é revertida para o Assinante que a iniciou.  
  
 O Queue Reader Agent detecta um conflito e comandos de compensação são gerados e propagados para o Assinante por meio de postagem no banco de dados da distribuição. O Distribution Agent, em seguida, aplica os comandos de compensação para o Assinante que originou a transação conflitante. As ações de compensação atualizam as linhas no Assinante para que correspondam às do Publicador.  
  
 Até que os comandos de compensação sejam aplicados, é possível ler os resultados de uma transação que será, em algum momento futuro, revertida para o Assinante. Isto equivale a uma leitura suja (nível de isolamento de leitura não confirmada). Não há compensações para as transações dependentes subsequentes que venham a ocorrer. Contudo, os limites da transação são mantidos e todas as ações dentro da transação são igualmente confirmadas, ou, em caso de conflito, revertidas.  
  
### <a name="publisher-wins-and-the-subscription-is-reinitialized"></a>O Publicador vence e a assinatura é reinicializada  
 Reinicializar o Assinante para resolver conflitos mantém uma consistência transacional explícita no Assinante, mas pode despender muito tempo caso a publicação contenha grandes quantidades de dados.  
  
 Quando o Queue Reader Agent detecta um conflito, todas as transações restantes na fila (inclusive a transação em conflito) são rejeitadas e o Assinante é marcado para reinicialização. O próximo instantâneo gerado para a publicação é aplicado pelo Distribution Agent para o Assinante.  
  
### <a name="subscriber-wins"></a>Assinante vence  
 A detecção de conflitos segundo a política Assinante vence significa que a última transação de Assinante que atualizar o Publicador vence. Nesse caso, quando um conflito é detectado, a transação enviada pelo Assinante ainda é usada, e o Publicador é atualizado. Essa política é adequada para aplicativos em que essas alterações não comprometem a integridade de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  

