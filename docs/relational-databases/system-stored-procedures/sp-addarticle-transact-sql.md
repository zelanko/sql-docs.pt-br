---
title: sp_addarticle (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addarticle
- sp_addarticle_TSQL
helpviewer_keywords:
- sp_addarticle
ms.assetid: 0483a157-e403-4fdb-b943-23c1b487bef0
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: e337e04714b0d8dcc9a8227ca48ad9dc33dcc3dc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68811389"
---
# <a name="sp_addarticle-transact-sql"></a>sp_addarticle (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Cria um artigo e adiciona-o a uma publicação. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addarticle [ @publication = ] 'publication'   
        , [ @article = ] 'article'   
    [ , [ @source_table = ] 'source_table' ]  
    [ , [ @destination_table = ] 'destination_table' ]   
    [ , [ @vertical_partition = ] 'vertical_partition' ]   
    [ , [ @type = ] 'type' ]   
    [ , [ @filter = ] 'filter' ]   
    [ , [ @sync_object= ] 'sync_object' ]   
        [ , [ @ins_cmd = ] 'ins_cmd' ]   
    [ , [ @del_cmd = ] 'del_cmd' ]   
        [ , [ @upd_cmd = ] 'upd_cmd' ]   
    [ , [ @creation_script = ] 'creation_script' ]   
    [ , [ @description = ] 'description' ]   
    [ , [ @pre_creation_cmd = ] 'pre_creation_cmd' ]   
    [ , [ @filter_clause = ] 'filter_clause' ]   
    [ , [ @schema_option = ] schema_option ]   
    [ , [ @destination_owner = ] 'destination_owner' ]   
    [ , [ @status = ] status ]   
    [ , [ @source_owner = ] 'source_owner' ]   
    [ , [ @sync_object_owner = ] 'sync_object_owner' ]   
    [ , [ @filter_owner = ] 'filter_owner' ]   
    [ , [ @source_object = ] 'source_object' ]   
    [ , [ @artid = ] article_ID  OUTPUT ]   
    [ , [ @auto_identity_range = ] 'auto_identity_range' ]   
    [ , [ @pub_identity_range = ] pub_identity_range ]   
    [ , [ @identity_range = ] identity_range ]   
    [ , [ @threshold = ] threshold ]   
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @use_default_datatypes = ] use_default_datatypes  
    [ , [ @identityrangemanagementoption = ] identityrangemanagementoption ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @fire_triggers_on_snapshot = ] 'fire_triggers_on_snapshot' ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação que contém o artigo. O nome deve ser exclusivo no banco de dados. a *publicação* é **sysname**, sem padrão.  
  
`[ @article = ] 'article'`É o nome do artigo. O nome deve ser exclusivo na publicação. o *artigo* é **sysname**, sem padrão.  
  
`[ @source_table = ] 'source_table'`Este parâmetro foi preterido; em vez disso, use *source_object* .  
  
 *Não há suporte para esse parâmetro em Publicadores Oracle.*  
  
`[ @destination_table = ] 'destination_table'`É o nome da tabela de destino (assinatura), se for diferente do *source_table*ou do procedimento armazenado. *destination_table* é **sysname**, com um padrão de NULL, o que significa que *source_table* é igual a *destination_table * *.*  
  
`[ @vertical_partition = ] 'vertical_partition'`Habilita e desabilita a filtragem de coluna em um artigo de tabela. *vertical_partition* é **nchar (5)**, com um padrão de false.  
  
 **false** indica que não há nenhuma filtragem vertical e publica todas as colunas.  
  
 **verdadeiro** limpa todas as colunas, exceto a chave primária declarada, colunas anuláveis sem padrão e colunas de chave exclusivas. As colunas são adicionadas usando [sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md).  
  
`[ @type = ] 'type'`É o tipo de artigo. o *tipo* é **sysname**e pode ser um dos valores a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**aggregate schema only**|Função de agregação apenas com esquema.|  
|**func schema only**|Função somente com esquema.|  
|**indexed view logbased**|Artigo de exibição indexada com base em log. Sem suporte para Publicadores Oracle. Para este tipo de artigo, a tabela base não precisa ser publicada separadamente.|  
|**indexed view logbased manualboth**|Artigo de exibição indexada com filtro manual e exibição manual. Essa opção requer que você especifique os parâmetros *sync_object* e *Filter* . Para este tipo de artigo, a tabela base não precisa ser publicada separadamente. Sem suporte para Publicadores Oracle.|  
|**indexed view logbased manualfilter**|Artigo de exibição indexada com filtro manual. Essa opção requer que você especifique os parâmetros *sync_object* e *Filter* . Para este tipo de artigo, a tabela base não precisa ser publicada separadamente. Sem suporte para Publicadores Oracle.|  
|**indexed view logbased manualview**|Artigo de exibição indexada com base em log com exibição manual. Essa opção requer que você especifique o parâmetro *sync_object* . Para este tipo de artigo, a tabela base não precisa ser publicada separadamente. Sem suporte para Publicadores Oracle.|  
|**indexed view schema only**|Exibição indexada somente com esquema Para esse tipo de artigo, a tabela base também deve ser publicada.|  
|**logbased** (padrão)|Artigo com base em log.|  
|**logbased manualboth**|Artigo com base em log com filtro manual e exibição manual. Essa opção requer que você especifique os parâmetros *sync_object* e *Filter* . Sem suporte para Publicadores Oracle.|  
|**logbased manualfilter**|Artigo com base em log com filtro manual. Essa opção requer que você especifique os parâmetros *sync_object* e *Filter* . Sem suporte para Publicadores Oracle.|  
|**logbased manualview**|Artigo com base em log com exibição manual. Essa opção requer que você especifique o parâmetro *sync_object* . Sem suporte para Publicadores Oracle.|  
|**proc exec**|Replica a execução do procedimento armazenado para todos os assinantes do artigo. Sem suporte para Publicadores Oracle. Recomendamos que você use a opção **proc exec serializável** em vez de **proc exec**. Para obter mais informações, consulte a seção "tipos de artigos de execução de procedimento armazenado" em [publicando a execução do procedimento armazenado na replicação transacional](../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md). Não disponível quando a opção alterar captura de dados está habilitada.|  
|**proc schema only**|Procedimento apenas com esquema. Sem suporte para Publicadores Oracle.|  
|**serializable proc exec**|Replica a execução do procedimento armazenado apenas se ele for executado no contexto de uma transação serializável. Sem suporte para Publicadores Oracle.<br /><br /> Você também deve executar o procedimento dentro de uma transação explícita para que a execução do mesmo seja replicada.|  
|**view schema only**|Exibição somente com esquema Sem suporte para Publicadores Oracle. Ao usar essa opção, você também deve publicar a tabela base.|  
  
`[ @filter = ] 'filter'`É o procedimento armazenado (criado com para replicação) usado para filtrar a tabela horizontalmente. *Filter* é **nvarchar (386)**, com um padrão de NULL. [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) e [sp_articlefilter](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) devem ser executadas manualmente para criar a exibição e filtrar o procedimento armazenado. Se não for NULL, o procedimento de filtro não é criado (supõe que o procedimento armazenado é criado manualmente).  
  
`[ @sync_object = ] 'sync_object'`É o nome da tabela ou exibição usada para produzir o arquivo de dados usado para representar o instantâneo deste artigo. *sync_object* é **nvarchar (386)**, com um padrão de NULL. Se for NULL, [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) será chamado para criar automaticamente a exibição usada para gerar o arquivo de saída. Isso ocorre depois de adicionar qualquer coluna com [sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md). Se não for NULL, uma exibição não será criada (supõe que a exibição é criada manualmente).  
  
`[ @ins_cmd = ] 'ins_cmd'`É o tipo de comando de replicação usado ao replicar inserções para este artigo. *ins_cmd* é **nvarchar (255)** e pode ser um dos valores a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**NONE**|Nenhuma ação é tomada.|  
|**CALL sp_MSins_**<br /> **_tabela_** (padrão)<br /><br /> -ou-<br /><br /> **CALL custom_stored_procedure_name**|Chama um procedimento armazenado a ser executado no Assinante. Para usar esse método de replicação, use *schema_option* para especificar a criação automática do procedimento armazenado ou crie o procedimento armazenado especificado no banco de dados de destino de cada assinante do artigo. *custom_stored_procedure* é o nome de um procedimento armazenado criado pelo usuário. <strong>sp_MSins_*tabela* </strong> contém o nome da tabela de destino no lugar da *_table* parte do parâmetro. Quando *destination_owner* é especificado, ele é anexado ao nome da tabela de destino. Por exemplo, para a tabela **ProductCategory** de Propriedade do esquema de **produção** no Assinante, o parâmetro seria `CALL sp_MSins_ProductionProductCategory`. Para um artigo em uma topologia de replicação ponto a ponto, *_table* é acrescentado com um valor de GUID. Não há suporte para a especificação de *custom_stored_procedure* para assinantes de atualização.|  
|**SQL** ou NULL|Replica uma instrução INSERT. A instrução INSERT fornece valores para todas as colunas publicadas no artigo. Esse comando é replicado em inserções:<br /><br /> `INSERT INTO <table name> VALUES (c1value, c2value, c3value, ..., cnvalue)`|  
  
 Para obter mais informações, consulte [Especificar como as alterações são propagadas para artigos transacionais](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
`[ @del_cmd = ] 'del_cmd'`É o tipo de comando de replicação usado ao replicar exclusões para este artigo. *del_cmd* é **nvarchar (255)** e pode ser um dos valores a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**NONE**|Nenhuma ação é tomada.|  
|**CALLsp_MSdel_**<br /> **_tabela_** (padrão)<br /><br /> -ou-<br /><br /> **CALL custom_stored_procedure_name**|Chama um procedimento armazenado a ser executado no Assinante. Para usar esse método de replicação, use *schema_option* para especificar a criação automática do procedimento armazenado ou crie o procedimento armazenado especificado no banco de dados de destino de cada assinante do artigo. *custom_stored_procedure* é o nome de um procedimento armazenado criado pelo usuário. <strong>sp_MSdel_*tabela* </strong> contém o nome da tabela de destino no lugar da *_table* parte do parâmetro. Quando *destination_owner* é especificado, ele é anexado ao nome da tabela de destino. Por exemplo, para a tabela **ProductCategory** de Propriedade do esquema de **produção** no Assinante, o parâmetro seria `CALL sp_MSdel_ProductionProductCategory`. Para um artigo em uma topologia de replicação ponto a ponto, *_table* é acrescentado com um valor de GUID. Não há suporte para a especificação de *custom_stored_procedure* para assinantes de atualização.|  
|**XCALL sp_MSdel_**<br /> **_tabela_**<br /><br /> -ou-<br /><br /> **XCALL custom_stored_procedure_name**|Chama um procedimento armazenado com o uso de parâmetros no estilo XCALL. Para usar esse método de replicação, use *schema_option* para especificar a criação automática do procedimento armazenado ou crie o procedimento armazenado especificado no banco de dados de destino de cada assinante do artigo. Não é permitido especificar um procedimento armazenado para atualizar assinantes.|  
|**SQL** ou NULL|Replica uma instrução DELETE. A instrução DELETE é fornecida em todos os valores de coluna de chave primária. Esse comando é replicado em exclusões:<br /><br /> `DELETE FROM <table name> WHERE pkc1 = pkc1value AND pkc2 = pkc2value AND pkcn = pkcnvalue`|  
  
 Para obter mais informações, consulte [Especificar como as alterações são propagadas para artigos transacionais](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
`[ @upd_cmd = ] 'upd_cmd'`É o tipo de comando de replicação usado ao replicar atualizações para este artigo. *upd_cmd* é **nvarchar (255)** e pode ser um dos valores a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**NONE**|Nenhuma ação é tomada.|  
|**CALL sp_MSupd_**<br /> **_tabela_**<br /><br /> -ou-<br /><br /> **CALL custom_stored_procedure_name**|Chama um procedimento armazenado a ser executado no Assinante. Para usar esse método de replicação, use *schema_option* para especificar a criação automática do procedimento armazenado ou crie o procedimento armazenado especificado no banco de dados de destino de cada assinante do artigo.|  
|**MCALL sp_MSupd_**<br /> **_tabela_**<br /><br /> -ou-<br /><br /> **MCALL custom_stored_procedure_name**|Chama um procedimento armazenado com o uso de parâmetros no estilo MCALL. Para usar esse método de replicação, use *schema_option* para especificar a criação automática do procedimento armazenado ou crie o procedimento armazenado especificado no banco de dados de destino de cada assinante do artigo. *custom_stored_procedure* é o nome de um procedimento armazenado criado pelo usuário. <strong>sp_MSupd_*tabela* </strong> contém o nome da tabela de destino no lugar da *_table* parte do parâmetro. Quando *destination_owner* é especificado, ele é anexado ao nome da tabela de destino. Por exemplo, para a tabela **ProductCategory** de Propriedade do esquema de **produção** no Assinante, o parâmetro seria `MCALL sp_MSupd_ProductionProductCategory`. Para um artigo em uma topologia de replicação ponto a ponto, *_table* é acrescentado com um valor de GUID. Não é permitido especificar um procedimento armazenado para atualizar assinantes.|  
|**SCALL sp_MSupd_**<br /> **_tabela_** (padrão)<br /><br /> -ou-<br /><br /> **SCALL custom_stored_procedure_name**|Chama um procedimento armazenado com o uso de parâmetros no estilo SCALL. Para usar esse método de replicação, use *schema_option* para especificar a criação automática do procedimento armazenado ou crie o procedimento armazenado especificado no banco de dados de destino de cada assinante do artigo. *custom_stored_procedure* é o nome de um procedimento armazenado criado pelo usuário. <strong>sp_MSupd_*tabela* </strong> contém o nome da tabela de destino no lugar da *_table* parte do parâmetro. Quando *destination_owner* é especificado, ele é anexado ao nome da tabela de destino. Por exemplo, para a tabela **ProductCategory** de Propriedade do esquema de **produção** no Assinante, o parâmetro seria `SCALL sp_MSupd_ProductionProductCategory`. Para um artigo em uma topologia de replicação ponto a ponto, *_table* é acrescentado com um valor de GUID. Não é permitido especificar um procedimento armazenado para atualizar assinantes.|  
|**XCALL sp_MSupd_**<br /> **_tabela_**<br /><br /> -ou-<br /><br /> **XCALL custom_stored_procedure_name**|Chama um procedimento armazenado com o uso de parâmetros no estilo XCALL. Para usar esse método de replicação, use *schema_option* para especificar a criação automática do procedimento armazenado ou crie o procedimento armazenado especificado no banco de dados de destino de cada assinante do artigo. Não é permitido especificar um procedimento armazenado para atualizar assinantes.|  
|**SQL** ou NULL|Replica uma instrução UPDATE. A instrução UPDATE é fornecida em todos os valores de coluna e os valores de coluna de chave primária. Esse comando é replicado em atualizações:<br /><br /> `UPDATE <table name> SET c1 = c1value, SET c2 = c2value, SET cn = cnvalue WHERE pkc1 = pkc1value AND pkc2 = pkc2value AND pkcn = pkcnvalue`|  
  
> [!NOTE]  
>  A sintaxe de CALL, MCALL, SCALL e XCALL varia a quantidade de dados propagada ao assinante. A sintaxe de CALL passa todos os valores para todas as colunas inseridas e excluídas. A sintaxe de SCALL passa valores apenas para as colunas afetadas. A sintaxe de XCALL passa valores para todas as colunas, alteradas ou não, inclusive o valor anterior da coluna. Para obter mais informações, consulte [Especificar como as alterações são propagadas para artigos transacionais](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
`[ @creation_script = ] 'creation_script'`É o caminho e o nome de um script de esquema de artigo opcional usado para criar o artigo no banco de dados de assinatura. *creation_script* é **nvarchar (255)**, com um padrão de NULL.  
  
`[ @description = ] 'description'`É uma entrada descritiva para o artigo. a *Descrição* é **nvarchar (255)**, com um padrão de NULL.  
  
`[ @pre_creation_cmd = ] 'pre_creation_cmd'`Especifica o que o sistema deve fazer se detectar um objeto existente de mesmo nome no Assinante ao aplicar o instantâneo deste artigo. *pre_creation_cmd* é **nvarchar (10)** e pode ser um dos valores a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**None**|Não usa um comando.|  
|**apagar**|Exclui dados da tabela de destino antes de aplicar o instantâneo. Quando o artigo é filtrado horizontalmente, apenas dados em colunas especificadas pela cláusula de filtro são excluídos. Não há suporte para Publicadores Oracle quando um filtro horizontal está definido.|  
|**descartar** (padrão)|Descarta a tabela de destino.|  
|**truncar**|Trunca a tabela de destino. Não é válido para assinantes ODBC ou OLE DB.|  
  
`[ @filter_clause = ] 'filter_clause'`É uma cláusula de restrição (WHERE) que define um filtro horizontal. Ao inserir a cláusula de restrição, omita a palavra-chave WHERE. *filter_clause* é **ntext**, com um padrão de NULL. Para obter mais informações, consulte [Filter Published Data](../../relational-databases/replication/publish/filter-published-data.md) (Filtrar dados publicados).  
  
`[ @schema_option = ] schema_option`É um bitmask da opção de geração de esquema para o artigo fornecido. *schema_option* é **binary (8)** e pode ser [| (OR-bit)](../../t-sql/language-elements/bitwise-or-transact-sql.md) produto de um ou mais destes valores:  
  
> [!NOTE]  
>  Se esse valor for NULL, o sistema gerará automaticamente uma opção de esquema válida para o artigo dependendo de outras propriedades do artigo. A tabela de **Opções de esquema padrão** fornecida nos comentários mostra o valor que será escolhido com base na combinação do tipo de artigo e do tipo de replicação.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**0x00**|Desabilita o script pelo Agente de Instantâneo e usa *creation_script*.|  
|**0x01**|Gera o script de criação de objeto (CREATE TABLE, CREATE PROCEDURE e assim por diante). Esse valor é o padrão para artigos de procedimento armazenado.|  
|**0x02**|Gera os procedimentos armazenados que propagam alterações para o artigo, se definido.|  
|**0x04**|Os scripts das colunas de identidade são executados com a propriedade IDENTITY.|  
|**0x08**|Replicar colunas **timestamp** . Se não for definido, as colunas de **carimbo de data/hora** serão replicadas como **binários**.|  
|**0x10**|Gera um índice clusterizado correspondente. Mesmo que essa opção não esteja definida, os índices relacionados às chaves primárias e às restrições exclusivas serão gerados caso já estejam definidos em uma tabela publicada.|  
|**0x20**|Converte UDTs (tipos de dados definidos pelo usuário) em tipos de dados básicos no Assinante. Essa opção não poderá ser usada quando houver uma restrição CHECK ou DEFAULT em uma coluna UDT, se uma coluna UDT for parte da chave primária ou se uma coluna computada fizer referência a uma coluna UDT. *Não há suporte para Publicadores Oracle*.|  
|**0x40**|Gera índices não clusterizados correspondentes. Mesmo que essa opção não esteja definida, os índices relacionados às chaves primárias e às restrições exclusivas serão gerados caso já estejam definidos em uma tabela publicada.|  
|**0x80**|Replica restrições de chave primária. Todos os índices relacionados à restrição também são replicados, mesmo se as opções **0x10** e **0x40** não estiverem habilitadas.|  
|**0x100**|Replica gatilhos de usuário em um artigo de tabela, se definido. *Não há suporte para Publicadores Oracle*.|  
|**0x200**|Replica restrições de chave estrangeira. Se a tabela referenciada não for parte de uma publicação, todas as restrições de chave estrangeira em uma tabela publicada não serão replicadas. *Não há suporte para Publicadores Oracle*.|  
|**0x400**|Replica restrições de verificação. *Não há suporte para Publicadores Oracle*.|  
|**0x800**|Replica padrões. *Não há suporte para Publicadores Oracle*.|  
|**0x1000**|Replica ordenação em nível de coluna.<br /><br /> **Observação:** Essa opção deve ser definida para Publicadores Oracle para habilitar comparações que diferenciam maiúsculas de minúsculas.|  
|**0x2000**|Replica propriedades estendidas associadas com o objeto de origem do artigo publicado. *Não há suporte para Publicadores Oracle*.|  
|**0x4000**|Replica restrições UNIQUE. Todos os índices relacionados à restrição também são replicados, mesmo se as opções **0x10** e **0x40** não estiverem habilitadas.|  
|**0x8000**|Esta opção não é válida para Publicadores [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
|**0x10000**|Replica instruções CHECK como NOT FOR REPLICATION para que as restrições não sejam forçadas durante a sincronização.|  
|**0x20000**|Replica instruções FOREIGN KEY como NOT FOR REPLICATION para que as restrições não sejam forçadas durante a sincronização.|  
|**0x40000**|Replica grupos de arquivos associados a uma tabela ou índice particionado.|  
|**0x80000**|Replica o esquema de partição para uma tabela particionada.|  
|**0x100000**|Replica o esquema de partição para um índice particionado.|  
|**0x200000**|Replica estatísticas de tabela.|  
|**0x400000**|Associações padrão|  
|**0x800000**|Associações de regra|  
|**0x1000000**|Índice de texto completo|  
|**0x2000000**|As coleções de esquema XML vinculadas a colunas **XML** não são replicadas.|  
|**0x4000000**|Replica índices em colunas **XML** .|  
|**0x8000000**|Cria qualquer esquema ainda não presente no assinante.|  
|**0x10000000**|Converte colunas **XML** em **ntext** no Assinante.|  
|**0x20000000**|Converte tipos de dados de objeto grande (**nvarchar (max)**, **varchar (max)** e **varbinary (max)**) introduzidos em [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] tipos de dados com suporte [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]no.|  
|**0x40000000**|Replicar permissões.|  
|**0x80000000**|Tente descartar as dependências de todos os objetos que não fazem parte da publicação.|  
|**0x100000000**|Use esta opção para replicar o atributo FILESTREAM se ele for especificado em colunas **varbinary (max)** . Não especifique essa opção se você estiver replicando tabelas para Assinantes [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Não há suporte para a replicação de tabelas [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] que têm colunas FILESTREAM para assinantes, independentemente de como essa opção de esquema está definida.<br /><br /> Consulte a opção relacionada **0x800000000**.|  
|**0x200000000**|Converte os tipos de dados de data e hora (**Date**, **time**, **DateTimeOffset**e **datetime2**) [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] introduzidos nos tipos de dados com suporte em versões [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]anteriores do.|  
|**0x400000000**|Replica a opção de compactação para dados e índices. Para saber mais, veja [Data Compression](../../relational-databases/data-compression/data-compression.md).|  
|**0x800000000**|Defina essa opção para armazenar dados FILESTREAM em seu próprio grupo de arquivos no Assinante. Se essa opção não for definida, os dados FILESTREAM serão armazenados no grupo de arquivos padrão. A replicação não cria grupos de arquivos; portanto, se você definir essa opção, deverá criar o grupo de arquivos antes de aplicar o instantâneo no Assinante. Para obter mais informações sobre como criar objetos antes de aplicar o instantâneo, consulte [executar scripts antes e depois que o instantâneo for aplicado](../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied).<br /><br /> Consulte a opção relacionada **0x100000000**.|  
|**0x1000000000**|Converte os UDTs (tipos definidos pelo usuário) Common Language Runtime (CLR) com mais de 8000 bytes em **varbinary (max)** para que as colunas do tipo UDT possam ser replicadas para os assinantes [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]que estão executando o.|  
|**0x2000000000**|Converte o tipo de dados **hierarchyid** em **varbinary (max)** para que as colunas do tipo **hierarchyid** possam ser replicadas para os assinantes que estão em execução [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Para obter mais informações sobre como usar colunas **hierarchyid** em tabelas replicadas, consulte [hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md).|  
|**0x4000000000**|Replica qualquer índice filtrado na tabela. Para obter mais informações sobre índices filtrados, consulte [criar índices filtrados](../../relational-databases/indexes/create-filtered-indexes.md).|  
|**0x8000000000**|Converte os tipos de dados **geography** e **Geometry** em **varbinary (max)** para que as colunas desses tipos possam ser replicadas para os [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]assinantes que estão em execução.|  
|**0x10000000000**|Replica índices em colunas do tipo **geography** e **Geometry**.|  
|**0x20000000000**|Replica o atributo SPARSE para colunas. Para obter mais informações sobre esse atributo, consulte [usar colunas esparsas](../../relational-databases/tables/use-sparse-columns.md).|  
|**0x40000000000**|Habilite o script pelo agente de instantâneo para criar a tabela com otimização de memória no Assinante.|  
|**0x80000000000**|Converte o índice clusterizado em índice não clusterizado para artigos com otimização de memória.|  
|**0x400000000000**|Replica quaisquer índices columnstore não clusterizados na (s) tabela (ões)|  
|**0x800000000000**|Replica quaisquer índices columnstore não clusterizados do flitered nas tabelas.|  
|NULO|A replicação define automaticamente *schema_option* como um valor padrão, o valor que depende de outras propriedades de artigo. A tabela "Opções de Esquema Padrão" na seção Observações mostra as opções de esquema padrão com base no tipo de artigo e tipo de replicação.<br /><br /> O padrão para não[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicações é **0x050D3**.|  
  
 Nem todos os valores de *schema_option* são válidos para cada tipo de replicação e tipo de artigo. A tabela de **Opções de esquema válida** na seção comentários mostra as opções de esquema válidas que podem ser escolhidas com base na combinação do tipo de artigo e do tipo de replicação.  
  
`[ @destination_owner = ] 'destination_owner'`É o nome do proprietário do objeto de destino. *destination_owner* é **sysname**, com um padrão de NULL. Quando *destination_owner* não é especificado, o proprietário é especificado automaticamente com base nas seguintes regras:  
  
|Condição|Proprietário do objeto de destino|  
|---------------|------------------------------|  
|Publicação usa a cópia em massa do modo nativo para gerar o instantâneo inicial que só aceita assinantes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|O padrão é o valor de *source_owner*.|  
|Publicado a partir de um não publicador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Assume o proprietário do banco de dados de destino como padrão.|  
|A publicação usa a cópia em massa do modo de caractere para gerar o instantâneo inicial que só aceita assinantes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Não atribuído.|  
  
 Para dar suporte a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes não, *DESTINATION_OWNER* deve ser nulo.  
  
`[ @status = ] status`Especifica se o artigo está ativo e opções adicionais de como as alterações são propagadas. o *status* é **tinyint**e pode ser [| (OR-bit)](../../t-sql/language-elements/bitwise-or-transact-sql.md) produto de um ou mais desses valores.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**1**|O artigo está ativo.|  
|**8**|Inclui o nome da coluna nas instruções INSERT.|  
|**16** (padrão)|Usa instruções parametrizadas.|  
|**24**|Inclui o nome da coluna nas instruções INSERT e usa instruções parametrizadas.|  
|**64**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
 Por exemplo, um artigo ativo que usa instruções com parâmetros teria um valor 17 nessa coluna. Um valor de **0** significa que o artigo está inativo e nenhuma propriedade adicional é definida.  
  
`[ @source_owner = ] 'source_owner'`É o proprietário do objeto de origem. *source_owner* é **sysname**, com um padrão de NULL. *source_owner* deve ser especificado para Publicadores Oracle.  
  
`[ @sync_object_owner = ] 'sync_object_owner'`É o proprietário da exibição que define o artigo publicado. *sync_object_owner* é **sysname**, com um padrão de NULL.  
  
`[ @filter_owner = ] 'filter_owner'`É o proprietário do filtro. *filter_owner* é **sysname**, com um padrão de NULL.  
  
`[ @source_object = ] 'source_object'`É o objeto de banco de dados a ser publicado. *source_object* é **sysname**, com um padrão de NULL. Se *source_table* for NULL, *source_object* não poderá ser nulo. *source_object* deve ser usado em vez de *source_table*. Para obter mais informações sobre os tipos de objetos que podem ser publicados usando a replicação de instantâneo ou transacional, consulte [Publish Data and Database Objects](../../relational-databases/replication/publish/publish-data-and-database-objects.md).  
  
`[ @artid = ] _article_ID_ OUTPUT`É a ID do artigo do novo artigo. *article_id* é **int** com um padrão de NULL e é um parâmetro de saída.  
  
`[ @auto_identity_range = ] 'auto_identity_range'`Habilita e desabilita o tratamento automático de intervalo de identidade em uma publicação no momento da criação. *auto_identity_range* é **nvarchar (5)** e pode ser um dos seguintes valores:  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**true**|Ativa a manipulação de intervalo de identidade automática.|  
|**for**|Desabilita a manipulação de intervalo de identidade automática.|  
|NULL (padrão)|O tratamento de intervalo de identidade é definido por *identityrangemanagementoption*.|  
  
> [!NOTE]  
>  o *auto_identity_range* foi preterido e é fornecido apenas para fins de compatibilidade com versões anteriores. Você deve usar *identityrangemanagementoption* para especificar opções de gerenciamento de intervalo de identidade. Para obter mais informações, consulte [Replicar colunas de identidade](../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
`[ @pub_identity_range = ] pub_identity_range`Controla o tamanho do intervalo no Publicador se o artigo tiver *identityrangemanagementoption* definido como **auto** ou *auto_identity_range* definido como **true**. *pub_identity_range* é **bigint**, com um padrão de NULL. *Não há suporte para Publicadores Oracle*.  
  
`[ @identity_range = ] identity_range`Controla o tamanho do intervalo no Assinante se o artigo tiver *identityrangemanagementoption* definido como **auto** ou *auto_identity_range* definido como **true**. *identity_range* é **bigint**, com um padrão de NULL. Usado quando *auto_identity_range* é definido como **true**. *Não há suporte para Publicadores Oracle*.  
  
`[ @threshold = ] threshold`É o valor percentual que controla quando o Agente de Distribuição atribui um novo intervalo de identidade. Quando a porcentagem de valores especificados no *limite* é usada, o agente de distribuição cria um novo intervalo de identidade. o *limite* é **bigint**, com um padrão de NULL. Usado quando *identityrangemanagementoption* é definido como **auto** ou *auto_identity_range* é definido como **true**. *Não há suporte para Publicadores Oracle*.  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot`O reconhece que a ação executada por esse procedimento armazenado pode invalidar um instantâneo existente. *force_invalidate_snapshot* é um **bit**, com um padrão de 0.  
  
 **0** especifica que a adição de um artigo não faz com que o instantâneo seja inválido. Se o procedimento armazenado detectar que a alteração exige um novo instantâneo, ocorrerá um erro e nenhuma alteração será feita.  
  
 **1** especifica que a adição de um artigo pode fazer com que o instantâneo seja inválido e, se houver assinaturas que exijam um novo instantâneo, dá permissão para que o instantâneo existente seja marcado como obsoleto e um novo instantâneo seja gerado.  
  
`[ @use_default_datatypes = ] use_default_datatypes`É se os mapeamentos de tipo de dados de coluna padrão são usados ao publicar um artigo de um Publicador Oracle. *use_default_datatypes* é bit, com um padrão de 1.  
  
 **1** = os mapeamentos de coluna de artigo padrão são usados. Os mapeamentos de tipo de dados padrão podem ser exibidos executando [sp_getdefaultdatatypemapping](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md).  
  
 **0** = os mapeamentos de coluna de artigo personalizado são definidos e, portanto, [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) não é chamado pelo **sp_addarticle**.  
  
 Quando *use_default_datatypes* é definido como **0**, você deve executar [sp_changearticlecolumndatatype](../../relational-databases/system-stored-procedures/sp-changearticlecolumndatatype-transact-sql.md) uma vez para cada mapeamento de coluna sendo alterado do padrão. Depois que todos os mapeamentos de coluna personalizados tiverem sido definidos, você deverá executar [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md).  
  
> [!NOTE]  
>  Esse parâmetro só deve ser usado para Publicadores Oracle. A configuração de *use_default_datatypes* como **0** para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador gera um erro.  
  
`[ @identityrangemanagementoption = ] identityrangemanagementoption`Especifica como o gerenciamento de intervalo de identidade é tratado para o artigo. *identityrangemanagementoption* é **nvarchar (10)** e pode ser um dos valores a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**None**|A replicação não faz nenhum gerenciamento de intervalo de identidade explícito. Essa opção só é recomendada para compatibilidade com versões anteriores do SQL Server. Não permitido para replicação hierárquica.|  
|**Manual**|Marca a coluna de identidade usando NOT FOR REPLICATION para ativar tratamento de intervalo de identidade manual.|  
|**Automático**|Especifica o gerenciamento automático de intervalos de identidade.|  
|NULL (padrão)|O padrão é **nenhum** quando o valor de *auto_identity_range* não é **verdadeiro**. O padrão é **manual** em um padrão de topologia ponto a ponto (*auto_identity_range* é ignorado).|  
  
 Para compatibilidade com versões anteriores, quando o valor de *identityrangemanagementoption* é NULL, o valor de *auto_identity_range* é verificado. No entanto, quando o valor de *identityrangemanagementoption* não for NULL, o valor de *auto_identity_range* será ignorado.  
  
 Para obter mais informações, consulte [Replicar colunas de identidade](../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
`[ @publisher = ] 'publisher'`Especifica um não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador. o *Publicador* é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  o *Publicador* não deve ser usado ao adicionar um artigo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a um Publicador.  
  
`[ @fire_triggers_on_snapshot = ] 'fire_triggers_on_snapshot'`É se os gatilhos de usuário replicados são executados quando o instantâneo inicial é aplicado. *fire_triggers_on_snapshot* é **nvarchar (5)**, com um padrão de false. **verdadeiro** significa que os gatilhos de usuário em uma tabela replicada são executados quando o instantâneo é aplicado. Para que os gatilhos sejam replicados, o valor de bitmask de *schema_option* deve incluir o valor **0x100**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_addarticle** é usado na replicação de instantâneo ou na replicação transacional.  
  
 Por padrão, a replicação não publica quaisquer colunas na tabela de origem quando o tipo de dados de coluna não tiver suporte pela replicação. Se você precisar publicar uma coluna desse tipo, deverá executar [sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) para adicionar a coluna.  
  
 Ao adicionar um artigo a uma publicação que oferece suporte à replicação transacional não hierárquica, as seguintes restrições se aplicam:  
  
-   Devem ser especificadas instruções parametrizadas para todos os artigos com base em log. Você deve incluir **16** no valor de *status* .  
  
-   O nome e proprietário da tabela de destino devem corresponder à tabela de origem.  
  
-   O artigo não pode ser filtrado horizontal ou verticalmente.  
  
-   Não há suporte para o gerenciamento de intervalo de identidade automática. Você deve especificar um valor de manual para *identityrangemanagementoption*.  
  
-   Se uma coluna **timestamp** existir na tabela, você deverá incluir 0x08 em *schema_option* para replicar a coluna como **carimbo de data/hora**.  
  
-   Não é possível especificar um valor de **SQL** para *ins_cmd*, *upd_cmd*e *del_cmd*.  
  
 Para obter mais informações, consulte [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 Quando você publicar objetos, suas definições são copiadas aos Assinantes. Se você estiver publicando um objeto de banco de dados que depende de outros objetos, precisará publicar todos os objetos referenciados. Por exemplo, se você publicar uma exibição que depende de uma tabela, terá de publicar a tabela também.  
  
 Se *vertical_partition* for definido como **true**, **sp_addarticle** adiará a criação da exibição até que [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) seja chamado (depois que a última [sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) for adicionada).  
  
 Se a publicação permitir assinaturas de atualização e a tabela publicada não tiver uma coluna **uniqueidentifier** , **sp_addarticle** adicionará uma coluna **uniqueidentifier** à tabela automaticamente.  
  
 Ao replicar para um assinante que não é uma instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do (replicação heterogênea), [!INCLUDE[tsql](../../includes/tsql-md.md)] somente instruções têm suporte para comandos de **inserção**, **atualização**e **exclusão** .  
  
 Quando o Agente de Leitor de Log estiver em execução, adicionar um artigo a uma publicação ponto a ponto poderá causar um deadlock entre o Agente de Leitor de Log e o processo que adiciona o artigo. Para evitar esse problema, antes de adicionar um artigo a uma publicação ponto a ponto, use o Monitor de Replicação para interromper o Agente de Leitor de Log no nó onde você está adicionando o artigo. Reinicie o Agente de Leitor de Log depois de adicionar o artigo.  
  
 Ao configurar `@del_cmd = 'NONE'` ou `@ins_cmd = 'NONE'`, a propagação de comandos **Update** também pode ser afetada por não enviar esses comandos quando ocorre uma atualização limitada. (A atualização limitada é o tipo de instrução UPDATE do publicador que se replica como um par DELETE/INSERT no assinante).  
  
## <a name="default-schema-options"></a>Opções de esquema padrão  
 Esta tabela descreve o valor padrão definido por replicação se *schema_options* não for especificado pelo usuário, em que esse valor depende do tipo de replicação (mostrado na parte superior) e do tipo de artigo (mostrado na primeira coluna).  
  
|Tipo de artigo|Tipo de replicação||  
|------------------|----------------------|------|  
||Transacional|Instantâneo|  
|**aggregate schema only**|**0x01**|**0x01**|  
|**func schema only**|**0x01**|**0x01**|  
|**indexed view schema only**|**0x01**|**0x01**|  
|**indexed view logbased**|**0x30F3**|**0x3071**|  
|**indexed view logbase manualboth**|**0x30F3**|**0x3071**|  
|**indexed view logbased manualfilter**|**0x30F3**|**0x3071**|  
|**indexed view logbased manualview**|**0x30F3**|**0x3071**|  
|**logbased**|**0x30F3**|**0x3071**|  
|**logbased manualfilter**|**0x30F3**|**0x3071**|  
|**logbased manualview**|**0x30F3**|**0x3071**|  
|**proc exec**|**0x01**|**0x01**|  
|**proc schema only**|**0x01**|**0x01**|  
|**serializable proc exec**|**0x01**|**0x01**|  
|**view schema only**|**0x01**|**0x01**|  
  
> [!NOTE]
>  Se uma publicação estiver habilitada para atualização em fila, um valor *schema_option* de **0x80** será adicionado ao valor padrão mostrado na tabela. O *schema_option* padrão para uma não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicação é **0x050D3**.  
  
## <a name="valid-schema-options"></a>Opções de esquema válidas  
 Esta tabela descreve os valores permitidos de *schema_option* com base no tipo de replicação (mostrado na parte superior) e no tipo de artigo (mostrado na primeira coluna).  
  
|Tipo de artigo|Tipo de replicação||  
|------------------|----------------------|------|  
||Transacional|Instantâneo|  
|**logbased**|Todas as opções|Todas as opções, mas **0x02**|  
|**logbased manualfilter**|Todas as opções|Todas as opções, mas **0x02**|  
|**logbased manualview**|Todas as opções|Todas as opções, mas **0x02**|  
|**indexed view logbased**|Todas as opções|Todas as opções, mas **0x02**|  
|**indexed view logbased manualfilter**|Todas as opções|Todas as opções, mas **0x02**|  
|**indexed view logbased manualview**|Todas as opções|Todas as opções, mas **0x02**|  
|**indexed view logbase manualboth**|Todas as opções|Todas as opções, mas **0x02**|  
|**proc exec**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**e **0x80000000**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**e **0x80000000**|  
|**serializable proc exec**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**e **0x80000000**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**e **0x80000000**|  
|**proc schema only**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**e **0x80000000**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**e **0x80000000**|  
|**view schema only**|**0x01**, **0x010**, **0x020**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x100000**, **0x200000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x40000000**e **0x80000000**|**0x01**, **0x010**, **0x020**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x100000**, **0x200000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x40000000**e **0x80000000**|  
|**func schema only**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**e **0x80000000**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**e **0x80000000**|  
|**indexed view schema only**|**0x01**, **0x010**, **0x020**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x100000**, **0x200000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x40000000**e **0x80000000**|**0x01**, **0x010**, **0x020**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x100000**, **0x200000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x40000000**e **0x80000000**|  
  
> [!NOTE]
>  Para publicações de atualização em fila, os valores de *schema_option* de **0x8000** e **0x80** devem ser habilitados. Os valores *de schema_option* com suporte para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicações não são **: 0x01**, **0x02**, **0x10**, **0x40**, **0x80**, **0x1000**, **0x4000** e **0x8000**.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-addarticle-transact-sql_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_addarticle**.  
  
## <a name="see-also"></a>Consulte Também  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [&#41;&#40;Transact-SQL de sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_articlefilter](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_changearticle](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_droparticle](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helparticle](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helparticlecolumns](../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [Publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
