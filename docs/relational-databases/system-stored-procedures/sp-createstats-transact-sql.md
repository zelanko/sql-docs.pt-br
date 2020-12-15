---
description: sp_createstats (Transact-SQL)
title: sp_createstats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_createstats_TSQL
- sp_createstats
dev_langs:
- TSQL
helpviewer_keywords:
- sp_createstats
ms.assetid: 8204f6f2-5704-40a7-8d51-43fc832eeb54
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7af34bd1bbe065012b18826f7edaec31940d1e50
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97466867"
---
# <a name="sp_createstats-transact-sql"></a>sp_createstats (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Chama a instrução [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) para criar estatísticas de coluna única em colunas que ainda não são a primeira coluna em um objeto de estatísticas. A criação de estatísticas de coluna única aumenta o número de histogramas, o que pode melhorar estimativas de cardinalidade, planos de consulta e desempenho de consulta. A primeira coluna de um objeto de estatísticas tem um histograma; outras colunas, não.  
  
 sp_createstats é útil para aplicativos como o benckmark, quando os tempos de execução de consulta são críticos e não podem aguardar a geração de estatísticas de coluna única pelo otimizador de consulta. Na maioria dos casos, não é necessário usar sp_createstats; o otimizador de consulta gera estatísticas de coluna única conforme necessário para melhorar os planos de consulta quando a opção de **AUTO_CREATE_STATISTICS** está ativada.  
  
 Para obter mais informações sobre estatísticas, consulte [Estatísticas](../../relational-databases/statistics/statistics.md). Para obter mais informações sobre como gerar estatísticas de coluna única, consulte a opção **AUTO_CREATE_STATISTICS** em [Opções ALTER DATABASE SET &#40;&#41;Transact-SQL](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_createstats   
    [   [ @indexonly =   ] { 'indexonly'   | 'NO' } ]   
    [ , [ @fullscan =    ] { 'fullscan'    | 'NO' } ]   
    [ , [ @norecompute = ] { 'norecompute' | 'NO' } ]  
    [ , [ @incremental = ] { 'incremental' | 'NO' } ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @indexonly = ] 'indexonly'` Cria estatísticas somente em colunas que estão em um índice existente e não são a primeira coluna em qualquer definição de índice. **indexonly** é **Char (9)**. O padrão é NO.  
  
`[ @fullscan = ] 'fullscan'` Usa a instrução [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) com a opção **FULLSCAN** . **FULLSCAN** é **Char (9)**.  O padrão é NO.  
  
`[ @norecompute = ] 'norecompute'` Usa a instrução [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) com a opção **NORECOMPUTE** . **NORECOMPUTE** é **Char (12)**.  O padrão é NO.  
  
`[ @incremental = ] 'incremental'` Usa a instrução [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) com a opção **incremental = on** . **Incremental** é **Char (12)**.  O padrão é NO.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Cada objeto de estatísticas novo tem o mesmo nome da coluna em que foi criado.  
  
## <a name="remarks"></a>Comentários  
 sp_createstats não cria nem atualiza estatísticas em colunas que são a primeira coluna em um objeto de estatísticas existente;  Isso inclui a primeira coluna de estatísticas criadas para índices, colunas com estatísticas de coluna única geradas com AUTO_CREATE_STATISTICS opção e a primeira coluna de estatísticas criada com a instrução CREATE STATISTICs. sp_createstats não cria estatísticas nas primeiras colunas de índices desabilitados, a menos que essa coluna seja usada em outro índice habilitado. sp_createstats não cria estatísticas em tabelas com um índice clusterizado desabilitado.  
  
 Quando a tabela contém um conjunto de colunas, sp_createstats não cria estatísticas em colunas esparsas. Para obter mais informações sobre conjuntos de colunas e colunas esparsas, consulte [usar conjuntos](../../relational-databases/tables/use-column-sets.md) de colunas e [usar colunas esparsas](../../relational-databases/tables/use-sparse-columns.md).  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados fixa db_owner.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-create-single-column-statistics-on-all-eligible-columns"></a>a. Criar estatísticas de coluna única em todas as colunas qualificadas  
 O exemplo a seguir cria estatísticas de coluna única em todas as colunas qualificadas do banco de dados atual.  
  
```  
EXEC sp_createstats;  
GO  
```  
  
### <a name="b-create-single-column-statistics-on-all-eligible-index-columns"></a>B. Criar estatísticas de coluna única em todas as colunas de índice qualificadas  
 O exemplo a seguir cria estatísticas de coluna única em todas as colunas qualificadas que já estejam em um índice, não sendo a primeira coluna no índice.  
  
```  
EXEC sp_createstats 'indexonly';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Estatística](../../relational-databases/statistics/statistics.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [Mecanismo de Banco de Dados procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
