---
title: Processamento de grafo com o SQL Server e banco de dados SQL do Azure | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: language-reference
helpviewer_keywords:
- SQL graph
- SQL graph, overview
ms.assetid: ''
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: dcabc19d3c83cd1ed4c9ee7b8047759e2550863e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62502472"
---
# <a name="graph-processing-with-sql-server-and-azure-sql-database"></a>Processamento de grafo com o SQL Server e banco de dados SQL
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece recursos de banco de dados do gráfo para o modelo de relações de muitos-para-muitos. As relações de gráfico estão integradas [!INCLUDE[tsql-md](../../includes/tsql-md.md)] e receber os benefícios de usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como o sistema de gerenciamento de banco de dados fundamentais.


## <a name="what-is-a-graph-database"></a>O que é um banco de dados do gráfico?  
Um banco de dados do grafo é uma coleção de nós (ou vértices) e bordas (ou relações). Um nó representa uma entidade (por exemplo, uma pessoa ou organização) e uma borda representa uma relação entre os dois nós que ela conecta (por exemplo, curtidas ou amigos). Nós e bordas podem ter propriedades associadas a eles. Aqui estão alguns recursos que tornam a um banco de dados do gráfico exclusivo:  
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
Extensões de grafo são totalmente integradas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mecanismo. Para armazenar e consultar dados do gráfico, use o mesmo mecanismo de armazenamento, metadados, o processador de consulta etc. Consulta em grafo e dados relacionais em uma única consulta. Combinar os recursos de gráfico com outros [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] as tecnologias, como o columnstore, alta disponibilidade, o R services, etc. O banco de dados do Sistema tempdb será criptografado se qualquer outro banco da instância do SQL Server for encriptado com o uso de TDE[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
 
### <a name="tooling-and-ecosystem"></a>Ferramentas e ecossistema

Se beneficiar de ferramentas existentes e ecossistema que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece. Ferramentas como o backup e restauração, importação e exportação, simplesmente funcionem BCP fora da caixa. Outras ferramentas ou serviços, como o SSIS, SSRS ou do Power BI funcionará com tabelas de grafo, exatamente como eles funcionam com tabelas relacionais.

## <a name="edge-constraints"></a>Restrições de borda
Uma restrição de borda é definida em uma tabela de borda do gráfico e é um par de tabelas de nó que pode se conectar a um tipo de borda especificado. Isso fornece aos usuários um melhor controle sobre seu esquema de grafo. Com a Ajuda de restrições de borda que os usuários podem restringir o tipo de nós de que uma determinada borda é permitida para se conectar. 

Para saber mais sobre como criar e usar restrições de borda, consulte [restrições de borda](../../relational-databases/tables/graph-edge-constraints.md)

## <a name="merge-dml"></a>Mesclar DML 
O [mesclar](../../t-sql/statements/merge-transact-sql.md) executa a instrução insert, atualizar ou excluir operações em uma tabela de destino com base nos resultados de uma junção com uma tabela de origem. Por exemplo, você pode sincronizar duas tabelas inserindo, atualizando ou excluindo linhas em uma tabela de destino com base nas diferenças entre a tabela de destino e a tabela de origem. Agora há suporte para o uso de predicados de correspondência em uma instrução de mesclagem no banco de dados SQL e SQL Server vNext. Ou seja, agora é possível mesclar seus dados de gráfico atual (tabelas de borda ou nó) com novos dados usando os predicados de correspondência para especificar relações de gráfico em uma única instrução, em vez de instruções de INSERT/UPDATE/DELETE separadas.

Para saber mais sobre como a correspondência pode ser usada em mesclagem DML consulte [instrução MERGE](../../t-sql/statements/merge-transact-sql.md)

 ## <a name="next-steps"></a>Próximas etapas  
Leia o [banco de dados de grafos SQL - arquitetura](./sql-graph-architecture.md)
   

