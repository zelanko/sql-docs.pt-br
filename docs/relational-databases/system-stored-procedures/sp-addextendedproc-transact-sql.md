---
title: sp_addextendedproc (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addextendedproc_TSQL
- sp_addextendedproc
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addextendedproc
ms.assetid: c0d4b47b-a855-451e-90e5-5fb2d836ebfa
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0bc8ea22699762927a026ae4cc811500c193555c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68072749"
---
# <a name="sp_addextendedproc-transact-sql"></a>sp_addextendedproc (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Registra o nome de um novo procedimento armazenado estendido [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]para.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Em vez disso, use a [integração CLR](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md) .  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addextendedproc [ @functname = ] 'procedure' ,   
     [ @dllname = ] 'dll'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @functname = ] 'procedure'`É o nome da função a ser chamada na biblioteca de vínculo dinâmico (DLL). o *procedimento* é **nvarchar (517)**, sem padrão. Opcionalmente, o *procedimento* pode incluir o nome do proprietário no formato *proprietário. função*.  
  
`[ @dllname = ] 'dll'`É o nome da DLL que contém a função. *dll* é **varchar (255)**, sem padrão. É recomendável especificar o caminho completo da DLL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 Depois que um procedimento armazenado estendido é criado, ele deve ser [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] adicionado ao usando **sp_addextendedproc**. Para obter mais informações, consulte [adicionando um procedimento armazenado estendido a SQL Server](../../relational-databases/extended-stored-procedures-programming/adding-an-extended-stored-procedure-to-sql-server.md).  
  
 Esse procedimento só pode ser executado no banco de dados **mestre** . Para executar um procedimento armazenado estendido de um banco de dados que não seja o **mestre**, qualifique o nome do procedimento armazenado estendido com **Master**.  
  
 **sp_addextendedproc** adiciona entradas à exibição do catálogo [Sys. Objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) , registrando o nome do novo procedimento armazenado estendido [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]com. Ele também adiciona uma entrada na exibição de catálogo [Sys. extended_procedures](../../relational-databases/system-catalog-views/sys-extended-procedures-transact-sql.md) .  
  
> [!IMPORTANT]  
>  DLLs existentes que não são registradas com um caminho completo não funcionarão depois da atualização do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para corrigir o problema, use **sp_dropextendedproc** para cancelar o registro da dll e, em seguida, registre-a novamente com **sp_addextendedproc**, especificando o caminho completo.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_addextendedproc**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir adiciona o procedimento armazenado estendido **xp_hello** .  
  
```  
USE master;  
GO  
EXEC sp_addextendedproc xp_hello, 'c:\xp_hello.dll';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [CONCEDER &#40;&#41;Transact-SQL](../../t-sql/statements/grant-transact-sql.md)   
 [REVOGAr &#40;&#41;de Transact-SQL](../../t-sql/statements/revoke-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropextendedproc](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpextendedproc](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
