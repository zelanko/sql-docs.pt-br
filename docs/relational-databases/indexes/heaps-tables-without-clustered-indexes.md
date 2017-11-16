---
title: "Heaps (tabelas sem índices clusterizados) | Microsoft Docs"
ms.custom: 
ms.date: 11/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: heaps
ms.assetid: df5c4dfb-d372-4d0f-859a-a2d2533ee0d7
caps.latest.revision: "8"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: ba60d021e8ba852825075f20db6e93ec87345744
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="heaps-tables-without-clustered-indexes"></a>Heaps (Tabelas sem índices clusterizados)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Heap é uma tabela sem índice clusterizado. Podem ser criados um ou mais índices não clusterizados em tabelas armazenadas como um heap. Dados são armazenados no heap sem especificar uma ordem. Normalmente, os dados são armazenados inicialmente na ordem em que as linhas são inseridas na tabela, mas o [!INCLUDE[ssDE](../../includes/ssde-md.md)] pode mover os dados no heap para armazenar as linhas de forma eficaz; portanto, a ordem de dados não pode ser prevista. Para garantir a ordem de linhas retornadas de um heap, você deve usar a cláusula **ORDER BY** . Para especificar a ordem de armazenamento das linhas, crie um índice clusterizado na tabela, de forma que a tabela não seja um heap.  
  
> [!NOTE]  
>  Às vezes, há boas razões para deixar uma tabela como heap em vez de criar um índice clusterizado, mas usar heaps efetivamente é uma habilidade avançada. A maioria das tabelas deve ter um índice clusterizado cuidadosamente escolhido, a menos que haja uma boa razão boa para deixar a tabela como heap.  
  
## <a name="when-to-use-a-heap"></a>Quando usar um heap  
 Se uma tabela for um heap e não tiver um índice clusterizado, a tabela inteira deverá ser examinada (análise de tabela) para localizar as linhas. Isso pode ser aceitável quando a tabela é pequena, como uma lista dos 12 escritórios regionais de uma empresa.  
  
 Quando uma tabela é armazenada como heap, linhas individuais são identificadas por referência a um RID (identificador de linha) que consiste em número do arquivo, número da página de dados e local na página. A ID de linha é uma estrutura pequena e eficiente. Às vezes, os arquitetos de dados usam heaps quando os dados são sempre acessados por índices não clusterizados e o RID é menor que uma chave de índice clusterizado.  
  
## <a name="when-not-to-use-a-heap"></a>Quando não usar um heap  
 Não use um heap quando os dados são retornados frequentemente em uma ordem classificada. Um índice clusterizado na coluna de classificação pode evitar a operação de classificação.  
  
 Não use um heap quando os dados forem agrupados com frequência. Os dados devem ser classificados antes de serem agrupados, e um índice clusterizado na coluna de classificação pode evitar a operação de classificação.  
  
 Não use um heap quando intervalos de dados são consultados frequentemente na tabela.  Um índice clusterizado na coluna de intervalo pode evitar a classificação do heap inteiro.  
  
 Não use um heap quando não houver índice não clusterizado e a tabela for grande. Em um heap, todas as linhas do heap devem ser lidas para localizar qualquer linha.  
  
## <a name="managing-heaps"></a>Gerenciando heaps  
 Para criar um heap, crie uma tabela sem um índice clusterizado. Se uma tabela já tiver um índice clusterizado, descarte o índice clusterizado para retornar a tabela a um heap.  
  
 Para remover um heap, crie um índice clusterizado no heap.  
  
 Para recriar um heap para recuperar o espaço desperdiçado, crie um índice clusterizado no heap e descarte esse índice clusterizado.  
  
> [!WARNING]  
>  Criar ou descartar índices clusterizados requer a regravação da tabela inteira. Se a tabela tiver índices não clusterizados, todos os índices não clusterizados deverão ser recriados sempre que o índice clusterizado for alterado. Portanto, mudar de um heap para uma estrutura de índice clusterizado ou vice-versa pode demorar muito e exigir espaço em disco para reorganizar os dados em tempdb.  

## <a name="heap-structures"></a>Estruturas de heap


Heap é uma tabela sem índice clusterizado. Heaps têm uma linha em [sys.partitions](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md), com `index_id = 0` para cada particionamento usado pelo heap. Por padrão, um heap tem um único particionamento. Quando um heap tem particionamentos múltiplos, cada particionamento tem uma estrutura de heap que contém os dados para aquele específico. Por exemplo, se um heap tiver quatro particionamentos, haverá quatro estruturas de heap; uma em cada particionamento.

Dependendo dos tipos de dados no heap, cada estrutura de heap terá uma ou mais unidades de alocação para armazenar e gerenciar os dados de um particionamento específico. No mínimo, cada heap terá uma `IN_ROW_DATA` unidade de alocação por particionamento. O heap também terá uma `LOB_DATA` unidade de alocação por particionamento, caso tenha colunas LOB (objetos grandes). Também terá uma `ROW_OVERFLOW_DATA` unidade de alocação por particionamento, se tiver colunas de comprimento variável excedendo o limite de tamanho de linha de 8.060 bytes.

A coluna `first_iam_page` no modo de exibição do sistema `sys.system_internals_allocation_units` aponta para a primeira página IAM na cadeia de páginas IAM, que gerencia o espaço alocado no heap em uma partição específica. SQL Server usa as páginas IAM para percorrer o heap. As páginas de dados e as linhas dentro delas não estão em nenhuma ordem específica e não estão vinculadas. A única conexão lógica entre as páginas de dados são as informações registradas nas páginas IAM.

> [!IMPORTANT]  
> O modo de exibição do sistema `sys.system_internals_allocation_units` é reservado somente para uso interno do Microsoft SQL Server. A compatibilidade futura não está garantida.
 
Os exames de tabela ou as leituras consecutivas de um heap podem ser executados examinando as páginas IAM para localizar as extensões que estão mantendo páginas do heap. Como o IAM representa extensões na mesma ordem que elas existem nos arquivos de dados, isso significa que esses exames de heap consecutivo progridem sequencialmente em cada arquivo. O uso das páginas IAM para definir a sequência de exame também significa que as linhas do heap não são retornadas normalmente na ordem em que foram inseridas.

A ilustração a seguir mostra como o Mecanismo de Banco de Dados do SQL Server usa páginas IAM para recuperar linhas de dados em um único heap de particionamento. 

![iam_heap](../../relational-databases/indexes/media/iam-heap.gif)

  
## <a name="related-content"></a>Conteúdo relacionado  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
  
 [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)  
  
 [Índices clusterizados e não clusterizados descritos](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)  
  
  
