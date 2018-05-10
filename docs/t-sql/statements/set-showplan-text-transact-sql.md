---
title: SET SHOWPLAN_TEXT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SHOWPLAN_TEXT
- SET_SHOWPLAN_TEXT_TSQL
- SET SHOWPLAN_TEXT
- SHOWPLAN_TEXT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- statements [SQL Server], estimates
- execution information and estimates [SQL Server]
- statements [SQL Server], information without processing
- SET SHOWPLAN_TEXT statement
- canceling statement execution
- SHOWPLAN_TEXT option
- stopping statement execution
- estimated execution information [SQL Server]
ms.assetid: 2c4f3fc8-ff2c-4790-8b74-e7e8ef58f9a6
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 11bdddd82efcbc4f0e97b8b33d99961caa9dcfd5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="set-showplantext-transact-sql"></a>SET SHOWPLAN_TEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Faz com que o Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não execute as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)]. Em vez disso, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna informações detalhadas sobre como as instruções são executadas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET SHOWPLAN_TEXT { ON | OFF }  
```  
  
## <a name="remarks"></a>Remarks  
 A configuração de SHOWPLAN_TEXT é definida durante a execução ou tempo de execução, e não no momento da análise.  
  
 Quando SET STATISTICS TEXT estiver ON (acionado), o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna informações de execução para cada instrução [!INCLUDE[tsql](../../includes/tsql-md.md)], sem executá-las. Depois que essa opção estiver definida como ON, as informações do plano de execução sobre todas as instruções [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] subsequentes serão retornadas, até que a opção esteja definida como OFF. Por exemplo, se uma instrução CREATE TABLE for executada enquanto SET SHOWPLAN_TEXT estiver como ON, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna uma mensagem de erro de uma instrução SELECT subsequente envolvendo essa mesma tabela, informando ao usuário que a tabela especificada não existe. Portanto, haverá falha nas referências subsequentes para essa tabela. Quando SET SHOWPLAN_TEXT for OFF, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa instruções sem gerar um relatório com informações do plano de execução.  
  
 SET SHOWPLAN_TEXT tem como objetivo retornar uma saída legível para aplicativos de prompt de comando do Microsoft Win32, como o utilitário **osql**. SET SHOWPLAN_ALL retorna uma saída mais detalhada, que deve ser usada com programas projetados para manipulá-la.  
  
 SET SHOWPLAN_TEXT e SET SHOWPLAN_ALL não devem ser especificados em um procedimento armazenado. Elas devem ser as únicas instruções em um lote.  
  
 SET SHOWPLAN_TEXT retorna informações como um conjunto de linhas que formam uma árvore hierárquica que representa as etapas cumpridas pelo processador de consultas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], à medida que ele executa cada instrução. Cada instrução refletida na saída contém uma única linha com o texto da instrução, seguida de várias linhas com os detalhes das etapas de execução. A tabela exibe a coluna contida na saída.  
  
|Nome da coluna|Description|  
|-----------------|-----------------|  
|**StmtText**|Para linhas que não são do tipo PLAN_ROW, essa coluna conterá o texto da instrução [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para linhas do tipo PLAN_ROW, essa coluna contém uma descrição da operação. Essa coluna contém o operador físico e pode também conter, opcionalmente, o operador lógico. Essa coluna também pode ser seguida de uma descrição, determinada pelo operador físico. Para obter mais informações sobre operadores físicos, veja a coluna **Argument** em [SET SHOWPLAN_ALL &#40;Transact-SQL&#41;](../../t-sql/statements/set-showplan-all-transact-sql.md).|  
  
 Para obter mais informações sobre os operadores lógicos e físicos que podem ser vistos na saída do plano de execução, veja [Referência de operadores lógicos e físicos do de plano de execução](../../relational-databases/showplan-logical-and-physical-operators-reference.md)  
  
## <a name="permissions"></a>Permissões  
 Para usar SET SHOWPLAN_TEXT, é preciso ter as permissões necessárias para executar as instruções nas quais SET SHOWPLAN_TEXT será executado e, ainda, é preciso ter permissão SHOWPLAN para todos os bancos de dados que contenham objetos referenciados.  
  
 Para instruções SELECT, INSERT, UPDATE, DELETE, EXEC *stored_procedure* e EXEC *user_defined_function*, para produzir um Plano de Execução, o usuário precisa:  
  
-   Ter as permissões apropriadas para executar as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Ter permissão SHOWPLAN em todos os bancos de dados que contenham objetos referenciados pelas instruções Transact-SQL, como tabelas, exibições e assim por diante.  
  
 Para todas as outras instruções, como DDL, USE *database_name*, SET, DECLARE, SQL dinâmico, e assim por diante, são necessárias apenas as permissões adequadas para executar as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="examples"></a>Exemplos  
 Este exemplo mostra como índices são usados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], na medida em que ele processa as instruções.  
  
 Esta é a consulta que usa um índice:  
  
```  
USE AdventureWorks2012;  
GO  
SET SHOWPLAN_TEXT ON;  
GO  
SELECT *  
FROM Production.Product   
WHERE ProductID = 905;  
GO  
SET SHOWPLAN_TEXT OFF;  
GO  
```  
  
 Este é o conjunto de resultados:  
  
```  
StmtText                                             
---------------------------------------------------  
SELECT *  
FROM Production.Product   
WHERE ProductID = 905;   
  
StmtText                                                                                                                                                                                        
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
|--Clustered Index Seek(OBJECT:([AdventureWorks2012].[Production].[Product].[PK_Product_ProductID]), SEEK:([AdventureWorks2012].[Production].[Product].[ProductID]=CONVERT_IMPLICIT(int,[@1],0)) ORDERED FORWARD)   
```  
  
 Aqui está a consulta que não usa um índice:  
  
```  
USE AdventureWorks2012;  
GO  
SET SHOWPLAN_TEXT ON;  
GO  
SELECT *  
FROM Production.ProductCostHistory  
WHERE StandardCost < 500.00;  
GO  
SET SHOWPLAN_TEXT OFF;  
GO  
```  
  
 Este é o conjunto de resultados:  
  
```  
StmtText                                                                  
------------------------------------------------------------------------  
SELECT *  
FROM Production.ProductCostHistory  
WHERE StandardCost < 500.00;   
  
StmtText                                                                                                                                                                                                  
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
|--Clustered Index Scan(OBJECT:([AdventureWorks2012].[Production].[ProductCostHistory].[PK_ProductCostHistory_ProductCostID]), WHERE:([AdventureWorks2012].[Production].[ProductCostHistory].[StandardCost]<[@1]))  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET SHOWPLAN_ALL &#40;Transact-SQL&#41;](../../t-sql/statements/set-showplan-all-transact-sql.md)  
  
  
