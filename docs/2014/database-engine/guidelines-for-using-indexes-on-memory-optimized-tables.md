---
title: Diretrizes para usar índices em tabelas com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
helpviewer_keywords:
- hash indexes
ms.assetid: 16ef63a4-367a-46ac-917d-9eebc81ab29b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 71d26e3f46034019d51bd69b86686f40eb9ce63e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62779220"
---
# <a name="guidelines-for-using-indexes-on-memory-optimized-tables"></a>Diretrizes para usar índices em tabelas com otimização de memória
  Os índices são usados para acessar dados com eficiência nas tabelas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Especificar os índices certos pode melhorar significativamente o desempenho da consulta. Considere, por exemplo, a consulta:  
  
```sql  
SELECT c1, c2 FROM t WHERE c1 = 1;  
```  
  
 Se não houver nenhum índice na coluna c1, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] precisará verificar a tabela t inteira e filtrar por linhas que atendam à condição c1=1. No entanto, se t tiver um índice na coluna c1, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] poderá buscar diretamente o valor 1 e recuperar as linhas.  
  
 Ao procurar por registros com um valor específico, ou intervalo de valores, para uma ou mais colunas na tabela, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode usar um índice nessas colunas para localizar rapidamente os registros correspondentes. As tabelas com base em disco e com otimização de memória se beneficiam dos índices. No entanto, há determinadas diferenças entre as estruturas de índice que precisam ser consideradas durante o uso de tabelas com otimização de memória. (Os índices em tabelas com otimização de memória são chamados de índices com otimização de memória.) Algumas das principais diferenças são:  
  
-   Os índices com otimização de memória devem ser criados com [CREATE TABLE &#40;&#41;Transact-SQL ](/sql/t-sql/statements/create-table-transact-sql). Os índices baseados em disco podem ser criados com `CREATE TABLE` e `CREATE INDEX`.  
  
-   Os índices com otimização de memória existem apenas na memória. As estruturas de índice não são persistentes no disco e as operações de índice não são registradas no log de transações. A estrutura de índice é criada quando a tabela com otimização de memória é criada na memória, tanto durante a instrução CREATE TABLE quanto durante a inicialização do banco de dados.  
  
-   Os índices com otimização de memória são inerentemente cobertos. A cobertura significa que, praticamente, todas as colunas são incluídas no índice e que as pesquisas de indicador não são necessárias em tabelas com otimização de memória. Em vez de uma referência à chave primária, os índices com otimização de memória simplesmente contêm um ponteiro de memória para a linha real na estrutura de dados da tabela.  
  
-   A fragmentação e o fator de preenchimento não se aplicam aos índices com otimização de memória. Em índices baseados em disco, a fragmentação se refere a páginas na árvore B sendo gravadas fora de ordem no disco. Os índices com otimização de memória não são gravados nem lidos no disco. O fator de preenchimento nos índices da árvore B baseados em disco se refere ao grau em que as estruturas de página física são preenchidas com dados reais. As estruturas de índice com otimização de memória não têm páginas de tamanho fixo.  
  
 Há dois tipos de índices com otimização de memória:  
  
-   Índices de hash não clusterizados, que são projetados para pesquisas de ponto. Para obter mais informações sobre índices de hash, consulte [hash Indexes](hash-indexes.md).  
  
-   Índices não clusterizados, que são projetados para exames de intervalo e exames ordenados.  
  
 Com um índice de hash, os dados são acessados por meio de uma tabela de hash na memória. Os índices de hash não possuem páginas e sempre são de um tamanho fixo. No entanto, um índice de hash pode ter buckets de hash vazios, o que resulta em espaço desperdiçado limitado. Os valores retornados por uma consulta que usa um índice de hash não são classificados. Os índices de hash são otimizados para buscas de índice em predicados de igualdade e oferecem suporte a exames completos de índice.  
  
 Os índices não clusterizados (não os índices de hash) oferecem suporte aos mesmos itens que os índices de hash, mais as operações de busca em predicados de desigualdade, como maior que ou menor que e ordem de classificação. As linhas podem ser recuperadas de acordo com a ordem especificada com a criação do índice. Se a ordem de classificação do índice corresponder à ordem de classificação necessária para uma consulta específica, por exemplo, se a chave de índice corresponder à cláusula ORDER BY, não haverá necessidade de classificar as linhas como parte da execução da consulta. Os índices não clusterizados com otimização de memória são unidirecionais; não oferecerão suporte a recuperação de linhas em uma ordem de classificação que for o oposto da ordem de classificação do índice. Por exemplo, para um índice especificado como (c1 ASC), não é possível digitalizar o índice em ordem inversa, como (c1 DESC).  
  
 Cada índice consome memória. Os índices de hash consomem uma quantidade fixa de memória, que é uma função do número de buckets. Para índices não clusterizados com otimização de memória, o consumo de memória é uma função da contagem de linhas e do tamanho das colunas de chave de índice, com alguma sobrecarga adicional, dependendo da carga de trabalho. A memória para índices com otimização de memória é separada da memória usada para armazenar linhas em tabelas com otimização de memória.  
  
 Valores de chave duplicados sempre compartilham o mesmo bucket de hash. Se um índice de hash contiver muitos valores de chave duplicados, as longas sequências de hash resultantes prejudicarão o desempenho. Colisões de hash, que ocorrem em qualquer índice de hash, reduzirão ainda mais o desempenho nesse cenário. Por esse motivo, se o número de chaves de índice exclusivas for pelo menos 100 vezes menor do que a contagem de linhas, você poderá reduzir o risco de colisões de hash, tornando o número de buckets muito maior (pelo menos oito vezes a quantidade de chaves de índice exclusivas; consulte [determinando a contagem de buckets correta para](../../2014/database-engine/determining-the-correct-bucket-count-for-hash-indexes.md) obter mais informações) ou elimine as colisões de hash por completo usando um índice não  
  
## <a name="determining-which-indexes-to-use-for-a-memory-optimized-table"></a>Determinando os índices a serem usados em uma tabela com otimização de memória  
 Cada tabela com otimização de memória deve ter pelo menos um índice. Observe que cada restrição PRIMARY KEY cria um índice implicitamente. Desse modo, se uma tabela tiver uma chave primária, ela terá um índice. Uma chave primária é um requisito para uma tabela com otimização de memória durável.  
  
 Ao consultar uma tabela com otimização de memória, os índices de hash são melhor executados quando a cláusula de predicado contém somente predicados de igualdade. O predicado deve incluir todas as colunas na chave de índice de hash. Um índice de hash reverterá para um exame de acordo com um predicado de desigualdade.  
  
 Uma coluna em uma tabela com otimização de memória pode fazer parte de um índice de hash e de um índice não clusterizado.  
  
 Ao consultar uma tabela com otimização de memória com predicados de desigualdade, os índices não clusterizados serão executados melhor do que os índices de hash não clusterizados.  
  
 O índice de hash requer uma chave (para submeter a hash) para realizar a busca no índice. Se uma chave de índice consiste em duas colunas e você fornece apenas a primeira coluna, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não tem uma chave completo ao hash. Isso resultará em um plano de consulta de exame de índice. O uso determina quais colunas devem ser indexadas.  
  
 Quando uma coluna em um índice não clusterizado tiver o mesmo valor em várias linhas (as colunas de chave de índice terão muitos valores duplicados), o desempenho pode diminuir nas atualizações, inserções e exclusões.  Uma maneira de melhorar o desempenho nessa situação é adicionar outra coluna ao índice não clusterizado.  
  
### <a name="operations-on-memory-optimized-and-disk-based-indexes"></a>Operações em índices com otimização de memória e baseados no disco.  
  
|Operação|Índice, hash não clusterizado, com otimização de memória|Índice não clusterizado com otimização de memória|Índice baseado em disco|  
|---------------|-------------------------------------------------|------------------------------------------|-----------------------|  
|Verificação de índice, recuperar todas as linhas da tabela.|Sim|Sim|Sim|  
|Busca de índice em predicados de igualdade (=).|Sim<br /><br /> (Chave completa necessária.)|Sim <sup>1</sup>|Sim|  
|Índice Seek em predicados de desigualdade (>, < \<, =, >=, entre).|Não (resultados em uma verificação de índice)|Sim <sup>1</sup>|Sim|  
|Recuperar linhas em uma ordem de classificação que corresponda à definição do índice.|Não|Sim|Sim|  
|Recuperar linhas em uma ordem de classificação que corresponda à inversão da definição do índice.|Não|Não|Sim|  
  
 Na tabela, Sim significa que o índice pode servir adequadamente o pedido e Não significa que o índice não pode ser usado com êxito para satisfazer o pedido.  
  
 <sup>1</sup> para um índice com otimização de memória não clusterizado, a chave completa não é necessária para executar uma busca de índice. Embora, de acordo com a ordem de colunas da chave de índice, ocorrerá um exame se o valor de uma coluna aparecer após uma coluna ausente.  
  
## <a name="index-count"></a>Contagem de índice  
 Uma tabela com otimização de memória pode ter até 8 índices, incluindo o índice criado com a chave primária.  
  
 Em relação ao número de índices criados em uma tabela com otimização de memória, considere o seguinte:  
  
-   Especifique os índices que você precisa quando cria a tabela. Não é possível criar um índice para uma tabela com otimização de memória depois que a tabela é criada. Se você deseja adicionar um índice a uma tabela com otimização de memória, solte e recrie a tabela.  
  
-   Não crie um índice que você use raramente:  
  
     A coleta de lixo funciona melhor se todos os índices na tabela forem usados frequentemente. Os índices usados raramente podem fazer com que o sistema de coleta de lixo não seja bem executado em versões de linha antigas.  
  
## <a name="creating-a-memory-optimized-index-code-samples"></a>Criando um índice com otimização de memória: exemplos de código  
 Índice de hash em nível de coluna:  
  
```sql  
CREATE TABLE t1   
   (c1 INT NOT NULL INDEX idx HASH WITH (BUCKET_COUNT = 100))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
```  
  
 Índice de hash em nível de tabela:  
  
```sql  
CREATE TABLE t1_1   
   (c1 INT NOT NULL,   
   INDEX IDX HASH (c1) WITH (BUCKET_COUNT = 100))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
```  
  
 Índice de hash chave primária em nível de coluna:  
  
```sql  
CREATE TABLE t2   
   (c1 INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT = 100))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
```  
  
 Índice de hash de chave primária em nível de tabela:  
  
```sql  
CREATE TABLE t2_2   
   (c1 INT NOT NULL,   
   PRIMARY KEY NONCLUSTERED HASH (c1) WITH (BUCKET_COUNT = 100))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
```  
  
 Índice não clusterizado em nível de coluna:  
  
```sql  
CREATE TABLE t3   
   (c1 INT NOT NULL INDEX ID)   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
```  
  
 Índice não clusterizado em nível de tabela:  
  
```sql  
CREATE TABLE t3_3   
   (c1 INT NOT NULL,   
   INDEX IDX NONCLUSTERED (c1))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
```  
  
 Índice não clusterizado de chave primária em nível de coluna:  
  
```sql  
CREATE TABLE t4   
   (c1 INT NOT NULL PRIMARY KEY NONCLUSTERED)   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
```  
  
 Índice não clusterizado de chave primária em nível de tabela:  
  
```sql  
CREATE TABLE t4_4   
   (c1 INT NOT NULL,   
   PRIMARY KEY NONCLUSTERED (c1))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
```  
  
 Índice de várias colunas definido depois que as colunas são definidas:  
  
```sql  
create table t (  
       a int not null constraint ta primary key nonclustered,  
       b int not null,  
       c int not null,  
       d int not null,  
       index idx_t_b_c_d nonclustered (b, c asc, d desc)  
) with (memory_optimized = on, durability = SCHEMA_AND_DATA)  
go  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Índices em tabelas com otimização de memória](../relational-databases/in-memory-oltp/memory-optimized-tables.md)   
 [Determinando o número correto de buckets para índices de hash](../../2014/database-engine/determining-the-correct-bucket-count-for-hash-indexes.md)   
 [Índices de hash](hash-indexes.md)  
  
  
