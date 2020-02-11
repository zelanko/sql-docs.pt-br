---
title: sysarticles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysarticles
- sysarticles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticles system table
ms.assetid: 9d9d5d51-6d8f-4e42-84a9-82e58eb0301e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0e43c3350b546a13a95392b9e916a1d98ddddc7d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68130502"
---
# <a name="sysarticles-transact-sql"></a>sysarticles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada artigo definido no banco de dados local. Essa tabela é armazenada no banco de dados publicado.  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|A coluna de identidade que fornece um número de ID exclusivo para o artigo.|  
|**creation_script**|**nvarchar (255)**|O script de esquema para o artigo.|  
|**del_cmd**|**nvarchar (255)**|O tipo de comando de replicação usado ao replicar exclusões com artigos de tabela. Para obter mais informações, consulte [Especificar como as alterações são propagadas para artigos transacionais](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).|  
|**ndescrição**|**nvarchar (255)**|A entrada descritiva para o artigo.|  
|**dest_table**|**sysname**|O nome da tabela de destino.|  
|**sem**|**int**|A ID do procedimento armazenado, usado para particionamento horizontal.|  
|**filter_clause**|**ntext**|A cláusula WHERE do artigo, usada para filtragem horizontal.|  
|**ins_cmd**|**nvarchar (255)**|O tipo de comando de replicação usado ao replicar inserções com artigos de tabela. Para obter mais informações, consulte [Especificar como as alterações são propagadas para artigos transacionais](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).|  
|**name**|**sysname**|O nome associado ao artigo, exclusivo dentro da publicação.|  
|**objID**|**int**|A ID do objeto de tabela publicada.|  
|**pubid**|**int**|A ID da publicação à qual o artigo pertence.|  
|**pre_creation_cmd**|**tinyint**|O comando de pré-criação para DROP TABLE, DELETE TABLE ou TRUNCATE:<br /><br /> **0** = nenhum.<br /><br /> **1** = descartar.<br /><br /> **2** = excluir.<br /><br /> **3** = truncar.|  
|**status**|**tinyint**|O bitmask de opções e status do artigo, que pode ser o resultado OR lógico bit a bit de um ou mais destes valores:<br /><br /> **1** = o artigo está ativo.<br /><br /> **8** = incluir o nome da coluna em instruções INSERT.<br /><br /> **16** = usar instruções parametrizadas.<br /><br /> **24** = ambos incluem o nome da coluna em instruções INSERT e usam instruções parametrizadas.<br /><br /> **64** = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> Por exemplo, um artigo ativo usando instruções parametrizadas teria um valor de **17** nesta coluna. Um valor de **0** significa que o artigo está inativo e nenhuma propriedade adicional é definida.|  
|**sync_objid**|**int**|A ID da tabela ou exibição que representa a definição de artigo.|  
|**tipo**|**tinyint**|O tipo de artigo:<br /><br /> **1** = artigo baseado em log.<br /><br /> **3** = artigo baseado em log com filtro manual.<br /><br /> **5** = artigo baseado em log com exibição manual.<br /><br /> **7** = artigo baseado em log com filtro manual e exibição manual.<br /><br /> **8** = execução de procedimento armazenado.<br /><br /> **24** = execução de procedimento armazenado serializável.<br /><br /> **32** = procedimento armazenado (somente esquema).<br /><br /> **64** = exibição (somente esquema).<br /><br /> **128** = função (somente esquema).|  
|**upd_cmd**|**nvarchar (255)**|O tipo de comando de replicação usado ao replicar atualizações com artigos de tabela. Para obter mais informações, consulte [Especificar como as alterações são propagadas para artigos transacionais](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).|  
|**schema_option**|**binário (8)**|Um bitmask das opções de geração de esquema para o artigo, que controla de qual parte do esquema de artigo é feito um script para entrega no Assinante. Para obter mais informações sobre opções de esquema, consulte [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).|  
|**dest_owner**|**sysname**|O proprietário da tabela no banco de dados de destino.|  
|**ins_scripting_proc**|**int**|O procedimento armazenado personalizado registrado ou script executado quando uma instrução INSERT é replicada.|  
|**del_scripting_proc**|**int**|O procedimento armazenado personalizado registrado ou script executado quando uma instrução DELETE é replicada.|  
|**upd_scripting_proc**|**int**|O procedimento armazenado personalizado registrado ou script executado quando uma instrução UPDATE é replicada.|  
|**custom_script**|**nvarchar (2048)**|O procedimento armazenado personalizado registrado ou script executado ao término do gatilho DDL.|  
|**fire_triggers_on_snapshot**|**bit**|Indica se os gatilhos replicados são executados ou não quando o instantâneo é aplicado, que pode ter um destes valores:<br /><br /> **0** = gatilhos não são executados.<br /><br /> **1** = gatilhos são executados.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addarticle](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_changearticle](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helparticle](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)  
  
  
