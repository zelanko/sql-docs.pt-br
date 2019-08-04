---
title: sp_removedbreplication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_removedbreplication
- sp_removedbreplication_TSQL
helpviewer_keywords:
- sp_removedbreplication
ms.assetid: cb98d571-d1eb-467b-91f7-a6e091009672
author: stevestein
ms.author: sstein
ms.openlocfilehash: fdae843c3918013ec850c5d807853c10a8f3f190
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771036"
---
# <a name="spremovedbreplication-transact-sql"></a>sp_removedbreplication (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Este procedimento armazenado remove todos os objetos de replicação no banco de dados de publicação na instância do Publicador do SQL Server ou no banco de dados de assinatura na instância do Assinante do SQL Server. Execute no banco de dados apropriado ou, se a execução for no contexto de outro banco de dados na mesma instância, especifique o banco de dados em que os objetos de replicação devem ser removidos. Esse procedimento não remove objetos de outros bancos de dados, como o banco de dados de distribuição.  
  
> [!NOTE]  
>  Esse procedimento só deve ser usado se outros métodos de remoção de objetos de replicação falharem.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_removedbreplication [ [ @dbname = ] 'dbname' ]  
    [ , [ @type = ] type ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @dbname = ] 'dbname'`É o nome do banco de dados. *dbname* é **sysname**, com um valor padrão de NULL. Quando for NULL, o banco de dados atual será usado.  
  
`[ @type = ] type`É o tipo de replicação para o qual os objetos de banco de dados estão sendo removidos. o *tipo* é **nvarchar (5)** e pode ser um dos valores a seguir.  
  
|||  
|-|-|  
|**transação**|Remove objetos de publicação de replicação transacional.|  
|**Mescle**|Remove objetos de publicação de replicação de mesclagem.|  
|**ambos** os|Remove todos os objetos de publicação de replicação.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_removedbreplication** é usado em todos os tipos de replicação.  
  
 **sp_removedbreplication** é útil ao restaurar um banco de dados replicado que não tem objetos de replicação que precisam ser restaurados.  
  
 **sp_removedbreplication** não pode ser usado em um banco de dados que está marcado como somente leitura.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_removedbreplication](../../relational-databases/replication/codesnippet/tsql/sp-removedbreplication-t_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_removedbreplication**.  
  
## <a name="example"></a>Exemplo  
  
```  
-- Remove replication objects from the subscription database on MYSUB.  
DECLARE @subscriptionDB AS sysname  
SET @subscriptionDB = N'AdventureWorksReplica'  
  
-- Remove replication objects from a subscription database (if necessary).  
USE master  
EXEC sp_removedbreplication @subscriptionDB  
GO  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Desabilitar a publicação e a distribuição](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
