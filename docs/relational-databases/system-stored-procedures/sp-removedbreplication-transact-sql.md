---
title: sp_removedbreplication (T-SQL)
description: Descreve o sp_removedbreplication procedimento armazenado usado para remover todos os objetos de replicação no banco de dados de publicação para SQL Server replicação.
ms.custom: seo-lt-2019
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 01fc666444891836011b80e77492b1cdebbefff5
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538634"
---
# <a name="sp_removedbreplication-transact-sql"></a>sp_removedbreplication (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Este procedimento armazenado remove todos os objetos de replicação no banco de dados de publicação na instância do Publicador do SQL Server ou no banco de dados de assinatura na instância do Assinante do SQL Server. Execute no banco de dados apropriado ou, se a execução for no contexto de outro banco de dados na mesma instância, especifique o banco de dados em que os objetos de replicação devem ser removidos. Esse procedimento não remove objetos de outros bancos de dados, como o banco de dados de distribuição.  
  
> [!NOTE]  
>  Esse procedimento só deve ser usado se outros métodos de remoção de objetos de replicação falharem.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_removedbreplication [ [ @dbname = ] 'dbname' ]  
    [ , [ @type = ] type ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @dbname = ] 'dbname'` É o nome do banco de dados. *dbname* é **sysname**, com um valor padrão de NULL. Quando for NULL, o banco de dados atual será usado.  
  
`[ @type = ] type` É o tipo de replicação para o qual os objetos de banco de dados estão sendo removidos. o *tipo* é **nvarchar (5)** e pode ser um dos valores a seguir.  
  
|||  
|-|-|  
|**transação**|Remove objetos de publicação de replicação transacional.|  
|**Mescle**|Remove objetos de publicação de replicação de mesclagem.|  
|**ambos** (padrão)|Remove todos os objetos de publicação de replicação.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_removedbreplication** é usado em todos os tipos de replicação.  
  
 **sp_removedbreplication** é útil ao restaurar um banco de dados replicado que não tem objetos de replicação que precisem ser restaurados.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Desabilitar a publicação e a distribuição](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
