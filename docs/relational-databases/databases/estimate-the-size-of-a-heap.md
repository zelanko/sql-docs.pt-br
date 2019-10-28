---
title: Estimar o tamanho de um heap | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- disk space [SQL Server], indexes
- estimating heap size
- size [SQL Server], heap
- space [SQL Server], indexes
- heaps
ms.assetid: 81fd5ec9-ce0f-4c2c-8ba0-6c483cea6c75
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 58d708811825fe42ca64c7e30f7e9ed0d92e62f3
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909050"
---
# <a name="estimate-the-size-of-a-heap"></a>Estimar o tamanho de um heap
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Você pode usar as seguintes etapas para estimar a quantidade de espaço exigida para armazenar dados em um heap:  
  
1.  Especifique o número de linhas que estarão presentes na tabela:  
  
     **_Num_Rows_** = número de linhas na tabela  
  
2.  Especifique o número de colunas de comprimento fixo e variável e calcule o espaço necessário para o seu armazenamento:  
  
     Calcule o espaço que cada um desses grupos de colunas ocupa dentro da linha de dados. O tamanho de uma coluna depende do tipo de dados e da especificação de comprimento.  
  
     **_Num_Cols_** = número total de colunas (comprimento fixo e tamanho variável)  
  
     **_Fixed_Data_Size_** = tamanho total em bytes de todas as colunas de tamanho fixo  
  
     **_Num_Variable_Cols_** = número de colunas de tamanho variável  
  
     **_Max_Var_Size_** = total máximo em bytes de todas as colunas de tamanho variável  
  
3.  Parte da linha, conhecida como bitmap nulo, é reservada para gerenciar a nulabilidade da coluna. Calcule seu tamanho:  
  
     **_Null_Bitmap_** = 2 + (( **_Num_Cols_** + 7) / 8)  
  
     Somente a parte do inteiro dessa expressão deve ser usada. Descarte todo o restante.  
  
4.  Calcule o tamanho dos dados de comprimento variável:  
  
     Se houver colunas de comprimento variável na tabela, determine quanto espaço será usado para armazenar as colunas dentro da linha:  
  
     **_Variable_Data_Size_** = 2 + ( **_Num_Variable_Cols_** x 2) + **_Max_Var_Size_**  
  
     Os bytes adicionados a **_Max_Var_Size_** servem para acompanhar cada coluna de tamanho variável. Essa fórmula presume que todas as colunas de comprimento variável estão 100% completas. Se você prevê que um percentual menor do espaço de armazenamento da coluna de tamanho variável será usado, pode ajustar o valor **_Max_Var_Size_** de acordo com esse percentual para obter uma estimativa mais precisa do tamanho geral da tabela.  
  
    > [!NOTE]  
    >  É possível combinar colunas **varchar**, **nvarchar**, **varbinary**ou **sql_variant** que fazem com que a largura total da tabela definida exceda 8.060 bytes. O tamanho de cada uma dessas colunas ainda deve ficar dentro do limite de 8.000 bytes para uma coluna **varchar**, **nvarchar, varbinary** ou **sql_variant**. Entretanto, as larguras combinadas podem exceder o limite de 8.060 bytes em uma tabela.  
  
     Se não houver colunas de tamanho variável, defina **_Variable_Data_Size_** como 0.  
  
5.  Calcule o tamanho total da linha:  
  
     **_Row_Size_**   =  **_Fixed_Data_Size_**  +  **_Variable_Data_Size_**  +  **_Null_Bitmap_** + 4  
  
     O valor 4 na fórmula é a sobrecarga do cabeçalho da linha de dados.  
  
6.  Calcule o número de linhas por página (8.096 bytes livres por página):  
  
     **_Rows_Per_Page_** = 8096 / ( **_Row_Size_** + 2)  
  
     Como as linhas não se estendem por mais de uma página, o número de linhas por página deve ser arredondado para baixo, para a linha inteira mais próxima. O valor 2 na fórmula é para a entrada da linha na matriz de slot da página.  
  
7.  Calcule o número de páginas necessário para armazenar todas as linhas:  
  
     **_Num_Pages_**   =  **_Num_Rows_**  /  **_Rows_Per_Page_**  
  
     O número de páginas estimado deve ser arredondado para cima, até a página inteira mais próxima.  
  
8.  Calcule a quantidade de espaço necessária para armazenar os dados no heap (total de 8.192 bytes por página):  

     Tamanho do heap (bytes) = 8192 x **_Num_Pages_**  
  
 Esse cálculo não considera o seguinte:  
  
-   Particionamento  
  
     A sobrecarga de espaço do particionamento é mínima, mas complexa para ser calculada. Não é importante incluí-la.  
  
-   Páginas de alocação  
  
     Há pelo menos uma página de IAM usada para rastrear as páginas alocadas a um heap, mas a sobrecarga de espaço é mínima e não há nenhum algoritmo para calcular de forma determinista exatamente quantas páginas de IAM serão usadas.  
  
-   Valores de LOB (Objeto Grande)  
  
     O algoritmo para determinar exatamente quanto espaço será usado para armazenar os tipos de dados LOB **varchar(max)** , **varbinary(max)** , **nvarchar(max)** , **text**e **ntextxml**e valores **image** é complexo. É suficiente apenas para adicionar o tamanho médio dos valores de LOB esperados e adicioná-lo ao tamanho do heap.  
  
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
  
  
