---
title: Processamento de grafo com o SQL Server e banco de dados SQL do Azure | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: graphs
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- SQL graph
- SQL graph, overview
ms.assetid: ''
caps.latest.revision: 1
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: 8c2ad7f5b31a97de5d0bfb22074b55bd61bb825b
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38015672"
---
# <a name="graph-processing-with-sql-server-and-azure-sql-database"></a>Processamento de grafo com o SQL Server e banco de dados SQL
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece recursos de banco de dados do gráfo para o modelo de relações de muitos-para-muitos. As relações de gráfico estão integradas [!INCLUDE[tsql-md](../../includes/tsql-md.md)] e receber os benefícios de usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como o sistema de gerenciamento de banco de dados fundamentais.


## <a name="what-is-a-graph-database"></a>O que é um banco de dados do gráfico?  
Um banco de dados do gráfico é uma coleção de nós (ou vértices) e bordas (ou relações). Um nó representa uma entidade (por exemplo, uma pessoa ou organização) e uma borda representa uma relação entre os dois nós que ele se conecta (por exemplo, curtidas ou amigos). Nós e bordas podem ter propriedades associadas a eles. Aqui estão alguns recursos que tornam a um banco de dados do gráfico exclusivo:  
-   Bordas ou as relações são entidades de primeira classe em um banco de dados do gráfico e podem ter atributos ou propriedades associadas com eles. 
-   Uma única borda com flexibilidade pode se conectar a vários nós em um banco de dados do gráfico.
-   Você pode expressar consultas de navegação com saltos múltiplos e correspondência de padrões com facilidade.
-   Você pode expressar consultas polimórficas e fechamento transitivo facilmente.

## <a name="when-to-use-a-graph-database"></a>Quando usar um banco de dados do gráfico

Não há nada que pode obter um banco de dados do gráfico, que não pode ser obtida usando um banco de dados relacional. No entanto, um banco de dados do gráfico pode tornar mais fácil expressar um determinado tipo de consultas. Além disso, com otimizações específicas, determinadas consultas podem funcionar melhor. Sua decisão para escolher um em detrimento do outro pode ser baseada nos seguintes fatores:  
-   Seu aplicativo tem dados hierárquicos. O tipo de dados HierarchyID pode ser usado para implementar hierarquias, mas ele tem algumas limitações. Por exemplo, ele não permitem que você armazene vários pais para um nó.
-   Seu aplicativo tem relações complexas de muitos-para-muitos; como o aplicativo evolui, novas relações são adicionadas.
-   Você precisa analisar os relacionamentos e interconectadas.

## <a name="graph-features-introduced-in-includesssqlv14includessssqlv14-mdmd"></a>Recursos de gráfico introduzidos no [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] 
Estamos começando a adicionar extensões de grafo para o SQL Server, para facilitar a armazenar e consultar dados do gráfico. Recursos a seguir são apresentados na primeira versão. 


### <a name="create-graph-objects"></a>Criar objetos de grafo
[!INCLUDE[tsql-md](../../includes/tsql-md.md)] extensões permitirá que os usuários criar tabelas de nó ou borda. Nós e bordas podem ter propriedades associadas a eles. Como nós e bordas são armazenadas como tabelas, todas as operações que têm suporte em tabelas relacionais têm suporte na tabela de nó ou borda. A seguir está um exemplo:  

```   
CREATE TABLE Person (ID INTEGER PRIMARY KEY, Name VARCHAR(100), Age INT) AS NODE;
CREATE TABLE friends (StartDate date) AS EDGE;
```   

![tabelas de pessoa-amigos](../../relational-databases/graphs/media/person-friends-tables.png "tabelas de borda de nó Person e seus amigos")  
Nós e bordas são armazenadas como tabelas  

### <a name="query-language-extensions"></a>Extensões de linguagem de consulta  
Nova `MATCH` cláusula é introduzida para dar suporte à correspondência de padrões e navegação com saltos múltiplos por meio do graph. O `MATCH` função usa a sintaxe de estilo de arte ASCII para correspondência de padrões. Por exemplo:  

```   
-- Find friends of John
SELECT Person2.Name 
FROM Person Person1, Friends, Person Person2
WHERE MATCH(Person1-(Friends)->Person2)
AND Person1.Name = 'John';
```   
 
### <a name="fully-integrated-in-includessnoversionincludesssnoversion-mdmd-engine"></a>Totalmente integrado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mecanismo 
Extensões de grafo são totalmente integradas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mecanismo. Usamos o mesmo mecanismo de armazenamento, metadados, o processador de consultas etc para armazenar e consultar dados do gráfico. Isso permite aos usuários consultar todos os seus grafo e dados relacionais em uma única consulta. Os usuários também podem se beneficiar da combinação de recursos de gráfico com outros [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] as tecnologias, como o columnstore, alta disponibilidade, o R services, etc. O banco de dados do Sistema tempdb será criptografado se qualquer outro banco da instância do SQL Server for encriptado com o uso de TDE[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
 
### <a name="tooling-and-ecosystem"></a>Ferramentas e ecossistema  
Os usuários se beneficiam de ferramentas existentes e ecossistema que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece. Ferramentas como o backup e restauração, importação e exportação, simplesmente funcionem BCP fora da caixa. Outras ferramentas ou serviços, como o SSIS, SSRS ou Power BI funcionará com tabelas de grafo, exatamente como eles funcionam com tabelas relacionais.
 
 ## <a name="next-steps"></a>Próximas etapas  
Leia o [banco de dados de grafos SQL - arquitetura](./sql-graph-architecture.md)
   

