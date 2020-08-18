---
description: sys.syscacheobjects (Transact-SQL)
title: sys.syscacheobjects (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 25160eb8e7a25e2a4ec6d2f8b318fc78e7af61ef
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88399672"
---
# <a name="syssyscacheobjects-transact-sql"></a>sys.syscacheobjects (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém informações sobre como o cache é usado.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**bucketid**|**int**|Identificação da partição de memória. O valor indica um intervalo de 0 a (tamanho de diretório - 1). O tamanho de diretório é o tamanho da tabela de hash.|  
|**cacheobjtype**|**nvarchar(17)**|Tipo de objeto no cache:<br /><br /> Plano compilado<br /><br /> Plano executável<br /><br /> Árvore de análise<br /><br /> Cursor<br /><br /> Procedimento armazenado estendido|  
|**objtype**|**nvarchar(8)**|Tipo de objeto:<br /><br /> Procedimento armazenado<br /><br /> Instrução preparada<br /><br /> Consulta ad hoc ( [!INCLUDE[tsql](../../includes/tsql-md.md)] enviada como eventos de linguagem dos utilitários **sqlcmd** ou **osql** , em vez de chamadas de procedimento remoto)<br /><br /> ReplProc (procedimento de replicação)<br /><br /> Gatilho<br /><br /> Visualizar<br /><br /> Padrão<br /><br /> Tabela de usuário<br /><br /> Tabela do sistema<br /><br /> Verificação<br /><br /> Regra|  
|**objid**|**int**|Uma das chaves principais usadas para pesquisar um objeto no cache. Essa é a ID de objeto armazenada em **sysobjects** para objetos de banco de dados (procedimentos, exibições, gatilhos e assim por diante). Para objetos de cache como ad hoc ou preparado para SQL, **objID** é um valor gerado internamente.|  
|**DBID**|**smallint**|A identificação do banco de dados no qual o objeto de cache foi compilado.|  
|**dbidexec**|**smallint**|A identificação de banco de dados da qual a consulta é executada.<br /><br /> Para a maioria dos objetos, **dbidexec** tem o mesmo valor que **DBID**.<br /><br /> Para exibições do sistema, **dbidexec** é a ID do banco de dados do qual a consulta é executada.<br /><br /> Para consultas ad hoc, **dbidexec** é 0. Isso significa que **dbidexec** tem o mesmo valor que **DBID**.|  
|**UID**|**smallint**|Indica o designer do plano para planos de consulta ad hoc e planos preparados.<br /><br /> -2 = O lote enviado não depende da resolução de nome implícita e pode ser compartilhado entre usuários diferentes. Este é o método preferencial. Qualquer outro valor representa a identificação do usuário que submete a consulta no banco de dados.<br /><br /> Excederá ou retornará NULL se o número de usuários e funções exceder 32.767.|  
|**refcounts**|**int**|Número de outros objetos de cache que fazem referência a este objeto de cache. Uma contagem de 1 é a base.|  
|**usecounts**|**int**|Número de vezes em que este objeto de cache foi usado desde o começo.|  
|**pagesused**|**int**|Número de páginas consumidas pelo objeto de cache.|  
|**setopts**|**int**|Configurações da opção SET que afetam um plano compilado. Essas configurações fazem parte da chave de cache. Alterações em valores desta coluna indica que os usuários modificaram as opções SET. Essas opções incluem:<br /><br /> **ANSI_PADDING**<br /><br /> **FORCEPLAN**<br /><br /> **CONCAT_NULL_YIELDS_NULL**<br /><br /> **ANSI_WARNINGS**<br /><br /> **ANSI_NULLS**<br /><br /> **QUOTED_IDENTIFIER**<br /><br /> **ANSI_NULL_DFLT_ON**<br /><br /> **ANSI_NULL_DFLT_OFF**|  
|**langid**|**smallint**|Identificação de idioma A identificação de idioma da conexão que criou o objeto de cache.|  
|**DateFormat**|**smallint**|O formato de data da conexão que criou o objeto de cache.|  
|**status**|**int**|Indica se o objeto de cache é um plano de cursor. Atualmente, apenas o bit menos significativo é usado.|  
|**lasttime**|**bigint**|Somente para compatibilidade com versões anteriores. Sempre retorna 0.|  
|**maxexectime**|**bigint**|Somente para compatibilidade com versões anteriores. Sempre retorna 0.|  
|**avgexectime**|**bigint**|Somente para compatibilidade com versões anteriores. Sempre retorna 0.|  
|**lastreads**|**bigint**|Somente para compatibilidade com versões anteriores. Sempre retorna 0.|  
|**lastwrites**|**bigint**|Somente para compatibilidade com versões anteriores. Sempre retorna 0.|  
|**sqlbytes**|**int**|O comprimento em bytes da definição de procedimento ou lote enviada.|  
|**SQL**|**nvarchar(3900)**|A definição de módulo ou os primeiros 3900 caracteres do lote enviados.|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  

