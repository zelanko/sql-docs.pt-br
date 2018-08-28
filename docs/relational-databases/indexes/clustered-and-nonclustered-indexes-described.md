---
title: Índices clusterizados e não clusterizados descritos | Microsoft Docs
ms.custom: ''
ms.date: 11/28/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- query optimizer [SQL Server], index usage
- index concepts [SQL Server]
ms.assetid: b7d6b323-728d-4763-a987-92e6292f6f7a
caps.latest.revision: 36
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: b63bbfd4f57460d78d11d463634c19b38a2604af
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40405495"
---
# <a name="clustered-and-nonclustered-indexes-described"></a>Índices clusterizados e não clusterizados descritos
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

 > Para ver o conteúdo relacionado a versões anteriores do SQL Server, consulte [Índices clusterizados e não clusterizados descritos](clustered-and-nonclustered-indexes-described.md).

  Um índice é uma estrutura em disco associada a uma tabela ou exibição, que agiliza a recuperação das linhas de uma tabela ou exibição. Um índice contém chaves criadas de uma ou mais colunas da tabela ou exibição. Essas chaves são armazenadas em uma estrutura (árvore B) que habilita o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a localizar a linha ou as linhas associadas aos valores de chave de forma rápida e eficaz.  
  
 Tabelas ou exibições podem conter os seguintes tipos de índices:  
  
-   Clusterizado  
  
    -   Os índices clusterizados classificam e armazenam as linhas de dados da tabela ou exibição com base em seus valores de chave. Essas são as colunas incluídas na definição do índice. Pode haver apenas um índice clusterizado por tabela, pois as linhas de dados podem ser classificadas somente em uma única ordem.  
  
    -   O único momento em que as linhas de dados de uma tabela são armazenadas na ordem de classificação é quando a tabela contém um índice clusterizado. Se a tabela contiver um índice clusterizado, será denominada tabela clusterizada. Se a tabela não possuir nenhum índice clusterizado, suas linhas de dados ficarão armazenadas em uma estrutura não ordenada denominada heap.  
  
-   Não clusterizado  
  
    -   Os índices não clusterizados têm uma estrutura distinta das linhas de dados. O índice não clusterizado contém os valores de chave de índice não clusterizado e cada entrada de valor de chave tem um ponteiro para a linha de dados que contém o valor de chave.  
  
    -   O ponteiro de uma linha de índice em um índice não clusterizado de uma linha de dados é denominado localizador de linhas. A estrutura do localizador de linhas depende de as páginas de dados serem armazenadas em um heap ou em uma tabela clusterizada. Para o heap, o localizador de linhas é um ponteiro para a linha. Para a tabela clusterizada, o localizador de linhas é a chave de índice clusterizado.  
  
    -   Você pode adicionar colunas não chave ao nível folha do índice não clusterizado para ignorar os limites de chave de índice existente e executar consultas completamente abrangidas e indexadas. Para obter mais informações, consulte [Create Indexes with Included Columns](../../relational-databases/indexes/create-indexes-with-included-columns.md). Para obter detalhes sobre os limites do índice de chave, consulte [Especificações de capacidade máxima do SQL Server](../../sql-server/maximum-capacity-specifications-for-sql-server.md). 
  
 Tanto os índices clusterizados quanto os não clusterizados podem ser exclusivos. Isso significa que duas linhas não podem ter o mesmo valor que a chave de índice. Caso contrário, o índice não será exclusivo e várias linhas poderão compartilhar o mesmo valor de chave. Para obter mais informações, confira [Criar índices exclusivos](../../relational-databases/indexes/create-unique-indexes.md).  
  
 Os índices são mantidos automaticamente para uma tabela ou exibição sempre que os dados da tabela são modificados.  
  
 Veja [Índices](../../relational-databases/indexes/indexes.md) para obter mais tipos de índices de uso geral.  
  
## <a name="indexes-and-constraints"></a>Índices e restrições  
 Os índices são criados automaticamente quando as restrições PRIMARY KEY e UNIQUE são definidas em colunas de tabelas. Por exemplo, ao criar uma tabela e identificar determinada coluna como a chave primária, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] cria automaticamente uma restrição PRIMARY KEY e o índice nessa coluna. Para obter mais informações, veja [Criar chaves primárias](../../relational-databases/tables/create-primary-keys.md) e [Criar restrições exclusivas](../../relational-databases/tables/create-unique-constraints.md).  
  
## <a name="how-indexes-are-used-by-the-query-optimizer"></a>Como os índices são usados pelo Otimizador de Consulta  
 Índices bem projetados podem reduzir as operações de E/S de disco e consumir menos recursos de sistema, aprimorando o desempenho das consultas. Os índices podem ser úteis para uma série de consultas que contêm instruções SELECT, UPDATE, DELETE ou MERGE. Considere a consulta `SELECT Title, HireDate FROM HumanResources.Employee WHERE EmployeeID = 250` no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Quando essa consulta é executada, o otimizador de consulta avalia cada método disponível para recuperar os dados e seleciona o mais eficaz. O método pode ser uma verificação de tabela ou verificação de um ou mais índices, se houver.  
  
 Ao executar uma verificação de tabela, o otimizador de consulta lê todas as linhas da tabela e extrai as linhas que atendem os critérios da consulta. Uma verificação de tabela gera várias operações de E/S de disco e pode utilizar muitos recursos. No entanto, a verificação de tabela poderá ser o método mais eficaz se, por exemplo, o conjunto de resultados da consulta contiver um alto percentual de linhas da tabela.  
  
 Quando o otimizador de consulta utiliza um índice, ele pesquisa as colunas de chave do índice, encontra o local de armazenamento das linhas necessárias à consulta e extrai as linhas que correspondem àquele local. Em geral, fazer pesquisas no índice é muito mais rápido do que na tabela, porque diferentemente da tabela, o índice contém, com frequência, poucas colunas por linha e as linhas ficam na ordem de classificação.  
  
 Normalmente, o otimizador de consulta seleciona o método mais eficaz ao executar consultas. No entanto, se não houver índices disponíveis, o otimizador de consulta precisará usar uma verificação de tabela. Sua tarefa é criar índices mais adequados ao seu ambiente, para que o otimizador de consulta tenha uma seleção de índices eficientes da qual selecionar. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece o [Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/database-engine-tuning-advisor.md) para ajudar com a análise de seu ambiente de banco de dados e na seleção de índices apropriados.  
  
> [!IMPORTANT] 
> Para obter mais informações sobre as diretrizes de design de índice e operações internas, consulte o [Guia de design de índice do SQL Server](../../relational-databases/sql-server-index-design-guide.md).

## <a name="related-content"></a>Conteúdo relacionado  
 [Guia de criação de índice do SQL Server](../../relational-databases/sql-server-index-design-guide.md)     
 [Criar índices clusterizados](../../relational-databases/indexes/create-clustered-indexes.md)  
 [Criar índices não clusterizados](../../relational-databases/indexes/create-nonclustered-indexes.md)  
  
  
