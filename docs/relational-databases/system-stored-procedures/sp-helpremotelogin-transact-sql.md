---
title: sp_helpremotelogin (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_helpremotelogin_TSQL
- sp_helpremotelogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpremotelogin
ms.assetid: 93f50869-2627-4642-899f-8f626f8833f4
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b34842bc6265d9a1615cb1f2e45d727b257a5c90
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="sphelpremotelogin-transact-sql"></a>sp_helpremotelogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Relata informações sobre logons remotos para um determinado servidor remoto, ou para todos os servidores, definido no servidor local.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] Use procedimentos armazenados de servidor vinculado e servidores vinculados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpremotelogin [ [ @remoteserver = ] 'remoteserver' ]   
     [ , [ @remotename = ] 'remote_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @remoteserver  **=**  ] **'***remoteserver***'**  
 É o servidor remoto sobre o qual as informações de logon remoto são retornadas. *remoteserver* é **sysname**, com um padrão NULL. Se *remoteserver* não é especificado, serão retornadas informações sobre todos os servidores remotos definidos no servidor local.  
  
 [ @remotename  **=**  ] **'***remote_name***'**  
 É um logon remoto específico no servidor remoto. *remote_name* é **sysname**, com um padrão NULL. Se *remote_name* não for especificado, as informações sobre todos os usuários remotos definidas para *remoteserver* é retornado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|servidor|**sysname**|Nome de um servidor remoto definido no servidor local.|  
|local_user_name|**sysname**|Logon no servidor local para os quais os logons remotos do servidor são mapeados.|  
|remote_user_name|**sysname**|Faça logon no servidor remoto que mapeia para local_user_name.|  
|opções|**sysname**|Confiável = O logon remoto não precisa fornecer uma senha ao se conectar ao servidor local a partir do servidor remoto.<br /><br /> Não confiável (ou em branco) = O logon remoto é solicitado a fornecer uma senha ao se conectar ao servidor local a partir do servidor remoto.|  
  
## <a name="remarks"></a>Comentários  
 Use sp_helpserver para listar os nomes de servidores remotos definidos no servidor local.  
  
## <a name="permissions"></a>Permissões  
 Nenhuma permissão é verificada.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-reporting-help-on-a-single-server"></a>A. Relatando ajuda em um único servidor  
 O exemplo a seguir exibe as informações sobre todos os usuários remotos no servidor remoto `Accounts`.  
  
```  
EXEC sp_helpremotelogin 'Accounts';  
```  
  
### <a name="b-reporting-help-on-all-remote-users"></a>B. Relatando ajuda em todos os usuários remotos  
 O exemplo a seguir exibe as informações sobre todos os usuários remotos em todos os servidores remotos conhecidos pelo servidor local.  
  
```  
EXEC sp_helpremotelogin;  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_addremotelogin &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md)   
 [sp_dropremotelogin &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropremotelogin-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_remoteoption &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-remoteoption-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
