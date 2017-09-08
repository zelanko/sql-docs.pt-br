---
title: SET SHOWPLAN_ALL (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET SHOWPLAN_ALL
- SET_SHOWPLAN_ALL_TSQL
- SHOWPLAN_ALL
- SHOWPLAN_ALL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- statements [SQL Server], estimates
- execution information and estimates [SQL Server]
- statements [SQL Server], information without processing
- SET SHOWPLAN_ALL statement
- SHOWPLAN_ALL option
- canceling statement execution
- stopping statement execution
- estimated execution information [SQL Server]
ms.assetid: a500b682-bae4-470f-9e00-47de905b851b
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: beb2d1647869da3ebb3f7463c896d8f6f986c387
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="set-showplanall-transact-sql"></a>SET SHOWPLAN_ALL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Faz com que o Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não execute as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)]. Em vez disso, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna informações detalhada sobre como as instruções são executadas e fornece estimativas dos requisitos de recurso para as instruções.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET SHOWPLAN_ALL { ON | OFF }  
```  
  
## <a name="remarks"></a>Comentários  
 A configuração de SHOWPLAN_ALL é definida durante a execução ou tempo de execução, e não no momento da análise.  
  
 Quando SET SHOWPLAN_ALL for ON, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará informações de execução para cada instrução, sem executá-las, e as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] não serão executadas. Depois que essa opção estiver definida como ON, as informações sobre todas as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] subsequentes serão retornadas até que a opção seja definida como OFF. Por exemplo, se uma instrução CREATE TABLE for executada que enquanto SET SHOWPLAN_ALL estiver definido como ON, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará uma mensagem de erro de uma instrução SELECT subsequente, envolvendo essa mesma tabela, informando os usuários de que a tabela especificada não existe. Portanto, haverá falha nas referências subsequentes para essa tabela. Quando SET SHOWPLAN_ALL for OFF, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executará as instruções sem gerar um relatório.  
  
 SET SHOWPLAN_ALL deve ser usado pelos aplicativos gravados para controlar sua saída. Use SET SHOWPLAN_TEXT para retornar uma saída legível para aplicativos de prompt de comando do Microsoft Win32, como o **osql** utilitário.  
  
 SET SHOWPLAN_TEXT e SET SHOWPLAN_ALL não podem ser especificados em um procedimento armazenado; eles devem ser as únicas instruções em um lote.  
  
 SET SHOWPLAN_ALL retorna informações como um conjunto de linhas que formam uma árvore hierárquica que representa as etapas cumpridas pelo processador de consultas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] à medida que ele executa cada instrução. Cada instrução refletida na saída contém uma única linha com o texto da instrução, seguida de várias linhas com os detalhes das etapas de execução. A tabela mostra as colunas que a saída contém.  
  
|Nome da coluna|Description|  
|-----------------|-----------------|  
|**StmtText**|Para linhas que não são do tipo PLAN_ROW, essa coluna contém o texto da instrução [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para linhas do tipo PLAN_ROW, essa coluna contém uma descrição da operação. Essa coluna contém o operador físico e pode também conter, opcionalmente, o operador lógico. Essa coluna também pode ser seguida de uma descrição determinada pelo operador físico. Para obter mais informações, consulte [lógicos de plano de execução e referência de operadores físicos](../../relational-databases/showplan-logical-and-physical-operators-reference.md).|  
|**StmtId**|Número da instrução no lote atual.|  
|**NodeId**|ID do nó da consulta atual.|  
|**Pai**|ID do nó da etapa pai.|  
|**PhysicalOp**|Algoritmo de implementação física para o nó. Somente para linhas do tipo PLAN_ROWS.|  
|**LogicalOp**|Operador algébrico relacional que esse nó representa. Somente para linhas do tipo PLAN_ROWS.|  
|**Argumento**|Fornece informações complementares sobre a operação em execução. O conteúdo dessa coluna depende do operador físico.|  
|**DefinedValues**|Contém uma lista de itens separados por vírgula, com os valores introduzidos por esse operador. Esses valores podem ser expressões computadas que presentes na consulta atual (por exemplo, na lista SELECT ou na cláusula WHERE), ou valores internos introduzidos pelo processador de consultas para processar essa consulta. Esses valores definidos podem ser referenciados em outro lugar nessa consulta. Somente para linhas do tipo PLAN_ROWS.|  
|**EstimateRows**|Número estimado de linhas de saída produzida por esse operador. Somente para linhas do tipo PLAN_ROWS.|  
|**EstimateIO**|Custo* estimado de E/S para esse operador. Somente para linhas do tipo PLAN_ROWS.|  
|**EstimateCPU**|Custo* estimado de CPU para esse operador. Somente para linhas do tipo PLAN_ROWS.|  
|**AvgRowSize**|Tamanho médio estimado (em bytes) da linha da linha que está sendo passada por esse operador.|  
|**TotalSubtreeCost**|Custo* estimado (cumulativo) dessa operação e de todas as operações filho.|  
|**OutputList**|Contém uma lista separada por vírgulas de colunas que estão sendo projetadas pela operação atual.|  
|**Warnings**|Contém uma lista separada por vírgulas de mensagens de aviso relativas à operação atual. As mensagens de aviso podem incluir a cadeia de caracteres "NO STATS:()" com uma lista de colunas. Essa mensagem de aviso significa que o otimizador de consulta tentou tomar uma decisão com base nas estatísticas dessa coluna, mas não havia nenhuma disponível. Por conseguinte, o otimizador de consulta precisou fazer uma suposição, que pode ter resultado na seleção de um plano de consulta ineficaz. Para obter mais informações sobre como criar ou atualizar as estatísticas de coluna (que ajudam o otimizador de consulta escolha um plano de consulta mais eficiente), consulte [UPDATE STATISTICS](../../t-sql/statements/update-statistics-transact-sql.md). Essa coluna pode incluir, opcionalmente, a cadeia de caracteres "MISSING JOIN PREDICATE", que significa que uma junção (envolvendo tabelas) está ocorrendo sem um predicado de junção. Descartar acidentalmente um predicado de junção pode resultar em uma consulta que leva mais tempo de execução que o esperado, e que retorna um grande conjunto de resultados. Se esse aviso estiver presente, verifique se a ausência do predicado de junção é intencional.|  
|**Tipo**|Tipo de nó. Para o nó pai de cada consulta, esse é o tipo de instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] (por exemplo, SELECT, INSERT, EXECUTE entre outras). Para os subnós que representam planos de execução, o tipo é PLAN_ROW.|  
|**Parallel**|**0** = operador não está em execução em paralelo.<br /><br /> **1** = operador está sendo executado em paralelo.|  
|**EstimateExecutions**|Número estimado de vezes que esse operador será executado durante a execução da consulta atual.|  
  
 *Unidades de custo se baseiam em uma medida interna de tempo, e não no tempo do relógio. Elas são usadas para determinar o custo relativo de um plano em comparação com outros planos.  
  
## <a name="permissions"></a>Permissões  
 Para usar SET SHOWPLAN_ALL, é necessário ter permissões suficientes para executar as instruções nas quais SET SHOWPLAN_ALL é executado, e ter a permissão SHOWPLAN para todos os bancos de dados que contenham objetos referenciados.  
  
 Para SELECT, INSERT, UPDATE, DELETE, EXEC *stored_procedure*e EXEC *user_defined_function* instruções para produzir um plano de execução que o usuário deve:  
  
-   Ter as permissões apropriadas para executar as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Ter permissão SHOWPLAN em todos os bancos de dados que contenham objetos referenciados pelas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)], como tabelas, exibições e assim por diante.  
  
 Para todas as outras instruções, como DDL, USE *database_name*, SET, DECLARE, dinâmico SQL e assim por diante, somente as permissões apropriadas para executar o [!INCLUDE[tsql](../../includes/tsql-md.md)] declarações são necessárias.  
  
## <a name="examples"></a>Exemplos  
 As duas instruções a seguir usam as configurações SET SHOWPLAN_ALL para mostrar o modo pelo qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] analisa e otimiza o uso de índices em consultas.  
  
 A primeira consulta usa o operador de comparação Igual (=) na cláusula WHERE em uma coluna indexada. Isso resulta no valor Clustered Index Seek no **LogicalOp** coluna e o nome do índice a **argumento** coluna.  
  
 A segunda consulta usa o operador LIKE na cláusula WHERE. Isto força o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a usar uma verificação de índice clusterizado e a localizar os dados que atendem à condição da cláusula WHERE. Isso resulta no valor de verificação de índice clusterizado no **LogicalOp** coluna com o nome do índice a **argumento** coluna e o valor do filtro no **LogicalOp** coluna com a condição da cláusula WHERE no **argumento** coluna.  
  
 Os valores de **EstimateRows** e **TotalSubtreeCost** colunas são menores para a primeira consulta indexada, indicando que ela é processada muito mais rapidamente e usa menos recursos do que a consulta não indexada .  
  
```  
USE AdventureWorks2012;  
GO  
SET SHOWPLAN_ALL ON;  
GO  
-- First query.  
SELECT BusinessEntityID   
FROM HumanResources.Employee  
WHERE NationalIDNumber = '509647174';  
GO  
-- Second query.  
SELECT BusinessEntityID, EmergencyContactID   
FROM HumanResources.Employee  
WHERE EmergencyContactID LIKE '1%';  
GO  
SET SHOWPLAN_ALL OFF;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET SHOWPLAN_TEXT &#40; Transact-SQL &#41;](../../t-sql/statements/set-showplan-text-transact-sql.md)   
 [SET SHOWPLAN_XML &#40; Transact-SQL &#41;](../../t-sql/statements/set-showplan-xml-transact-sql.md)  
  
  

