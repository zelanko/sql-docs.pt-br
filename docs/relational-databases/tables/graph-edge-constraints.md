---
title: Restrições de borda de grafo | Microsoft Docs
ms.custom: ''
ms.date: 04/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- edge constraints [SQL Server]
- CONNECTION constraints
- edge constraints [Azure SQL Database]
- graph edge constraints
- SQL Graph
ms.assetid: ''
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 86544dee5262a1d04c1ff1d8e59f8ddac5e9b5ce
ms.sourcegitcommit: d5cd4a5271df96804e9b1a27e440fb6fbfac1220
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64774650"
---
# <a name="edge-constraints"></a>Restrições do Microsoft Edge
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

  Restrições de borda podem ser usadas para impor a integridade dos dados e uma semântica específica às tabelas de borda no banco de dados de gráfico do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
  
Este artigo inclui as seções a seguir.  
  
[Restrições de borda](../../relational-databases/tables/graph-edge-constraints.md#Connection)  

[Restrições de borda](../../relational-databases/tables/graph-edge-constraints.md#Connection)  
  
[Tarefas relacionadas](../../relational-databases/tables/graph-edge-constraints.md#Tasks)  
  
##  <a name="Connection"></a> Restrições de borda
 Na primeira versão dos recursos de gráfico, as tabelas de borda não impunham nada aos pontos de extremidade da borda. Ou seja, uma borda em um banco de dados de gráfico podia conectar qualquer nó a qualquer outro nó, independentemente do tipo. 

 Esta versão introduz restrições de borda, que permitem aos usuários adicionar restrições a suas tabelas de borda, imponto assim uma semântica específica e mantendo a integridade dos dados. Quando uma nova borda é adicionada a uma tabela de borda com restrições de borda, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] impõe que os nós que a borda está tentando conectar existem nas tabelas de nó adequadas. Também é garantido que um nó não possa ser removido se ele ainda for referenciado por uma borda. 

 ### <a name="edge-constraint-clauses"></a>Cláusulas de restrição de borda
 Cada restrição de borda é composta por uma ou mais cláusulas de restrição de borda. Uma cláusula de restrição de borda é o par de nós DE e PARA que a borda em questão poderia conectar. 

 Considere que você tem os nós `Product` e `Customer` em seu gráfico e você usa a borda `Bought` para conectar a esses nós. A cláusula de restrição de borda especifica o par de nós DE e PARA e a direção da borda. Nesse caso, a cláusula de restrição de borda será `Customer` PARA `Product`. Ou seja, será permitido inserir um `Bought` que vai de um `Customer` para `Product`. Tentativas de inserir uma borda que vai de `Product` para `Customer` falham. 
  
- Uma cláusula de restrição de borda contém um par de tabelas de nós DE e PARA a que a restrição de borda é imposta. 
  
- Os usuários podem especificar várias cláusulas de restrição de borda por restrição de borda, que serão aplicadas como uma disjunção.

- Se várias restrições de borda forem criadas em uma única tabela de borda, as bordas deverão atender a TODAS as restrições para serem permitidas.
  
### <a name="indexes-on-edge-constraints"></a>Índices em restrições de borda
 Criar uma restrição de borda não cria automaticamente um índice correspondente nas colunas `$from_id` e `$to_id` da tabela de borda. Criar manualmente um índice em um par `$from_id`, `$to_id` é recomendado se você tem consultas de pesquisa de ponto ou carga de trabalho de OLTP. 

##  <a name="Tasks"></a> Tarefas relacionadas  
 A tabela a seguir lista as tarefas comuns associadas às restrições de borda.  
  
|Tarefa|Artigo|  
|----------|-----------|  
|Descreve como criar restrições de borda.|[Criar restrições de borda](../../relational-databases/tables/create-edge-constraints.md)|  
|Descreve como excluir uma restrição de borda.|[Excluir restrição de borda](../../relational-databases/tables/delete-edge-constraint.md)|  
|Descreve como modificar uma restrição de borda.|[Modificar restrição de borda](../../relational-databases/tables/modify-edge-constraint.md)|  
|Descreve como exibir propriedades de restrição de borda.|[Exibir propriedades de restrição de borda](../../relational-databases/tables/view-edge-constraint-properties.md)|  
