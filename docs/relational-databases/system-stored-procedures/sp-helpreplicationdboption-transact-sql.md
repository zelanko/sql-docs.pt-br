---
title: sp_helpreplicationdboption (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
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
- sp_helpreplicationdboption_TSQL
- sp_helpreplicationdboption
helpviewer_keywords:
- sp_helpreplicationdboption
ms.assetid: 143ce689-108b-49d7-9892-fd3a86897f38
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c67c6c6f6f74d3cedf2aa8acc4232886b6d52a9f
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43038748"
---
# <a name="sphelpreplicationdboption-transact-sql"></a>sp_helpreplicationdboption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Mostra se os bancos de dados no Publicador estão habilitados para replicação. Esse procedimento armazenado é executado no Publicador, em qualquer banco de dados. *Não tem suporte para Publicadores Oracle.*  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpreplicationdboption [ [ @dbname =] 'dbname' ]  
    [ , [ @type = ] 'type' ]  
    [ , [ @reserved = ] reserved ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@dbname=**] **'***dbname***'**  
 É o nome do banco de dados. *DBName* está **sysname**, com um padrão de **%**. Se **%**, em seguida, o conjunto de resultados contém todos os bancos de dados no publicador, caso contrário, apenas informações sobre o banco de dados especificado serão retornadas. Não são retornadas informações para nenhum banco de dados para o qual o usuário não tenha a permissão apropriada, como descrita abaixo.  
  
 [  **@type=**] **'***tipo***'**  
 Restringe o conjunto de resultados para conter apenas bancos de dados no qual a opção de replicação especificada *tipo* valor tiver sido habilitado. *tipo de* está **sysname**, e pode ser um dos valores a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|**Publicar**|Replicação transacional permitida.|  
|**publicação de mesclagem**|Replicação de mesclagem permitida.|  
|**replicação permitida** (padrão)|Replicação transacional ou replicação de mesclagem permitida.|  
  
 [  **@reserved=** ] *reservado*  
 Especifica se as informações sobre as publicações e assinaturas existentes são retornadas. *reservado* está **bit**, com um valor padrão de 0. Se **1**, o conjunto de resultados inclui informações sobre se o banco de dados especificado tem qualquer publicações ou assinaturas existentes.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome do banco de dados.|  
|**id**|**int**|Identificador de banco de dados.|  
|**transpublish**|**bit**|Se o banco de dados tiver sido habilitado para instantâneo ou publicação transacional; onde um valor de **1** significa que o instantâneo ou publicação transacional está habilitada.|  
|**mergepublish**|**bit**|Se o banco de dados tiver sido habilitado para mesclagem de publicação; onde um valor de **1** significa que a publicação de mesclagem está habilitado.|  
|**dbowner**|**bit**|Se o usuário for um membro do **db_owner** fixo de função de banco de dados; onde um valor de **1** indica que o usuário é um membro dessa função.|  
|**dbreadonly**|**bit**|É se o banco de dados está marcado como somente leitura; onde um valor de **1** significa que o banco de dados é somente leitura.|  
|**haspublications**|**bit**|Se o banco de dados tiver qualquer publicação existente; onde um valor de **1** significa que há publicações existentes.|  
|**haspullsubscriptions**|**bit**|Se o banco de dados tiver qualquer assinatura pull existente; onde um valor de **1** significa que existem assinaturas pull.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_helpreplicationdboption** é usado em instantâneo, transacional e replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Os membros de **sysadmin** pode executar a função de servidor fixa **sp_helpreplicationdboption** para qualquer banco de dados. Os membros de **db_owner** pode executar a função de banco de dados fixa **sp_helpreplicationdboption** desse banco de dados.  
  
## <a name="see-also"></a>Consulte também  
 [sp_replicationdboption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
