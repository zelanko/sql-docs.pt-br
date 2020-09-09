---
description: sp_helpreplicationdboption (Transact-SQL)
title: sp_helpreplicationdboption (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpreplicationdboption_TSQL
- sp_helpreplicationdboption
helpviewer_keywords:
- sp_helpreplicationdboption
ms.assetid: 143ce689-108b-49d7-9892-fd3a86897f38
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6733b1f473c91094bd8af177bce4b13f3cf1b03e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89526848"
---
# <a name="sp_helpreplicationdboption-transact-sql"></a>sp_helpreplicationdboption (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Mostra se os bancos de dados no Publicador estão habilitados para replicação. Esse procedimento armazenado é executado no Publicador, em qualquer banco de dados. *Sem suporte para Publicadores Oracle.*  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpreplicationdboption [ [ @dbname =] 'dbname' ]  
    [ , [ @type = ] 'type' ]  
    [ , [ @reserved = ] reserved ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @dbname = ] 'dbname'` É o nome do banco de dados. *dbname* é **sysname**, com um padrão de **%** . Se **%** , em seguida, o conjunto de resultados contiver todos os bancos de dados no Publicador, caso contrário, apenas as informações sobre o banco de dados especificado serão retornadas. Não são retornadas informações para nenhum banco de dados para o qual o usuário não tenha a permissão apropriada, como descrita abaixo.  
  
`[ @type = ] 'type'` Restringe o conjunto de resultados para conter somente os bancos de dados nos quais o valor do *tipo* de opção de replicação especificado foi habilitado. o *tipo* é **sysname**e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**publicou**|Replicação transacional permitida.|  
|**publicação de mesclagem**|Replicação de mesclagem permitida.|  
|**replicação permitida** (padrão)|Replicação transacional ou replicação de mesclagem permitida.|  
  
`[ @reserved = ] reserved` Especifica se as informações sobre publicações e assinaturas existentes são retornadas. *reservado* é um **bit**, com um valor padrão de 0. Se **1**, o conjunto de resultados incluirá informações sobre se o banco de dados especificado tem alguma publicação ou assinatura existente.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome do banco de dados.|  
|**id**|**int**|Identificador de banco de dados.|  
|**transpublish**|**bit**|Se o banco de dados tiver sido habilitado para publicação de instantâneo ou transacional; em que um valor de **1** significa que a publicação de instantâneo ou transacional está habilitada.|  
|**mergepublish**|**bit**|Se o banco de dados tiver sido habilitado para publicação de mesclagem; em que um valor de **1** significa que a publicação de mesclagem está habilitada.|  
|**dbowner**|**bit**|Se o usuário for membro da função de banco de dados fixa **db_owner** ; em que um valor de **1** indica que o usuário é um membro dessa função.|  
|**dbreadonly**|**bit**|Se o banco de dados estiver marcado como somente leitura; em que um valor de **1** significa que o banco de dados é somente leitura.|  
|**haspublications**|**bit**|É se o banco de dados tiver qualquer publicação existente; em que um valor de **1** significa que há publicações existentes.|  
|**haspullsubscriptions**|**bit**|É se o banco de dados tiver qualquer assinatura pull existente; em que um valor de **1** significa que há assinaturas pull existentes.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpreplicationdboption** é usado em replicação de instantâneo, transacional e de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Os membros da função de servidor fixa **sysadmin** podem executar **sp_helpreplicationdboption** para qualquer banco de dados. Os membros da função de banco de dados fixa **db_owner** podem executar **sp_helpreplicationdboption** para esse banco de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_replicationdboption ](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
