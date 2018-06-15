---
title: Assinaturas atualizáveis para replicação transacional | Microsoft Docs
ms.custom: ''
ms.date: 07/21/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, updatable subscriptions
- updatable subscriptions, about updatable subscriptions
- queued updating subscriptions [SQL Server replication]
- immediate updating subscriptions
- subscriptions [SQL Server replication], updatable
- updatable subscriptions
ms.assetid: 8eec95cb-3a11-436e-bcee-bdcd05aa5c5a
caps.latest.revision: 60
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d52ee6d23418e83fb19a9029efe615b0f796f5e8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32964311"
---
# <a name="updatable-subscriptions---for-transactional-replication"></a>Assinaturas atualizáveis – para a replicação transacional
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

    
> [!NOTE]  
>  Este recurso permanecerá com suporte em versões do [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] de 2012 até 2016. [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 Replicação transacional oferece suporte para atualizações em Assinantes por meio de assinaturas atualizáveis e replicação ponto a ponto. A seguir, dois tipos de assinaturas atualizáveis:  
  
-   Atualização imediata. O Publicador e o Assinante devem estar conectados para atualizar dados no Assinante.  
  
-   A atualização em fila do Publicador e Assinante não precisa estar conectada para atualizar dados no Assinante. As atualizações podem ser feitas enquanto o Assinante ou o Publicador está offline.  
  
 Quando os dados são atualizados em um Assinante, eles são primeiro propagados para o Publicador e, então, para outros Assinantes. Se a atualização imediata for usada, as alterações são propagadas imediatamente usando-se o protocolo de confirmação de duas fases. Se a atualização enfileirada for usada, as alterações são armazenadas em uma fila; as transações enfileiradas são então aplicadas de forma assíncrona no Publicador sempre que a conectividade de rede estiver disponível. Como as atualizações são propagadas de forma assíncrona para o Publicador, os mesmos dados podem ter sido atualizados pelo Publicador ou por outro Assinante, podendo ocorrer conflitos ao se aplicar as atualizações. Conflitos são detectados e resolvidos de acordo com uma política de resolução de conflito estabelecida quando a publicação é criada.  
  
 Se você criar uma publicação transacional com assinaturas atualizáveis no Assistente para Nova Publicação, tanto a atualização imediata quanto a enfileirada são habilitadas. Se você criar uma publicação com procedimentos armazenados, é possível habilitar uma ou ambas as opções. Ao criar uma assinatura para a publicação, você especifica o modo de atualização a ser usado. É possível então alternar entre modos de atualização se necessário. Para obter mais informações, consulte a seguinte seção "Alternando entre modos de atualização".  
  
 Para habilitar assinaturas atualizáveis para publicações transacionais, [Enable Updating Subscriptions for Transactional Publications](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
 Para criar assinaturas atualizáveis para publicações transacionais, consulte [Criar uma assinatura atualizável para uma publicação transacional (Management Studio)](../../../relational-databases/replication/publish/create-an-updatable-subscription-to-a-transactional-publication.md) 
  
## <a name="switching-between-update-modes"></a>Alternando entre modos de atualização  
 Ao usar assinaturas atualizáveis você pode especificar que uma assinatura use um modo de atualização e, então, passe para o outro se o aplicativo assim o exigir. Por exemplo, é possível especificar que uma assinatura use atualização imediata, mas alterne para atualização enfileirada se uma falha do sistema resultar na perda de conectividade de rede.  
  
> [!NOTE]  
>  Replicação não alterna automaticamente entre modos de atualização. Você deve definir o modo de atualização por meio do SQL Server Management Studio ou seu aplicativo deve chamar [sp_setreplfailovermode &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql.md) para alternar entre os modos.  
  
 Se você alternar de atualização imediata para atualização enfileirada, não é possível alternar de volta para atualização imediata até que o Assinante ou Publicador esteja conectado e o Agente de Leitor de Fila tenha aplicado todas as mensagens pendentes na fila para o Publicador.  
  
 **Para alternar entre modos de atualização**  
  
 Para alternar entre modos de atualização, deve-se habilitar a publicação e a assinatura para ambos os modos de atualização e, então, alternar entre eles, se necessário. Para obter mais informações, consulte  
[Switch Between Update Modes for an Updatable Transactional Subscription](../../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md).  
  
### <a name="considerations-for-using-updatable-subscriptions"></a>Considerações para o uso de assinaturas atualizáveis  
  
-   Depois que uma publicação é habilitada para assinaturas de atualização ou assinaturas de atualização enfileiradas, a opção não pode ser desabilitada para a publicação (embota assinaturas não precisem usá-la). Para desabilitar a opção, a publicação deve ser excluída e uma nova deve ser criada.  
  
-   Dados de republicação não oferecem suporte.  
  
-   A replicação adiciona a coluna **msrepl_tran_version** a tabelas publicadas para propósitos de rastreamento. Devido à coluna adicional, todas as instruções **INSERT** devem incluir uma lista de colunas.  
  
-   Para efetuar alterações de esquema em uma tabela em uma publicação que ofereça suporte a assinaturas de atualização, toda a atividade na tabela deve ser interrompida no Publicador e Assinantes, e alterações de dados pendentes devem ser propagadas a todos os nós antes de fazer qualquer alteração de esquema. Isso assegura que transações pendentes não entrem em conflito com a alteração de esquema pendente. Depois que as alterações de esquema tenham se propagado para todos os nós, a atividade pode ser retomada nas tabelas publicadas. Para obter mais informações, consulte [Como confirmar uma topologia de replicação &#40;Programação Transact-SQL de replicação&#41;](../../../relational-databases/replication/administration/quiesce-a-replication-topology-replication-transact-sql-programming.md).  
  
-   Se você planeja alternar entre modos de atualização, o Agente de Leitor de Fila deve ser executado pelo menos uma vez depois de a assinatura ser inicializada (por padrão, o Agente de Leitor de Fila é executado de forma contínua).  
  
-   Se o banco de dados do Assinante for particionado horizontalmente e houver linhas na partição que existam no Assinante, mas não no Publicador, o Assinante não pode atualizar as linhas preexistentes. A tentativa de atualizar essas linhas retorna um erro. As linhas devem ser excluídas da tabela e, então, adicionadas ao Publicador.  

-   A replicação transacional com assinantes atualizáveis na fila pode apresentar um desempenho lento quando índices exclusivos filtrados são usados. Se ocorrer um conflito em um artigo que tem índices filtrados exclusivos e a resolução de conflitos levaria a exclusões e inserções adicionais no assinante para as linhas que não são cobertas pelo índice filtrado exclusivo.
  
### <a name="updates-at-the-subscriber"></a>Atualizações no Assinante  
  
-   Atualizações no Assinante são propagadas para o Publicador mesmo se uma assinatura tiver expirado ou estiver inativa. Assegure-se de que qualquer dessas assinaturas seja cancelada ou reinicializada.  
  
-   Se as colunas **TIMESTAMP** ou **IDENTITY** forem usadas e replicadas como seus tipos de dados básicos, os valores nessas colunas não devem ser atualizados no Assinante.  
  
-   Assinantes não podem atualizar ou inserir valores **text**, **ntext** ou **image** uma vez que não é possível ler das tabelas inseridas ou excluídas dentro dos gatilhos de replicação de controle de alterações. Da mesma forma, Assinantes não podem atualizar ou inserir valores **text** ou **image** usando **WRITETEXT** ou **UPDATETEXT** , porque os dados são substituídos pelo Publicador. Em vez disso, é possível particionar as colunas **text** e **image** em uma tabela separada e modificar as duas tabelas na transação.  
  
     Para atualizar objetos grandes em um assinante, use os tipos de dados **varchar(max)**, **nvarchar(max)** e **varbinary(max)** em vez dos tipos de dados **text**, **ntext**e **image** , respectivamente.  
  
-   Atualizações em chaves exclusivas (incluindo chaves primárias) que geram duplicatas (por exemplo, uma atualização do formato `UPDATE <column> SET <column> =<column>+1` ) não são permitidas e serão rejeitadas devido a uma violação de exclusividade. Isso ocorre porque atualizações configuradas feitas no Assinante são propagadas por replicação como instruções **UPDATE** individuais para cada linha afetada.  
  
-   Se o banco de dados do Assinante for particionado horizontalmente e houver linhas na partição que existam no Assinante, mas não no Publicador, o Assinante não pode atualizar as linhas preexistentes. A tentativa de atualizar essas linhas retorna um erro. As linhas devem ser excluídas da tabela e inseridas novamente.  
  
### <a name="user-defined-triggers"></a>Gatilhos definidos pelo usuário  
  
-   Se o aplicativo exige gatilhos no Assinante, os gatilhos devem ser definidos com a opção `NOT FOR REPLICATION` no Publicador e no Assinante. Isso assegura que gatilhos sejam acionados apenas para a alteração de dados original, mas não quando aquela alteração é reproduzida.  
  
     Verifique se o gatilho definido pelo usuário não é acionado quando o gatilho de replicação atualiza a tabela. Isso é feito usando-se o procedimento **sp_check_for_sync_trigger** no corpo do gatilho definido pelo usuário. Para obter mais informações, veja [sp_check_for_sync_trigger &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-check-for-sync-trigger-transact-sql.md).  
  
### <a name="immediate-updating"></a>Atualização imediata  
  
-   Para assinaturas de atualizações imediatas, alterações no Assinante são propagadas para o Publicador e aplicadas usando-se o MS DTC (Coordenador de Transações Distribuídas da Microsoft). Certifique-se de que o MS DTC está instalado e configurado no Publicador e no Assinante. Para obter mais informações, consulte a documentação do Windows.  
  
-   Os gatilhos usados por assinaturas de atualização imediatas exigem uma conexão com o Publicador para replicar alterações.  
  
-   Se a publicação permitir assinaturas de atualização imediata e um artigo na publicação tiver um filtro de coluna, não é possível filtrar colunas não anuláveis sem padrões.  
  
### <a name="queued-updating"></a>Atualização enfileirada  
  
-   Tabelas incluídas em uma publicação de mesclagem também não podem ser publicadas como parte de uma publicação transacional que permita assinaturas de atualização enfileirada.  
  
-   Atualizações feitas para colunas de chave primária não são recomendadas quando se usa atualização enfileirada, uma vez que a chave primária é usada como um localizador de registro para todas as consultas. Quando a política de resolução de conflito é definida como Assinante Vence, atualizações para chaves primárias devem ser feitas com cuidado. Se atualizações para a chave primária são feitas tanto no Publicador quanto no Assinante, o resultado será duas linhas com chaves primárias diferentes.  
  
-   Para colunas de tipo de dados **SQL_VARIANT**: quando os dados são inseridos ou atualizados no Assinante, eles são mapeados da seguinte forma pelo Agente de Leitor de Fila ao serem copiados do Assinante para a fila:  
  
    -   **BIGINT**, **DECIMAL**, **NUMERIC**, **MONEY**e **SMALLMONEY** são mapeados para **NUMERIC**.  
  
    -   **BINARY** e **VARBINARY** são mapeados para os dados **VARBINARY** .  
  
### <a name="conflict-detection-and-resolution"></a>Detecção de conflito e resolução  
  
-   Para a política de conflito Assinante Vence: resolução de conflito não oferece suporte para atualizações para colunas de chave primária.  
  
-   Conflitos devido a falhas de restrição de chave estrangeira não são resolvidos por replicação:  
  
    -   Se conflitos não são esperados e os dados são bem particionados (Assinantes não atualizam as mesmas linhas), é possível usar restrições de chave estrangeira no Publicador e Assinante.  
  
    -   Se conflitos são esperados: não se deve usar restrições de chave estrangeira no Publicador ou Assinante se usar resolução de conflito "Assinante vence"; não se deve usar restrições de chave estrangeira no Assinante se você usar resolução de conflito "Publicador vence".  
  
## <a name="see-also"></a>Consulte Também  
 [Peer-to-Peer Transactional Replication](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [Tipos de publicação para a Replicação Transacional](../../../relational-databases/replication/transactional/publication-types-for-transactional-replication.md)   
 [Publicar dados e objetos de banco de dados](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Assinar publicações](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  
