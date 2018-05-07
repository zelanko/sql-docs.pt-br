---
title: syscacheobjects (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-compatibility-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.syscacheobjects_TSQL
- sys.syscacheobjects
- syscacheobjects
- syscacheobjects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syscacheobjects system table
- sys.syscacheobjects compatibility view
ms.assetid: 9b14f37c-b7f5-4f71-b070-cce89a83f69e
caps.latest.revision: 37
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: de76f70e43c7b8d4cc043be069c2b412bb03f69b
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="syssyscacheobjects-transact-sql"></a>sys.syscacheobjects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém informações sobre como o cache é usado.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**BucketID**|**Int**|Identificação da partição de memória. O valor indica um intervalo de 0 a (tamanho de diretório - 1). O tamanho de diretório é o tamanho da tabela de hash.|  
|**cacheobjtype**|**nvarchar(17)**|Tipo de objeto no cache:<br /><br /> Plano compilado<br /><br /> Plano executável<br /><br /> Árvore de análise<br /><br /> Cursor<br /><br /> Procedimento armazenado estendido|  
|**objtype**|**nvarchar(8)**|Tipo de objeto:<br /><br /> Procedimento armazenado<br /><br /> Instrução preparada<br /><br /> Consulta ad hoc ([!INCLUDE[tsql](../../includes/tsql-md.md)] enviado como eventos de linguagem do **sqlcmd** ou **osql** utilitários, em vez de chamadas de procedimento remoto)<br /><br /> ReplProc (procedimento de replicação)<br /><br /> Gatilho<br /><br /> Exibição<br /><br /> Padrão<br /><br /> Tabela de usuário<br /><br /> Tabela do sistema<br /><br /> Verificar<br /><br /> Regra|  
|**objid**|**Int**|Uma das chaves principais usadas para pesquisar um objeto no cache. Este é o objeto ID armazenada na **sysobjects** para objetos de banco de dados (procedimentos, exibições, gatilhos e assim por diante). Para objetos de cache como ad hoc ou SQL preparado, **objid** é um valor gerado internamente.|  
|**dbid**|**smallint**|A identificação do banco de dados no qual o objeto de cache foi compilado.|  
|**dbidexec**|**smallint**|A identificação de banco de dados da qual a consulta é executada.<br /><br /> Para a maioria dos objetos, **dbidexec** tem o mesmo valor como **dbid**.<br /><br /> Para exibições do sistema, **dbidexec** é a ID de banco de dados do qual a consulta é executada.<br /><br /> Para consultas ad hoc, **dbidexec** é 0. Isso significa **dbidexec** tem o mesmo valor como **dbid**.|  
|**UID**|**smallint**|Indica o designer do plano para planos de consulta ad hoc e planos preparados.<br /><br /> -2 = O lote enviado não depende da resolução de nome implícita e pode ser compartilhado entre usuários diferentes. Este é o método preferencial. Qualquer outro valor representa a identificação do usuário que submete a consulta no banco de dados.<br /><br /> Excederá ou retornará NULL se o número de usuários e funções exceder 32.767.|  
|**refcounts**|**Int**|Número de outros objetos de cache que fazem referência a este objeto de cache. Uma contagem de 1 é a base.|  
|**usecounts**|**Int**|Número de vezes em que este objeto de cache foi usado desde o começo.|  
|**pagesused**|**Int**|Número de páginas consumidas pelo objeto de cache.|  
|**setopts**|**Int**|Configurações da opção SET que afetam um plano compilado. Essas configurações fazem parte da chave de cache. Alterações em valores desta coluna indica que os usuários modificaram as opções SET. Essas opções incluem:<br /><br /> **ANSI_PADDING**<br /><br /> **FORCEPLAN**<br /><br /> **CONCAT_NULL_YIELDS_NULL**<br /><br /> **ANSI_WARNINGS**<br /><br /> **ANSI_NULLS**<br /><br /> **QUOTED_IDENTIFIER**<br /><br /> **ANSI_NULL_DFLT_ON**<br /><br /> **ANSI_NULL_DFLT_OFF**|  
|**langid**|**smallint**|Identificação de idioma A identificação de idioma da conexão que criou o objeto de cache.|  
|**dateformat**|**smallint**|O formato de data da conexão que criou o objeto de cache.|  
|**status**|**Int**|Indica se o objeto de cache é um plano de cursor. Atualmente, apenas o bit menos significativo é usado.|  
|**lasttime**|**bigint**|Somente para compatibilidade com versões anteriores. Sempre retorna 0.|  
|**maxexectime**|**bigint**|Somente para compatibilidade com versões anteriores. Sempre retorna 0.|  
|**avgexectime**|**bigint**|Somente para compatibilidade com versões anteriores. Sempre retorna 0.|  
|**lastreads**|**bigint**|Somente para compatibilidade com versões anteriores. Sempre retorna 0.|  
|**lastwrites**|**bigint**|Somente para compatibilidade com versões anteriores. Sempre retorna 0.|  
|**sqlbytes**|**Int**|O comprimento em bytes da definição de procedimento ou lote enviada.|  
|**sql**|**nvarchar(3900)**|A definição de módulo ou os primeiros 3900 caracteres do lote enviados.|  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  

