---
title: "Propriedades da Publica&#231;&#227;o, Op&#231;&#245;es de Assinatura | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newpubwizard.pubproperties.subscriptionoptions.f1"
ms.assetid: 31abd605-b273-419d-86df-d0ecf539a507
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# Propriedades da Publica&#231;&#227;o, Op&#231;&#245;es de Assinatura
  A página **Opções de Assinatura** da caixa de diálogo **Propriedades de Publicação** permite visualizar e definir propriedades de nível de publicação associadas a assinaturas. As propriedades são agrupadas nas categorias seguintes:  
  
-   Propriedades que se aplicam a todas as publicações.  
  
-   Propriedades que se aplicam a publicações de instantâneo e transacional (inclusive as que permitem assinaturas de atualização).  
  
-   Propriedades que se aplicam a publicações de mesclagem.  
  
> [!NOTE]  
>  Algumas propriedades são somente leitura; as razões são abrangidas nas descrições de propriedade neste tópico. Algumas alterações de propriedade requerem um novo instantâneo para a publicação e algumas requerem que todas as assinaturas sejam reiniciadas. Para obter mais informações, consulte [alterar propriedades da publicação e artigo](../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
## Opções para todas as publicações.  
  
### Criação e sincronização  
 **Permitir assinaturas anônimas**  
 Determina se as assinaturas pull anônimas devem ser permitidas. Há suporte para assinaturas anônimas para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEWEd2005](../../includes/ssewed2005-md.md)], [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssMobileEd2005](../../includes/ssmobileed2005-md.md)]e [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para Windows CE. Para usar essa opção para publicações de instantâneo e transacional, a opção **Instantâneo sempre disponível** deve ser definida como **True**.  
  
 **Banco de dados de assinaturas anexável**  
 Determina se as assinaturas podem ser criadas por anexar uma cópia de um banco de dados de assinatura (requer que a opção **instantâneo sempre disponível** é definido como **True** para instantâneo e publicações transacionais).  
  
> [!IMPORTANT]  
>  Assinaturas anexáveis não estarão disponíveis em uma versão futura. O recurso é preterido.  
  
 **Permitir assinaturas pull**  
 Determina se os Assinantes devem ou não ter permissão para criar assinaturas pull para essa publicação. Para obter mais informações, consulte [assinar publicações](../../relational-databases/replication/subscribe-to-publications.md).  
  
### Replicação de esquema  
 **Replicar alterações de esquema**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores. Determina se as alterações de esquema (como adicionar uma coluna a uma tabela ou alterar tipos de dados de uma coluna) devem ou não ser replicadas para objetos publicados. Para obter mais informações, consulte [fazer alterações de esquema em bancos de dados de publicação](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
## Opções para publicações transacionais e de instantâneo  
  
### Criação e sincronização  
 **Independent Agente de Distribuição**  
 Determina se um agente independente de outras publicações deste banco de dados deve ser usado. Essa opção é somente leitura; ele é definido como **True** por padrão para publicações criadas com o Assistente para nova publicação e não podem ser alteradas após a publicação é criada. Para obter mais informações, consulte [Administração do agente de replicação](../../relational-databases/replication/agents/replication-agent-administration.md).  
  
 **Instantâneo sempre disponível**  
 Determina se os arquivos de instantâneo são criados toda vez que o Snapshot Agent é executado (requer **agente de distribuição independente**). Essa opção é somente leitura; ele é definido como **True** se você selecionar **criar um instantâneo imediatamente e mantê-lo disponível para inicializar assinaturas** no **Snapshot Agent** página do Assistente de nova publicação (o padrão). Para obter mais informações, consulte [criar e aplicar o instantâneo](../../relational-databases/replication/create-and-apply-the-snapshot.md).  
  
 **Permitir inicialização com base nos arquivos de backup**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores. Determina se deve haver permissão para que os arquivos de backup sejam usados para inicializar assinaturas. Para obter mais informações, consulte [inicializar um transacional assinatura sem um instantâneo](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
 **Permitir Assinantes não SQL Server **  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores. Determina se a publicação oferece suporte a Assinantes não -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Definir essa opção como **True** define outras propriedades de publicação para dar suporte a não -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes. Essa opção é somente leitura se houver assinaturas; ele não pode ser definido como **True** se **Permitir assinaturas de atualização imediata**, **Permitir assinaturas de atualização enfileirada**, ou **Permitir assinaturas ponto a ponto** é definido como **True**. Para obter mais informações, consulte [assinantes não-SQL Server](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md).  
  
### Transformação de dados  
 **Permitir transformações de dados**  
 Determina se DTS (Data Transformation Services) deve ser usado para transformar dados antes de distribuí-los a um Assinante. Essa opção é somente leitura; transformações de dados só poderão ser habilitadas se uma publicação for criada usando procedimentos armazenados.  
  
> [!IMPORTANT]  
>  Assinaturas transformáveis não estarão disponíveis em uma versão futura. O recurso é preterido.  
  
### Replicação ponto a ponto  
 **Permitir assinaturas ponto a ponto**  
 Aplica-se apenas ao [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores. Determina se a publicação oferece suporte a replicação ponto a ponto. Definir essa opção como **True** define outras propriedades de publicação para dar suporte à replicação ponto a ponto. Essa opção será somente leitura se existirem assinaturas. Essa opção não pode ser definida como **True** se **Permitir assinaturas de atualização imediata** ou **Permitir assinaturas de atualização enfileirada**, ou **Permitir assinantes não - SQL Server** é definido como **True**. Para obter mais informações, consulte [replicação transacional ponto a ponto](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 **Permitir a detecção de conflitos ponto a ponto**  
 Aplica-se apenas ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versões posteriores. Especifica se a detecção de conflito está habilitada para esta publicação. Para usar detecção de conflitos, todos os nós devem ser executados no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou uma versão posterior, e a detecção deve estar habilitada para todos os nós. Para usar a detecção de conflitos, você também deve especificar um valor para **Identificação do originador do par**. Para obter mais informações, consulte [detecção de conflitos em replicação ponto a ponto](../../relational-databases/replication/transactional/conflict-detection-in-peer-to-peer-replication.md).  
  
 **Identificação do originador de nível**  
 Aplica-se apenas ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versões posteriores. Especifica uma ID para um nó em uma topologia ponto a ponto. Essa ID é usada para detecção de conflitos se **permitem a detecção de conflitos ponto a ponto** é definido como **True**. Especifique uma ID positiva, diferente de zero, que nunca foi usada na topologia. Para obter uma lista de IDs que já foram usadas, consulte o [Mspeer_originatorid_history](../../relational-databases/system-tables/mspeer-originatorid-history-transact-sql.md) tabela do sistema.  
  
### Assinaturas Atualizáveis  
 **Permitir assinaturas de atualização imediata**  
 Determina se as alterações de dados do Assinante podem ser replicadas imediatamente para o Publicador. Essa opção é somente leitura; a atualização de assinaturas só pode ser habilitada quando uma publicação é criada. Para obter mais informações, consulte [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
 **Permitir assinaturas de atualização enfileirada**  
 Determina se as alterações de dados do Assinante podem ser enfileiradas e replicadas posteriormente para o Publicador. Essa opção é somente leitura; a atualização de assinaturas só pode ser habilitada quando uma publicação é criada. Para obter mais informações, consulte [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
 **Reportar conflitos centralmente**  
 Determina se deve relatar alterações conflitantes de dados somente no publicador ou no publicador e assinante (requer a opção **Permitir assinaturas de atualização enfileirada**). Essa opção é somente leitura; ele é definido como **True** por padrão para publicações criadas com o Assistente para nova publicação e não podem ser alteradas após a publicação é criada. Um valor de **Verdadeiro** significa que os conflitos só são informados no Publicador. Os conflitos só podem ser exibidos quando são informados.  
  
 **Política de resolução de conflito**  
 Especifica a ação a ser tomada quando uma alteração no assinante entra em conflito com uma alteração do publicador (requer a opção **Permitir assinaturas de atualização enfileirada**). Para obter mais informações, consulte [Queued Updating Conflict Detection and Resolution](../../relational-databases/replication/transactional/queued-updating-conflict-detection-and-resolution.md).  
  
 **Tipo de fila**  
 Determina se deve usar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fila ou [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing (MSMQ) para enfileirar alterações no assinante até que elas podem ser aplicadas ao publicador (requer a opção **Permitir assinaturas de atualização enfileirada**). Essa opção só é relevante para o [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]; versões posteriores sempre usam tabelas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para filas.  
  
## Opções para publicações de mesclagem  
  
### Relatório de conflito  
 **Reportar conflitos centralmente**  
 Determina se as alterações de dados conflitantes devem ser informadas somente ao Publicador ou ao Publicador e ao Assinante. Essa opção é somente leitura; ele é definido como **True** por padrão para publicações criadas com o Assistente para nova publicação e não podem ser alteradas após a publicação é criada. Um valor de **Verdadeiro** significa que os conflitos só são informados no Publicador. Os conflitos só podem ser exibidos quando são informados. Para obter mais informações, consulte a seção "Exibindo conflitos" em [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
### Filtragem  
 **Permitir filtros com parâmetros**  
 Defina com base no uso ou não de filtros com parâmetros na publicação. Essa opção é sempre somente leitura. Para obter mais informações, consulte [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
 **Validar Assinantes**  
 Determina quais funções usar ao validar que um Assinante tem a partição correta de dados. Separe valores múltiplos por vírgulas. Para obter mais informações, consulte [validar informações de partição para um assinante de mesclagem](../../relational-databases/replication/validate-partition-information-for-a-merge-subscriber.md).  
  
 **Pré-calcular partições**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores. Determina se a sincronização deve ser otimizada calculando com antecedência quais linhas de dados pertencem a quais partições. Essa configuração assumira **Verdadeiro** como padrão, se a publicação atender aos critérios de partições pré-calculadas. Para obter mais informações, consulte [otimizar desempenho de filtro parametrizado com partições pré-calculadas](../../relational-databases/replication/merge/optimize-parameterized-filter-performance-with-precomputed-partitions.md).  
  
 **Otimizar sincronização**  
 Determina se o processamento de mesclagem deve ser otimizado armazenando metadados adicional em cada Assinante. Essa otimização foi substituída por partições pré-computadas; a opção **Otimizar sincronização** só será relevante se **Pré- calcular partições** for definida como **Falso**. Para obter mais informações, consulte [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
### Processos de mesclagem  
 **Limitar processos simultâneos**  
 Determina se o número de Agente de Mesclagems que podem executar ao mesmo tempo deve ser limitado. Isso geralmente é usado se uma publicação tiver muitas assinaturas push que possam ser sincronizadas ao mesmo tempo.  
  
 **Máximo de processos simultâneos**  
 O número máximo de agentes de mesclagem que podem ser executados ao mesmo tempo (requer **limitar processos simultâneos**). Se o número máximo de agentes em sincronização exceder o máximo, os agentes serão enfileirados até que o número fique abaixo do máximo.  
  
## Consulte também  
 [Crie uma publicação](../../relational-databases/replication/publish/create-a-publication.md)   
 [Visualizar e modificar as propriedades da publicação](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  