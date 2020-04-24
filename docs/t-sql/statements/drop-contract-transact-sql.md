---
title: DROP CONTRACT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_CONTRACT_TSQL
- DROP CONTRACT
dev_langs:
- TSQL
helpviewer_keywords:
- dropping contracts
- removing contracts
- deleting contracts
- contracts [Service Broker], dropping
- DROP CONTRACT statement
ms.assetid: fdd0f81e-3c22-4cdf-9416-b4977a6ac3b6
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f52928e5badd204d84b6cb0b51c68cebc164e1c2
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81635387"
---
# <a name="drop-contract-transact-sql"></a>DROP CONTRACT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Descarta um contrato existente de um banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
  
DROP CONTRACT contract_name   
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *contract_name*  
 O nome do contrato para descartar. Os nomes de servidor, banco de dados e esquema não podem ser especificados.  
  
## <a name="remarks"></a>Comentários  
 Você não poderá descartar um contrato se qualquer prioridade de serviço ou de conversa se referir ao contrato.  
  
 Quando você descartar um contrato, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] termina qualquer conversa existente que usa o contrato com um erro.  
  
## <a name="permissions"></a>Permissões  
 A permissão para descartar um contrato assume como padrão o proprietário desse contrato, os membros das funções de banco de dados fixas db_ddladmin ou db_owner e os membros da função de servidor fixa sysadmin.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir remove o contrato `//Adventure-Works.com/Expenses/ExpenseSubmission` do banco de dados.  
  
```  
DROP CONTRACT   
    [//Adventure-Works.com/Expenses/ExpenseSubmission] ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-broker-priority-transact-sql.md)   
 [ALTER SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-service-transact-sql.md)   
 [CREATE CONTRACT &#40;Transact-SQL&#41;](../../t-sql/statements/create-contract-transact-sql.md)   
 [DROP BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-broker-priority-transact-sql.md)   
 [DROP SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-service-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
