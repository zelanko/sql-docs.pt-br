---
description: sp_msx_enlist (Transact-SQL)
title: sp_msx_enlist (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_msx_enlist_TSQL
- sp_msx_enlist
dev_langs:
- TSQL
helpviewer_keywords:
- sp_msx_enlist
ms.assetid: ceb3b2bc-0cc4-48d8-9bdc-6a809556e35f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9435c4b8628bb119b0ac81126e50e37a67650532
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541610"
---
# <a name="sp_msx_enlist-transact-sql"></a>sp_msx_enlist (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Adiciona o servidor atual à lista de servidores disponíveis no servidor mestre.  
  
> [!CAUTION]  
>  O procedimento armazenado **sp_msx_enlist** edita o registro. A edição manual do registro não é recomendada, pois alterações incorretas ou não apropriadas podem causar sérios problemas de configuração para o sistema. Portanto, apenas usuários experientes deveriam usar o programa Editor do Registro para editar o registro. Para obter mais informações, consulte a documentação do Microsoft Windows.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_msx_enlist [@msx_server_name =] 'msx_server'   
     [, [@location =] 'location']  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @msx_server_name = ] 'msx_server'` O nome do servidor de administração multisservidor (Mestre). *msx_server* é **sysname**, sem padrão.  
  
`[ @location = ] 'location'` O local do servidor de destino a ser adicionado. *Location* é **nvarchar (100)**, com um padrão de NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="permissions"></a>Permissões  
 As permissões para executar este procedimento assumem como padrão os membros da função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir inscreve o servidor atual no servidor mestre `AdventureWorks1`. O local do servidor atual é `Building 21, Room 309, Rack 5`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_msx_enlist N'AdventureWorks1',   
    N'Building 21, Room 309, Rack 5' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_msx_defect ](../../relational-databases/system-stored-procedures/sp-msx-defect-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de xp_cmdshell ](../../relational-databases/system-stored-procedures/xp-cmdshell-transact-sql.md)  
  
  
