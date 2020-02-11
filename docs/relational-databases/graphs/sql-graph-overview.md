---
title: Processamento de grafo
titleSuffix: SQL Server and Azure SQL Database
ms.date: 06/26/2019
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
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3ca26af4738de25937b71e0c97c6272414a0957a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74096083"
---
# <a name="graph-processing-with-sql-server-and-azure-sql-database"></a>Processamento do Graph com o SQL Server e o Banco de Dados SQL do Azure
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]oferece recursos de banco de dados de grafo para modelar relações muitos para muitos. As relações de grafo são integradas [!INCLUDE[tsql-md](../../includes/tsql-md.md)] e recebem os benefícios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usar como o sistema de gerenciamento de banco de dados básico.


## <a name="what-is-a-graph-database"></a>O que é um banco de dados de grafo?  
Um banco de dados do grafo é uma coleção de nós (ou vértices) e bordas (ou relações). Um nó representa uma entidade (por exemplo, uma pessoa ou uma organização) e uma borda representa uma relação entre os dois nós que ela conecta (por exemplo, curtidas ou amigos). Os nós e as bordas podem ter propriedades associadas a eles. Aqui estão alguns recursos que tornam um banco de dados de grafo único:  
-   Bordas ou relações são entidades de primeira classe em um Banco de Dados de Grafo e podem ter atributos ou propriedades associadas a elas. 
-   Uma única borda pode conectar com flexibilidade vários nós em um banco de dados de grafo.
-   É possível expressar facilmente consultas de correspondência de padrões e navegação de salto múltiplo.
-   É possível expressar fechamento transitivo e consultas polimórficas com facilidade.

## <a name="when-to-use-a-graph-database"></a>Quando usar um banco de dados de grafo

Não há nada que um banco de dados de grafo possa obter, que não possa ser obtido usando um banco de dados relacional. No entanto, um banco de dados de grafo pode facilitar a expressa de determinado tipo de consulta. Além disso, com otimizações específicas, algumas consultas podem ter um desempenho melhor. A decisão para a escolha de um ou de outro pode ser baseada nos seguintes fatores:  
-   Seu aplicativo tem dados hierárquicos. O tipo de dados hierarchyid pode ser usado para implementar hierarquias, mas tem algumas limitações. Por exemplo, ele não permite que você armazene vários pais para um nó.
-   Seu aplicativo tem relacionamentos muitos-para-muitos complexos; à medida que o aplicativo evolui, novas relações são adicionadas.
-   É necessário analisar as relações e os dados interconectados.

## <a name="graph-features-introduced-in-includesssqlv14includessssqlv14-mdmd"></a>Recursos de grafo introduzidos no[!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] 
Estamos começando a adicionar extensões de grafo ao SQL Server, para facilitar o armazenamento e a consulta de dados de grafo. Os recursos a seguir são introduzidos na primeira versão. 


### <a name="create-graph-objects"></a>Criar objetos de grafo
[!INCLUDE[tsql-md](../../includes/tsql-md.md)]as extensões permitirão que os usuários criem tabelas de nó ou borda. Os nós e as bordas podem ter propriedades associadas a eles. Como os nós e as bordas são armazenados como tabelas, todas as operações com suporte em tabelas relacionais têm suporte na tabela de nó ou borda. Veja um exemplo:  

```   
CREATE TABLE Person (ID INTEGER PRIMARY KEY, Name VARCHAR(100), Age INT) AS NODE;
CREATE TABLE friends (StartDate date) AS EDGE;
```   

![pessoa-amigos-tabelas](../../relational-databases/graphs/media/person-friends-tables.png "Nó Person e tabelas de borda de amigos")  
Os nós e as bordas são armazenados como tabelas  

### <a name="query-language-extensions"></a>Extensões de linguagem de consulta  
A `MATCH` nova cláusula é introduzida para dar suporte à correspondência de padrões e à navegação de vários saltos por meio do grafo. A `MATCH` função usa sintaxe de estilo de arte ASCII para correspondência de padrões. Por exemplo:  

```   
-- Find friends of John
SELECT Person2.Name 
FROM Person Person1, Friends, Person Person2
WHERE MATCH(Person1-(Friends)->Person2)
AND Person1.Name = 'John';
```   
 
### <a name="fully-integrated-in-includessnoversionincludesssnoversion-mdmd-engine"></a>Totalmente integrado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mecanismo 
As extensões de grafo são totalmente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] integradas no mecanismo. Use o mesmo mecanismo de armazenamento, metadados, processador de consultas, etc. para armazenar e consultar dados de grafo. Consulta entre grafo e dados relacionais em uma única consulta. Combinação de recursos de grafo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com outras tecnologias como COLUMNSTORE, ha, R Services, etc. O banco de dados SQL Graph também dá suporte a todos os recursos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de segurança e conformidade disponíveis com o.
 
### <a name="tooling-and-ecosystem"></a>Ferramentas e ecossistema

Beneficie-se de ferramentas existentes e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ecossistema que oferece. Ferramentas como backup e restauração, importação e exportação, BCP simplesmente funcionam prontos para uso. Outras ferramentas ou serviços como SSIS, SSRS ou Power BI funcionarão com tabelas de grafo, exatamente como funcionam com tabelas relacionais.

## <a name="edge-constraints"></a>Restrições de borda
Uma restrição de borda é definida em uma tabela de borda de gráfico e é um par de tabelas de nó que um determinado tipo de borda pode conectar. Isso dá aos usuários um melhor controle sobre o esquema do grafo. Com a ajuda de restrições de borda, os usuários podem restringir o tipo de nós que uma determinada borda tem permissão para se conectar. 

Para saber mais sobre como criar e usar restrições de borda, consulte [restrições de borda](../../relational-databases/tables/graph-edge-constraints.md)

## <a name="merge-dml"></a>Mesclar DML 
A instrução [Merge](../../t-sql/statements/merge-transact-sql.md) executa operações de inserção, atualização ou exclusão em uma tabela de destino com base nos resultados de uma junção com uma tabela de origem. Por exemplo, você pode sincronizar duas tabelas inserindo, atualizando ou excluindo linhas em uma tabela de destino com base nas diferenças entre a tabela de destino e a tabela de origem. O uso de predicados MATCH em uma instrução MERGE agora tem suporte no banco de dados SQL do Azure e SQL Server vNext. Ou seja, agora é possível mesclar seus dados de grafo atuais (tabelas de nó ou borda) com novos dados usando os predicados de correspondência para especificar relações de grafo em uma única instrução, em vez de instruções INSERT/UPDATE/DELETE separadas.

Para saber mais sobre como a correspondência pode ser usada em mesclar DML, consulte a [instrução MERGE](../../t-sql/statements/merge-transact-sql.md)

## <a name="shortest-path"></a>Caminho mais curto
A função [SHORTEST_PATH](./sql-graph-shortest-path.md) localiza o caminho mais curto entre os dois nós em um grafo ou a partir de um determinado nó para todos os outros nós no grafo. O caminho mais curto também pode ser usado para encontrar um fechamento transitório ou para passagens de comprimento arbitrário no grafo. 

 ## <a name="next-steps"></a>Próximas etapas  
Ler a [arquitetura do banco de dados do SQL Graph](./sql-graph-architecture.md)
   

