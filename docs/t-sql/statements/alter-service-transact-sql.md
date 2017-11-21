---
title: ALTER SERVICE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER SERVICE
- ALTER_SERVICE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- modifying services
- contracts [Service Broker], modifying
- ALTER SERVICE statement
- services [Service Broker], modifying
ms.assetid: 2b4608f7-bb2e-4246-aa29-b52c55995b3a
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f0f09a018648566cd928258da958bb06dedc6022
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="alter-service-transact-sql"></a>ALTER SERVICE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera um serviço existente.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ALTER SERVICE service_name   
   [ ON QUEUE [ schema_name . ]queue_name ]   
   [ ( < opt_arg > [ , ...n ] ) ]  
[ ; ]  
  
<opt_arg> ::=  
   ADD CONTRACT contract_name | DROP CONTRACT contract_name  
```  
  
## <a name="arguments"></a>Argumentos  
 *SERVICE_NAME*  
 É o nome do serviço a ser alterado. Os nomes de servidor, banco de dados e esquema não podem ser especificados.  
  
 FILA de ON [ *schema_name***.** ] *nome_da_fila*  
 Especifica a nova fila deste serviço. O [!INCLUDE[ssSB](../../includes/sssb-md.md)] move todas as mensagens deste serviço da fila atual para uma nova fila.  
  
 Adicionar contrato *contract_name*  
 Especifica um contrato para acrescentar ao conjunto de contratos exposto por este serviço.  
  
 DROP CONTRACT *contract_name*  
 Especifica um contrato a ser excluído do conjunto de contratos exposto por este serviço. O [!INCLUDE[ssSB](../../includes/sssb-md.md)] envia uma mensagem de erro em quaisquer conversas existentes com este serviço que usem este contrato.  
  
## <a name="remarks"></a>Comentários  
 Quando a instrução ALTER SERVICE exclui um contrato de um serviço, o serviço não pode mais ser um destino das conversas que usam esse contrato. Portanto, [!INCLUDE[ssSB](../../includes/sssb-md.md)] não permite conversas novas ao serviço naquele contrato. As conversas existentes que usam o contrato não são afetadas.  
  
 Para alterar a AUTHORIZATION para um serviço, use a instrução ALTER AUTHORIZATION.  
  
## <a name="permissions"></a>Permissões  
 Permissão para alterar um serviço assume como padrão o proprietário do serviço, os membros do **db_ddladmin** ou **db_owner** fixa de funções de banco de dados e os membros do **sysadmin** função de servidor fixa.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-changing-the-queue-for-a-service"></a>A. Alterando a fila para um serviço  
 O exemplo a seguir altera o serviço `//Adventure-Works.com/Expenses` para usar a fila `NewQueue`.  
  
```  
ALTER SERVICE [//Adventure-Works.com/Expenses]  
    ON QUEUE NewQueue ;  
```  
  
### <a name="b-adding-a-new-contract-to-the-service"></a>B. Adicionando um novo contrato ao serviço  
 O exemplo a seguir altera o serviço `//Adventure-Works.com/Expenses` para permitir caixas de diálogo no contrato `//Adventure-Works.com/Expenses`.  
  
```  
ALTER SERVICE [//Adventure-Works.com/Expenses]  
    (ADD CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission]) ;  
```  
  
### <a name="c-adding-a-new-contract-to-the-service-dropping-existing-contract"></a>C. Adicionando um novo contrato ao serviço, descartando um contrato existente  
 O exemplo a seguir altera o serviço `//Adventure-Works.com/Expenses` para permitir caixas de diálogo no contrato `//Adventure-Works.com/Expenses/ExpenseProcessing` e para não permitir caixas de diálogo no contrato `//Adventure-Works.com/Expenses/ExpenseSubmission`.  
  
```  
ALTER SERVICE [//Adventure-Works.com/Expenses]  
    (ADD CONTRACT [//Adventure-Works.com/Expenses/ExpenseProcessing],   
     DROP CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission]) ;  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/create-service-transact-sql.md)   
 [Remover serviço &#40; Transact-SQL &#41;](../../t-sql/statements/drop-service-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

