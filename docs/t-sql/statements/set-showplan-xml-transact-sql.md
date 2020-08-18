---
description: SET SHOWPLAN_XML (Transact-SQL)
title: SET SHOWPLAN_XML (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET SHOWPLAN_XML
- SET_SHOWPLAN_XML_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- statements [SQL Server], estimates
- SET SHOWPLAN_XML statement
- execution information and estimates [SQL Server]
- statements [SQL Server], information without processing
- XML [SQL Server], statement execution information
- SHOWPLAN_XML option
- estimated execution information [SQL Server]
ms.assetid: a467a1b3-10a5-43c4-9085-13d8aed549c9
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c9ba02ca79db2e79f14483e632eaa6fa77c3d4a0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88304637"
---
# <a name="set-showplan_xml-transact-sql"></a>SET SHOWPLAN_XML (Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

Faz com que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não execute instruções [!INCLUDE[tsql](../../includes/tsql-md.md)]. Em vez disso, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna informações detalhadas sobre como as instruções serão executadas no formulário de um documento XML bem-definido.

![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>Sintaxe

```syntaxsql
SET SHOWPLAN_XML { ON | OFF }
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="remarks"></a>Comentários

A configuração de SHOWPLAN_XML é definida durante a execução ou o tempo de execução, e não no momento da análise.

Quando SET SHOWPLAN_XML for ON, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará informações de plano de execução para cada instrução sem executá-la, e as instruções do [!INCLUDE[tsql](../../includes/tsql-md.md)] não serão executadas. Depois que essa opção estiver definida como ON, as informações do plano de execução sobre todas as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] subsequentes serão retornadas, até que a opção esteja definida como OFF. Por exemplo, se uma instrução CREATE TABLE for executada enquanto SET SHOWPLAN_XML estiver definido como ON, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará uma mensagem de erro de uma instrução SELECT subsequente, envolvendo essa mesma tabela. A tabela especificada não existe. Portanto, haverá falha nas referências subsequentes para essa tabela. Quando SET SHOWPLAN_XML for OFF, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executará as instruções sem gerar relatório.

SET SHOWPLAN_XML deve retornar uma saída como **nvarchar(max)** para aplicativos como o utilitário **sqlcmd**, em que a saída XML será usada em seguida por outras ferramentas para exibir e processar as informações do plano de consulta.

> [!NOTE]
> A exibição de gerenciamento dinâmico **sys.dm_exec_query_plan** retorna as mesmas informações que SET SHOWPLAN XML para o tipo de dados **XML**. Essas informações são retornadas da coluna **query_plan** de **sys.dm_exec_query_plan**. Para obter mais informações, confira [sys.dm_exec_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md).

SET SHOWPLAN_XML não pode ser especificado em um procedimento armazenado. Ele precisa ser a única instrução em um lote.

SET SHOWPLAN_XML retorna informações como um conjunto de documentos XML. Cada lote posterior à instrução SET SHOWPLAN_XML ON é refletido na saída por um único documento. Cada documento contém o texto das instruções do lote, seguido dos detalhes das etapas de execução. O documento mostra os custos estimados, os números de linhas, os índices acessados e os tipos de operadores executados, a ordem de junção e mais informações sobre os planos de execução.

> [!NOTE]
> Se **Incluir Plano de Execução Real** estiver selecionado no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], essa opção SET não produzirá a saída do plano de execução XML. Desmarque o botão **Incluir Plano de Execução Real** antes de usar esta opção SET.

### <a name="location-of-showplan-output"></a>Local de saída de SHOWPLAN

O documento que contém o esquema XML para a saída XML gerada por SET SHOWPLAN_XML é copiado durante a instalação em um diretório local no computador no qual o Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está instalado. O documento pode ser encontrado na unidade que contém os arquivos de instalação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], em um caminho semelhante ao seguinte:

- `\Microsoft SQL Server\130\Tools\Binn\schemas\sqlserver\2004\07\showplan\showplanxml.xsd`

No caminho anterior, o nó `130\` é usado pelo SQL Server 2016. O número de 130 deriva do primeiro nó do valor retornado por `SELECT @@VERSION`, que é 13. Para o SQL Server 2017, o caminho usaria `140\`, porque o primeiro nó do seu valor @@VERSION é 14. Para SQL Server 2019, o primeiro o valor de @@VERSION é 15.

O esquema do plano de execução também pode ser encontrado [neste site](https://go.microsoft.com/fwlink/?linkid=43100&clcid=0x409).

## <a name="permissions"></a>Permissões

Para usar SET SHOWPLAN_XML, é preciso ter permissões suficientes para executar as instruções nas quais SET SHOWPLAN_XML é executado e é preciso ter a permissão SHOWPLAN para todos os bancos de dados que contenham objetos referenciados.

Para instruções SELECT, INSERT, UPDATE, DELETE, EXEC *stored_procedure* e EXEC *user_defined_function*, para produzir um Plano de Execução, o usuário precisa:

- Ter as permissões apropriadas para executar as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)].

- Ter permissão SHOWPLAN em todos os bancos de dados que contenham objetos referenciados pelas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)], como tabelas, exibições e assim por diante.

Para todas as outras instruções, como DDL, USE *database_name*, SET, DECLARE, SQL dinâmico, e assim por diante, são necessárias apenas as permissões adequadas para executar as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)].

## <a name="examples"></a>Exemplos

As duas instruções a seguir usam as configurações SET SHOWPLAN_XML para mostrar o modo pelo qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] analisa e otimiza o uso de índices em consultas.

A primeira consulta usa o operador de comparação Igual (=) na cláusula WHERE em uma coluna indexada. A segunda consulta usa o operador LIKE na cláusula WHERE. Isso força o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a usar uma verificação de índice clusterizado e a localizar os dados que satisfazem a condição da cláusula WHERE. Os valores nos atributos **EstimateRows** e **EstimatedTotalSubtreeCost** são menores na primeira consulta indexada, indicando que ela é processada com mais rapidez e usa menos recursos que a consulta não indexada.

```sql
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

## <a name="see-also"></a>Consulte Também

[Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)
