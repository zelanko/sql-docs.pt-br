---
title: sp_altermessage (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_altermessage_TSQL
- sp_altermessage
dev_langs:
- TSQL
helpviewer_keywords:
- sp_altermessage
ms.assetid: 1b28f280-8ef9-48e9-bd99-ec14d79abaca
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4949307cdaf2cc712e56525e872381c2af8256fd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72304798"
---
# <a name="sp_altermessage-transact-sql"></a>sp_altermessage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera o estado de mensagens definidas pelo usuário ou do sistema em uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. As mensagens definidas pelo usuário podem ser exibidas usando a exibição do catálogo **Sys. messages** .  

  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_altermessage [ @message_id = ] message_number   ,[ @parameter = ]'write_to_log'  
   ,[ @parameter_value = ]'value'   
```  
  
## <a name="arguments"></a>Argumentos  
 [**@message_id =** ] *message_number*  
 É o número do erro da mensagem a ser alterado de **Sys. messages**. *message_number* é **int** sem valor padrão.  
  
`[ @parameter = ] 'write\_to\_log_'`É usado com ** \@parameter_value** para indicar que a mensagem deve ser gravada no log [!INCLUDE[msCoName](../../includes/msconame-md.md)] de aplicativos do Windows. *write_to_log* é **sysname** sem valor padrão. *write_to_log* deve ser definido como WITH_LOG ou nulo. Se *write_to_log* for definido como WITH_LOG ou NULL e o valor de ** \@parameter_value** for **true**, a mensagem será gravada no log de aplicativos do Windows. Se *write_to_log* for definido como WITH_LOG ou NULL e o valor de ** \@parameter_value** for **false**, a mensagem nem sempre será gravada no log de aplicativos do Windows, mas poderá ser gravada dependendo de como o erro foi gerado. Se *write_to_log* for especificado, o valor de ** \@parameter_value** também deverá ser especificado.  
  
> [!NOTE]  
>  Se uma mensagem for gravada no log do aplicativo do Windows, ela também será gravada no arquivo de log de erros do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
`[ @parameter_value = ]'value_'`É usado com ** \@o parâmetro** para indicar que o erro deve ser gravado no log [!INCLUDE[msCoName](../../includes/msconame-md.md)] de aplicativos do Windows. o *valor* é **varchar (5)**, sem valor padrão. Se **for true**, o erro será sempre gravado no log de aplicativos do Windows. Se **for false**, o erro nem sempre será gravado no log de aplicativos do Windows, mas poderá ser gravado dependendo de como o erro foi gerado. Se *Value* for especificado, *write_to_log* para ** \@o parâmetro** também deverá ser especificado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 O efeito de **sp_altermessage** com a opção with_log é semelhante ao do parâmetro RAISERROR com log, exceto que **sp_altermessage** altera o comportamento de log de uma mensagem existente. Se uma mensagem foi alterada para ser WITH_LOG, ela sempre será gravada no log de aplicativos do Windows, independentemente de como um usuário invocar o erro. Até mesmo se RAISERROR for executado sem a opção WITH_LOG, o erro será gravado no log de aplicativos do Windows.  
  
 As mensagens do sistema podem ser modificadas usando **sp_altermessage**.  
  
## <a name="permissions"></a>Permissões  
 Requer a associação na função de servidor fixa **ServerAdmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir faz com que a mensagem `55001` existente seja registrada no log de aplicativos do Windows.  
  
```  
EXECUTE sp_altermessage 55001, 'WITH_LOG', 'true';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [sp_addmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)   
 [sp_dropmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmessage-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
