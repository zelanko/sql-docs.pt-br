---
title: sp_helpmergealternatepublisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergealternatepublisher_TSQL
- sp_helpmergealternatepublisher
helpviewer_keywords:
- sp_helpmergealternatepublisher
ms.assetid: a96e365f-5967-4580-9d79-5bacf2d12211
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c00e7c26a429836f0d350e60530d2dc1db8c2a61
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58526408"
---
# <a name="sphelpmergealternatepublisher-transact-sql"></a>sp_helpmergealternatepublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma lista de todos os servidores habilitados como Publicadores alternativos para publicações de mesclagem. Esse procedimento armazenado é executado no assinante, no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpmergealternatepublisher [ @publisher = ] 'publisher', [ @publisher_db = ] 'publisher_db', [ @publication = ] 'publication'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'` É o nome do publicador alternativo. *publisher* é **sysname**, sem padrão.  
  
`[ @publisher_db = ] 'publisher_db'` É o nome do banco de dados de publicação. *publisher_db* é **sysname**, sem padrão.  
  
`[ @publication = ] 'publication'` É o nome da publicação. *publicação* é **sysname**, sem padrão.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**alternate_publisher**|**sysname**|Nome do Publicador alternativo.|  
|**alternate_publisher_db**|**sysname**|Nome do banco de dados de publicação.|  
|**alternate_publication**|**sysname**|Nome da publicação.|  
|**alternate_distributor**|**sysname**|Nome do distribuidor.|  
|**friendly_name**|**nvarchar(255)**|Descrição do Publicador alternativo.|  
|**enabled**|**bit**|Especifica se o servidor é um Publicador alternativo. **1** Especifica que o publicador está habilitado como um publicador alternativo. **0** Especifica que não está habilitado.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpmergealternatepublisher** é usado em replicação de mesclagem.  
  
 Durante cada sessão de mesclagem, o sistema examina o Publicador e o Assinante para a lista de cada um de publicadores alternativos. O processo de mesclagem adiciona ou descarta entradas na lista de publicadores alternativos, cujo resultado é a lista de publicadores alternativos na correspondência de Publicador e Assinante.  
  
## <a name="permissions"></a>Permissões  
 Somente membros da lista de acesso de publicação para a publicação podem executar **sp_helpmergealternatepublisher**.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
