---
title: sp_createstats (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_createstats_TSQL
- sp_createstats
dev_langs: TSQL
helpviewer_keywords: sp_createstats
ms.assetid: 8204f6f2-5704-40a7-8d51-43fc832eeb54
caps.latest.revision: "47"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1b9811ca7824426900f77fc625bfa50732d7ba69
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spcreatestats-transact-sql"></a>sp_createstats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Chamadas de [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) instrução para criar estatísticas de coluna única em colunas que não ainda a primeira coluna em um objeto de estatísticas. A criação de estatísticas de coluna única aumenta o número de histogramas, o que pode melhorar estimativas de cardinalidade, planos de consulta e desempenho de consulta. A primeira coluna de um objeto de estatísticas tem um histograma; outras colunas, não.  
  
 sp_createstats é útil para aplicativos como o benckmark, quando os tempos de execução de consulta são críticos e não podem aguardar a geração de estatísticas de coluna única pelo otimizador de consulta. Na maioria dos casos, não é necessário usar sp_createstats; o otimizador de consultas gera estatísticas de coluna única conforme necessário para melhorar a consulta planos quando o **AUTO_CREATE_STATISTICS** opção está ativada.  
  
 Para obter mais informações sobre estatísticas, consulte [estatísticas](../../relational-databases/statistics/statistics.md). Para obter mais informações sobre como gerar estatísticas de coluna única, consulte o **AUTO_CREATE_STATISTICS** opção [opções ALTER DATABASE SET &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_createstats   
    [   [ @indexonly =   ] { 'indexonly'   | 'NO' } ]   
    [ , [ @fullscan =    ] { 'fullscan'    | 'NO' } ]   
    [ , [ @norecompute = ] { 'norecompute' | 'NO' } ]  
    [ , [ @incremental = ] { 'incremental' | 'NO' } ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@indexonly=** ] **'indexonly'**  
 Cria estatísticas apenas em colunas que estão em um índice existente e não são a primeira coluna em qualquer definição de índice. **indexonly** é **char(9)**. O padrão é NO.  
  
 [  **@fullscan=** ] **'fullscan'**  
 Usa o [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) instrução com o **FULLSCAN** opção. **FULLSCAN** é **char(9)**.  O padrão é NO.  
  
 [  **@norecompute=** ] **'norecompute'**  
 Usa o [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) instrução com o **NORECOMPUTE** opção. **NORECOMPUTE** é **char(12)**.  O padrão é NO.  
  
 [  **@incremental=** ] **'incremental'**  
 Usa o [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) instrução com o **INCREMENTAL = ON** opção. **Incremental** é **char(12)**.  O padrão é NO.  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Cada objeto de estatísticas novo tem o mesmo nome da coluna em que foi criado.  
  
## <a name="remarks"></a>Comentários  
 sp_createstats não cria nem atualiza estatísticas em colunas que são a primeira coluna em um objeto de estatísticas existente;  Isso inclui a primeira coluna de estatísticas criada para índices, colunas com estatísticas de coluna única geradas com a opção AUTO_CREATE_STATISTICS e a primeira coluna de estatísticas criadas com a instrução CREATE STATISTICS. sp_createstats não cria estatísticas nas primeiras colunas de índices desabilitados a menos que essa coluna é usada em outro índice habilitado. sp_createstats não cria estatísticas em tabelas com um índice clusterizado desabilitado.  
  
 Quando a tabela contém um conjunto de colunas, sp_createstats não cria estatísticas em colunas esparsas. Para obter mais informações sobre conjuntos de colunas e as colunas esparsas, consulte [usar conjuntos de colunas](../../relational-databases/tables/use-column-sets.md) e [usar colunas esparsas](../../relational-databases/tables/use-sparse-columns.md).  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados fixa db_owner.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-create-single-column-statistics-on-all-eligible-columns"></a>A. Criar estatísticas de coluna única em todas as colunas qualificadas  
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
  
## <a name="see-also"></a>Consulte também  
 [Estatísticas](../../relational-databases/statistics/statistics.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [Mecanismo de banco de dados armazenados procedimentos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
