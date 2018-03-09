---
title: sp_prepare (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 02/28/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepare_TSQL
- sp_cursor_prepare
dev_langs:
- TSQL
helpviewer_keywords:
- sp_prepare
ms.assetid: f328c9eb-8211-4863-bafa-347e1bf7bb3f
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9917490d96272d948560789201f4455a12ab2584
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2018
---
# <a name="spprepare-transact-sql"></a>sp_prepare (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Prepara uma parametrizadas [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução e retorna uma instrução *tratar* para execução. sp_prepare é invocado pela especificação de ID = 11 em um pacote de protocolo TDS de dados tabulares.  
  
 ![Ícone de link do artigo](../../database-engine/configure-windows/media/topic-link.gif "ícone de link do tópico") [convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_prepare handle OUTPUT, params, stmt, options  
```  
  
## <a name="arguments"></a>Argumentos  
 *handle*  
 É gerado um SQL Server *identificador preparado* identificador. *tratar* é um parâmetro obrigatório com um **int** valor de retorno.  
  
 *params*  
 Identifica instruções parametrizadas. O *params* definição de variáveis é substituída para marcadores de parâmetro na instrução. *params* é um parâmetro obrigatório que chama uma **ntext**, **nchar**, ou **nvarchar** valor de entrada. Insira um valor NULL se a instrução não for parametrizada.  
  
 *stmt*  
 Define o conjunto de resultados do cursor. O *stmt* parâmetro é obrigatório e chama um **ntext**, **nchar**, ou **nvarchar** valor de entrada.  
  
 *options*  
 Um parâmetro opcional que retorna uma descrição das colunas do conjunto de resultados de cursor. *opções* requer o seguinte valor de entrada de int:  
  
|Value|Description|  
|-----------|-----------------|  
|0x0001|RETURN_METADATA|  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir prepara e executa uma instrução simples.  
  
```  
Declare @P1 int;  
Exec sp_prepare @P1 output,   
    N'@P1 nvarchar(128), @P2 nvarchar(100)',  
    N'SELECT database_id, name FROM sys.databases WHERE name=@P1 AND state_desc = @P2';  
Exec sp_execute @P1, N'tempdb', N'ONLINE';  
EXEC sp_unprepare @P1;  
```  

  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

