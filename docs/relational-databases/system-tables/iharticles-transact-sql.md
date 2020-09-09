---
description: IHarticles (Transact-SQL)
title: IHarticles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHarticles
- IHarticles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHarticles system table
ms.assetid: 773ef9b7-c993-4629-9516-70c47b9dcf65
author: markingmyname
ms.author: maghan
ms.openlocfilehash: fc67de5d66f897ccc54a1cc06cf88aac35e572b5
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540958"
---
# <a name="iharticles-transact-sql"></a>IHarticles (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela do sistema **IHarticles** contém uma linha para cada artigo sendo replicado de um Publicador não SQL Server usando o distribuidor atual. Esta tabela é armazenada no banco de dados de distribuição.  
  
## <a name="definition"></a>Definição  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**article_id**|**int**|A coluna de identidade que fornece um número de ID exclusivo para o artigo.|  
|**name**|**sysname**|O nome associado ao artigo, exclusivo dentro da publicação.|  
|**publication_id**|**smallint**|A ID da publicação à qual o artigo pertence.|  
|**table_id**|**int**|A ID da tabela que está sendo publicada a partir de [IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md).|  
|**publisher_id**|**smallint**|A ID do Editor não SQL Server.|  
|**creation_script**|**nvarchar(255)**|O script de esquema para o artigo.|  
|**del_cmd**|**nvarchar(255)**|O tipo de comando de replicação usado ao replicar exclusões com artigos de tabela. Para obter mais informações, consulte [Especificar como as alterações são propagadas para artigos transacionais](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).|  
|**filter**|**int**|Esta coluna não é usada e está incluída apenas para tornar a exibição [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) da tabela **IHarticles** compatível com a exibição [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) usada para artigos de SQL Server ([sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)).|  
|**filter_clause**|**ntext**|A cláusula WHERE do artigo, usada para filtragem horizontal e gravação de um Transact-SQL padrão que pode ser interpretado por um Editor não SQL.|  
|**ins_cmd**|**nvarchar(255)**|O tipo de comando de replicação usado ao replicar inserções com artigos de tabela. Para obter mais informações, consulte [Especificar como as alterações são propagadas para artigos transacionais](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).|  
|**pre_creation_cmd**|**tinyint**|O comando a ser executado antes que o instantâneo inicial seja aplicado quando um objeto com o mesmo nome já existir no Assinante.<br /><br /> **0** = nenhum-um comando não é executado.<br /><br /> **1** = descartar a tabela de destino.<br /><br /> **2** = excluir-excluir dados da tabela de destino.<br /><br /> **3** = truncar-truncar a tabela de destino.|  
|**status**|**tinyint**|O bitmask de opções e status do artigo, que pode ser o resultado OR lógico bit a bit de um ou mais destes valores:<br /><br /> **0** = nenhuma propriedade adicional.<br /><br /> **1** = ativo.<br /><br /> **8** = incluir o nome da coluna em instruções INSERT.<br /><br /> **16** = usar instruções parametrizadas.<br /><br /> Por exemplo, um artigo ativo que usa instruções com parâmetros teria um valor 17 nessa coluna. Um valor 0 significa que o artigo está inativo e nenhuma propriedade adicional está definida.|  
|**tipo**|**tinyint**|O tipo de artigo:<br /><br /> **1** = artigo baseado em log.|  
|**upd_cmd**|**nvarchar(255)**|O tipo de comando de replicação usado ao replicar atualizações com artigos de tabela. Para obter mais informações, consulte [Especificar como as alterações são propagadas para artigos transacionais](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).|  
|**schema_option**|**binário (8)**|O bitmap da opção schema generation para o artigo determinado, que pode ser o resultado OR lógico bit a bit de um ou mais desses valores:<br /><br /> **0x00** = desabilitar o script pelo agente de instantâneo e usa o CreationScript fornecido.<br /><br /> **0x01** = gerar a criação do objeto (CREATE TABLE, criar procedimento e assim por diante).<br /><br /> **0x10** = gerar um índice clusterizado correspondente.<br /><br /> **0x40** = gerar índices não clusterizados correspondentes.<br /><br /> **0x80** = incluir integridade referencial declarada nas chaves primárias.<br /><br /> **0x1000** = Replica o agrupamento em nível de coluna. Observação: essa opção é definida por padrão para Publicadores Oracle para habilitar comparações que diferenciam maiúsculas de minúsculas.<br /><br /> **0x4000** = replicar chaves exclusivas, se definido em um artigo de tabela.<br /><br /> **0x8000** = replicar uma chave primária e chaves exclusivas em um artigo de tabela como restrições usando instruções ALTER TABLE.|  
|**dest_owner**|**sysname**|O proprietário da tabela no banco de dados de destino.|  
|**dest_table**|**sysname**|O nome da tabela de destino.|  
|**tablespace_name**|**nvarchar(255)**|Identifica o espaço de tabela usado pela tabela de log para o artigo.|  
|**objid**|**int**|Esta coluna não é usada e está incluída apenas para tornar a exibição [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) da tabela **IHarticles** compatível com a exibição [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) usada para artigos de SQL Server ([sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)).|  
|**sync_objid**|**int**|Esta coluna não é usada e está incluída apenas para tornar a exibição [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) da tabela **IHarticles** compatível com a exibição [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) usada para artigos de SQL Server ([sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)).|  
|**descrição**|**nvarchar(255)**|A entrada descritiva para o artigo.|  
|**publisher_status**|**int**|É usado para indicar se a exibição que define o artigo publicado foi definida chamando [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md).<br /><br /> **0**  =  [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) foi chamado.<br /><br /> **1**  =  [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) não foi chamado.|  
|**article_view_owner**|**nvarchar(255)**|O proprietário do objeto de sincronização no Publicador usado pelo Log Reader Agent.|  
|**article_view**|**nvarchar(255)**|O objeto de sincronização no Publicador usado pelo Log Reader Agent.|  
|**ins_scripting_proc**|**int**|Esta coluna não é usada e está incluída apenas para tornar a exibição [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) da tabela **IHarticles** compatível com a exibição [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) usada para artigos de SQL Server ([sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)).|  
|**del_scripting_proc**|**int**|Esta coluna não é usada e está incluída apenas para tornar a exibição [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) da tabela **IHarticles** compatível com a exibição [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) usada para artigos de SQL Server ([sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)).|  
|**upd_scripting_proc**|**int**|Esta coluna não é usada e está incluída apenas para tornar a exibição [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) da tabela **IHarticles** compatível com a exibição [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) usada para artigos de SQL Server ([sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)).|  
|**custom_script**|**int**|Esta coluna não é usada e está incluída apenas para tornar a exibição [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) da tabela **IHarticles** compatível com a exibição [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) usada para artigos de SQL Server ([sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)).|  
|**fire_triggers_on_snapshot**|**bit**|Esta coluna não é usada e está incluída apenas para tornar a exibição [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) da tabela **IHarticles** compatível com a exibição [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) usada para artigos de SQL Server ([sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)).|  
|**instance_id**|**int**|Identifica a instância atual do log de artigo para a tabela publicada.|  
|**use_default_datatypes**|**bit**|Indica se o artigo usa mapeamentos de tipo de dados padrão; um valor de **1** indica que os mapeamentos de tipo de dados padrão são usados.|  
  
## <a name="see-also"></a>Consulte Também  
 [Replicação de banco de dados heterogênea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addarticle ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)  
  
  
