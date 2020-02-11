---
title: sp_addmergearticle (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergearticle
- sp_addmergearticle_TSQL
helpviewer_keywords:
- sp_addmergearticle
ms.assetid: 0df654ea-24e2-4c61-a75a-ecaa7a140a6c
author: stevestein
ms.author: sstein
ms.openlocfilehash: a9163e6d34a0de6200eafd413d163bb6d92fd4a5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72174001"
---
# <a name="sp_addmergearticle-transact-sql"></a>sp_addmergearticle (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Adiciona um artigo a uma publicação existente Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addmergearticle [ @publication = ] 'publication'   
        , [ @article = ] 'article'   
        , [ @source_object = ] 'source_object'   
    [ , [ @type = ] 'type' ]   
    [ , [ @description = ] 'description' ]   
    [ , [ @column_tracking = ] 'column_tracking' ]   
    [ , [ @status = ] 'status' ]   
    [ , [ @pre_creation_cmd = ] 'pre_creation_cmd' ]   
    [ , [ @creation_script = ] 'creation_script' ]   
    [ , [ @schema_option = ] schema_option ]   
    [ , [ @subset_filterclause = ] 'subset_filterclause' ]   
    [ , [ @article_resolver = ] 'article_resolver' ]   
    [ , [ @resolver_info = ] 'resolver_info' ]   
    [ , [ @source_owner = ] 'source_owner' ]   
    [ , [ @destination_owner = ] 'destination_owner' ]   
    [ , [ @vertical_partition = ] 'vertical_partition' ]   
    [ , [ @auto_identity_range = ] 'auto_identity_range' ]   
    [ , [ @pub_identity_range = ] pub_identity_range ]   
    [ , [ @identity_range = ] identity_range ]   
    [ , [ @threshold = ] threshold ]   
    [ , [ @verify_resolver_signature = ] verify_resolver_signature ]   
    [ , [ @destination_object = ] 'destination_object' ]   
    [ , [ @allow_interactive_resolver = ] 'allow_interactive_resolver' ]   
    [ , [ @fast_multicol_updateproc = ] 'fast_multicol_updateproc' ]   
    [ , [ @check_permissions = ] check_permissions ]   
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @published_in_tran_pub = ] 'published_in_tran_pub' ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @logical_record_level_conflict_detection = ] 'logical_record_level_conflict_detection' ]  
    [ , [ @logical_record_level_conflict_resolution = ] 'logical_record_level_conflict_resolution' ]  
    [ , [ @partition_options = ] partition_options ]  
    [ , [ @processing_order = ] processing_order ]  
    [ , [ @subscriber_upload_options = ] subscriber_upload_options ]  
    [ , [ @identityrangemanagementoption = ] 'identityrangemanagementoption' ]  
    [ , [ @delete_tracking = ] delete_tracking ]  
    [ , [ @compensate_for_errors = ] 'compensate_for_errors' ]   
    [ , [ @stream_blob_columns = ] 'stream_blob_columns' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação que contém o artigo. a *publicação* é **sysname**, sem padrão.  
  
`[ @article = ] 'article'`É o nome do artigo. O nome deve ser exclusivo na publicação. o *artigo* é **sysname**, sem padrão. o *artigo* deve estar no computador local que [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]está sendo executado e deve estar em conformidade com as regras para identificadores.  
  
`[ @source_object = ] 'source_object'`É o objeto de banco de dados a ser publicado. *source_object* é **sysname**, sem padrão. Para obter mais informações sobre os tipos de objetos que podem ser publicados usando a replicação de mesclagem, consulte [Publish Data and Database Objects](../../relational-databases/replication/publish/publish-data-and-database-objects.md).  
  
`[ @type = ] 'type'`É o tipo de artigo. o *tipo* é **sysname**, com um padrão de **Table**, e pode ser um dos valores a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**tabela** (padrão)|Tabela com esquema e dados. A replicação monitora a tabela para determinar os dados a serem replicados.|  
|**func schema only**|Função somente com esquema.|  
|**somente esquema** de **exibição indexada**|Exibição indexada somente com esquema|  
|**proc schema only**|Procedimento armazenado somente com esquema.|  
|**somente esquema de sinônimo**|Sinônimo somente com esquema).|  
|**view schema only**|Exibição somente com esquema|  
  
`[ @description = ] 'description'`É uma descrição do artigo. a *Descrição* é **nvarchar (255)**, com um padrão de NULL.  
  
`[ @column_tracking = ] 'column_tracking'`É a configuração para controle no nível de coluna. *column_tracking* é **nvarchar (10)**, com um padrão de false. **verdadeiro**ativa o controle de coluna. **false** desativa o rastreamento de coluna e deixa a detecção de conflitos no nível de linha. Se a tabela já tiver sido publicada em outras publicações de mesclagem, o controle da coluna deverá ser o mesmo que o valor usado por artigos existentes com base nessa tabela. Esse parâmetro só é específico a artigos de tabela.  
  
> [!NOTE]  
>  Se o controle de linha for usado para detecção de conflitos (o padrão), a tabela de base poderá incluir no máximo 1.024 colunas, mas as colunas deverão ser filtradas do artigo de modo que seja publicado no máximo 246 colunas. Se o rastreamento de coluna for usado, a tabela base poderá incluir no máximo 246 colunas.  
  
`[ @status = ] 'status'`É o status do artigo. o *status* é **nvarchar (10)**, com um padrão de não **sincronizado**. Se **ativo**, o script de processamento inicial para publicar a tabela é executado. Se não **sincronizado**, o script de processamento inicial para publicar a tabela será executado na próxima vez em que o agente de instantâneo for executado.  
  
`[ @pre_creation_cmd = ] 'pre_creation_cmd'`Especifica o que o sistema deve fazer se a tabela existir no Assinante ao aplicar o instantâneo. *pre_creation_cmd* é **nvarchar (10)** e pode ser um dos valores a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**None**|Se a tabela já existir no Assinante, nenhuma ação será tomada.|  
|**apagar**|Emite uma exclusão com base na cláusula WHERE no filtro de subconjunto.|  
|**descartar** (padrão)|Cancela a tabela antes de recriá-la. Necessário para dar [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)] suporte a assinantes.|  
|**truncar**|Trunca a tabela de destino.|  
  
`[ @creation_script = ] 'creation_script'`É o caminho e o nome de um script de esquema de artigo opcional usado para criar o artigo no banco de dados de assinatura. *creation_script* é **nvarchar (255)**, com um padrão de NULL.  
  
> [!NOTE]  
>  Scripts de criação em Assinantes [!INCLUDE[ssEW](../../includes/ssew-md.md)] não são executados  
  
`[ @schema_option = ] schema_option`É um bitmap da opção de geração de esquema para o artigo fornecido. *schema_option* é **binary (8)** e pode ser [| (OR-bit)](../../t-sql/language-elements/bitwise-or-transact-sql.md) produto de um ou mais desses valores.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**0x00**|Desabilita o script pelo Agente de Instantâneo e usa o script de precriação de esquema fornecido definido em *creation_script*.|  
|**0x01**|Gera a criação do objeto (CREATE TABLE, CREATE PROCEDURE, e assim por diante). Esse valor é o padrão para artigos de procedimento armazenado.|  
|**0x10**|Gera um índice clusterizado correspondente. Mesmo se esta opção não estiver definida, os índices relacionados às chaves primárias e as restrições UNIQUE são geradas caso já estejam definidas em uma tabela publicada.|  
|**0x20**|Converte UDTs (tipos de dados definidos pelo usuário) em tipos de dados básicos no Assinante. Essa opção não poderá ser usada quando houver uma restrição CHECK ou DEFAULT em uma coluna UDT, se uma coluna UDT for parte da chave primária ou se uma coluna computada fizer referência a uma coluna UDT.|  
|**0x40**|Gera índices não clusterizados correspondentes. Mesmo se esta opção não estiver definida, os índices relacionados às chaves primárias e as restrições UNIQUE são geradas caso já estejam definidas em uma tabela publicada.|  
|**0x80**|Replica restrições PRIMARY KEY. Todos os índices relacionados à restrição também são replicados, mesmo se as opções **0x10** e **0x40** não estiverem habilitadas.|  
|**0x100**|Replica gatilhos de usuário em um artigo de tabela, se definido.|  
|**0x200**|Replica restrições FOREIGN KEY. Se a tabela referenciada não fizer parte de uma publicação, todas as restrições FOREIGN KEY em uma tabela publicada não serão replicadas.|  
|**0x400**|Replica restrições CHECK.|  
|**0x800**|Replica padrões.|  
|**0x1000**|Replica ordenação em nível de coluna.|  
|**0x2000**|Replica propriedades estendidas associadas com o objeto de origem do artigo publicado.|  
|**0x4000**|Replica restrições UNIQUE. Todos os índices relacionados à restrição também são replicados, mesmo se as opções **0x10** e **0x40** não estiverem habilitadas.|  
|**0x8000**|Esta opção não é válida para Editores que executam [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou versões posteriores.|  
|**0x10000**|Replica instruções CHECK como NOT FOR REPLICATION para que as restrições não sejam forçadas durante a sincronização.|  
|**0x20000**|Replica instruções FOREIGN KEY como NOT FOR REPLICATION para que as restrições não sejam forçadas durante a sincronização.|  
|**0x40000**|Replica grupos de arquivos associados a uma tabela ou índice particionado.|  
|**0x80000**|Replica o esquema de partição para uma tabela particionada.|  
|**0x100000**|Replica o esquema de partição para um índice particionado.|  
|**0x200000**|Replica estatísticas de tabela.|  
|**0x400000**|Replica associações padrão.|  
|**0x800000**|Replica associações de regra.|  
|**0x1000000**|Replica índice de texto completo.|  
|**0x2000000**|As coleções de esquema XML vinculadas a colunas **XML** não são replicadas.|  
|**0x4000000**|Replica índices em colunas **XML** .|  
|**0x8000000**|Cria esquemas ainda não presentes no assinante.|  
|**0x10000000**|Converte colunas **XML** em **ntext** no Assinante.|  
|**0x20000000**|Converte tipos de dados de objeto grande (**nvarchar (max)**, **varchar (max)** e **varbinary (max)**) introduzidos em [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] tipos de dados com suporte [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]no.|  
|**0x40000000**|Replica permissões.|  
|**0x80000000**|Tenta descartar dependências de qualquer objeto que não faz parte da publicação.|  
|**0x100000000**|Use esta opção para replicar o atributo FILESTREAM se ele for especificado em colunas **varbinary (max)** . Não especifique essa opção se você estiver replicando tabelas para Assinantes [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Não há suporte para a replicação de tabelas [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] que têm colunas FILESTREAM para assinantes, independentemente de como essa opção de esquema está definida. Consulte a opção relacionada **0x800000000**.|  
|**0x200000000**|Converte os tipos de dados de data e hora (**Date**, **time**, **DateTimeOffset**e **datetime2**) [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] introduzidos nos tipos de dados com suporte em versões [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]anteriores do.|  
|**0x400000000**|Replica a opção de compactação para dados e índices. Para saber mais, veja [Data Compression](../../relational-databases/data-compression/data-compression.md).|  
|**0x800000000**|Defina essa opção para armazenar dados FILESTREAM em seu próprio grupo de arquivos no Assinante. Se essa opção não for definida, os dados FILESTREAM serão armazenados no grupo de arquivos padrão. A replicação não cria grupos de arquivos; portanto, se você definir essa opção, deverá criar o grupo de arquivos antes de aplicar o instantâneo no Assinante. Para obter mais informações sobre como criar objetos antes de aplicar o instantâneo, consulte [executar scripts antes e depois que o instantâneo for aplicado](../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied).<br /><br /> Consulte a opção relacionada **0x100000000**.|  
|**0x1000000000**|Converte os UDTs (tipos definidos pelo usuário) Common Language Runtime (CLR) em **varbinary (max)** para que as colunas do tipo UDT possam ser replicadas para os assinantes que estão em execução [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
|**0x2000000000**|Converte o tipo de dados **hierarchyid** em **varbinary (max)** para que as colunas do tipo **hierarchyid** possam ser replicadas para os assinantes que estão em execução [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Para obter mais informações sobre como usar colunas **hierarchyid** em tabelas replicadas, consulte [hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md).|  
|**0x4000000000**|Replica qualquer índice filtrado na tabela. Para obter mais informações sobre índices filtrados, consulte [criar índices filtrados](../../relational-databases/indexes/create-filtered-indexes.md).|  
|**0x8000000000**|Converte os tipos de dados **geography** e **Geometry** em **varbinary (max)** para que as colunas desses tipos possam ser replicadas para os [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]assinantes que estão em execução.|  
|**0x10000000000**|Replica índices em colunas do tipo **geography** e **Geometry**.|  
  
 Se este valor for NULO, o sistema gera automaticamente uma opção de esquema válida para o artigo. A tabela **opção de esquema padrão** na seção comentários mostra o valor escolhido com base no tipo de artigo. Além disso, nem todos os valores de *schema_option* são válidos para cada tipo de replicação e tipo de artigo. A tabela de **opção de esquema válida** fornecida nos comentários mostra as opções que podem ser especificadas para um determinado tipo de artigo.  
  
> [!NOTE]  
>  O parâmetro *schema_option* só afeta as opções de replicação para o instantâneo inicial. Depois que o esquema inicial tiver sido gerado pelo Agente de Instantâneo e aplicado ao Assinante, a replicação das alterações de esquema de publicação no Assinante ocorrerá com base nas regras de replicação de alteração de esquema e na configuração de parâmetro *replicate_ddl* especificada em [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Para obter mais informações, consulte [Make Schema Changes on Publication Databases](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md) (Fazer alterações de esquema em bancos de dados de publicação).  
  
`[ @subset_filterclause = ] 'subset_filterclause'`É uma cláusula WHERE que especifica a filtragem horizontal de um artigo de tabela sem a palavra onde está incluído. *subset_filterclause* é de **nvarchar (1000)**, com um padrão de uma cadeia de caracteres vazia.  
  
> [!IMPORTANT]  
>  Por motivos de desempenho, recomendamos que não sejam aplicadas funções a nomes de colunas em cláusulas de filtro de linha com parâmetros, como `LEFT([MyColumn]) = SUSER_SNAME()`. Se você usar [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) em uma cláusula de filtro e substituir o valor de HOST_NAME, talvez seja necessário converter os tipos de dados usando [converter](../../t-sql/functions/cast-and-convert-transact-sql.md). Para obter mais informações sobre as práticas recomendadas para esse caso, consulte a seção "substituindo o valor de HOST_NAME ()" em [filtros de linha com parâmetros](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
`[ @article_resolver = ] 'article_resolver'`É o resolvedor baseado em COM usado para resolver conflitos no artigo de tabela ou o assembly .NET Framework invocado para executar lógica de negócios personalizada no artigo de tabela. *article_resolver* é **varchar (255)**, com um padrão de NULL. São listados valores disponíveis para este parâmetro em [!INCLUDE[msCoName](../../includes/msconame-md.md)] Resolvedores Personalizados. Se o valor fornecido não for um dos [!INCLUDE[msCoName](../../includes/msconame-md.md)] resolvedores, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa o resolvedor especificado ao invés do resolvedor fornecido pelo sistema. Use **sp_enumcustomresolvers** para enumerar a lista de resolvedores personalizados disponíveis. Para obter mais informações, consulte [executar lógica de negócios durante a sincronização de mesclagem](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md) e [detecção e resolução avançadas de conflitos de replicação de mesclagem](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
`[ @resolver_info = ] 'resolver_info'`É usado para especificar informações adicionais exigidas por um resolvedor personalizado. Alguns resolvedores do [!INCLUDE[msCoName](../../includes/msconame-md.md)] necessitam de uma coluna fornecida como entrada para o resolvedor. *resolver_info* é **nvarchar (255)**, com um padrão de NULL. Para obter mais informações, consulte [Resolvedores Microsoft baseados em COM](../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md).  
  
`[ @source_owner = ] 'source_owner'`É o nome do proprietário do *source_object*. *source_owner* é **sysname**, com um padrão de NULL. Se NULO, presume-se que o usuário atual seja o proprietário.  
  
`[ @destination_owner = ] 'destination_owner'`É o proprietário do objeto no banco de dados de assinatura, se não for ' dbo '. *destination_owner* é **sysname**, com um padrão de NULL. Se NULo, presume-se que o 'dbo' é o proprietário.  
  
`[ @vertical_partition = ] 'column_filter'`Habilita e desabilita a filtragem de coluna em um artigo de tabela. *vertical_partition* é **nvarchar (5)** com um padrão de false.  
  
 **false** indica que não há nenhuma filtragem vertical e publica todas as colunas.  
  
 **verdadeiro** limpa todas as colunas, exceto a chave primária declarada e as colunas ROWGUID. As colunas são adicionadas usando **sp_mergearticlecolumn**.  
  
`[ @auto_identity_range = ] 'automatic_identity_range'`Habilita e desabilita o tratamento automático de intervalo de identidade para este artigo de tabela em uma publicação no momento em que é criado. *auto_identity_range* é **nvarchar (5)**, com um padrão de false. **true** habilita o tratamento automático do intervalo de identidade, enquanto **false** o desabilita.  
  
> [!NOTE]  
>  o *auto_identity_range* foi preterido e é fornecido apenas para fins de compatibilidade com versões anteriores. Você deve usar *identityrangemanagementoption* para especificar opções de gerenciamento de intervalo de identidade. Para obter mais informações, consulte [Replicar colunas de identidade](../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
`[ @pub_identity_range = ] pub_identity_range`Controla o tamanho do intervalo de identidade alocado a um assinante com uma assinatura de servidor quando o gerenciamento automático do intervalo de identidade é usado. Esse intervalo de identidade é reservado para um Assinante de republicação para ser alocado a seus próprios Assinantes. *pub_identity_range* é **bigint**, com um padrão de NULL. Você deve especificar esse parâmetro se *identityrangemanagementoption* for **auto** ou se *auto_identity_range* for **true**.  
  
`[ @identity_range = ] identity_range`Controla o tamanho do intervalo de identidade alocado para o Publicador e para o Assinante quando o gerenciamento automático do intervalo de identidade é usado. *identity_range* é **bigint**, com um padrão de NULL. Você deve especificar esse parâmetro se *identityrangemanagementoption* for **auto** ou se *auto_identity_range* for **true**.  
  
> [!NOTE]  
>  *identity_range* controla o tamanho do intervalo de identidade em assinantes de republicação usando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]versões anteriores do.  
  
`[ @threshold = ] threshold`Valor percentual que controla quando o Agente de Mesclagem atribui um novo intervalo de identidade. Quando a porcentagem de valores especificados no *limite* é usada, o agente de mesclagem cria um novo intervalo de identidade. o *limite* é **int**, com um padrão de NULL. Você deve especificar esse parâmetro se *identityrangemanagementoption* for **auto** ou se *auto_identity_range* for **true**.  
  
`[ @verify_resolver_signature = ] verify_resolver_signature`Especifica se uma assinatura digital é verificada antes de usar um resolvedor na replicação de mesclagem. *verify_resolver_signature* é **int**, com um padrão de 1.  
  
 **0** especifica que a assinatura não será verificada.  
  
 **1** especifica que a assinatura será verificada para ver se ela é de uma fonte confiável.  
  
`[ @destination_object = ] 'destination_object'`É o nome do objeto no banco de dados de assinatura. *destination_object* é **sysname**, com um valor padrão de o que está em ** \@source_object**. Este parâmetro é especificado somente se o artigo for um artigo apenas de esquema, como procedimentos armazenados, exibições e UDFs. Se o artigo especificado for um artigo de tabela, o valor *@source_object* em substituirá o valor em *destination_object*.  
  
`[ @allow_interactive_resolver = ] 'allow_interactive_resolver'`Habilita ou desabilita o uso do resolvedor interativo em um artigo. *allow_interactive_resolver* é **nvarchar (5)**, com um padrão de false. **verdadeiro** habilita o uso do resolvedor interativo no artigo; **false** desabilita.  
  
> [!NOTE]  
>  O Resolvedor Interativo não tem o suporte dos Assinantes [!INCLUDE[ssEW](../../includes/ssew-md.md)].  
  
`[ @fast_multicol_updateproc = ] 'fast_multicol_updateproc'`Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts.  
  
`[ @check_permissions = ] check_permissions`É um bitmap das permissões em nível de tabela que são verificadas quando o Agente de Mesclagem aplica alterações ao Publicador. Se o logon/conta de usuário do Publicador usado pelo processo de mesclagem não possuir as permissões corretas de tabela, as alterações inválidas serão registradas como conflitos. *check_permissions* é **int**e pode ser [| (OR-bit)](../../t-sql/language-elements/bitwise-or-transact-sql.md) produto de um ou mais dos valores a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**0x00** (padrão)|As permissões não são verificadas.|  
|**0x10**|Verifica as permissões no Editor antes que as operações de inserção realizadas em um Assinante possam ser carregadas.|  
|**0x20**|Verifica as permissões no Publicador antes que as operações de atualização feitas em um assinante possam ser carregadas.|  
|**0x40**|Verifica as permissões no Editor antes que as operações de atualização realizadas em um Assinante possam ser carregadas.|  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot`O reconhece que a ação executada por esse procedimento armazenado pode invalidar um instantâneo existente. *force_invalidate_snapshot* é um **bit**, com um padrão de 0.  
  
 **0** especifica que a adição de um artigo não faz com que o instantâneo seja inválido. Se o procedimento armazenado detectar que a alteração requer um novo instantâneo, ocorrerá um erro e nenhuma alteração será feita.  
  
 **1** especifica que a adição de um artigo pode fazer com que o instantâneo seja inválido e, se houver assinaturas que exijam um novo instantâneo, dá permissão para que o instantâneo existente seja marcado como obsoleto e um novo instantâneo gerado. *force_invalidate_snapshot* é definido como **1** ao adicionar um artigo a uma publicação com um instantâneo existente.  
  
`[ @published_in_tran_pub = ] 'published_in_tran_pub'`Indica que um artigo em uma publicação de mesclagem também é publicado em uma publicação transacional. *published_in_tran_pub* é **nvarchar (5)**, com um padrão de false. **verdadeiro** especifica que o artigo também é publicado em uma publicação transacional.  
  
`[ @force_reinit_subscription = ] force_reinit_subscription`Reconhece que a ação executada por este procedimento armazenado pode exigir que as assinaturas existentes sejam reinicializadas. *force_reinit_subscription* é um **bit**, com um padrão de 0.  
  
 **0** especifica que a adição de um artigo não faz com que a assinatura seja reinicializada. Se o procedimento armazenado detectar que a alteração irá requerer assinaturas existentes para ser reiniciada, ocorrerá um erro e nenhuma alteração será feita.  
  
 **1** significa que as alterações no artigo de mesclagem fazem com que as assinaturas existentes sejam reinicializadas e concede a permissão para que a reinicialização da assinatura ocorra. *force_reinit_subscription* é definido como **1** quando *subset_filterclause* especifica um filtro de linha com parâmetros.  
  
`[ @logical_record_level_conflict_detection = ] 'logical_record_level_conflict_detection'`Especifica o nível de detecção de conflito para um artigo que é membro de um registro lógico. *logical_record_level_conflict_detection* é **nvarchar (5)**, com um padrão de false.  
  
 **verdadeiro** especifica que um conflito será detectado se as alterações forem feitas em qualquer lugar no registro lógico.  
  
 **false** especifica que a detecção de conflito padrão é usada conforme especificado pelo *column_tracking*. Para obter mais informações, consulte [Agrupar alterações a linhas relacionadas com registros lógicos](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
> [!NOTE]  
>  Como os registros lógicos não são [!INCLUDE[ssEW](../../includes/ssew-md.md)] suportados pelos assinantes, você deve especificar um valor de **false** para *logical_record_level_conflict_detection* para dar suporte a esses assinantes.  
  
`[ @logical_record_level_conflict_resolution = ] 'logical_record_level_conflict_resolution'`Especifica o nível de resolução de conflitos para um artigo que é membro de um registro lógico. *logical_record_level_conflict_resolution* é **nvarchar (5)**, com um padrão de false.  
  
 **verdadeiro** especifica que todo o registro lógico vencedor substitui o registro lógico perdido.  
  
 **false** especifica que as linhas vencedoras não são restritas ao registro lógico. Se *logical_record_level_conflict_detection* for **true**, *logical_record_level_conflict_resolution* também deverá ser definido como **true**. Para obter mais informações, consulte [Agrupar alterações a linhas relacionadas com registros lógicos](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
> [!NOTE]  
>  Como os registros lógicos não são [!INCLUDE[ssEW](../../includes/ssew-md.md)] suportados pelos assinantes, você deve especificar um valor de **false** para *logical_record_level_conflict_resolution* para dar suporte a esses assinantes.  
  
`[ @partition_options = ] partition_options`Define a maneira como os dados no artigo são particionados, o que permite otimizações de desempenho quando todas as linhas pertencem a apenas uma partição ou em apenas uma assinatura. *partition_options* é **tinyint**e pode ser um dos valores a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**0** (padrão)|A filtragem para o artigo ou é estática ou não gera um único subconjunto de dados para cada partição, ou seja, uma partição "sobreposta".|  
|**1**|As partições são sobrepostas e as atualizações de linguagem de manipulação de dados (DML) feitas ao Assinante não podem alterar a partição à qual uma linha pertence.|  
|**2**|A filtragem do artigo gera partições não sobrepostas, mas vários Assinantes podem receber a mesma partição.|  
|**Beta**|A filtragem para o artigo gera partições não sobrepostas exclusivas de cada assinatura.|  
  
> [!NOTE]  
>  Se a tabela de origem de um artigo já estiver publicada em outra publicação, o valor de *partition_options* deverá ser o mesmo para ambos os artigos.  
  
`[ @processing_order = ] processing_order`Indica a ordem de processamento dos artigos em uma publicação de mesclagem. *processing_order* é **int**, com um padrão de 0. **0** especifica que o artigo não está ordenado e qualquer outro valor representa o valor ordinal da ordem de processamento deste artigo. Os artigos são processados em ordem crescente de valores. Se dois artigos tiverem o mesmo valor, a ordem de processamento será determinada pela ordem do apelido do artigo na tabela do sistema [sysmergearticles](../../relational-databases/system-tables/sysmergearticles-transact-sql.md) . Para obter mais informações, confira [propriedades de Especificar Replicação de Mesclagem](../../relational-databases/replication/merge/specify-merge-replication-properties.md).  
  
`[ @subscriber_upload_options = ] subscriber_upload_options`Define restrições em atualizações feitas em um assinante com uma assinatura de cliente. Para obter mais informações, consulte [Otimizar o desempenho da replicação de mesclagem com artigos somente para download](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md). *subscriber_upload_options* é **tinyint**e pode ser um dos valores a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**0** (padrão)|Sem restrições. As alterações feitas no Assinante são carregadas no Publicador.|  
|**1**|As alterações são permitidas no Assinante, mas não são carregadas no Publicador.|  
|**2**|As alterações não são permitidas no Assinante.|  
  
 A alteração *subscriber_upload_options* requer que a assinatura seja reinicializada chamando [sp_reinitmergepullsubscription &#40;&#41;do Transact-SQL ](../../relational-databases/system-stored-procedures/sp-reinitmergepullsubscription-transact-sql.md).  
  
> [!NOTE]  
>  Se a tabela de origem de um artigo já estiver publicada em outra publicação, o valor de *subscriber_upload_options* deverá ser o mesmo para ambos os artigos.  
  
`[ @identityrangemanagementoption = ] identityrangemanagementoption`Especifica como o gerenciamento de intervalo de identidade é tratado para o artigo. *identityrangemanagementoption* é **nvarchar (10)** e pode ser um dos valores a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**None**|Desabilita o gerenciamento de intervalo de identidade.|  
|**Manual**|Marca a coluna de identidade usando NOT FOR REPLICATION para ativar tratamento de intervalo de identidade manual.|  
|**Automático**|Especifica o gerenciamento automático de intervalos de identidade.|  
|NULL (padrão)|O padrão é **nenhum**quando o valor de *auto_identity_range* não é **verdadeiro**.|  
  
 Para compatibilidade com versões anteriores, quando o valor de *identityrangemanagementoption* é NULL, o valor de *auto_identity_range* é verificado. No entanto, quando o valor de *identityrangemanagementoption* não for NULL, o valor de *auto_identity_range* será ignorado. Para obter mais informações, consulte [Replicar colunas de identidade](../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
`[ @delete_tracking = ] 'delete_tracking'`Indica se as exclusões são replicadas. *delete_tracking* é **nvarchar (5)**, com um padrão de true. **false** indica que as exclusões não são replicadas e **true** indica que as exclusões são replicadas, o que é o comportamento normal da replicação de mesclagem. Quando *delete_tracking* é definido como **false**, as linhas excluídas no Assinante devem ser removidas manualmente no Publicador e as linhas excluídas no Publicador devem ser manualmente removidas no Assinante.  
  
> [!IMPORTANT]  
>  Definir *delete_tracking* como **false** resulta em não convergência. Se a tabela de origem de um artigo já estiver publicada em outra publicação, o valor de *delete_tracking* deverá ser o mesmo para ambos os artigos.  
  
> [!NOTE]  
>  *delete_tracking* opções não podem ser definidas usando o **Assistente para nova publicação** ou a caixa de diálogo **Propriedades da publicação** .  
  
`[ @compensate_for_errors = ] 'compensate_for_errors'`Indica se as ações de compensação são tomadas quando são encontrados erros durante a sincronização. *compensate_for_errors i*s **nvarchar (5)**, com um padrão de false. Quando definido como **true**, as alterações que não podem ser aplicadas em um assinante ou Publicador durante a sincronização sempre levam a ações de compensação para desfazer a alteração; no entanto, um assinante configurado incorretamente que gera um erro pode fazer com que as alterações em outros assinantes e editores sejam desfeitas. **false** desabilita essas ações de compensação. no entanto, os erros ainda são registrados como com compensação e as mesclagens subsequentes continuam tentando aplicar as alterações até que tenham êxito.  
  
> [!IMPORTANT]  
>  Embora os dados nas linhas afetadas pareçam estar fora de convergência, assim que você resolver qualquer erro, as alterações poderão ser aplicadas e os dados convergidos. Se a tabela de origem de um artigo já estiver publicada em outra publicação, o valor de *compensate_for_errors* deverá ser o mesmo para ambos os artigos.  
  
`[ @stream_blob_columns = ] 'stream_blob_columns'`Especifica que uma otimização de fluxo de dados será usada ao replicar colunas de objeto binário grande. *stream_blob_columns* é **nvarchar (5)**, com um padrão de false. **verdadeiro** significa que a otimização será tentada. *stream_blob_columns* é definido como true quando o FileStream está habilitado. Isso permite a replicação de dados FILESTREAM para executar da maneira ideal e reduzir a utilização de memória. Para forçar os artigos da tabela FILESTREAM a não usarem o streaming de BLOB, use **sp_changemergearticle** para definir *stream_blob_columns* como false.  
  
> [!IMPORTANT]  
>  A habilitação dessa otimização de memória pode reduzir o desempenho do Agente de Mesclagem durante a sincronização. Esta opção só deve ser usada ao replicar colunas que contêm megabytes de dados.  
  
> [!NOTE]  
>  Determinadas funcionalidades de replicação de mesclagem, como registros lógicos, ainda podem impedir que a otimização do fluxo seja usada ao replicar objetos binários grandes, mesmo com *stream_blob_columns* definido como **true**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_addmergearticle** é usado na replicação de mesclagem.  
  
 Quando você publicar objetos, suas definições são copiadas aos Assinantes. Se você estiver publicando um objeto de banco de dados que depende de outros objetos, precisará publicar todos os objetos referenciados. Por exemplo, se você publicar uma exibição que depende de uma tabela, terá de publicar a tabela também.  
  
 Se você especificar um valor de **3** para *partition_options*, pode haver apenas uma única assinatura para cada partição de dados nesse artigo. Se uma segunda assinatura for criada na qual o critério de filtragem da nova assinatura for resolvido para a mesma partição como a assinatura existente, a assinatura existente será cancelada.  
  
 Ao especificar um valor de 3 para *partition_options*, os metadados são limpos sempre que o agente de mesclagem é executado e o instantâneo particionado expira mais rapidamente. Ao usar essa opção, considere habilitar o instantâneo particionado solicitado pelo assinante. Para obter mais informações, consulte [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
 Adicionar um artigo com um filtro horizontal estático, usando *subset_filterclause*, a uma publicação existente com artigos que têm filtros com parâmetros exige que as assinaturas sejam reinicializadas.  
  
 Ao especificar *processing_order*, recomendamos deixar lacunas entre os valores de ordem dos artigos, o que torna mais fácil definir novos valores no futuro. Por exemplo, se você tiver três artigos Article1, Article2 e Article3, defina *processing_order* como 10, 20 e 30, em vez de 1, 2 e 3. Para obter mais informações, confira [propriedades de Especificar Replicação de Mesclagem](../../relational-databases/replication/merge/specify-merge-replication-properties.md).  
  
## <a name="default-schema-option-table"></a>Tabela de opção de esquema padrão  
 Esta tabela descreve o valor padrão definido pelo procedimento armazenado se um valor nulo for especificado para *schema_option*, que depende do tipo de artigo.  
  
|Tipo de artigo|Valor de opção de esquema|  
|------------------|-------------------------|  
|**func schema only**|**0x01**|  
|**indexed view schema only**|**0x01**|  
|**proc schema only**|**0x01**|  
|**tabela**|**** -  0x0C034FD1[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e publicações mais recentes compatíveis com um instantâneo de modo nativo.<br /><br /> **** -  0x08034FF1[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e publicações mais recentes compatíveis com um instantâneo de modo de caractere.|  
|**view schema only**|**0x01**|  
  
> [!NOTE]  
>  Se a publicação oferecer suporte a versões [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]anteriores do, a opção de esquema padrão para a **tabela** será **0x30034FF1**.  
  
## <a name="valid-schema-option-table"></a>Tabela de opção de esquema válida  
 A tabela a seguir descreve os valores permitidos *schema_option* dependendo do tipo de artigo.  
  
|Tipo de artigo|Valores de opção de esquema|  
|------------------|--------------------------|  
|**func schema only**|**0x01** e **0x2000**|  
|**indexed view schema only**|**0x01**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x1000000**e **0x200000**|  
|**proc schema only**|**0x01** e **0x2000**|  
|**tabela**|Todas as opções.|  
|**view schema only**|**0x01**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x1000000**e **0x200000**|  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_AddMergeArticle](../../relational-databases/replication/codesnippet/tsql/sp-addmergearticle-trans_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Exige associação à função de servidor fixa **sysadmin** ou à função de banco de dados fixa **db_owner** .  
  
## <a name="see-also"></a>Consulte Também  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [Publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Replicar colunas de identidade](../../relational-databases/replication/publish/replicate-identity-columns.md)   
 [&#41;&#40;Transact-SQL de sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropmergearticle](../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpmergearticle](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
