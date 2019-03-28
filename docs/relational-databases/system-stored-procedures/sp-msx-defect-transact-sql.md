---
title: sp_msx_defect (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_msx_defect
- sp_msx_defect_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_msx_defect
ms.assetid: 0dfd963a-3bc5-4b58-94f7-aec976da2883
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 16e523bc26b8469f3ee7306f3e6fd2902ef727bb
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58528528"
---
# <a name="spmsxdefect-transact-sql"></a>sp_msx_defect (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove o servidor atual de operações multisservidor.  
  
> [!CAUTION]  
>  **sp_msx_defect** edita o registro. A edição manual do registro não é recomendada, pois alterações incorretas ou não apropriadas podem causar sérios problemas de configuração para o sistema. Portanto, apenas usuários experientes deveriam usar o programa Editor do Registro para editar o registro. Para obter mais informações, consulte a documentação do Microsoft Windows.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_msx_defect [@forced_defection =] forced_defection  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @forced_defection = ] forced_defection` Especifica se deve ou não forçar a remoção ocorra se o Master SQLServerAgent foi perdido permanentemente devido a um irreversivelmente danificado **msdb** banco de dados, ou no **msdb** backup de banco de dados. *forced_defection*está **bit**, com um padrão de **0**, que indica que nenhuma remoção forçada deve ocorrer. Um valor de **1** força a remoção.  
  
 Depois de forçar uma remoção pela execução **sp_msx_defect**, um membro das **sysadmin** a função de servidor fixa no Master SQLServerAgent deve executar o comando a seguir para concluir a remoção:  
  
```  
EXECUTE msdb.dbo.sp_delete_targetserver @server_name = 'tsx-server', @post_defection =  0;  
```  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentários  
 Quando **sp_msx_defect** for concluído corretamente, uma mensagem será retornada.  
  
## <a name="permissions"></a>Permissões  
 Para executar este procedimento armazenado, o usuário deve ser um membro da função de servidor fixa **sysadmin** .  
  
## <a name="see-also"></a>Consulte também  
 [sp_msx_enlist &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
