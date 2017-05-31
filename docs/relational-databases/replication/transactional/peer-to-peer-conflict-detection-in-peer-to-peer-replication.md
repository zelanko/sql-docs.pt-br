---
title: "Detecção de conflitos na replicação ponto a ponto | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transactional replication, peer-to-peer replication
- peer-to-peer transactional replication, conflict detection
ms.assetid: 754a1070-59bc-438d-998b-97fdd77d45ca
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: c2b248262e1344a7dc4652ed5d48aefa081a2f40
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="peer-to-peer---conflict-detection-in-peer-to-peer-replication"></a>Ponto a ponto – Detecção de conflitos na replicação ponto a ponto
  A replicação transacional ponto a ponto permite inserir, atualizar ou excluir dados em qualquer modo em uma topologia e faz com que as alterações de dados sejam propagadas para os outros nós. Uma vez que você pode alterar dados em qualquer nó, as alterações de dados em nós diferentes podem entrar em conflito umas com as outras. Se uma linha for modificada em mais de um nó, isso poderá causar um conflito ou mesmo uma atualização perdida quando a linha for propagada para outros nós.  
  
 A replicação ponto a ponto no [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] e em versões posteriores oferece a opção de habilitar a detecção de conflito em uma topologia ponto a ponto. Essa opção ajuda a evitar os problemas causados por conflitos não detectados, inclusive o comportamento inconsistente do aplicativo e as atualizações perdidas. Com essa opção habilitada, por padrão uma alteração de conflito é tratada como erro crítico que causa a falha do Agente de Distribuição. No evento de um conflito, a topologia é mantida em um estado inconsistente até que o conflito seja resolvido e os dados sejam tornados consistentes em toda a topologia.  
  
> [!NOTE]  
>  Para evitar inconsistência potencial de dados, certifique-se de evitar conflitos em uma topologia ponto a ponto, mesmo com a detecção de conflitos ativada. Para assegurar que as operações de gravação de uma linha particular sejam realizadas em um único nó, os aplicativos que acessam e alteram dados devem realizar operações de partição, inserção, atualização e exclusão. Esse particionamento assegurará que as modificações em uma determinada linha originária de um nó sejam sincronizadas com todos os outros nós da topologia antes que a linha seja modificada por um outro nó. Se um aplicativo requerer detecção de conflito e recursos de resolução sofisticados, use a replicação de mesclagem. Para obter mais informações, consulte [Mesclar a replicação](../../../relational-databases/replication/merge/merge-replication.md) e [Detectar e resolver conflitos na replicação de mesclagem](../../../relational-databases/replication/merge/advanced-merge-replication-resolve-merge-replication-conflicts.md).  
  
## <a name="understanding-conflicts-and-conflict-detection"></a>Entendendo conflitos e detecção de conflitos  
 Em um único banco de dados, as alterações feitas na mesma linha por aplicativos diferentes não causam um conflito. Isso ocorre uma vez que as transações são serializadas, e os bloqueios são usados para controlar as alterações simultâneas. Em um sistema distribuído assíncrono como a replicação ponto a ponto, as transações agem de maneira independente em cada nó e não há nenhum mecanismo para serializar as transações por diversos nós. Um protocolo como o protocolo 2PC pode ser usado, mas isso afeta o desempenho significativamente.  
  
 Em sistemas como replicação ponto a ponto, os conflitos não são detectados quando as alterações são confirmadas em pontos individuais. Ao contrário, eles são detectados quando essas alterações são replicadas e aplicadas em outros pontos. Na replicação ponto a ponto, os conflitos são detectados pelos procedimentos armazenados que se aplicam a alterações em cada nó, com base em uma coluna oculta em cada tabela publicada. Essa coluna oculta armazena uma ID que combina uma *ID de originador* que você especifica para cada nó e a versão da linha. Durante a sincronização, o Agente de Distribuição executa procedimentos para cada tabela. Esses procedimentos aplicam operações de inserção, atualização e exclusão de outros pontos. Se um dos procedimentos detectar um conflito quando ele ler o valor de coluna oculta, ocorrerá o erro 22815 que tem um nível de severidade de 16:  
  
 `A conflict of type '%s' was detected at peer %d between peer %d (incoming), transaction id %s  and peer %d (on disk), transaction id %s`  
  
 Por padrão, esse erro faz o Agente de Distribuição pare de aplicar alterações naquele nó. Para obter informações sobre como controlar os conflitos detectados, consulte "Controlando conflitos" posteriormente neste tópico.  
  
> [!NOTE]  
>  A coluna oculta pode ser acessada somente por um usuário registrado pela conexão de administrador dedicada (DAC). Para obter informações sobre o DAC, consulte [Conexão de diagnóstico para administradores de banco de dados](../../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md).  
  
 A replicação ponto a ponto detecta os seguintes tipos de conflitos:  
  
-   Inserção-inserção  
  
     Todas as linhas em cada tabela que participa da replicação ponto a ponto são identificadas exclusivamente usando valores de chave primários. Um conflito inserção-inserção ocorre quando uma linha com o mesmo valor de chave é inserida em mais de um nó.  
  
-   Atualização-atualização  
  
     Ocorre quando a mesma linha foi atualizada em mais de um nó.  
  
-   Inserção-atualização  
  
     Ocorre se uma linha foi atualizada em um nó, mas a mesma linha foi excluída e, em seguida, reinserida em outro nó.  
  
-   Inserção-exclusão  
  
     Ocorre se uma linha foi excluída em um nó, mas a mesma linha foi excluída e, em seguida, reinserida em outro nó.  
  
-   Atualização-exclusão  
  
     Ocorre se uma linha foi atualizada em um nó, mas a mesma linha foi excluída em outro.  
  
-   Exclusão-exclusão  
  
     Ocorre quando uma linha foi excluída em mais de um nó.  
  
## <a name="enabling-conflict-detection"></a>Habilitando a detecção de conflito  
 Para usar detecção de conflito, todos os nós devem ser executados no [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] ou uma versão posterior, e a detecção deve estar habilitada para todos os nós. No [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] e versões posteriores, por padrão, a detecção de conflito é habilitada em [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. Recomendamos que você habilite a detecção, até mesmo em cenários nos quais você não espera nenhum conflito. A detecção de conflito pode ser habilitada e desabilitada usando os procedimentos armazenados do [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] ou [!INCLUDE[tsql](../../../includes/tsql-md.md)] :  
  
-   Você pode habilitar e desabilitar a detecção no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] usando a página **Opções de Assinatura** da caixa de diálogo **Propriedades de Publicação** ou a página **Configurar Topologia** do Assistente para Configurar Topologia Ponto a Ponto. Para obter mais informações, consulte [Conflict Detection in Peer-to-Peer Replication](../../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).  
  
     Se você configurar a detecção de conflito usando o [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)], o Agente de Distribuição será configurado para parar de aplicar as alterações quando um conflito for detectado.  
  
-   Você também pode habilitar e desabilitar a detecção usando os seguintes procedimentos armazenados: [sp_addpublication](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) ou [sp_configure_peerconflictdetection](../../../relational-databases/system-stored-procedures/sp-configure-peerconflictdetection-transact-sql.md).  
  
     Se você configurar a detecção de conflito usando os procedimentos armazenados, poderá especificar se o Agente de Distribuição deve parar de aplicar as alterações quando um conflito for detectado. O padrão é o agente parar. Recomendamos o uso da configuração padrão.  
  
## <a name="handling-conflicts"></a>Controlando conflitos  
 Quando ocorrer um conflito na replicação ponto a ponto, o alerta de detecção de conflito ponto a ponto é emitido. Recomendamos que você configure esse alerta de forma que você seja notificado quando ocorrer um conflito. Para obter mais informações sobre alertas, consulte [Usar alertas para eventos do agente de replicação](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md).  
  
 Depois que o Agente de Distribuição parar e o alerta for emitido, use uma das abordagens a seguir para controlar os conflitos ocorridos:  
  
-   Reinicialize o nó no qual o conflito foi detectado a partir do backup de um nó que contém os dados obrigatórios (a abordagem recomendada). Esse método garante que os dados estejam em um estado consistente.  
  
-   Tente sincronizar o nó novamente permitindo que o Agente de Distribuição continue a aplicar as alterações:  
  
    1.  Execute [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md): especifique “p2p_continue_onconflict” para o parâmetro @property e **true** para o parâmetro @value.  
  
    2.  Reinicie o Agente de Distribuição.  
  
    3.  Verifique os conflitos detectados usando o visualizador de conflitos e determine as linhas que foram envolvidas, o tipo de conflito e o vencedor. O conflito é resolvido com base no valor da ID do originador especificado durante a configuração: a linha originada no nó com a ID mais alta vence o conflito. Para obter mais informações, consulte [Exibir conflitos de dados em publicações transacionais &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/view-data-conflicts-for-transactional-publications-sql-server-management-studio.md).  
  
    4.  Execute a validação para garantir que as linhas de conflito se encontraram corretamente. Para obter mais informações, consulte [Validar os dados replicados](../../../relational-databases/replication/validate-replicated-data.md).  
  
        > [!NOTE]  
        >  Se os dados forem inconsistentes depois dessa etapa, você deve atualizar manualmente as linhas no nó que tem a prioridade mais alta e, em seguida, permitir que as alterações propagem a partir desse nó. Se não houver nenhuma outra alteração conflitante na topologia, todos os nós serão levados para um estado consistente.  
  
    5.  Execute [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md): especifique “p2p_continue_onconflict” para o parâmetro @property e **false** para o parâmetro @value.  
  
## <a name="see-also"></a>Consulte também  
 [Peer-to-Peer Transactional Replication](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
