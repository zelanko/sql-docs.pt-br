---
title: Estimar o tamanho de um heap | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: databases
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- disk space [SQL Server], indexes
- estimating heap size
- size [SQL Server], heap
- space [SQL Server], indexes
- heaps
ms.assetid: 81fd5ec9-ce0f-4c2c-8ba0-6c483cea6c75
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d36c98bc94a3f2b83c87526bb6de10f83b0f3f06
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43109109"
---
# <a name="estimate-the-size-of-a-heap"></a>Estimar o tamanho de um heap
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Você pode usar as seguintes etapas para estimar a quantidade de espaço exigida para armazenar dados em um heap:  
  
1.  Especifique o número de linhas que estarão presentes na tabela:  
  
     ***Num_Rows***  = número de linhas na tabela  
  
2.  Especifique o número de colunas de comprimento fixo e variável e calcule o espaço necessário para o seu armazenamento:  
  
     Calcule o espaço que cada um desses grupos de colunas ocupa dentro da linha de dados. O tamanho de uma coluna depende do tipo de dados e da especificação de comprimento.  
  
     ***Num_Cols***  = número total de colunas (comprimento fixo e tamanho variável)  
  
     ***Fixed_Data_Size***  = tamanho total em bytes de todas as colunas de tamanho fixo  
  
     ***Num_Variable_Cols***  = número de colunas de tamanho variável  
  
     ***Max_Var_Size***  = total máximo em bytes de todas as colunas de tamanho variável  
  
3.  Parte da linha, conhecida como bitmap nulo, é reservada para gerenciar a nulabilidade da coluna. Calcule seu tamanho:  
  
     ***Null_Bitmap***  = 2 + ((***Num_Cols*** + 7) / 8)  
  
     Somente a parte do inteiro dessa expressão deve ser usada. Descarte todo o restante.  
  
4.  Calcule o tamanho dos dados de comprimento variável:  
  
     Se houver colunas de comprimento variável na tabela, determine quanto espaço será usado para armazenar as colunas dentro da linha:  
  
     ***Variable_Data_Size***  = 2 + (***Num_Variable_Cols*** x 2) + ***Max_Var_Size***  
  
     Os bytes adicionados a ***Max_Var_Size*** servem para acompanhar cada coluna de tamanho variável. Essa fórmula presume que todas as colunas de comprimento variável estão 100% completas. Se você prevê que um percentual menor do espaço de armazenamento da coluna de tamanho variável será usada, poderá ajustar o valor ***Max_Var_Size*** de acordo com esse percentual para obter uma estimativa mais precisa do tamanho geral da tabela.  
  
    > [!NOTE]  
    >  É possível combinar colunas **varchar**, **nvarchar**, **varbinary**ou **sql_variant** que fazem com que a largura total da tabela definida exceda 8.060 bytes. O tamanho de cada uma dessas colunas ainda deve ficar dentro do limite de 8.000 bytes para uma coluna **varchar**, **nvarchar,****varbinary**ou **sql_variant** . Entretanto, as larguras combinadas podem exceder o limite de 8.060 bytes em uma tabela.  
  
     Se não houver colunas de tamanho variável, defina ***Variable_Data_Size*** como 0.  
  
5.  Calcule o tamanho total da linha:  
  
     ***Row_Size***  = ***Fixed_Data_Size*** + ***Variable_Data_Size*** + ***Null_Bitmap*** + 4  
  
     O valor 4 na fórmula é a sobrecarga do cabeçalho da linha de dados.  
  
6.  Calcule o número de linhas por página (8.096 bytes livres por página):  
  
     ***Rows_Per_Page***  = 8096 / (***Row_Size*** + 2)  
  
     Como as linhas não se estendem por mais de uma página, o número de linhas por página deve ser arredondado para baixo, para a linha inteira mais próxima. O valor 2 na fórmula é para a entrada da linha na matriz de slot da página.  
  
7.  Calcule o número de páginas necessário para armazenar todas as linhas:  
  
     ***Num_Pages***  = ***Num_Rows*** / ***Rows_Per_Page***  
  
     O número de páginas estimado deve ser arredondado para cima, até a página inteira mais próxima.  
  
8.  Calcule a quantidade de espaço necessária para armazenar os dados no heap (total de 8.192 bytes por página):  
  
     Tamanho do heap (bytes) = 8192 x ***Num_Pages***  
  
 Esse cálculo não considera o seguinte:  
  
-   Particionamento  
  
     A sobrecarga de espaço do particionamento é mínima, mas complexa para ser calculada. Não é importante incluí-la.  
  
-   Páginas de alocação  
  
     Há pelo menos uma página de IAM usada para rastrear as páginas alocadas a um heap, mas a sobrecarga de espaço é mínima e não há nenhum algoritmo para calcular de forma determinista exatamente quantas páginas de IAM serão usadas.  
  
-   Valores de LOB (Objeto Grande)  
  
     O algoritmo para determinar exatamente quanto espaço será usado para armazenar os tipos de dados LOB **varchar(max)**, **varbinary(max)**, **nvarchar(max)**, **text**e **ntextxml**e valores **image** é complexo. É suficiente apenas para adicionar o tamanho médio dos valores de LOB esperados e adicioná-lo ao tamanho do heap.  
  
-   Compactação  
  
     Não é possível pré-calcular o tamanho de um heap compactado.  
  
-   Colunas esparsas  
  
     Para obter informações sobre os requisitos de espaço de colunas esparsas, consulte [Use Sparse Columns](../../relational-databases/tables/use-sparse-columns.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Heaps &#40;Tabelas sem índices clusterizados&#41;](../../relational-databases/indexes/heaps-tables-without-clustered-indexes.md)   
 [Índices clusterizados e não clusterizados descritos](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)   
 [Criar índices clusterizados](../../relational-databases/indexes/create-clustered-indexes.md)   
 [Criar índices não clusterizados](../../relational-databases/indexes/create-nonclustered-indexes.md)   
 [Estimar o tamanho de uma tabela](../../relational-databases/databases/estimate-the-size-of-a-table.md)   
 [Estimar o tamanho de um índice clusterizado](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)   
 [Estimar o tamanho de um índice não clusterizado](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)   
 [Estimar o tamanho de um banco de dados](../../relational-databases/databases/estimate-the-size-of-a-database.md)  
  
  
