---
title: sp_addmergearticle (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_addmergearticle
- sp_addmergearticle_TSQL
helpviewer_keywords:
- sp_addmergearticle
ms.assetid: 0df654ea-24e2-4c61-a75a-ecaa7a140a6c
caps.latest.revision: 69
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9ac83f7ffeb53b501090c7fe1e5f65e08eee07d0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="spaddmergearticle-transact-sql"></a>sp_addmergearticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Adiciona um artigo a uma publicação existente Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [  **@publication=** ] **'***publicação***'**  
 É o nome da publicação que contém o artigo. *publicação* é **sysname**, sem padrão.  
  
 [  **@article=** ] **'***artigo***'**  
 É o nome do artigo. O nome deve ser exclusivo na publicação. *artigo* é **sysname**, sem padrão. *artigo* devem estar em um computador local executando o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], de acordo com as regras para identificadores.  
  
 [  **@source_object=** ] **'***source_object***'**  
 É o objeto de banco de dados a ser publicado. *source_object* é **sysname**, sem padrão. Para obter mais informações sobre os tipos de objetos que podem ser publicados usando replicação de mesclagem, consulte [publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md).  
  
 [  **@type=** ] **'***tipo***'**  
 É o tipo de artigo. *tipo* é **sysname**, com um padrão de **tabela**, e pode ser um dos valores a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**tabela** (padrão)|Tabela com esquema e dados. A replicação monitora a tabela para determinar os dados a serem replicados.|  
|**somente esquema de função**|Função somente com esquema.|  
|**modo de exibição indexado** **somente esquema**|Exibição indexada somente com esquema|  
|**somente esquema de PROC**|Procedimento armazenado somente com esquema.|  
|**somente esquema sinônimo**|Sinônimo somente com esquema).|  
|**somente o esquema de exibição**|Exibição somente com esquema|  
  
 [  **@description=** ] **'***descrição***'**  
 É uma descrição do artigo. *Descrição* é **nvarchar (255)**, com um padrão NULL.  
  
 [  **@column_tracking=** ] **'***column_tracking***'**  
 É a configuração para acompanhamento do nível de coluna. *column_tracking* é **nvarchar (10)**, com um padrão de FALSE. **True**ativa o rastreamento de coluna. **False** desativa o rastreamento de coluna e deixa a detecção de conflito em nível de linha. Se a tabela já tiver sido publicada em outras publicações de mesclagem, o controle da coluna deverá ser o mesmo que o valor usado por artigos existentes com base nessa tabela. Esse parâmetro só é específico a artigos de tabela.  
  
> [!NOTE]  
>  Se o controle de linha for usado para detecção de conflitos (o padrão), a tabela de base poderá incluir no máximo 1.024 colunas, mas as colunas deverão ser filtradas do artigo de modo que seja publicado no máximo 246 colunas. Se o rastreamento de coluna for usado, a tabela base poderá incluir no máximo 246 colunas.  
  
 [  **@status=** ] **'***status***'**  
 É o status do artigo. *status* é **nvarchar (10)**, com um padrão de **unsynced**. Se **active**, o script de processamento inicial para publicar a tabela é executado. Se **unsynced**, o script de processamento inicial para publicar a tabela é executado na próxima vez que o Snapshot Agent é executado.  
  
 [  **@pre_creation_cmd=** ] **'***pre_creation_cmd***'**  
 Especifica o que o sistema deve fazer se a tabela existe no assinante quando aplicar o instantâneo. *pre_creation_cmd* é **nvarchar (10)**, e pode ser um dos valores a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Nenhum**|Se a tabela já existir no Assinante, nenhuma ação será tomada.|  
|**delete**|Emite uma exclusão com base na cláusula WHERE no filtro de subconjunto.|  
|**Descartar** (padrão)|Cancela a tabela antes de recriá-la. Necessário para dar suporte a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)] assinantes.|  
|**Truncar**|Trunca a tabela de destino.|  
  
 [  **@creation_script=** ] **'***creation_script***'**  
 Corresponde ao caminho e ao nome de um script de esquema de artigo opcional usados para criar o artigo no banco de dados de assinatura. *creation_script* é **nvarchar (255)**, com um padrão NULL.  
  
> [!NOTE]  
>  Scripts de criação em Assinantes [!INCLUDE[ssEW](../../includes/ssew-md.md)] não são executados  
  
 [  **@schema_option=** ] *schema_option*  
 É um bitmap da opção de geração de esquema para o artigo determinado. *schema_option* é **binary (8)**e pode ser o [| (OR bit a bit) ](../../t-sql/language-elements/bitwise-or-transact-sql.md) produto de um ou mais desses valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**0x00**|Desabilita a execução de script pelo Snapshot Agent e usa o script de pré-criação de esquema fornecido definido em *creation_script*.|  
|**0x01**|Gera a criação do objeto (CREATE TABLE, CREATE PROCEDURE, e assim por diante). Esse valor é o padrão para artigos de procedimento armazenado.|  
|**0x10**|Gera um índice clusterizado correspondente. Mesmo se esta opção não estiver definida, os índices relacionados às chaves primárias e as restrições UNIQUE são geradas caso já estejam definidas em uma tabela publicada.|  
|**0x20**|Converte UDTs (tipos de dados definidos pelo usuário) em tipos de dados básicos no Assinante. Essa opção não poderá ser usada quando houver uma restrição CHECK ou DEFAULT em uma coluna UDT, se uma coluna UDT for parte da chave primária ou se uma coluna computada fizer referência a uma coluna UDT.|  
|**0x40**|Gera índices não clusterizados correspondentes. Mesmo se esta opção não estiver definida, os índices relacionados às chaves primárias e as restrições UNIQUE são geradas caso já estejam definidas em uma tabela publicada.|  
|**0x80**|Replica restrições PRIMARY KEY. Quaisquer índices relacionadas à restrição também são replicados, mesmo se opções **0x10** e **0x40** não estão habilitados.|  
|**0x100**|Replica gatilhos de usuário em um artigo de tabela, se definido.|  
|**0x200**|Replica restrições FOREIGN KEY. Se a tabela referenciada não fizer parte de uma publicação, todas as restrições FOREIGN KEY em uma tabela publicada não serão replicadas.|  
|**0x400**|Replica restrições CHECK.|  
|**0x800**|Replica padrões.|  
|**0x1000**|Replica agrupamento em nível de coluna.|  
|**0x2000**|Replica propriedades estendidas associadas com o objeto de origem do artigo publicado.|  
|**0x4000**|Replica restrições UNIQUE. Quaisquer índices relacionadas à restrição também são replicados, mesmo se opções **0x10** e **0x40** não estão habilitados.|  
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
|**0x2000000**|Coleções de esquemas XML associada a **xml** colunas não são replicadas.|  
|**0x4000000**|Replica índices em **xml** colunas.|  
|**0x8000000**|Cria esquemas ainda não presentes no assinante.|  
|**0x10000000**|Converte **xml** colunas **ntext** no assinante.|  
|**0x20000000**|Converte tipos de dados objeto grande (**nvarchar (max)**, **varchar (max)**, e **varbinary (max)**) introduzido no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] para tipos de dados que têm suporte em [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].|  
|**0x40000000**|Replica permissões.|  
|**0x80000000**|Tenta descartar dependências de qualquer objeto que não faz parte da publicação.|  
|**0x100000000**|Use esta opção para replicar o atributo FILESTREAM, se for especificado em **varbinary (max)** colunas. Não especifique essa opção se você estiver replicando tabelas para Assinantes [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Replicação de tabelas com colunas FILESTREAM para [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] assinantes não tem suporte, independentemente de como essa opção de esquema é definida. Consulte a opção relacionada **0x800000000**.|  
|**0x200000000**|Converte tipos de dados de data e hora (**data**, **tempo**, **datetimeoffset**, e **datetime2**) introduzido no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] aos dados tipos com suporte em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**0x400000000**|Replica a opção de compactação para dados e índices. Para obter mais informações, consulte [Data Compression](../../relational-databases/data-compression/data-compression.md).|  
|**0x800000000**|Defina essa opção para armazenar dados FILESTREAM em seu próprio grupo de arquivos no Assinante. Se essa opção não for definida, os dados FILESTREAM serão armazenados no grupo de arquivos padrão. A replicação não cria grupos de arquivos; portanto, se você definir essa opção, deverá criar o grupo de arquivos antes de aplicar o instantâneo no Assinante. Para obter mais informações sobre como criar objetos antes de aplicar o instantâneo, consulte [executar Scripts antes e após a aplicação do instantâneo](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md).<br /><br /> Consulte a opção relacionada **0x100000000**.|  
|**0x1000000000**|Converte tipos common language runtime (CLR) definidos pelo usuário (UDTs) em **varbinary (max)** para que as colunas do tipo UDT possam ser replicadas para os assinantes que executam o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
|**0x2000000000**|Converte o **hierarchyid** tipo de dados **varbinary (max)** para que colunas do tipo **hierarchyid** podem ser replicadas para assinantes que executam o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Para obter mais informações sobre como usar **hierarchyid** colunas em tabelas replicadas, consulte [hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md).|  
|**0x4000000000**|Replica qualquer índice filtrado na tabela. Para obter mais informações sobre índices filtrados, consulte [criar índices filtrados](../../relational-databases/indexes/create-filtered-indexes.md).|  
|**0x8000000000**|Converte o **geografia** e **geometria** para tipos de dados **varbinary (max)** para que colunas desses tipos podem ser replicadas para assinantes que executam o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
|**0x10000000000**|Replica índices em colunas do tipo **geografia** e **geometria**.|  
  
 Se este valor for NULO, o sistema gera automaticamente uma opção de esquema válida para o artigo. O **opção de esquema padrão** tabela na seção comentários mostra o valor escolhido com base no tipo de artigo. Além disso, nem todos os *schema_option* valores são válidos para cada tipo de replicação e tipo de artigo. O **opção de esquema válido** tabela fornecida nas observações mostra as opções que podem ser especificadas para um determinado tipo de artigo.  
  
> [!NOTE]  
>  O *schema_option* parâmetro afeta somente as opções de replicação para o instantâneo inicial. Depois que o esquema inicial foi gerado pelo Snapshot Agent e aplicado ao assinante, a replicação de alterações de esquema de publicação para o assinante ocorrer com base nas regras de replicação de alteração de esquema e o *replicate_ddl* a configuração de parâmetro especificada em [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Para obter mais informações, consulte [Make Schema Changes on Publication Databases](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md) (Fazer alterações de esquema em bancos de dados de publicação).  
  
 [  **@subset_filterclause=** ] **'***subset_filterclause***'**  
 Há uma cláusula WHERE especificando a filtragem horizontal de um artigo de tabela sem ter a palavra WHERE incluída. *subset_filterclause* é de **nvarchar (1000)**, com um padrão de uma cadeia de caracteres vazia.  
  
> [!IMPORTANT]  
>  Por motivos de desempenho, recomendamos que não sejam aplicadas funções a nomes de colunas em cláusulas de filtro de linha com parâmetros, como `LEFT([MyColumn]) = SUSER_SNAME()`. Se você usar [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) em uma cláusula de filtro e substituir o valor HOST_NAME, talvez você precise converter tipos de dados usando [converter](../../t-sql/functions/cast-and-convert-transact-sql.md). Para obter mais informações sobre as práticas recomendadas para esse caso, consulte a seção "Substituindo o valor de HOST_NAME ()" em [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 [  **@article_resolver=** ] **'***article_resolver***'**  
 O resolvedor baseado em COM é usado para resolver conflitos no artigo da tabela ou o assembly do .NET Framework é chamado para executar a lógica de negócios personalizada no artigo de tabela. *article_resolver* é **varchar (255)**, com um padrão NULL. São listados valores disponíveis para este parâmetro em [!INCLUDE[msCoName](../../includes/msconame-md.md)] Resolvedores Personalizados. Se o valor fornecido não for um dos [!INCLUDE[msCoName](../../includes/msconame-md.md)] resolvedores, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa o resolvedor especificado ao invés do resolvedor fornecido pelo sistema. Use **sp_enumcustomresolvers** para enumerar a lista de determinadores personalizados disponíveis. Para obter mais informações, consulte [executar lógica de negócios durante a sincronização direta](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md) e [avançada detecção de conflitos de replicação de mesclagem e a resolução](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
 [  **@resolver_info=** ] **'***resolver_info***'**  
 É usado para especificar informações adicionais requeridas por um determinador personalizado. Alguns resolvedores do [!INCLUDE[msCoName](../../includes/msconame-md.md)] necessitam de uma coluna fornecida como entrada para o resolvedor. *resolver_info* é **nvarchar (255)**, com um padrão NULL. Para obter mais informações, consulte [Resolvedores Microsoft baseados em COM](../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md).  
  
 [  **@source_owner=** ] **'***source_owner***'**  
 É o nome do proprietário do *source_object*. *source_owner* é **sysname**, com um padrão NULL. Se NULO, presume-se que o usuário atual seja o proprietário.  
  
 [  **@destination_owner=** ] **'***destination_owner***'**  
 É o proprietário do objeto no banco de dados de assinatura, se não for 'dbo'. *destination_owner* é **sysname**, com um padrão NULL. Se NULo, presume-se que o 'dbo' é o proprietário.  
  
 [  **@vertical_partition=** ] **'***column_filter***'**  
 Habilita e desabilita a filtragem de coluna em um artigo de tabela. *vertical_partition* é **nvarchar (5)** com um padrão de FALSE.  
  
 **False** indica que não há filtragem vertical e publica todas as colunas.  
  
 **True** limpa todas as colunas exceto a chave primária declarada e as colunas ROWGUID. Colunas são adicionadas usando **sp_mergearticlecolumn**.  
  
 [  **@auto_identity_range=** ] **'***automatic_identity_range***'**  
 Habilita e desabilita o intervalo de identidade automática desse artigo de tabela em uma publicação no momento em que ela é criada. *auto_identity_range* é **nvarchar (5)**, com um padrão de FALSE. **True** permite que o intervalo de identidade automática durante a manipulação, **false** desabilita.  
  
> [!NOTE]  
>  *auto_identity_range* foi preterido e é fornecida para compatibilidade com versões anteriores apenas. Você deve usar *identityrangemanagementoption* para especificar opções de gerenciamento de intervalo de identidade. Para obter mais informações, consulte [Replicar colunas de identidade](../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
 [  **@pub_identity_range=** ] *pub_identity_range*  
 Controla o tamanho do intervalo de identidades alocado a um Assinante com assinatura de servidor quando o gerenciamento automático do intervalo de identidades for usado. Esse intervalo de identidade é reservado para um Assinante de republicação para ser alocado a seus próprios Assinantes. *pub_identity_range* é **bigint**, com um padrão NULL. Você deve especificar esse parâmetro se *identityrangemanagementoption* é **automática** ou se *auto_identity_range* é **true**.  
  
 [  **@identity_range=** ] *identity_range*  
 Controla o tamanho do intervalo de identidades alocado ao Publicador e ao Assinante quando o gerenciamento automático do intervalo é usado. *identity_range* é **bigint**, com um padrão NULL. Você deve especificar esse parâmetro se *identityrangemanagementoption* é **automática** ou se *auto_identity_range* é **true**.  
  
> [!NOTE]  
>  *identity_range* controla o tamanho do intervalo de identidade nos assinantes de republicação usando versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [  **@threshold=** ] *limite*  
 Valor de porcentagem que controla quando o Merge Agent atribui um novo intervalo de identidade. Quando a porcentagem de valores especificada em *limite* é usado, o agente de mesclagem cria um novo intervalo de identidade. *limite de* é **int**, com um padrão NULL. Você deve especificar esse parâmetro se *identityrangemanagementoption* é **automática** ou se *auto_identity_range* é **true**.  
  
 [  **@verify_resolver_signature=** ] *verify_resolver_signature*  
 Especifica se uma assinatura digital é verificada antes de usar um resolvedor em replicação de mesclagem. *verify_resolver_signature* é **int**, com um padrão de 1.  
  
 **0** Especifica que a assinatura não será verificada.  
  
 **1** Especifica que a assinatura será verificada para ver se ele é de uma fonte confiável.  
  
 [  **@destination_object=** ] **'***destination_object***'**  
 É o nome do objeto criado no banco de dados de assinatura. *destination_object* é **sysname**, com um valor padrão do que **@source_object**. Este parâmetro é especificado somente se o artigo for um artigo apenas de esquema, como procedimentos armazenados, exibições e UDFs. Se o artigo especificado for um artigo de tabela, o valor em *@source_object* substitui o valor no *destination_object*.  
  
 [  **@allow_interactive_resolver=** ] **'***allow_interactive_resolver***'**  
 Habilita ou desabilita o uso do Resolvedor Interativo de um artigo. *allow_interactive_resolver* é **nvarchar (5)**, com um padrão de FALSE. **True** permite o uso do resolvedor interativo no artigo; **false** desabilita.  
  
> [!NOTE]  
>  O Resolvedor Interativo não tem o suporte dos Assinantes [!INCLUDE[ssEW](../../includes/ssew-md.md)].  
  
 [  **@fast_multicol_updateproc=** ] **'***fast_multicol_updateproc***'**  
 Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts.  
  
 [  **@check_permissions=** ] *check_permissions*  
 É um bitmap das permissões do nível de tabela que são verificadas quando o Merge Agent aplica alterações ao Editor. Se o logon/conta de usuário do Publicador usado pelo processo de mesclagem não possuir as permissões corretas de tabela, as alterações inválidas serão registradas como conflitos. *check_permissions* é **int**e pode ser o [| (OR bit a bit) ](../../t-sql/language-elements/bitwise-or-transact-sql.md) produto de um ou mais dos valores a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**0x00** (padrão)|As permissões não são verificadas.|  
|**0x10**|Verifica as permissões no Editor antes que as operações de inserção realizadas em um Assinante possam ser carregadas.|  
|**0x20**|Verifica as permissões no publicador antes que as operações de atualização no assinante sejam carregadas.|  
|**0x40**|Verifica as permissões no Editor antes que as operações de atualização realizadas em um Assinante possam ser carregadas.|  
  
 [  **@force_invalidate_snapshot=** ] *force_invalidate_snapshot*  
 Confirma que a ação tomada por esse procedimento armazenado pode invalidar um instantâneo existente. *force_invalidate_snapshot* é um **bit**, com um padrão de 0.  
  
 **0** Especifica que a adição de um artigo não faz com que o instantâneo seja inválido. Se o procedimento armazenado detectar que a alteração requer um novo instantâneo, ocorrerá um erro e nenhuma alteração será feita.  
  
 **1** Especifica que adicionar um artigo pode invalidar o instantâneo inválido e se houver assinaturas existentes que exigem um novo instantâneo, dará permissão para que o instantâneo existente seja marcado como obsoleto e um novo instantâneo seja gerado. *force_invalidate_snapshot* é definido como **1** ao adicionar um artigo em uma publicação com um instantâneo existente.  
  
 [  **@published_in_tran_pub=** ] **'***published_in_tran_pub***'**  
 Indica que um artigo em uma publicação de mesclagem também é publicado em uma publicação transacional. *published_in_tran_pub* é **nvarchar (5)**, com um padrão de FALSE. **True** Especifica que o artigo também é publicado em uma publicação transacional.  
  
 [  **@force_reinit_subscription=** ] *force_reinit_subscription*  
 Confirma que a ação tomada por esse procedimento armazenado pode exigir que as assinaturas existentes sejam reinicializadas. *force_reinit_subscription* é um **bit**, com um padrão de 0.  
  
 **0** Especifica que a adição de um artigo não faz com que a assinatura ser reiniciada. Se o procedimento armazenado detectar que a alteração irá requerer assinaturas existentes para ser reiniciada, ocorrerá um erro e nenhuma alteração será feita.  
  
 **1** significa que as alterações no artigo de mesclagem faz com que as assinaturas existentes sejam reinicializadas e dá permissão para que ocorra a reinicialização da assinatura. *force_reinit_subscription* é definido como **1** quando *subset_filterclause* Especifica um filtro de linha com parâmetros.  
  
 [  **@logical_record_level_conflict_detection=** ] **'***logical_record_level_conflict_detection***'**  
 Especifica o nível de detecção de conflito para um artigo que é um membro de um registro lógico. *logical_record_level_conflict_detection* é **nvarchar (5)**, com um padrão de FALSE.  
  
 **True** Especifica que um conflito será detectado se alterações forem feitas em qualquer lugar no registro lógico.  
  
 **False** Especifica que a detecção de conflito padrão é usada conforme especificado por *column_tracking*. Para obter mais informações, consulte [Agrupar alterações a linhas relacionadas com registros lógicos](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
> [!NOTE]  
>  Porque não há suporte para registros lógicos por [!INCLUDE[ssEW](../../includes/ssew-md.md)] assinantes, você deve especificar um valor de **false** para *logical_record_level_conflict_detection* para dar suporte a esses assinantes.  
  
 [  **@logical_record_level_conflict_resolution=** ] **'***logical_record_level_conflict_resolution***'**  
 Especifica o nível de resolução de conflito para um artigo que é um membro de um registro lógico. *logical_record_level_conflict_resolution* é **nvarchar (5)**, com um padrão de FALSE.  
  
 **True** Especifica que todo registro lógico vencedor substituirá o registro lógico perdedor.  
  
 **False** Especifica que as linhas vencedoras não são restritas ao registro lógico. Se *logical_record_level_conflict_detection* é **true**, em seguida, *logical_record_level_conflict_resolution* também deve ser definido como **true**. Para obter mais informações, consulte [Agrupar alterações a linhas relacionadas com registros lógicos](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
> [!NOTE]  
>  Porque não há suporte para registros lógicos por [!INCLUDE[ssEW](../../includes/ssew-md.md)] assinantes, você deve especificar um valor de **false** para *logical_record_level_conflict_resolution* para dar suporte a esses assinantes.  
  
 [  **@partition_options=** ] *partition_options*  
 Define a forma pela qual os dados no artigo são particionados, o que habilita otimizações de desempenho quando todas as linhas pertencem a apenas uma partição ou assinatura. *partition_options* é **tinyint**, e pode ser um dos valores a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**0** (padrão)|A filtragem para o artigo ou é estática ou não gera um único subconjunto de dados para cada partição, ou seja, uma partição "sobreposta".|  
|**1**|As partições são sobrepostas e as atualizações de linguagem de manipulação de dados (DML) feitas ao Assinante não podem alterar a partição à qual uma linha pertence.|  
|**2**|A filtragem do artigo gera partições não sobrepostas, mas vários Assinantes podem receber a mesma partição.|  
|**3**|A filtragem para o artigo gera partições não sobrepostas exclusivas de cada assinatura.|  
  
> [!NOTE]  
>  Se a tabela de origem para um artigo já estiver publicada em outra publicação, em seguida, o valor de *partition_options* devem ser as mesmas para os dois artigos.  
  
 [  **@processing_order=** ] *processing_order*  
 Indica a ordem de processamento de artigos em uma publicação de mesclagem. *processing_order* é **int**, com um padrão de 0. **0** Especifica que o artigo está fora de ordem, e qualquer outro valor representa o valor ordinal da ordem de processamento para esse artigo. Os artigos são processados em ordem crescente de valores. Se dois artigos tiverem o mesmo valor, ordem de processamento é determinada pela ordem o apelido do artigo no [sysmergearticles](../../relational-databases/system-tables/sysmergearticles-transact-sql.md) tabela do sistema. Para obter mais informações, consulte [Especificar a ordem de processamento dos artigos de mesclagem](../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md).  
  
 [  **@subscriber_upload_options=** ] *subscriber_upload_options*  
 Define restrições em atualizações realizadas em um Assinante com uma assinatura de cliente. Para obter mais informações, consulte [Optimize Merge Replication Performance with Download-Only Articles](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md) (Otimizar o desempenho da replicação de mesclagem com artigos somente para download). *subscriber_upload_options* é **tinyint**, e pode ser um dos valores a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**0** (padrão)|Sem restrições. As alterações feitas no Assinante são carregadas no Publicador.|  
|**1**|As alterações são permitidas no Assinante, mas não são carregadas no Publicador.|  
|**2**|As alterações não são permitidas no Assinante.|  
  
 Alterar *subscriber_upload_options* exige que a assinatura seja reinicializada chamando [sp_reinitmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-reinitmergepullsubscription-transact-sql.md).  
  
> [!NOTE]  
>  Se a tabela de origem para um artigo já estiver publicada em outra publicação, o valor de *subscriber_upload_options* devem ser as mesmas para os dois artigos.  
  
 [  **@identityrangemanagementoption=** ] *identityrangemanagementoption*  
 Especifica como o gerenciamento de intervalo de identidade é tratado para o artigo. *identityrangemanagementoption* é **nvarchar (10)**, e pode ser um dos valores a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Nenhum**|Desabilita o gerenciamento de intervalo de identidade.|  
|**Manual**|Marca a coluna de identidade usando NOT FOR REPLICATION para ativar tratamento de intervalo de identidade manual.|  
|**Automático**|Especifica o gerenciamento automático de intervalos de identidade.|  
|NULL(default)|O padrão será a **nenhum**quando o valor de *auto_identity_range* não é **true**.|  
  
 Para compatibilidade com versões anteriores, quando o valor de *identityrangemanagementoption* for NULL, o valor de *auto_identity_range* é verificada. No entanto, quando o valor de *identityrangemanagementoption* não é nulo, então o valor de *auto_identity_range* será ignorado. Para obter mais informações, consulte [Replicar colunas de identidade](../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
 [  **@delete_tracking=** ] **'***delete_tracking***'**  
 Indica se as exclusões são replicadas. *delete_tracking* é **nvarchar (5)**, com um padrão de TRUE. **False** indica que as exclusões não são replicadas, e **true** indica que as exclusões são replicadas, que é o comportamento comum para replicação de mesclagem. Quando *delete_tracking* é definido como **false**, linhas excluídas no assinante devem ser removidas manualmente no publicador e linhas excluídas no publicador devem ser removidas manualmente no assinante.  
  
> [!IMPORTANT]  
>  Configuração *delete_tracking* para **false** resulta em não convergência. Se a tabela de origem para um artigo já estiver publicada em outra publicação, em seguida, o valor de *delete_tracking* devem ser as mesmas para os dois artigos.  
  
> [!NOTE]  
>  *delete_tracking* opções não podem ser definidas usando o **Assistente para nova publicação** ou **propriedades de publicação** caixa de diálogo.  
  
 [  **@compensate_for_errors=** ] **'***compensate_for_errors***'**  
 Indica se ações de compensação são executadas quando são encontrados erros durante a sincronização. *compensate_for_errors i*s **nvarchar (5)**, com um padrão de FALSE. Quando definido como **true**, as alterações que não podem ser aplicadas no assinante ou publicador durante sincronização sempre levam a ações de compensação para desfazer a alteração; no entanto, uma configurada incorretamente assinante que gera um erro pode fazer com que as alterações em outros assinantes e Publicadores sejam desfeitos. **False** desabilita essas ações de compensação, no entanto, os erros ainda são registradas como com compensação e as mesclagens subsequentes continua a tentativa de aplicar as alterações até obter êxito.  
  
> [!IMPORTANT]  
>  Embora os dados nas linhas afetadas pareçam estar fora de convergência, assim que você resolver qualquer erro, as alterações poderão ser aplicadas e os dados convergidos. Se a tabela de origem para um artigo já estiver publicada em outra publicação, em seguida, o valor de *compensate_for_errors* devem ser as mesmas para os dois artigos.  
  
 [  **@stream_blob_columns=** ] **'***stream_blob_columns***'**  
 Especifica que uma otimização de fluxo de dados ser usada ao replicar colunas de objeto binário grande. *stream_blob_columns* é **nvarchar (5)**, com um padrão de FALSE. **True** significa que a otimização será tentada. *stream_blob_columns* é definida como true quando FILESTREAM está habilitado. Isso permite a replicação de dados FILESTREAM para executar da maneira ideal e reduzir a utilização de memória. Para forçar os artigos de tabela FILESTREAM a não usarem o fluxo de blob, use **sp_changemergearticle** definir *stream_blob_columns* como false.  
  
> [!IMPORTANT]  
>  A habilitação dessa otimização de memória pode reduzir o desempenho do Agente de Mesclagem durante a sincronização. Esta opção só deve ser usada ao replicar colunas que contêm megabytes de dados.  
  
> [!NOTE]  
>  Certas funcionalidades de replicação de mesclagem, como registros lógicos, ainda podem impedir que a otimização de fluxo seja usada quando replicar objetos grandes binários mesmo com *stream_blob_columns* definida como **true**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_addmergearticle** é usado em replicação de mesclagem.  
  
 Quando você publicar objetos, suas definições são copiadas aos Assinantes. Se você estiver publicando um objeto de banco de dados que depende de outros objetos, precisará publicar todos os objetos referenciados. Por exemplo, se você publicar uma exibição que depende de uma tabela, terá de publicar a tabela também.  
  
 Se você especificar um valor de **3** para *partition_options*, pode haver apenas uma única assinatura para cada partição de dados nesse artigo. Se uma segunda assinatura for criada na qual o critério de filtragem da nova assinatura for resolvido para a mesma partição como a assinatura existente, a assinatura existente será cancelada.  
  
 Ao especificar um valor de 3 para *partition_options*, metadados são limpos sempre que o Merge Agent é executado e o instantâneo particionado irá expirar mais rapidamente. Ao usar essa opção, considere habilitar o instantâneo particionado solicitado pelo assinante. Para obter mais informações, consulte [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
 Adicionar um artigo com um filtro estático horizontal, usando *subset_filterclause*, para uma publicação existente com artigos que têm filtros parametrizados requer que as assinaturas sejam reinicializadas.  
  
 Ao especificar *processing_order*, recomendamos deixar lacunas entre os valores da ordem de artigo, que torna mais fácil definir novos valores no futuro. Por exemplo, se você tiver três artigos artigo1, artigo2 e artigo3, definir *processing_order* 10, 20, 30, em vez de 1, 2 e 3. Para obter mais informações, consulte [Especificar a ordem de processamento dos artigos de mesclagem](../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md).  
  
## <a name="default-schema-option-table"></a>Tabela de opção de esquema padrão  
 Esta tabela descreve o valor padrão é definido pelo procedimento armazenado se um valor nulo for especificado para *schema_option*, que depende do tipo de artigo.  
  
|Tipo de artigo|Valor de opção de esquema|  
|------------------|-------------------------|  
|**somente esquema de função**|**0x01**|  
|**somente o esquema de exibição indexada**|**0x01**|  
|**somente esquema de PROC**|**0x01**|  
|**table**|**0x0C034FD1**  -  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e publicações compatíveis posteriores com um instantâneo de modo nativo.<br /><br /> **0x08034FF1**  -  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e publicações compatíveis posteriores com um instantâneo de modo de caractere.|  
|**somente o esquema de exibição**|**0x01**|  
  
> [!NOTE]  
>  Se a publicação oferece suporte a versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a opção de esquema padrão para **tabela** é **0x30034FF1**.  
  
## <a name="valid-schema-option-table"></a>Tabela de opção de esquema válida  
 A tabela a seguir descreve os valores permitidos *schema_option* dependendo do tipo de artigo.  
  
|Tipo de artigo|Valores de opção de esquema|  
|------------------|--------------------------|  
|**somente esquema de função**|**0x01** e **0x2000**|  
|**somente o esquema de exibição indexada**|**0x01**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x1000000**e **0x200000**|  
|**somente esquema de PROC**|**0x01** e **0x2000**|  
|**table**|Todas as opções.|  
|**somente o esquema de exibição**|**0x01**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x1000000**e **0x200000**|  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_AddMergeArticle](../../relational-databases/replication/codesnippet/tsql/sp-addmergearticle-trans_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Exige associação à função de servidor fixa **sysadmin** ou à função de banco de dados fixa **db_owner** .  
  
## <a name="see-also"></a>Consulte também  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [Publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Replicar colunas de identidade](../../relational-databases/replication/publish/replicate-identity-columns.md)   
 [sp_changemergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [sp_dropmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md)   
 [sp_helpmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
