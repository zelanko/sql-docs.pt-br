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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: fd1071dd1ca4e2951dc3a7d1fbc759ae13b968f6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85733138"
---
# <a name="sp_helpmergealternatepublisher-transact-sql"></a>sp_helpmergealternatepublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma lista de todos os servidores habilitados como Publicadores alternativos para publicações de mesclagem. Esse procedimento armazenado é executado no Assinante no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpmergealternatepublisher [ @publisher = ] 'publisher', [ @publisher_db = ] 'publisher_db', [ @publication = ] 'publication'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'`É o nome do Publicador alternativo. o *Publicador* é **sysname**, sem padrão.  
  
`[ @publisher_db = ] 'publisher_db'`É o nome do banco de dados de publicação. *publisher_db* é **sysname**, sem padrão.  
  
`[ @publication = ] 'publication'`É o nome da publicação. a *publicação* é **sysname**, sem padrão.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**alternate_publisher**|**sysname**|Nome do Publicador alternativo.|  
|**alternate_publisher_db**|**sysname**|Nome do banco de dados de publicação.|  
|**alternate_publication**|**sysname**|Nome da publicação.|  
|**alternate_distributor**|**sysname**|Nome do distribuidor.|  
|**friendly_name**|**nvarchar (255)**|Descrição do Publicador alternativo.|  
|**habilitado**|**bit**|Especifica se o servidor é um Publicador alternativo. **1** especifica que o Publicador está habilitado como um Publicador alternativo. **0** especifica que não está habilitado.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpmergealternatepublisher** é usado na replicação de mesclagem.  
  
 Durante cada sessão de mesclagem, o sistema examina o Publicador e o Assinante para a lista de cada um de publicadores alternativos. O processo de mesclagem adiciona ou descarta entradas na lista de publicadores alternativos, cujo resultado é a lista de publicadores alternativos na correspondência de Publicador e Assinante.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da lista de acesso à publicação da publicação podem ser executados **sp_helpmergealternatepublisher**.  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
