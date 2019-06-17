---
title: Propriedades da publicação, opções de assinatura | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.pubproperties.subscriptionoptions.f1
ms.assetid: 31abd605-b273-419d-86df-d0ecf539a507
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a204ee5d34e37736ddd433636cf0e86564718b77
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63047492"
---
# <a name="publication-properties-subscription-options"></a>Propriedades da Publicação, Opções de Assinatura
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  A página **Opções de Assinatura** da caixa de diálogo **Propriedades de Publicação** permite visualizar e definir propriedades de nível de publicação associadas a assinaturas. As propriedades são agrupadas nas categorias seguintes:  
  
-   Propriedades que se aplicam a todas as publicações.  
  
-   Propriedades que se aplicam a publicações de instantâneo e transacional (inclusive as que permitem assinaturas de atualização).  
  
-   Propriedades que se aplicam a publicações de mesclagem.  
  
> [!NOTE]  
>  Algumas propriedades são somente leitura; as razões são abrangidas nas descrições de propriedade neste tópico. Algumas alterações de propriedade requerem um novo instantâneo para a publicação e algumas requerem que todas as assinaturas sejam reiniciadas. Para obter mais informações, consulte [Alterar propriedade da publicação e do artigo](../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
## <a name="options-for-all-publications"></a>Opções para todas as publicações.  
  
### <a name="creation-and-synchronization"></a>Criação e sincronização  
 **Permitir assinaturas anônimas**  
 Determina se as assinaturas pull anônimas devem ser permitidas. Há suporte para assinaturas anônimas para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEWEd2005](../../includes/ssewed2005-md.md)], [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssMobileEd2005](../../includes/ssmobileed2005-md.md)]e [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para Windows CE. Para usar essa opção para publicações de instantâneo e transacional, a opção **Instantâneo sempre disponível** deve ser definida como **True**.  
  
 **Banco de dados de assinaturas anexável**  
 Para usar essa opção para publicações de instantâneo e transacional, a opção **Instantâneo sempre disponível** deve ser definida como **Verdadeiro** .  
  
> [!IMPORTANT]  
>  Assinaturas anexáveis não estarão disponíveis em uma versão futura. O recurso é preterido.  
  
 **Permitir assinaturas pull**  
 Determina se os Assinantes devem ou não ter permissão para criar assinaturas pull para essa publicação. Para obter mais informações, consulte [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md) (Assinar publicações).  
  
### <a name="schema-replication"></a>Replicação de esquema  
 **Replicar alterações de esquema**  
 Somente[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores. Determina se as alterações de esquema (como adicionar uma coluna a uma tabela ou alterar tipos de dados de uma coluna) devem ou não ser replicadas para objetos publicados. Para obter mais informações, consulte [Make Schema Changes on Publication Databases](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md) (Fazer alterações de esquema em bancos de dados de publicação).  
  
## <a name="options-for-snapshot-and-transactional-publications"></a>Opções para publicações transacionais e de instantâneo  
  
### <a name="creation-and-synchronization"></a>Criação e sincronização  
 **Independent Agente de Distribuição**  
 Determina se um agente independente de outras publicações deste banco de dados deve ser usado. Essa opção é somente leitura; Ela é definida como **Verdadeiro** por padrão, para publicações criadas com o Assistente para Nova Publicação e não pode ser alterada depois que a publicação é criada. Para obter mais informações, consulte [Replication Agent Administration](../../relational-databases/replication/agents/replication-agent-administration.md) (Administração do agente de replicação).  
  
 **Instantâneo sempre disponível**  
 Determina se são criados arquivos de instantâneo cada vez que o Agente de Instantâneo é executado (requer **Agente de Distribuição Independente**). Essa opção é somente leitura; ela será definida como **Verdadeiro** se você selecionar **Criar um instantâneo imediatamente e mantê-lo disponível para inicializar assinaturas** na página **Agente de Instantâneo** do Assistente para Nova Publicação (o padrão). Para obter mais informações, consulte [Create and Apply the Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md) (Criar e aplicar o instantâneo).  
  
 **Permitir inicialização com base nos arquivos de backup**  
 Somente o[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores. Determina se deve haver permissão para que os arquivos de backup sejam usados para inicializar assinaturas. Para obter mais informações, consulte [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
 **Permitir Assinantes não SQL Server**  
 Somente o[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores. Determina se a publicação é compatível com não assinantes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A definição dessa opção como **True** define outras propriedades da publicação como compatíveis com não assinantes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se houver assinaturas, essa opção será somente leitura; ela não poderá ser definida como **Verdadeiro** se **Permitir assinaturas de atualização imediata**, **Permitir assinaturas de atualização enfileirada**ou **Permitir assinaturas ponto a ponto** forem definidas como **Verdadeiro**. Para obter mais informações, consulte [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md).  
  
### <a name="data-transformation"></a>Transformação de dados  
 **Permitir transformações de dados**  
 Determina se DTS (Data Transformation Services) deve ser usado para transformar dados antes de distribuí-los a um Assinante. Essa opção é somente leitura; transformações de dados só poderão ser habilitadas se uma publicação for criada usando procedimentos armazenados.  
  
> [!IMPORTANT]  
>  Assinaturas transformáveis não estarão disponíveis em uma versão futura. O recurso é preterido.  
  
### <a name="peer-to-peer-replication"></a>Replicação ponto a ponto  
 **Permitir assinaturas ponto a ponto**  
 Aplica-se apenas ao [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores. Determina se a publicação oferece suporte a replicação ponto a ponto. Definir essa opção como **Verdadeiro** define outras propriedades de publicação para dar suporte a replicação ponto a ponto. Essa opção será somente leitura se existirem assinaturas. Essa opção não poderá ser definida como **Verdadeiro** se **Permitir assinaturas de atualização imediata** , **Permitir assinaturas de atualização enfileirada**ou **Permitir Assinantes não SQL Server** for definida como **Verdadeiro**. Para obter mais informações, consulte [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 **Permitir a detecção de conflitos ponto a ponto**  
 Aplica-se apenas ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versões posteriores. Especifica se a detecção de conflito está habilitada para esta publicação. Para usar detecção de conflitos, todos os nós devem ser executados no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou uma versão posterior, e a detecção deve estar habilitada para todos os nós. Para usar a detecção de conflitos, você também deve especificar um valor para **Identificação do originador do par**. Para obter mais informações, consulte [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).  
  
 **Identificação do originador do par**  
 Aplica-se apenas ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versões posteriores. Especifica uma ID para um nó em uma topologia ponto a ponto. Essa ID será usada para detecção de conflito se **Permitir a detecção de conflitos ponto a ponto** for definido como **Verdadeiro**. Especifique uma ID positiva, diferente de zero, que nunca foi usada na topologia. Para uma lista de IDs que já foram usadas, consulte a tabela do sistema [Mspeer_originatorid_history](../../relational-databases/system-tables/mspeer-originatorid-history-transact-sql.md) .  
  
### <a name="updatable-subscriptions"></a>Assinaturas Atualizáveis  
 **Permitir assinaturas de atualização imediata**  
 Determina se as alterações de dados do Assinante podem ser replicadas imediatamente para o Publicador. Essa opção é somente leitura; a atualização de assinaturas só pode ser habilitada quando uma publicação é criada. Para obter mais informações, consulte [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
 **Permitir assinaturas de atualização enfileirada**  
 Determina se as alterações de dados do Assinante podem ser enfileiradas e replicadas posteriormente para o Publicador. Essa opção é somente leitura; a atualização de assinaturas só pode ser habilitada quando uma publicação é criada. Para obter mais informações, consulte [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
 **Reportar conflitos centralmente**  
 Determina se as alterações de dados conflitantes devem ser informadas somente no Publicador ou no Publicador e no Assinante (requer a opção **Permitir assinaturas de atualização enfileirada**). Essa opção é somente leitura; Ela é definida como **Verdadeiro** por padrão, para publicações criadas com o Assistente para Nova Publicação e não pode ser alterada depois que a publicação é criada. Um valor de **Verdadeiro** significa que os conflitos só são informados no Publicador. Os conflitos só podem ser exibidos quando são informados.  
  
 **Política de resolução de conflito**  
 Especifica a ação a ser tomada quando uma alteração no Assinante conflita com uma alteração no Publicador (requer a opção **Permitir assinaturas de atualização enfileirada**). Para obter mais informações, consulte [Queued Updating Conflict Detection and Resolution](../../relational-databases/replication/transactional/updatable-subscriptions-queued-updating-conflict-resolution.md).  
  
 **Tipo de fila**  
 Determina se deve ser usada uma fila do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o MSMQ (Serviço de Enfileiramento de Mensagens) da [!INCLUDE[msCoName](../../includes/msconame-md.md)] para enfileirar alterações no Assinante até que possam ser aplicadas no Publicador (requer a opção **Permitir assinaturas de atualização enfileirada**). Essa opção só é relevante para o [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]; versões posteriores sempre usam tabelas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para filas.  
  
## <a name="options-for-merge-publications"></a>Opções para publicações de mesclagem  
  
### <a name="conflict-reporting"></a>Relatório de conflito  
 **Reportar conflitos centralmente**  
 Determina se as alterações de dados conflitantes devem ser informadas somente ao Publicador ou ao Publicador e ao Assinante. Essa opção é somente leitura; Ela é definida como **Verdadeiro** por padrão, para publicações criadas com o Assistente para Nova Publicação e não pode ser alterada depois que a publicação é criada. Um valor de **Verdadeiro** significa que os conflitos só são informados no Publicador. Os conflitos só podem ser exibidos quando são informados. Para obter mais informações, consulte a seção "Exibindo conflitos" em [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
### <a name="filtering"></a>Filtragem  
 **Permitir filtros com parâmetros**  
 Defina com base no uso ou não de filtros com parâmetros na publicação. Essa opção é sempre somente leitura. Para obter mais informações, consulte [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 **Validar Assinantes**  
 Determina quais funções usar ao validar que um Assinante tem a partição correta de dados. Separe valores múltiplos por vírgulas. Para obter mais informações, consulte [Validate Partition Information for a Merge Subscriber](../../relational-databases/replication/validate-partition-information-for-a-merge-subscriber.md) (Validar informações de partição para um assinante de mesclagem).  
  
 **Pré-calcular partições**  
 Somente o[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores. Determina se a sincronização deve ser otimizada calculando com antecedência quais linhas de dados pertencem a quais partições. Essa configuração assumira **Verdadeiro** como padrão, se a publicação atender aos critérios de partições pré-calculadas. Para obter mais informações, consulte [Optimize Parameterized Filter Performance with Precomputed Partitions](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md) (Otimizar o desempenho do filtro parametrizado com partições pré-computadas).  
  
 **Otimizar sincronização**  
 Determina se o processamento de mesclagem deve ser otimizado armazenando metadados adicional em cada Assinante. Essa otimização foi substituída por partições pré-computadas; a opção **Otimizar sincronização** só será relevante se **Pré- calcular partições** for definida como **Falso**. Para obter mais informações, consulte [Filtros de linha com parâmetros](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
### <a name="merge-processes"></a>Processos de mesclagem  
 **Limitar processos simultâneos**  
 Determina se o número de Agente de Mesclagems que podem executar ao mesmo tempo deve ser limitado. Isso geralmente é usado se uma publicação tiver muitas assinaturas push que possam ser sincronizadas ao mesmo tempo.  
  
 **Máximo de processos simultâneos**  
 O número máximo de Agente de Mesclagems que podem executar ao mesmo tempo (requer **Limitar processos simultâneos**). Se o número máximo de agentes em sincronização exceder o máximo, os agentes serão enfileirados até que o número fique abaixo do máximo.  
  
## <a name="see-also"></a>Consulte Também  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Exibir e modificar as propriedades da publicação](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
