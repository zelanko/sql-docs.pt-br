---
title: SET SHOWPLAN_XML (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET SHOWPLAN_XML
- SET_SHOWPLAN_XML_TSQL
dev_langs: TSQL
helpviewer_keywords:
- statements [SQL Server], estimates
- SET SHOWPLAN_XML statement
- execution information and estimates [SQL Server]
- statements [SQL Server], information without processing
- XML [SQL Server], statement execution information
- SHOWPLAN_XML option
- estimated execution information [SQL Server]
ms.assetid: a467a1b3-10a5-43c4-9085-13d8aed549c9
caps.latest.revision: "48"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 2b51e19f70b0ff2119cfe3f89404fe61accf4656
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="set-showplanxml-transact-sql"></a>SET SHOWPLAN_XML (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Faz com que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não execute instruções [!INCLUDE[tsql](../../includes/tsql-md.md)]. Em vez disso, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna informações detalhadas sobre como as instruções serão executadas no formulário de um documento XML bem-definido.  
 
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET SHOWPLAN_XML { ON | OFF }  
```  
  
## <a name="remarks"></a>Comentários  
 A configuração de SHOWPLAN_XML é definida durante a execução ou o tempo de execução, e não no momento da análise.  
  
 Quando SET SHOWPLAN_XML for ON, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna informações de plano de execução para cada instrução sem executá-la, e [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções não são executadas. Depois que essa opção estiver definida como ON, as informações do plano de execução sobre todas as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] subsequentes serão retornadas, até que a opção esteja definida como OFF. Por exemplo, se uma instrução CREATE TABLE for executada enquanto SET SHOWPLAN_XML estiver definido como ON, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará uma mensagem de erro de uma instrução SELECT subsequente, envolvendo essa mesma tabela. A tabela especificada não existe. Portanto, haverá falha nas referências subsequentes para essa tabela. Quando SET SHOWPLAN_XML for OFF, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executará as instruções sem gerar relatório.  
  
 SET SHOWPLAN_XML deve retornar a saída como **nvarchar (max)** para aplicativos, como o **sqlcmd** utilitário, onde a saída XML é subsequentemente usada por outras ferramentas para exibir e processar a consulta informações do plano.  
  
> [!NOTE]  
>  A exibição de gerenciamento dinâmico **sys.DM exec_query_plan**, retorna as mesmas informações que SET SHOWPLAN XML o **xml** tipo de dados. Essas informações são retornadas do **query_plan** coluna **sys.DM exec_query_plan**. Para obter mais informações, consulte [sys.DM exec_query_plan &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md).  
  
 SET SHOWPLAN_XML não pode ser especificado em um procedimento armazenado. Ele precisa ser a única instrução em um lote.  
  
 SET SHOWPLAN_XML retorna informações como um conjunto de documentos XML. Cada lote posterior à instrução SET SHOWPLAN_XML ON é refletido na saída por um único documento. Cada documento contém o texto das instruções do lote, seguido dos detalhes das etapas de execução. O documento mostra os custos estimados, os números de linhas, os índices acessados e os tipos de operadores executados, a ordem de junção e mais informações sobre os planos de execução.  
  
 O documento que contém o esquema XML para a saída XML gerada por SET SHOWPLAN_XML é copiado durante a instalação em um diretório local no computador no qual o Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está instalado. Ele pode ser encontrado na unidade que contém os arquivos de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], em:  
  
 \Microsoft SQL Server\130\Tools\Binn\schemas\sqlserver\2004\07\showplan\showplanxml.xsd  
  
 O esquema do plano de execução também podem ser encontrado em [este site](http://go.microsoft.com/fwlink/?linkid=43100&clcid=0x409).  
  
> [!NOTE]  
>  Se **incluir plano de execução real** está selecionado no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], essa opção SET produz saída de Showplan XML. Limpar o **incluir plano de execução real** botão antes de usar essa opção SET.  
  
## <a name="permissions"></a>Permissões  
 Para usar SET SHOWPLAN_XML, é preciso ter permissões suficientes para executar as instruções nas quais SET SHOWPLAN_XML é executado e é preciso ter a permissão SHOWPLAN para todos os bancos de dados que contenham objetos referenciados.  
  
 Para SELECT, INSERT, UPDATE, DELETE, EXEC *stored_procedure*e EXEC *user_defined_function* instruções para produzir um plano de execução que o usuário deve:  
  
-   Ter as permissões apropriadas para executar as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Ter permissão SHOWPLAN em todos os bancos de dados que contenham objetos referenciados pelas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)], como tabelas, exibições e assim por diante.  
  
 Para todas as outras instruções, como DDL, USE *database_name*, SET, DECLARE, dinâmico SQL e assim por diante, somente as permissões apropriadas para executar o [!INCLUDE[tsql](../../includes/tsql-md.md)] declarações são necessárias.  
  
## <a name="examples"></a>Exemplos  
 As duas instruções a seguir usam as configurações SET SHOWPLAN_XML para mostrar o modo pelo qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] analisa e otimiza o uso de índices em consultas.  
  
 A primeira consulta usa o operador de comparação Igual (=) na cláusula WHERE em uma coluna indexada. A segunda consulta usa o operador LIKE na cláusula WHERE. Isso força o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a usar uma verificação de índice clusterizado e a localizar os dados que satisfazem a condição da cláusula WHERE. Os valores de **EstimateRows** e o **EstimatedTotalSubtreeCost** atributos são menores para a primeira consulta indexada, indicando que ela é processada muito mais rapidamente e usa menos recursos do que o consulta não indexada.  
  
```  
USE AdventureWorks2012;  
GO  
SET SHOWPLAN_XML ON;  
GO  
-- First query.  
SELECT BusinessEntityID   
FROM HumanResources.Employee  
WHERE NationalIDNumber = '509647174';  
GO  
-- Second query.  
SELECT BusinessEntityID, JobTitle  
FROM HumanResources.Employee  
WHERE JobTitle LIKE 'Production%';  
GO  
SET SHOWPLAN_XML OFF;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
