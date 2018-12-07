---
title: Estimar requisitos de memória para tabelas com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 12/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 5c5cc1fc-1fdf-4562-9443-272ad9ab5ba8
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1cdacecf1c6d6c8c08411eff57c65adc0872dd39
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52531510"
---
# <a name="estimate-memory-requirements-for-memory-optimized-tables"></a>Estimar requisitos de memória para tabelas com otimização de memória
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

As tabelas com otimização de memória requerem a existência de memória suficiente para manter todas as linhas e índices na memória. Como a memória é um recurso finito, é importante compreender e gerenciar o uso de memória no sistema. Os tópicos nessa seção abordam os cenários comuns de uso e gerenciamento de memória.

Se você estiver criando uma nova tabela com otimização de memória ou estiver migrando uma tabela com base em disco existente para uma tabela com otimização de memória [!INCLUDE[hek_2](../../includes/hek-2-md.md)], é importante ter uma estimativa razoável das necessidades de memória de cada tabela para que você possa provisionar ao servidor memória suficiente. Esta seção descreve como estimar a quantidade de memória necessária para manter dados para uma tabela com otimização de memória.  
  
Se você pretende migrar de tabelas baseadas em disco para tabelas com otimização de memória, antes de continuar neste tópico, veja o tópico [Determinando se uma tabela ou procedimento armazenado deve ser movido para OLTP in-memory](../../relational-databases/in-memory-oltp/determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md) para obter diretrizes sobre as melhores tabelas para migração. Todos os tópicos em [Migrando para OLTP in-memory](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md) fornecem diretrizes sobre como migrar de tabelas baseadas em disco para tabelas com otimização de memória. 
  
## <a name="basic-guidance-for-estimating-memory-requirements"></a>Diretrizes básicas para estimar os requisitos de memória

A partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], não há nenhum limite no tamanho das tabelas com otimização de memória, embora as tabelas precisem caber na memória.  No [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] , o tamanho dos dados com suporte é de 256 GB para tabelas SCHEMA_AND_DATA.

O tamanho de uma tabela com otimização de memória corresponde ao tamanho dos dados, além da sobrecarga para cabeçalhos de linha. Ao migrar uma tabela baseada em disco para uma tabela com otimização de memória, o tamanho da tabela com otimização de memória aproximadamente corresponderá ao tamanho do índice clusterizado ou do heap da tabela original baseada em disco.

Índices em tabelas com otimização de memória tendem a ser menores que os índices não clusterizados em tabelas baseadas em disco. O tamanho dos índices não clusterizados está na ordem de `[primary key size] * [row count]`. O tamanho dos índices de hash é `[bucket count] * 8 bytes`. 

Quando houver uma carga de trabalho ativa, é necessária memória adicional para a conta para o controle de versão de linha e de várias operações. A quantidade de memória necessária na prática depende na carga de trabalho, mas para segurança, a recomendação é iniciar com duas vezes o tamanho esperado de tabelas com otimização de memória e índices e observar quais são os requisitos de memória na prática. A sobrecarga de controle de versão de linha sempre depende das características da carga de trabalho – especialmente, transações de longa duração aumentam a sobrecarga. Para a maioria das cargas de trabalho com bancos de dados maiores (por exemplo, >100 GB), a sobrecarga tende a ser limitada (25% ou menos).

  
## <a name="detailed-computation-of-memory-requirements"></a>Computação detalhada dos requisitos de memória 
  
- [Exemplo de tabela com otimização de memória](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md#bkmk_ExampleTable)  
  
- [Memória da tabela](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md#bkmk_MemoryForTable)  
  
- [Memória para índices](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md#bkmk_IndexMeemory)  
  
- [Memória para o controle de versão de linha](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md#bkmk_MemoryForRowVersions)  
  
- [Memória para variáveis de tabela](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md#bkmk_TableVariables)  
  
- [Memória para o crescimento](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md#bkmk_MemoryForGrowth)  
  
###  <a name="bkmk_ExampleTable"></a> Exemplo de tabela com otimização de memória  

Considere o esquema de tabela com otimização de memória a seguir:
  
```sql  
CREATE TABLE t_hk
(  
  col1 int NOT NULL  PRIMARY KEY NONCLUSTERED,  

  col2 int NOT NULL  INDEX t1c2_index   
      HASH WITH (bucket_count = 5000000),  

  col3 int NOT NULL  INDEX t1c3_index   
      HASH WITH (bucket_count = 5000000),  

  col4 int NOT NULL  INDEX t1c4_index   
      HASH WITH (bucket_count = 5000000),  

  col5 int NOT NULL  INDEX t1c5_index NONCLUSTERED,  

  col6 char (50) NOT NULL,  
  col7 char (50) NOT NULL,   
  col8 char (30) NOT NULL,   
  col9 char (50) NOT NULL  

  WITH (memory_optimized = on)  
);
GO  
```  

Usando esse esquema, determinaremos a memória mínima necessária para essa tabela com otimização de memória.  
  
###  <a name="bkmk_MemoryForTable"></a> Memória da tabela  

Uma linha de tabela com otimização de memória é composta de três partes:
  
- **Carimbos de data/hora**   
    Cabeçalho de linha/carimbos de data/hora = 24 bytes.  
  
- **Ponteiros de índice**   
    Para cada índice de hash na tabela, cada linha tem um ponteiro de endereço de 8 bytes para a próxima linha no índice.  Uma vez que há 4 índices, cada linha alocará 32 bytes para ponteiros de índice (um ponteiro de 8 bytes para cada índice).  
  
- **Dados**   
    O tamanho da parte dos dados da linha é determinado pela adição do tamanho de tipo para cada coluna de dados.  Em nossa tabela temos cinco números inteiros de 4 bytes, três colunas de caracteres de 50 bytes e uma coluna de caracteres de 30 bytes.  Como consequência, a parte de dados de cada linha tem 4 + 4 + 4 + 4 + 4 + 50 + 50 + 30 + 50 ou 200 bytes.  
  
Veja a seguir uma computação de tamanho para 5.000.000 (5 milhões) de linhas em uma tabela com otimização de memória. A memória total usada pelas linhas de dados é estimada como se segue:  
  
#### <a name="memory-for-the-tables-rows"></a>Memória para linhas da tabela  
  
Pelos cálculos acima, o tamanho de cada linha na tabela com otimização de memória é 24 + 32 + 200 ou 256 bytes.  Como temos 5 milhões de linhas, a tabela consumirá 5.000.000 * 256 bytes ou 1.280.000.000 bytes – aproximadamente 1,28 GB.  
  
###  <a name="bkmk_IndexMeemory"></a> Memória para índices  

#### <a name="memory-for-each-hash-index"></a>Memória para cada índice de hash  
  
Cada índice de hash é uma matriz de hash de ponteiros de endereço de 8 bytes.  O tamanho da matriz é melhor determinado pelo número de valores de índice exclusivos para esse índice – por exemplo, o número de valores exclusivos Col2 é um bom ponto de partida para o tamanho da matriz para o t1c2_index. Uma matriz de hash que é muito grande desperdiça memória.  Uma matriz de hash que é muito pequena reduz o desempenho já que haverá muitas colisões pelos valores de índice que usam o hash para o mesmo índice.  
  
Os índices de hash atingem muito rápido pesquisas de igualdade como:  
  
```sql  
SELECT * FROM t_hk  
   WHERE Col2 = 3;
```  
  
Os índices não clusterizados são mais rápidos para pesquisas de intervalo como:  
  
```sql  
SELECT * FROM t_hk  
   WHERE Col2 >= 3;
```  
  
Se você estiver migrando uma tabela com base em disco, poderá usar o seguinte para determinar o número de valores exclusivos para o índice t1c2_index.  
  
```sql
SELECT COUNT(DISTINCT [Col2])  
  FROM t_hk;
```  
  
Se você estiver criando uma nova tabela, precisará estimar o tamanho da matriz ou a coleta de dados dos testes antes da implantação.  
  
Para obter informações sobre como os índices de hash funcionam em tabelas com otimização de memória [!INCLUDE[hek_2](../../includes/hek-2-md.md)] , veja [Índices de hash](https://msdn.microsoft.com/library/f4bdc9c1-7922-4fac-8183-d11ec58fec4e).  
  
#### <a name="setting-the-hash-index-array-size"></a>Definindo o tamanho da matriz de índice de hash  
  
O tamanho da matriz de hash é definido por `(bucket_count= value)` , em que `value` é um valor inteiro maior que zero. Se `value` não for uma potência de 2, o bucket_count real será arredondado até a potência seguinte mais próxima de 2.  Em nossa tabela de exemplo, (bucket_count = 5000000), já que 5.000.000 não é a uma potência de 2, o número de buckets real é arredondado até 8.388.608 (2^23).  Você deve usar esse número, e não 5.000.000 quando calcular a memória necessária à matriz de hash.  
  
Assim, em nosso exemplo, a memória necessária para cada matriz de hash é:  
  
8,388,608 * 8 = 2^23 \* 8 = 2^23 \* 2^3 = 2^26 = 67.108.864 ou aproximadamente 64 MB.  
  
Como temos três índices de hash, a memória necessária para os índices de hash é 3 * 64MB = 192MB.  
  
#### <a name="memory-for-non-clustered-indexes"></a>Memória para índices não clusterizados  
  
Os índices não clusterizados são implementados como árvores B com os nós internos que contêm o valor e ponteiros de índice aos nós subsequentes.  Os nós folha contêm o valor de índice e um ponteiro para a linha da tabela na memória.  
  
Diferentemente dos índices de hash, os índices não clusterizados não têm um tamanho fixo do bucket. O índice aumenta e diminui dinamicamente com os dados.  
  
A memória necessária pelos índices não clusterizados pode ser computada da seguinte forma:  
  
- **Memória alocada a nós que não são nós folha**   
    Para uma configuração comum, a memória alocada para nós não folha é uma porcentagem muito pequena da memória total usada pelo índice. Ela é tão pequena que pode seguramente ser ignorada.  
  
- **Memória para nós folha**   
    Os nós folha têm uma linha para cada chave exclusiva na tabela que aponta para as linhas de dados com essa chave exclusiva.  Se você tiver várias linhas com a mesma chave (isto é, tiver um índice não clusterizado não exclusivo), há apenas uma linha no nó folha de índice que aponta para uma das linhas com as outras linhas vinculadas entre si.  Assim, a memória total necessária pode ser aproximado por:
  - memoryForNonClusteredIndex = (pointerSize + sum(keyColumnDataTypeSizes)) * rowsWithUniqueKeys  
  
 Os índices não clusterizados são os melhores quando usado para pesquisas de intervalo, como exemplificadas pela seguinte consulta:  
  
```sql  
SELECT * FRON t_hk  
   WHERE c2 > 5;  
```  
  
###  <a name="bkmk_MemoryForRowVersions"></a> Memória para o controle de versão de linha

Para evitar bloqueios, OLTP de memória usa a simultaneidade otimista ao atualizar ou excluir linhas. Isso significa que quando uma linha é atualizada, uma versão de linha adicional será criada. Além disso, as exclusões são lógicas – a linha existente é marcada como excluída, mas não é removida imediatamente. O sistema mantém as versões de linhas antigas (incluindo as linhas excluídas) disponíveis até que todas as transações que possivelmente poderiam usar a versão tenham concluído a execução. 
  
Como pode haver um número de linhas adicionais na memória a qualquer momento aguardando o ciclo de coleta de lixo para liberar a memória, você deve ter memória suficiente para acomodar estas linhas adicionais.  
  
O número de linhas adicionais podem ser estimado calculando o número máximo de linhas por segundo de atualizações e exclusões de linha, então multiplicando que o número de segundos a transação mais longa demora (um mínimo de 1).  
  
Esse valor é então multiplicado pelo tamanho da linha para obter o número de bytes necessários para o controle de versão de linha.  
  
`rowVersions = durationOfLongestTransctoinInSeconds * peakNumberOfRowUpdatesOrDeletesPerSecond`  
  
A necessidade de memória para linhas obsoletas é estimada pela multiplicação do número de linhas obsoletas pelo tamanho de uma linha da tabela com otimização de memória (Veja [Memória para a tabela](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md#bkmk_MemoryForTable) acima).  
  
`memoryForRowVersions = rowVersions * rowSize`  
  
###  <a name="bkmk_TableVariables"></a> Memória para variáveis de tabela
  
A memória usada para uma variável de tabela é liberada apenas quando a variável de tabela sai do escopo. As linhas excluídas, inclusive as linhas excluídas como parte de uma atualização, de uma variável de tabela, não estão sujeitas à coleta de lixo. Nenhuma memória é liberada até a variável de tabela sair do escopo.  
  
As variáveis de tabela definidas em um lote SQL grande, e não em um escopo do procedimento, que são usadas em muitas transações podem consumir bastante memória. Como elas não têm coleta de lixo, as linhas excluídas em uma variável de tabela podem consumir muita memória e diminuir o desempenho, pois as operações de leitura precisam verificar as linhas excluídas.  
  
###  <a name="bkmk_MemoryForGrowth"></a> Memória para o crescimento

Os cálculos acima estima suas necessidades de memória para a tabela como existe atualmente. Além dessa memória, você precisa estimar o aumento da tabela e fornecimento de memória suficiente para acomodar esse crescimento.  Por exemplo, se você antecipar o crescimento de 10% no múltiplo da necessidade dos resultados acima por 1,1 para obter a memória total necessária para a tabela.  
  
## <a name="see-also"></a>Consulte Também

[Migrando para OLTP na memória](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  

