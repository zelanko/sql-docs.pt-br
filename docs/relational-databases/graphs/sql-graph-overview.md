---
title: "Gráfico de processamento com o SQL Server e banco de dados do SQL Azure | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: graphs
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- SQL graph
- SQL graph, overview
ms.assetid: 
caps.latest.revision: 
author: shkale-msft
ms.author: shkale;barbkess
manager: craigg
ms.workload: Active
ms.openlocfilehash: 77a50d48ee5c6d5baa8b05b327146e74b5eff815
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2018
---
# <a name="graph-processing-with-sql-server-and-azure-sql-database"></a>Gráfico de processamento com o SQL Server e banco de dados do SQL Azure
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece recursos de banco de dados do gráfico para o modelo de relações de muitos-para-muitos. As relações de gráfico estão integradas [!INCLUDE[tsql-md](../../includes/tsql-md.md)] e obtenha os benefícios de usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como o sistema de gerenciamento de banco de dados básico.


## <a name="what-is-a-graph-database"></a>O que é um banco de dados do gráfico?  
Um banco de dados do gráfico é uma coleção de nós (ou vértices) e bordas (ou relações). Um nó representa uma entidade (por exemplo, uma pessoa ou organização) e uma borda representa uma relação entre os dois nós que ele se conecta (por exemplo, gosta ou amigos). Nós e bordas podem ter propriedades associadas a eles. Aqui estão alguns recursos que tornam a um banco de dados do gráfico exclusivo:  
-   Bordas ou relações são entidades de primeira classe em um banco de dados do gráfico e podem ter atributos ou propriedades associadas com eles. 
-   Uma única borda com flexibilidade pode se conectar a vários nós em um banco de dados do gráfico.
-   Você pode expressar correspondência de padrões e consultas de navegação de vários saltos facilmente.
-   Você pode expressar consultas polimórficas e fechamento transitivo facilmente.

## <a name="when-to-use-a-graph-database"></a>Quando usar um banco de dados do gráfico

Não há nada que pode atingir um banco de dados do gráfico, que não pode ser alcançado usando um banco de dados relacional. No entanto, um banco de dados do gráfico pode tornar mais fácil expressar um determinado tipo de consultas. Além disso, com otimizações específicas, determinadas consultas podem executar melhor. Sua decisão para escolher um em detrimento do outro pode ser baseada nos seguintes fatores:  
-   Seu aplicativo tiver dados hierárquicos. O tipo de dados HierarchyID pode ser usado para implementar hierarquias, mas ele tem algumas limitações. Por exemplo, ele não permite vários pais para um nó de armazenamento.
-   Seu aplicativo tem relações complexas de muitos-para-muitos; como o aplicativo evoluir, novas relações são adicionadas.
-   Você precisa analisar os dados interconectados e relações.

## <a name="graph-features-introduced-in-includesssqlv14includessssqlv14-mdmd"></a>Recursos de gráfico introduzidos no [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] 
Estamos começando a adicionar extensões de gráfico para o SQL Server, para facilitar a armazenar e consultar dados do gráfico. Recursos a seguir são introduzidos na primeira versão. 


### <a name="create-graph-objects"></a>Criar objetos de gráfico
[!INCLUDE[tsql-md](../../includes/tsql-md.md)] extensões permitirá aos usuários criar tabelas de nó ou borda. Nós e bordas podem ter propriedades associadas a eles. Como nós e bordas são armazenadas como tabelas, todas as operações que têm suporte em tabelas relacionais são suportadas na tabela de borda ou nó. A seguir está um exemplo:  

```   
CREATE TABLE Person (ID INTEGER PRIMARY KEY, Name VARCHAR(100), Age INT) AS NODE;
CREATE TABLE friends (StartDate date) AS EDGE;
```   

![tabelas de amigos pessoa](../../relational-databases/graphs/media/person-friends-tables.png "tabelas de borda do nó de pessoa e amigos")  
Nós e bordas são armazenadas como tabelas  

### <a name="query-language-extensions"></a>Extensões de linguagem de consulta  
Nova `MATCH` cláusula é introduzida para dar suporte a correspondência de padrões e navegação de vários salto por meio de graph. O `MATCH` função usa a sintaxe de estilo de arte ASCII para correspondência de padrões. Por exemplo:  

```   
-- Find friends of John
SELECT Person2.Name 
FROM Person Person1, Friends, Person Person2
WHERE MATCH(Person1-(Friends)->Person2)
AND Person1.Name = 'John';
```   
 
### <a name="fully-integrated-in-includessnoversionincludesssnoversion-mdmd-engine"></a>Totalmente integrado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mecanismo 
Extensões de gráfico são completamente integradas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mecanismo. Usamos o mesmo mecanismo de armazenamento metadados, o processador de consultas, etc. para armazenar e consultar dados do gráfico. Isso permite que os usuários consultem em seu gráfico e dados relacionais em uma única consulta. Os usuários também podem se beneficiar da combinação de recursos de gráfico com outros [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tecnologias como columnstore, alta disponibilidade, serviços de R, etc. O banco de dados do SQL gráfico também oferece suporte a todos os segurança e conformidade recursos disponíveis com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
 
### <a name="tooling-and-ecosystem"></a>Ferramentas e o ecossistema  
Os usuários se beneficiar com as ferramentas existentes e o ecossistema que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece. Ferramentas como o backup e restauração, importação e exportação, funcionarem BCP fora da caixa. Outras ferramentas ou serviços como o SSIS, SSRS ou PowerBI funcionará com tabelas de gráfico, o forma como funcionam com tabelas relacionais.
 
 ## <a name="next-steps"></a>Próximas etapas  
Leitura de [banco de dados de gráfico SQL - arquitetura](./sql-graph-architecture.md)
   

