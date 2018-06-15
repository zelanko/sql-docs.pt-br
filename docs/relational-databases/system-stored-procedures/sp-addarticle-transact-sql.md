---
title: sp_addarticle (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.prod_service: database-engine
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
- sp_addarticle
- sp_addarticle_TSQL
helpviewer_keywords:
- sp_addarticle
ms.assetid: 0483a157-e403-4fdb-b943-23c1b487bef0
caps.latest.revision: 108
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 6f18769e9742c2af74efa991532bde347a676083
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32993453"
---
# <a name="spaddarticle-transact-sql"></a>sp_addarticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria um artigo e adiciona-o a uma publicação. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [  **@publication =** ] **'***publicação***'**  
 É o nome da publicação que contém o artigo. O nome deve ser exclusivo no banco de dados. *publicação* é **sysname**, sem padrão.  
  
 [  **@article =** ] **'***artigo***'**  
 É o nome do artigo. O nome deve ser exclusivo na publicação. *artigo* é **sysname**, sem padrão.  
  
 [  **@source_table =** ] **'***source_table***'**  
 Esse parâmetro foi preterido; Use *source_object* em vez disso.  
  
 *Não há suporte para esse parâmetro para editores Oracle.*  
  
 [  **@destination_table =** ] **'***destination_table***'**  
 É o nome da tabela de destino (assinatura), se for diferente do *source_table*ou o procedimento armazenado. *destination_table* é **sysname**, com um padrão NULL, o que significa que *source_table* é igual a *destination_table * *.*  
  
 [  **@vertical_partition =** ] **'***vertical_partition***'**  
 Habilita e desabilita a filtragem de coluna em um artigo de tabela. *vertical_partition* é **nchar(5)**, com um padrão de FALSE.  
  
 **False** indica que não há filtragem vertical e publica todas as colunas.  
  
 **True** limpa todas as colunas, exceto a chave primária declarada, colunas anuláveis sem nenhum padrão e as colunas de chave exclusivas. Colunas são adicionadas usando [sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md).  
  
 [  **@type =** ] **'***tipo***'**  
 É o tipo de artigo. *tipo* é **sysname**, e pode ser um dos valores a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**somente esquema de agregação**|Função de agregação apenas com esquema.|  
|**somente esquema de função**|Função somente com esquema.|  
|**modo de exibição indexado logbased**|Artigo de exibição indexada com base em log. Sem suporte para Publicadores Oracle. Para este tipo de artigo, a tabela base não precisa ser publicada separadamente.|  
|**modo de exibição indexado logbased manualboth**|Artigo de exibição indexada com filtro manual e exibição manual. Essa opção requer que você especifique os *sync_object* e *filtro* parâmetros. Para este tipo de artigo, a tabela base não precisa ser publicada separadamente. Sem suporte para Publicadores Oracle.|  
|**modo de exibição indexado logbased manualfilter**|Artigo de exibição indexada com filtro manual. Essa opção requer que você especifique os *sync_object* e *filtro* parâmetros. Para este tipo de artigo, a tabela base não precisa ser publicada separadamente. Sem suporte para Publicadores Oracle.|  
|**modo de exibição indexado logbased manualview**|Artigo de exibição indexada com base em log com exibição manual. Essa opção requer que você especifique o *sync_object* parâmetro. Para este tipo de artigo, a tabela base não precisa ser publicada separadamente. Sem suporte para Publicadores Oracle.|  
|**somente o esquema de exibição indexada**|Exibição indexada somente com esquema Para esse tipo de artigo, a tabela base também deve ser publicada.|  
|**logbased** (padrão)|Artigo com base em log.|  
|**logbased manualboth**|Artigo com base em log com filtro manual e exibição manual. Essa opção requer que você especifique os *sync_object* e *filtro* parâmetros. Sem suporte para Publicadores Oracle.|  
|**logbased manualfilter**|Artigo com base em log com filtro manual. Essa opção requer que você especifique os *sync_object* e *filtro* parâmetros. Sem suporte para Publicadores Oracle.|  
|**logbased manualview**|Artigo com base em log com exibição manual. Essa opção requer que você especifique o *sync_object* parâmetro. Sem suporte para Publicadores Oracle.|  
|**proc exec**|Replica a execução do procedimento armazenado para todos os assinantes do artigo. Sem suporte para Publicadores Oracle. Recomendamos que você use a opção **serializable proc exec** em vez de **proc exec**. Para obter mais informações, consulte a seção "Tipos de artigos de armazenado do procedimento execução" em [Publishing Stored Procedure Execution em replicação transacional](../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md). Não disponível quando a opção alterar captura de dados está habilitada.|  
|**somente esquema de PROC**|Procedimento apenas com esquema. Sem suporte para Publicadores Oracle.|  
|**Serializable proc exec**|Replica a execução do procedimento armazenado apenas se ele for executado no contexto de uma transação serializável. Sem suporte para Publicadores Oracle.<br /><br /> O procedimento também deve ser executado dentro de uma transação explícita para a execução do procedimento ser replicadas.|  
|**somente o esquema de exibição**|Exibição somente com esquema Sem suporte para Publicadores Oracle. Ao usar essa opção, você também deve publicar a tabela base.|  
  
 [  **@filter =** ] **'***filtro***'**  
 É o procedimento armazenado (criado com FOR REPLICATION) usado para filtrar a tabela horizontalmente. *filtro* é **nvarchar (386)**, com um padrão NULL. [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) e [sp_articlefilter](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) devem ser executados manualmente para criar o modo de exibição e o procedimento armazenado de filtro. Se não for NULL, o procedimento de filtro não é criado (supõe que o procedimento armazenado é criado manualmente).  
  
 [  **@sync_object =** ] **'***sync_object***'**  
 É o nome da tabela ou exibição usada para criar o arquivo de dados usado para representar o instantâneo desse artigo. *sync_object* é **nvarchar (386)**, com um padrão NULL. Se for NULL, [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) é chamado para criar automaticamente a exibição usada para gerar o arquivo de saída. Isso ocorre após a adição de colunas com [sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md). Se não for NULL, uma exibição não será criada (supõe que a exibição é criada manualmente).  
  
 [  **@ins_cmd =** ] **'***ins_cmd***'**  
 É o tipo de comando de replicação usado ao replicar inserções para esse artigo. *ins_cmd* é **nvarchar (255)**, e pode ser um dos valores a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**NONE**|Nenhuma ação é tomada.|  
|**CALL sp_msins _**<br /> ***tabela*** (padrão)<br /><br /> -ou-<br /><br /> **CHAMAR custom_stored_procedure_name**|Chama um procedimento armazenado a ser executado no Assinante. Para usar esse método de replicação, use *schema_option* para especificar a criação automática do procedimento armazenado, ou criar o procedimento armazenado especificado no banco de dados de destino de cada assinante do artigo. *custom_stored_procedure* é o nome de um procedimento armazenado criado pelo usuário. **sp_msins _ * tabela*** contém o nome da tabela de destino em vez do *_table* parte do parâmetro. Quando *destination_owner* for especificado, ele é anexado ao nome da tabela de destino. Por exemplo, para o **ProductCategory** tabela pertencentes a **produção** esquema no assinante, o parâmetro seria `CALL sp_MSins_ProductionProductCategory`. Para um artigo em uma topologia de replicação ponto a ponto, *_table* é acrescentado com um valor de GUID. Especificando *custom_stored_procedure* não há suporte para assinantes de atualização.|  
|**SQL** ou nulo|Replica uma instrução INSERT. A instrução INSERT fornece valores para todas as colunas publicadas no artigo. Esse comando é replicado em inserções:<br /><br /> `INSERT INTO <table name> VALUES (c1value, c2value, c3value, ..., cnvalue)`|  
  
 Para obter mais informações, consulte [Especificar como as alterações são propagadas para artigos transacionais](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
 [  **@del_cmd =**] **'***del_cmd***'**  
 É o tipo de comando de replicação usado ao replicar exclusões para esse artigo. *del_cmd* é **nvarchar (255)**, e pode ser um dos valores a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**NONE**|Nenhuma ação é tomada.|  
|**CALLsp_MSdel_**<br /> ***tabela*** (padrão)<br /><br /> -ou-<br /><br /> **CHAMAR custom_stored_procedure_name**|Chama um procedimento armazenado a ser executado no Assinante. Para usar esse método de replicação, use *schema_option* para especificar a criação automática do procedimento armazenado, ou criar o procedimento armazenado especificado no banco de dados de destino de cada assinante do artigo. *custom_stored_procedure* é o nome de um procedimento armazenado criado pelo usuário. **sp_msdel _ * tabela*** contém o nome da tabela de destino em vez do *_table* parte do parâmetro. Quando *destination_owner* for especificado, ele é anexado ao nome da tabela de destino. Por exemplo, para o **ProductCategory** tabela pertencentes a **produção** esquema no assinante, o parâmetro seria `CALL sp_MSdel_ProductionProductCategory`. Para um artigo em uma topologia de replicação ponto a ponto, *_table* é acrescentado com um valor de GUID. Especificando *custom_stored_procedure* não há suporte para assinantes de atualização.|  
|**Sp_msdel _ XCALL**<br /> ***table***<br /><br /> -ou-<br /><br /> **Custom_stored_procedure_name XCALL**|Chama um procedimento armazenado com o uso de parâmetros no estilo XCALL. Para usar esse método de replicação, use *schema_option* para especificar a criação automática do procedimento armazenado, ou criar o procedimento armazenado especificado no banco de dados de destino de cada assinante do artigo. Não é permitido especificar um procedimento armazenado para atualizar assinantes.|  
|**SQL** ou nulo|Replica uma instrução DELETE. A instrução DELETE é fornecida em todos os valores de coluna de chave primária. Esse comando é replicado em exclusões:<br /><br /> `DELETE FROM <table name> WHERE pkc1 = pkc1value AND pkc2 = pkc2value AND pkcn = pkcnvalue`|  
  
 Para obter mais informações, consulte [Especificar como as alterações são propagadas para artigos transacionais](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
 [  **@upd_cmd =**] **'***upd_cmd***'**  
 É o tipo de comando de replicação usado ao replicar atualizações para esse artigo. *upd_cmd* é **nvarchar (255)**, e pode ser um dos valores a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**NONE**|Nenhuma ação é tomada.|  
|**CHAMAR sp_msupd _**<br /> ***table***<br /><br /> -ou-<br /><br /> **CHAMAR custom_stored_procedure_name**|Chama um procedimento armazenado a ser executado no Assinante. Para usar esse método de replicação, use *schema_option* para especificar a criação automática do procedimento armazenado, ou criar o procedimento armazenado especificado no banco de dados de destino de cada assinante do artigo.|  
|**Sp_msupd _ MCALL**<br /> ***table***<br /><br /> -ou-<br /><br /> **Custom_stored_procedure_name MCALL**|Chama um procedimento armazenado com o uso de parâmetros no estilo MCALL. Para usar esse método de replicação, use *schema_option* para especificar a criação automática do procedimento armazenado, ou criar o procedimento armazenado especificado no banco de dados de destino de cada assinante do artigo. *custom_stored_procedure* é o nome de um procedimento armazenado criado pelo usuário. **sp_msupd _ * tabela*** contém o nome da tabela de destino em vez do *_table* parte do parâmetro. Quando *destination_owner* for especificado, ele é anexado ao nome da tabela de destino. Por exemplo, para o **ProductCategory** tabela pertencentes a **produção** esquema no assinante, o parâmetro seria `MCALL sp_MSupd_ProductionProductCategory`. Para um artigo em uma topologia de replicação ponto a ponto, *_table* é acrescentado com um valor de GUID. Não é permitido especificar um procedimento armazenado para atualizar assinantes.|  
|**SCALL sp_msupd _**<br /> ***tabela*** (padrão)<br /><br /> -ou-<br /><br /> **SCALL custom_stored_procedure_name**|Chama um procedimento armazenado com o uso de parâmetros no estilo SCALL. Para usar esse método de replicação, use *schema_option* para especificar a criação automática do procedimento armazenado, ou criar o procedimento armazenado especificado no banco de dados de destino de cada assinante do artigo. *custom_stored_procedure* é o nome de um procedimento armazenado criado pelo usuário. **sp_msupd _ * tabela*** contém o nome da tabela de destino em vez do *_table* parte do parâmetro. Quando *destination_owner* for especificado, ele é anexado ao nome da tabela de destino. Por exemplo, para o **ProductCategory** tabela pertencentes a **produção** esquema no assinante, o parâmetro seria `SCALL sp_MSupd_ProductionProductCategory`. Para um artigo em uma topologia de replicação ponto a ponto, *_table* é acrescentado com um valor de GUID. Não é permitido especificar um procedimento armazenado para atualizar assinantes.|  
|**Sp_msupd _ XCALL**<br /> ***table***<br /><br /> -ou-<br /><br /> **Custom_stored_procedure_name XCALL**|Chama um procedimento armazenado com o uso de parâmetros no estilo XCALL. Para usar esse método de replicação, use *schema_option* para especificar a criação automática do procedimento armazenado, ou criar o procedimento armazenado especificado no banco de dados de destino de cada assinante do artigo. Não é permitido especificar um procedimento armazenado para atualizar assinantes.|  
|**SQL** ou nulo|Replica uma instrução UPDATE. A instrução UPDATE é fornecida em todos os valores de coluna e os valores de coluna de chave primária. Esse comando é replicado em atualizações:<br /><br /> `UPDATE <table name> SET c1 = c1value, SET c2 = c2value, SET cn = cnvalue WHERE pkc1 = pkc1value AND pkc2 = pkc2value AND pkcn = pkcnvalue`|  
  
> [!NOTE]  
>  A sintaxe de CALL, MCALL, SCALL e XCALL varia a quantidade de dados propagada ao assinante. A sintaxe de CALL passa todos os valores para todas as colunas inseridas e excluídas. A sintaxe de SCALL passa valores apenas para as colunas afetadas. A sintaxe de XCALL passa valores para todas as colunas, alteradas ou não, inclusive o valor anterior da coluna. Para obter mais informações, consulte [Especificar como as alterações são propagadas para artigos transacionais](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
 [  **@creation_script =**] **'***creation_script***'**  
 Corresponde ao caminho e ao nome de um script de esquema de artigo opcional usados para criar o artigo no banco de dados de assinatura. *creation_script* é **nvarchar (255)**, com um padrão NULL.  
  
 [  **@description =**] **'***descrição***'**  
 É uma entrada descritiva para o artigo. *Descrição* é **nvarchar (255)**, com um padrão NULL.  
  
 [  **@pre_creation_cmd =**] **'***pre_creation_cmd***'**  
 Especifica o que o sistema deve fazer se detectar um objeto existente com o mesmo nome no assinante, ao aplicar o instantâneo para esse artigo: *pre_creation_cmd* é **nvarchar (10)**, e pode ser um dos valores a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Nenhum**|Não usa um comando.|  
|**delete**|Exclui dados da tabela de destino antes de aplicar o instantâneo. Quando o artigo é filtrado horizontalmente, apenas dados em colunas especificadas pela cláusula de filtro são excluídos. Não há suporte para Publicadores Oracle quando um filtro horizontal está definido.|  
|**Descartar** (padrão)|Descarta a tabela de destino.|  
|**Truncar**|Trunca a tabela de destino. Não é válido para assinantes ODBC ou OLE DB.|  
  
 [  **@filter_clause=**] **'***filter_clause***'**  
 É uma cláusula de restrição (WHERE) que define um filtro horizontal. Ao inserir a cláusula de restrição, omita a palavra-chave onde. *filter_clause* é **ntext**, com um padrão NULL. Para obter mais informações, consulte [Filter Published Data](../../relational-databases/replication/publish/filter-published-data.md) (Filtrar dados publicados).  
  
 [  **@schema_option =**] *schema_option*  
 É um bitmask da opção de geração de esquema para o artigo determinado. *schema_option* é **binary (8)** e pode ser o [| (OR bit a bit) ](../../t-sql/language-elements/bitwise-or-transact-sql.md) produto de um ou mais desses valores:  
  
> [!NOTE]  
>  Se esse valor for NULL, o sistema gerará automaticamente uma opção de esquema válida para o artigo dependendo de outras propriedades do artigo. O **opções de esquema padrão** tabela na seção comentários mostra o valor será escolhido com base na combinação de tipo de artigo e o tipo de replicação.  
  
|Value|Description|  
|-----------|-----------------|  
|**0x00**|Desabilita a execução de script pelo Snapshot Agent e usa *creation_script*.|  
|**0x01**|Gera o script de criação de objeto (CREATE TABLE, CREATE PROCEDURE e assim por diante). Esse valor é o padrão para artigos de procedimento armazenado.|  
|**0x02**|Gera os procedimentos armazenados que propagam alterações para o artigo, se definido.|  
|**0x04**|Os scripts das colunas de identidade são executados com a propriedade IDENTITY.|  
|**0x08**|Replicar **timestamp** colunas. Se não for definido, **timestamp** colunas são replicadas como **binário**.|  
|**0x10**|Gera um índice clusterizado correspondente. Mesmo que essa opção não esteja definida, os índices relacionados às chaves primárias e às restrições exclusivas serão gerados caso já estejam definidos em uma tabela publicada.|  
|**0x20**|Converte UDTs (tipos de dados definidos pelo usuário) em tipos de dados básicos no Assinante. Essa opção não poderá ser usada quando houver uma restrição CHECK ou DEFAULT em uma coluna UDT, se uma coluna UDT for parte da chave primária ou se uma coluna computada fizer referência a uma coluna UDT. *Não há suportada para editores Oracle*.|  
|**0x40**|Gera índices não clusterizados correspondentes. Mesmo que essa opção não esteja definida, os índices relacionados às chaves primárias e às restrições exclusivas serão gerados caso já estejam definidos em uma tabela publicada.|  
|**0x80**|Replica restrições de chave primária. Quaisquer índices relacionadas à restrição também são replicados, mesmo se opções **0x10** e **0x40** não estão habilitados.|  
|**0x100**|Replica gatilhos de usuário em um artigo de tabela, se definido. *Não há suportada para editores Oracle*.|  
|**0x200**|Replica restrições de chave estrangeira. Se a tabela referenciada não for parte de uma publicação, todas as restrições de chave estrangeira em uma tabela publicada não serão replicadas. *Não há suportada para editores Oracle*.|  
|**0x400**|Replica restrições de verificação. *Não há suportada para editores Oracle*.|  
|**0x800**|Replica padrões. *Não há suportada para editores Oracle*.|  
|**0x1000**|Replica agrupamento em nível de coluna.<br /><br /> **Observação:** essa opção deve ser definida para Publicadores Oracle para habilitar comparações diferencia maiusculas de minúsculas.|  
|**0x2000**|Replica propriedades estendidas associadas com o objeto de origem do artigo publicado. *Não há suportada para editores Oracle*.|  
|**0x4000**|Replica restrições UNIQUE. Quaisquer índices relacionadas à restrição também são replicados, mesmo se opções **0x10** e **0x40** não estão habilitados.|  
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
|**0x2000000**|Coleções de esquemas XML associada a **xml** colunas não são replicadas.|  
|**0x4000000**|Replica índices em **xml** colunas.|  
|**0x8000000**|Cria qualquer esquema ainda não presente no assinante.|  
|**0x10000000**|Converte **xml** colunas **ntext** no assinante.|  
|**0x20000000**|Converte tipos de dados objeto grande (**nvarchar (max)**, **varchar (max)**, e **varbinary (max)**) introduzido no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] para tipos de dados que têm suporte em [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].|  
|**0x40000000**|Replica permissões.|  
|**0x80000000**|Tentativa de remover dependências de todos os objetos que não fazem parte da publicação.|  
|**0x100000000**|Use esta opção para replicar o atributo FILESTREAM, se for especificado em **varbinary (max)** colunas. Não especifique essa opção se você estiver replicando tabelas para Assinantes [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Replicação de tabelas com colunas FILESTREAM para [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] assinantes não tem suporte, independentemente de como essa opção de esquema é definida.<br /><br /> Consulte a opção relacionada **0x800000000**.|  
|**0x200000000**|Converte tipos de dados de data e hora (**data**, **tempo**, **datetimeoffset**, e **datetime2**) introduzido no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] aos dados tipos com suporte em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**0x400000000**|Replica a opção de compactação para dados e índices. Para obter mais informações, consulte [Data Compression](../../relational-databases/data-compression/data-compression.md).|  
|**0x800000000**|Defina essa opção para armazenar dados FILESTREAM em seu próprio grupo de arquivos no Assinante. Se essa opção não for definida, os dados FILESTREAM serão armazenados no grupo de arquivos padrão. A replicação não cria grupos de arquivos; portanto, se você definir essa opção, deverá criar o grupo de arquivos antes de aplicar o instantâneo no Assinante. Para obter mais informações sobre como criar objetos antes de aplicar o instantâneo, consulte [executar Scripts antes e após a aplicação do instantâneo](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md).<br /><br /> Consulte a opção relacionada **0x100000000**.|  
|**0x1000000000**|Converte tipos common language runtime (CLR) definidos pelo usuário (UDTs) maiores que 8000 bytes em **varbinary (max)** para que as colunas do tipo UDT possam ser replicadas para os assinantes que executam o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
|**0x2000000000**|Converte o **hierarchyid** tipo de dados **varbinary (max)** para que colunas do tipo **hierarchyid** podem ser replicadas para assinantes que executam o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Para obter mais informações sobre como usar **hierarchyid** colunas em tabelas replicadas, consulte [hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md).|  
|**0x4000000000**|Replica qualquer índice filtrado na tabela. Para obter mais informações sobre índices filtrados, consulte [criar índices filtrados](../../relational-databases/indexes/create-filtered-indexes.md).|  
|**0x8000000000**|Converte o **geografia** e **geometria** para tipos de dados **varbinary (max)** para que colunas desses tipos podem ser replicadas para assinantes que executam o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
|**0x10000000000**|Replica índices em colunas do tipo **geografia** e **geometria**.|  
|**0x20000000000**|Replica o atributo SPARSE para colunas. Para obter mais informações sobre esse atributo, consulte [usar colunas esparsas](../../relational-databases/tables/use-sparse-columns.md).|  
|**0x40000000000**|Habilite o script pelo snapshot agent para criar a tabela com otimização de memória no assinante.|  
|**0x80000000000**|Converte um índice clusterizado em índice não clusterizado para artigos com otimização de memória.|  
|**0x400000000000**|Replica qualquer índice não clusterizado columnstore em tabelas de|  
|**0x800000000000**|Replica qualquer índice de columnstore não clusterizado flitered sobre as tabelas.|  
|NULL|A replicação define automaticamente *schema_option* para um valor padrão, o valor do qual depende de outras propriedades do artigo. A tabela "Opções de Esquema Padrão" na seção Observações mostra as opções de esquema padrão com base no tipo de artigo e tipo de replicação.<br /><br /> O padrão de não -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicações é **0x050D3**.|  
  
 Nem todos os *schema_option* valores são válidos para cada tipo de replicação e tipo de artigo. O **opções de esquema válido** tabela na seção comentários mostra as opções de esquema válido que podem ser escolhidas com base na combinação de tipo de artigo e o tipo de replicação.  
  
 [  **@destination_owner =**] **'***destination_owner***'**  
 É o nome do proprietário do objeto de destino. *destination_owner* é **sysname**, com um padrão NULL. Quando *destination_owner* não for especificado, o proprietário é especificado automaticamente com base nas seguintes regras:  
  
|Condição|Proprietário do objeto de destino|  
|---------------|------------------------------|  
|Publicação usa a cópia em massa do modo nativo para gerar o instantâneo inicial que só aceita assinantes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|O valor padrão é *source_owner*.|  
|Publicado a partir de um não publicador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Assume o proprietário do banco de dados de destino como padrão.|  
|A publicação usa a cópia em massa do modo de caractere para gerar o instantâneo inicial que só aceita assinantes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Não atribuído.|  
  
 Para dar suporte a não -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes, *destination_owner* deve ser NULL.  
  
 [  **@status=**] *status*  
 Especifica se o artigo está ativo e opções adicionais sobre como as alterações são propagadas. *status* é **tinyint**e pode ser o [| (OR bit a bit) ](../../t-sql/language-elements/bitwise-or-transact-sql.md) produto de um ou mais desses valores.  
  
|Value|Descrição|  
|-----------|-----------------|  
|**1**|O artigo está ativo.|  
|**8**|Inclui o nome da coluna nas instruções INSERT.|  
|**16** (padrão)|Usa instruções parametrizadas.|  
|**24**|Inclui o nome da coluna nas instruções INSERT e usa instruções parametrizadas.|  
|**64**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
 Por exemplo, um artigo ativo que usa instruções com parâmetros teria um valor 17 nessa coluna. Um valor de **0** significa que o artigo está inativo e nenhuma propriedade adicional está definida.  
  
 [  **@source_owner =**] **'***source_owner***'**  
 É o proprietário do objeto de origem. *source_owner* é **sysname**, com um padrão NULL. *source_owner* deve ser especificado para editores Oracle.  
  
 [  **@sync_object_owner =**] **'***sync_object_owner***'**  
 É o proprietário da exibição que define o artigo publicado. *sync_object_owner* é **sysname**, com um padrão NULL.  
  
 [  **@filter_owner =**] **'***filter_owner***'**  
 É o proprietário do filtro. *filter_owner* é **sysname**, com um padrão NULL.  
  
 [  **@source_object =**] **'***source_object***'**  
 É o objeto de banco de dados a ser publicado. *source_object* é **sysname**, com um padrão NULL. Se *source_table* for NULL, *source_object* não pode ser NULL. *source_object* deve ser usado em vez de *source_table*. Para obter mais informações sobre os tipos de objetos que podem ser publicados usando replicação de instantâneo ou transacional, consulte [publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md).  
  
 [  **@artid =** ] *article_ID* **saída**  
 É a ID do artigo do novo artigo. *article_ID* é **int** com um padrão de NULL e é um parâmetro de saída.  
  
 [  **@auto_identity_range =** ] **'***auto_identity_range***'**  
 Habilita e desabilita o intervalo de identidade automática em uma publicação no momento em que ela é criada. *auto_identity_range* é **nvarchar (5)**, e pode ser um dos seguintes valores:  
  
|Value|Description|  
|-----------|-----------------|  
|**true**|Ativa a manipulação de intervalo de identidade automática.|  
|**false**|Desabilita a manipulação de intervalo de identidade automática.|  
|NULL(default)|Tratamento de intervalo de identidade é definido por *identityrangemanagementoption*.|  
  
> [!NOTE]  
>  *auto_identity_range* foi preterido e é fornecida para compatibilidade com versões anteriores apenas. Você deve usar *identityrangemanagementoption* para especificar opções de gerenciamento de intervalo de identidade. Para obter mais informações, consulte [Replicar colunas de identidade](../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
 [  **@pub_identity_range =** ] *pub_identity_range*  
 Controla o tamanho do intervalo no publicador se o artigo tiver *identityrangemanagementoption* definida como **automática** ou *auto_identity_range* definida como **true** . *pub_identity_range* é **bigint**, com um padrão NULL. *Não há suportada para editores Oracle*.  
  
 [  **@identity_range =** ] *identity_range*  
 Controla o tamanho do intervalo no assinante se o artigo tiver *identityrangemanagementoption* definida como **automática** ou *auto_identity_range* definida como **true** . *identity_range* é **bigint**, com um padrão NULL. Usado quando *auto_identity_range* é definido como **true**. *Não há suportada para editores Oracle*.  
  
 [  **@threshold =** ] *limite*  
 É o valor percentual que controla quando o Distribution Agent atribui um novo intervalo de identidade. Quando a porcentagem de valores especificada em *limite* é usado, o agente de distribuição cria um novo intervalo de identidade. *limite de* é **bigint**, com um padrão NULL. Usado quando *identityrangemanagementoption* é definido como **automática** ou *auto_identity_range* é definido como **true**. *Não há suportada para editores Oracle*.  
  
 [  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 Confirma que a ação tomada por esse procedimento armazenado pode invalidar um instantâneo existente. *force_invalidate_snapshot* é um **bit**, com um padrão de 0.  
  
 **0** Especifica que a adição de um artigo não faz com que o instantâneo seja inválido. Se o procedimento armazenado detectar que a alteração exige um novo instantâneo, ocorrerá um erro e nenhuma alteração será feita.  
  
 **1** Especifica que a adição de um artigo pode invalidar o instantâneo e, se houver assinaturas que exigem um novo instantâneo, dará permissão para que o instantâneo existente seja marcado como obsoleto e um novo instantâneo seja gerado.  
  
 [  **@use_default_datatypes =** ] *use_default_datatypes*  
 É se os mapeamentos de tipo de dados de coluna padrão são usados ao publicar um artigo de um Publicador Oracle. *use_default_datatypes* é bit, com um padrão de 1.  
  
 **1** = a coluna de artigo padrão são usados mapeamentos. Os mapeamentos de tipo de dados padrão podem ser exibidos executando [sp_getdefaultdatatypemapping](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md).  
  
 **0** = coluna de artigo personalizados mapeamentos são definidos, e, portanto, [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) não é chamado por **sp_addarticle**.  
  
 Quando *use_default_datatypes* é definido como **0**, você deve executar [sp_changearticlecolumndatatype](../../relational-databases/system-stored-procedures/sp-changearticlecolumndatatype-transact-sql.md) uma vez para cada mapeamento de coluna que está sendo alterado do padrão. Depois que todos os mapeamentos de coluna personalizados tiverem sido definidos, você deve executar [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md).  
  
> [!NOTE]  
>  Esse parâmetro só deve ser usado para Publicadores Oracle. Configuração *use_default_datatypes* para **0** para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador gera um erro.  
  
 [  **@identityrangemanagementoption =** ] *identityrangemanagementoption*  
 Especifica como o gerenciamento de intervalo de identidade é tratado para o artigo. *identityrangemanagementoption* é **nvarchar (10)**, e pode ser um dos valores a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Nenhum**|A replicação não faz nenhum gerenciamento de intervalo de identidade explícito. Essa opção só é recomendada para compatibilidade com versões anteriores do SQL Server. Não permitido para replicação hierárquica.|  
|**Manual**|Marca a coluna de identidade usando NOT FOR REPLICATION para ativar tratamento de intervalo de identidade manual.|  
|**Automático**|Especifica o gerenciamento automático de intervalos de identidade.|  
|NULL(default)|O padrão será a **nenhum** quando o valor de *auto_identity_range* não é **true**. O padrão será a **manual** em um padrão de topologia ponto a ponto (*auto_identity_range* é ignorado).|  
  
 Para compatibilidade com versões anteriores, quando o valor de *identityrangemanagementoption* for NULL, o valor de *auto_identity_range* é verificada. No entanto, quando o valor de *identityrangemanagementoption* não é nulo, então o valor de *auto_identity_range* será ignorado.  
  
 Para obter mais informações, consulte [Replicar colunas de identidade](../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
 [  **@publisher =** ] **'***publicador***'**  
 Especifica um Publicador que não é do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *publicador* é **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  *publicador* não deve ser usado ao adicionar um artigo para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador.  
  
 [  **@fire_triggers_on_snapshot =** ] **'***fire_triggers_on_snapshot***'**  
 Se os gatilhos de usuário replicados forem executados quando o instantâneo inicial for aplicado. *fire_triggers_on_snapshot* é **nvarchar (5)**, com um padrão de FALSE. **True** significa que os gatilhos de usuário em uma tabela replicada são executados quando o instantâneo é aplicado. Para gatilhos a serem replicados, o valor de máscara de bits de *schema_option* deve incluir o valor **0x100**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_addarticle** é usado em replicação de instantâneo ou replicação transacional.  
  
 Por padrão, a replicação não publica quaisquer colunas na tabela de origem quando o tipo de dados de coluna não tiver suporte pela replicação. Se você precisar publicar essa coluna, você deve executar [sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) para adicionar a coluna.  
  
 Ao adicionar um artigo a uma publicação que oferece suporte à replicação transacional não hierárquica, as seguintes restrições se aplicam:  
  
-   Devem ser especificadas instruções parametrizadas para todos os artigos com base em log. Você deve incluir **16** no *status* valor.  
  
-   O nome e proprietário da tabela de destino devem corresponder à tabela de origem.  
  
-   O artigo não pode ser filtrado horizontal ou verticalmente.  
  
-   Não há suporte para o gerenciamento de intervalo de identidade automática. Você deve especificar um valor de manual para *identityrangemanagementoption*.  
  
-   Se um **timestamp** coluna existe na tabela, você deve incluir 0x08 na *schema_option* para replicar a coluna como **timestamp**.  
  
-   Um valor de **SQL** não pode ser especificado para *ins_cmd*, *upd_cmd*, e *del_cmd*.  
  
 Para obter mais informações, consulte [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 Quando você publicar objetos, suas definições são copiadas aos Assinantes. Se você estiver publicando um objeto de banco de dados que depende de outros objetos, precisará publicar todos os objetos referenciados. Por exemplo, se você publicar uma exibição que depende de uma tabela, terá de publicar a tabela também.  
  
 Se *vertical_partition* é definido como **true**, **sp_addarticle** adia a criação da exibição até [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) é chamado (após a última [sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) é adicionado).  
  
 Se a publicação permite atualização de assinaturas e a tabela publicada não tiver um **uniqueidentifier** coluna, **sp_addarticle** adiciona um **uniqueidentifier** coluna para a tabela automaticamente.  
  
 Ao replicar para um assinante que não é uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (replicação heterogênea), somente [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções têm suporte para **inserir**, **atualização**e **Excluir** comandos.  
  
 Quando o Agente de Leitor de Log estiver em execução, adicionar um artigo a uma publicação ponto a ponto poderá causar um deadlock entre o Agente de Leitor de Log e o processo que adiciona o artigo. Para evitar esse problema, antes de adicionar um artigo a uma publicação ponto a ponto, use o Monitor de Replicação para interromper o Agente de Leitor de Log no nó onde você está adicionando o artigo. Reinicie o Agente de Leitor de Log depois de adicionar o artigo.  
  
 Ao definir `@del_cmd = 'NONE'` ou `@ins_cmd = 'NONE'`, a propagação de **atualizar** comandos também podem ser afetados por não enviar esses comandos quando ocorrer uma atualização limitada. (A atualização limitada é o tipo de instrução UPDATE do publicador que se replica como um par DELETE/INSERT no assinante).  
  
## <a name="default-schema-options"></a>Opções de esquema padrão  
 Esta tabela descreve o valor padrão definido pela replicação se *schema_options* não é especificado pelo usuário, em que esse valor depende do tipo de replicação (mostrados na parte superior) e o tipo de artigo (mostrado abaixo da primeira coluna).  
  
|Tipo de artigo|Tipo de replicação||  
|------------------|----------------------|------|  
||Transacional.|Instantâneo|  
|**somente esquema de agregação**|**0x01**|**0x01**|  
|**somente esquema de função**|**0x01**|**0x01**|  
|**somente o esquema de exibição indexada**|**0x01**|**0x01**|  
|**modo de exibição indexado logbased**|**0x30F3**|**0x3071**|  
|**modo de exibição indexado logbase manualboth**|**0x30F3**|**0x3071**|  
|**modo de exibição indexado logbased manualfilter**|**0x30F3**|**0x3071**|  
|**modo de exibição indexado logbased manualview**|**0x30F3**|**0x3071**|  
|**logbased**|**0x30F3**|**0x3071**|  
|**logbased manualfilter**|**0x30F3**|**0x3071**|  
|**logbased manualview**|**0x30F3**|**0x3071**|  
|**proc exec**|**0x01**|**0x01**|  
|**somente esquema de PROC**|**0x01**|**0x01**|  
|**Serializable proc exec**|**0x01**|**0x01**|  
|**somente o esquema de exibição**|**0x01**|**0x01**|  
  
> [!NOTE]  
>  Se uma publicação for habilitada para atualização em fila, um *schema_option* valor **0x80** é adicionado ao valor padrão mostrado na tabela. O padrão *schema_option* para um não[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicação é **0x050D3**.  
  
## <a name="valid-schema-options"></a>Opções de esquema válidas  
 Esta tabela descreve os valores permitidos de *schema_option* com base no tipo de replicação (mostrados na parte superior) e o tipo de artigo (mostrado abaixo da primeira coluna).  
  
|Tipo de artigo|Tipo de replicação||  
|------------------|----------------------|------|  
||Transacional.|Instantâneo|  
|**logbased**|Todas as opções|Todas as opções, mas **0x02**|  
|**logbased manualfilter**|Todas as opções|Todas as opções, mas **0x02**|  
|**logbased manualview**|Todas as opções|Todas as opções, mas **0x02**|  
|**modo de exibição indexado logbased**|Todas as opções|Todas as opções, mas **0x02**|  
|**modo de exibição indexado logbased manualfilter**|Todas as opções|Todas as opções, mas **0x02**|  
|**modo de exibição indexado logbased manualview**|Todas as opções|Todas as opções, mas **0x02**|  
|**modo de exibição indexado logbase manualboth**|Todas as opções|Todas as opções, mas **0x02**|  
|**proc exec**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**, e **0x80000000**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**, e **0x80000000**|  
|**Serializable proc exec**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**, e **0x80000000**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**, e **0x80000000**|  
|**somente esquema de PROC**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**, e **0x80000000**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**, e **0x80000000**|  
|**somente o esquema de exibição**|**0x01**, **0x010**, **0x020**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x100000**, **0x200000**, **0x400000**, **0x800000**,  **0x2000000**, **0x8000000**, **0x40000000**, e **0x80000000**|**0x01**, **0x010**, **0x020**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x100000**, **0x200000**, **0x400000**, **0x800000**,  **0x2000000**, **0x8000000**, **0x40000000**, e **0x80000000**|  
|**somente esquema de função**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**, e **0x80000000**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**, e **0x80000000**|  
|**somente o esquema de exibição indexada**|**0x01**, **0x010**, **0x020**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x100000**, **0x200000**, **0x400000**, **0x800000**,  **0x2000000**, **0x8000000**, **0x40000000**, e **0x80000000**|**0x01**, **0x010**, **0x020**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x100000**, **0x200000**, **0x400000**, **0x800000**,  **0x2000000**, **0x8000000**, **0x40000000**, e **0x80000000**|  
  
> [!NOTE]  
>  Para publicações de atualização enfileiradas, o *schema_option* valores de **0x8000** e **0x80** deve ser habilitado. Com o suporte *schema_option* valores não -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicações são: **0x01**, **0x02**, **0x10**,  **0x40**, **0x80**, **0x1000**, **0x4000** e **0X8000**.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-addarticle-transact-sql_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_addarticle**.  
  
## <a name="see-also"></a>Consulte também  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [sp_articlecolumn &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sp_articlefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)   
 [sp_articleview &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sp_helparticlecolumns &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [Publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
