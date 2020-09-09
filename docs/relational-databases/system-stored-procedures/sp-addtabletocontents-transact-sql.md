---
description: sp_addtabletocontents (Transact-SQL)
title: sp_addtabletocontents (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addtabletocontents_TSQL
- sp_addtabletocontents
helpviewer_keywords:
- sp_addtabletocontents
ms.assetid: 2ea27001-74f4-463e-bf1b-b6b5a86b9219
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 26b1946d03fe949bd0a2af52ce07d64198dd1bbf
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548321"
---
# <a name="sp_addtabletocontents-transact-sql"></a>sp_addtabletocontents (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Insere referências em tabelas de controle de mesclagem para linhas em uma tabela de origem atualmente não incluída nas tabelas de controle. Use esta opção se você tiver carregado em massa uma grande quantidade de dados usando o **bcp**, que não acionará gatilhos de rastreamento de mesclagem. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addtabletocontents [ @table_name = ] 'table_name'  
    [ , [ @owner_name = ] 'owner_name' ]  
    [ , [ @filter_clause = ] 'filter_clause' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @table_name = ] 'table_name'` É o nome da tabela. *table_name* é **sysname**, sem padrão.  
  
`[ @owner_name = ] 'owner_name'` É o nome do proprietário da tabela. *owner_name* é **sysname**, com um padrão de NULL.  
  
`[ @filter_clause = ] 'filter_clause'` Especifica uma cláusula de filtro que controla quais linhas dos dados carregados recentemente devem ser adicionadas às tabelas de controle de mesclagem. *filter_clause* é **nvarchar (4000)**, com um valor padrão de NULL. Se *filter_clause* for **NULL**, todas as linhas carregadas em massa serão adicionadas.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_addtabletocontents** é usado somente na replicação de mesclagem.  
  
 As linhas na *table_name* são referenciadas por sua **ROWGUIDCOL** e as referências são adicionadas às tabelas de controle de mesclagem. **sp_addtabletocontents** deve ser usado após a cópia em massa de dados em uma tabela que é publicada usando a replicação de mesclagem. Esse procedimento armazenado inicia o controle das linhas copiadas e assegura que as novas linhas sejam incluídas na próxima sincronização.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_addtabletocontents**.  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
