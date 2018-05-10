---
title: sys.dm_repl_articles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_repl_articles_TSQL
- dm_repl_articles
- dm_repl_articles_TSQL
- sys.dm_repl_articles
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_repl_articles dynamic management function
ms.assetid: 794d514e-bacd-432e-a8ec-3a063a97a37b
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4d1e7ccd9f4bc09bde7ac3be680356b8e93a3827
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmreplarticles-transact-sql"></a>sys.dm_repl_articles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre objetos de banco de dados publicados como artigos em uma topologia de replicação.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**artcache_db_address**|**varbinary(8)**|Endereço na memória da estrutura de banco de dados em cache para o banco de dados de publicação.|  
|**artcache_table_address**|**varbinary(8)**|Endereço na memória da estrutura de tabela em cache para um artigo de tabela publicado.|  
|**artcache_schema_address**|**varbinary(8)**|Endereço na memória da estrutura do esquema de artigo em cache para um artigo de tabela publicado.|  
|**artcache_article_address**|**varbinary(8)**|Endereço na memória da estrutura de artigo em cache para um artigo de tabela publicado.|  
|**artid**|**bigint**|Identifica exclusivamente cada entrada dessa tabela.|  
|**artfilter**|**bigint**|ID do procedimento armazenado usado para filtrar horizontalmente o artigo.|  
|**artobjid**|**bigint**|ID do objeto publicado.|  
|**artpubid**|**bigint**|ID da publicação à qual pertence o artigo.|  
|**artstatus**|**tinyint**|Bitmask de opções e status do artigo, que pode ser o resultado OR lógico bit a bit de um ou mais destes valores:<br /><br /> **1** = artigo está ativo.<br /><br /> **8** = incluir o nome da coluna em instruções INSERT.<br /><br /> **16** = usar instruções com parâmetros.<br /><br /> **24** = ambos incluem o nome da coluna em instruções INSERT e usar instruções com parâmetros.<br /><br /> Por exemplo, um artigo ativo que usa instruções com parâmetros teria um valor 17 nessa coluna. Um valor 0 significa que o artigo está inativo e nenhuma propriedade adicional está definida.|  
|**arttype**|**tinyint**|O tipo de artigo:<br /><br /> **1** = artigo com base em log.<br /><br /> **3** = artigo com base em log com filtro manual.<br /><br /> **5** = artigo com base em log com exibição manual.<br /><br /> **7** = artigo com base em log com filtro manual e exibição manual.<br /><br /> **8** = execução de procedimento armazenado.<br /><br /> **24** = a execução do procedimento armazenado serializável.<br /><br /> **32** = procedimento armazenado (somente esquema).<br /><br /> **64** = exibição (somente esquema).<br /><br /> **128** = função (somente esquema).|  
|**wszArtdesttable**|**nvarchar(514)**|Nome do objeto publicado no destino.|  
|**wszArtdesttableowner**|**nvarchar(514)**|Proprietário do objeto publicado no destino.|  
|**wszArtinscmd**|**nvarchar(510)**|Comando ou procedimento armazenado usado para inserções.|  
|**cmdTypeIns**|**Int**|Sintaxe de chamada do procedimento armazenado de inserção, podendo ser um destes valores.<br /><br /> **1** = CHAMADA<br /><br /> **2** = SQL<br /><br /> **3** = NENHUM<br /><br /> **7** = DESCONHECIDO|  
|**wszArtdelcmd**|**nvarchar(510)**|Comando ou procedimento armazenado usado em exclusões.|  
|**cmdTypeDel**|**Int**|Sintaxe de chamada do procedimento armazenado de exclusão, podendo ser um destes valores.<br /><br /> **0** = XCALL<br /><br /> **1** = CHAMADA<br /><br /> **2** = SQL<br /><br /> **3** = NENHUM<br /><br /> **7** = DESCONHECIDO|  
|**wszArtupdcmd**|**nvarchar(510)**|Comando ou procedimento armazenado usado em atualizações.|  
|**cmdTypeUpd**|**Int**|Sintaxe de chamada do procedimento armazenado de atualização, podendo ser um destes valores.<br /><br /> **0** = XCALL<br /><br /> **1** = CHAMADA<br /><br /> **2** = SQL<br /><br /> **3** = NENHUM<br /><br /> **4** = MCALL<br /><br /> **5** = VCALL<br /><br /> **6** = SCALL<br /><br /> **7** = DESCONHECIDO|  
|**wszArtpartialupdcmd**|**nvarchar(510)**|Comando ou procedimento armazenado usado em atualizações parciais.|  
|**cmdTypePartialUpd**|**Int**|Sintaxe de chamada do procedimento armazenado de atualização parcial, podendo ser um destes valores.<br /><br /> **2** = SQL|  
|**numcol**|**Int**|Número de colunas na partição de um artigo filtrado verticalmente.|  
|**artcmdtype**|**tinyint**|Tipo de comando atualmente sendo replicado, podendo ser um destes valores.<br /><br /> **1** = INSERT<br /><br /> **2** = EXCLUIR<br /><br /> **3** = ATUALIZAÇÃO<br /><br /> **4** = UPDATETEXT<br /><br /> **5** = nenhum<br /><br /> **6** = somente para uso interno<br /><br /> **7** = somente para uso interno<br /><br /> **8** = UPDATE parcial|  
|**artgeninscmd**|**nvarchar(510)**|Modelo de comando INSERT baseado nas colunas incluídas no artigo.|  
|**artgendelcmd**|**nvarchar(510)**|Modelo de comando DELETE, que pode incluir a chave primária ou as colunas incluídas no artigo, dependendo de a sintaxe de chamada ser usada ou não.|  
|**artgenupdcmd**|**nvarchar(510)**|Modelo de comando UPDATE, que pode incluir a chave primária, colunas atualizadas ou uma lista de colunas completa, dependendo de a sintaxe de chamada ser usada ou não.|  
|**artpartialupdcmd**|**nvarchar(510)**|Modelo de comando UPDATE parcial, que inclui a chave primária e as colunas atualizadas.|  
|**artupdtxtcmd**|**nvarchar(510)**|Modelo de comando UPDATETEXT, que inclui a chave primária e as colunas atualizadas.|  
|**artgenins2cmd**|**nvarchar(510)**|Modelo de comando INSERT usado quando um artigo é reconciliado durante o processamento de instantâneo simultâneo.|  
|**artgendel2cmd**|**nvarchar(510)**|Modelo de comando DELETE usado quando um artigo é reconciliado durante o processamento de instantâneo simultâneo.|  
|**fInReconcile**|**tinyint**|Indica se um artigo está sendo reconciliado no momento do processamento de instantâneo simultâneo.|  
|**fPubAllowUpdate**|**tinyint**|Indica se a publicação permite a atualização de assinatura.|  
|**intPublicationOptions**|**bigint**|Bitmap que especifica opções de publicação adicionais, onde os valores de opção bit a bit são:<br /><br /> **0x1** - habilitado para replicação ponto a ponto.<br /><br /> **0x2** -publicar somente alterações locais.<br /><br /> **0x4** - habilitado para assinantes não SQL Server.|  
  
## <a name="permissions"></a>Permissões  
 Requer permissão VIEW DATABASE STATE no banco de dados de publicação para chamar **dm_repl_articles**.  
  
## <a name="remarks"></a>Remarks  
 As informações só serão retornadas para objetos de banco de dados replicados atualmente armazenados no cache de artigo de replicação.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições de gerenciamento dinâmico relacionadas à replicação &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/replication-related-dynamic-management-views-transact-sql.md)  
  
  

