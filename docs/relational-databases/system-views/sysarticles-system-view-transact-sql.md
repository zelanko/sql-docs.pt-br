---
title: sysarticles (exibição do sistema) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sysarticles
- sysarticles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticles view
ms.assetid: 18f8c9b3-cab7-4e8f-8754-11ac38c3f789
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2165a1e6909e8c02468a89bf18a0fe9cdb280c56
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sysarticles-system-view-transact-sql"></a>sysarticles (exibição de sistema) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **sysarticles** expõe propriedades de artigo de exibição. Essa exibição é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**Int**|A coluna de identidade que fornece um número de ID exclusivo para o artigo.|  
|**creation_script**|**nvarchar(255)**|O script de esquema para o artigo.|  
|**del_cmd**|**nvarchar(255)**|O comando para executar em DELETE; caso contrário, construir do log.|  
|**Descrição**|**nvarchar(255)**|A entrada descritiva para o artigo.|  
|**dest_table**|**sysname**|O nome da tabela de destino.|  
|**filtro**|**Int**|A ID do procedimento armazenado, usado para particionamento horizontal.|  
|**filter_clause**|**ntext**|A cláusula WHERE do artigo, usado para filtragem horizontal.|  
|**ins_cmd**|**nvarchar(255)**|O comando para executar em INSERT; caso contrário, construir do log.|  
|**name**|**sysname**|O nome associado ao artigo, exclusivo dentro da publicação.|  
|**objid**|**Int**|A ID do objeto de tabela publicada.|  
|**pubid**|**Int**|A ID da publicação à qual o artigo pertence.|  
|**pre_creation_cmd**|**tinyint**|O comando de pré-criação para DROP TABLE, DELETE TABLE ou TRUNCATE:<br /><br /> **0** = none.<br /><br /> **1** = DESCARTAR.<br /><br /> **2** = EXCLUIR.<br /><br /> **3** = TRUNCAR.|  
|**status**|**tinyint**|O bitmask de opções e status do artigo, que pode ser o resultado OR lógico bit a bit de um ou mais destes valores:<br /><br /> **1** = artigo está ativo.<br /><br /> **8** = incluir o nome da coluna em instruções INSERT.<br /><br /> **16** = usar instruções com parâmetros.<br /><br /> **24** = ambos incluem o nome da coluna em instruções INSERT e usar instruções com parâmetros.<br /><br /> **64** = a partição horizontal para o artigo é definido por uma assinatura transformável.<br /><br /> Por exemplo, um artigo ativo que usa instruções com parâmetros teria um valor de **17** nesta coluna. Um valor de **0** significa que o artigo está inativo e nenhuma propriedade adicional está definida.|  
|**sync_objid**|**Int**|A ID da tabela ou exibição que representa a definição de artigo.|  
|**type**|**tinyint**|O tipo de artigo:<br /><br /> **1** = artigo com base em log.<br /><br /> **3** = artigo com base em log com filtro manual.<br /><br /> **5** = artigo com base em log com exibição manual.<br /><br /> **7** = artigo com base em log com filtro manual e exibição manual.<br /><br /> **8** = execução de procedimento armazenado.<br /><br /> **24** = a execução do procedimento armazenado serializável.<br /><br /> **32** = procedimento armazenado (somente esquema).<br /><br /> **64** = exibição (somente esquema).<br /><br /> **128** = função (somente esquema).|  
|**upd_cmd**|**nvarchar(255)**|O comando para executar em UPDATE; caso contrário, construir do log.|  
|**schema_option**|**binary(8)**|Um bitmask das opções de geração de esquema para o artigo, que controla de qual parte do esquema de artigo é feito um script para entrega no Assinante. Para obter mais informações sobre opções de esquema, consulte [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).|  
|**dest_owner**|**sysname**|O proprietário da tabela no banco de dados de destino.|  
|**ins_scripting_proc**|**Int**|O procedimento armazenado personalizado registrado ou script executado quando uma instrução INSERT é replicada.|  
|**del_scripting_proc**|**Int**|O procedimento armazenado personalizado registrado ou script executado quando uma instrução DELETE é replicada.|  
|**upd_scripting_proc**|**Int**|O procedimento armazenado personalizado registrado ou script executado quando uma instrução UPDATE é replicada.|  
|**custom_script**|**nvarchar(2048)**|O procedimento armazenado personalizado registrado ou script executado ao término do gatilho DDL.|  
|**fire_triggers_on_snapshot**|**bit**|Indica se os gatilhos replicados são executados quando o instantâneo é aplicado, que pode ser um destes valores:<br /><br /> **0** = gatilhos não são executados.<br /><br /> **1** = os gatilhos são executados.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sysarticles &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysarticles-transact-sql.md)  
  
  
