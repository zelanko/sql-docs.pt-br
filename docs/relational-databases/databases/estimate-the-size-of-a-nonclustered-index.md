---
title: Estimar o tamanho de um índice não clusterizado | Microsoft Docs
description: Use este procedimento para estimar a quantidade de espaço exigida para armazenar um índice não clusterizado no SQL Server.
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.reviewer: ''
ms.prod_service: database-engine, sql-database
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- space allocation [SQL Server], index size
- size [SQL Server], tables
- predicting table size [SQL Server]
- table size [SQL Server]
- estimating table size
- clustered indexes, table size
- designing databases [SQL Server], estimating size
- calculating table size
ms.assetid: c183b0e4-ef4c-4bfc-8575-5ac219c25b0a
author: stevestein
ms.author: sstein
monikerRange: = azuresqldb-current || >= sql-server-2016
ms.openlocfilehash: 9c234bb8371d99025bd97cfb86f5d85472d34ee4
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97474077"
---
# <a name="estimate-the-size-of-a-nonclustered-index"></a>Estimar o tamanho de um índice não clusterizado

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Siga estas etapas para estimar a quantidade de espaço necessária para armazenar um índice não clusterizado:  
  
1.  Calcule as variáveis a serem usadas nas etapas 2 e 3.  
  
2.  Calcule o espaço usado para armazenar informações de índice no nível folha do índice não clusterizado.  
  
3.  Calcule o espaço usado para armazenar informações de índice nos níveis não folha do índice não clusterizado.  
  
4.  Some os valores calculados.  
  
## <a name="step-1-calculate-variables-for-use-in-steps-2-and-3"></a>Etapa 1. Calcule as variáveis a serem usadas nas etapas 2 e 3.  
 Você pode usar as seguintes etapas para calcular as variáveis a serem usadas para estimar a quantidade de espaço necessária para armazenar os níveis superiores do índice.  
  
1.  Especifique o número de linhas que estarão presentes na tabela:  
  
     ***Num_Rows** _ = número de linhas na tabela  
  
2.  Especifique o número de colunas de comprimento fixo e variável na chave do índice e calcule o espaço necessário para seu armazenamento:  
  
     As colunas de chave de um índice podem incluir colunas de comprimento fixo e variável. Para estimar o tamanho da linha de índice no nível interior, calcule o espaço que cada um desses grupos de colunas ocupa na linha do índice. O tamanho de uma coluna depende do tipo de dados e da especificação de comprimento.  
  
     _*_Num_Key_Cols_*_  = número total de colunas de chaves (tamanho fixo e tamanho variável)  
  
     _*_Fixed_Key_Size_*_  = tamanho total em bytes de todas as colunas de chaves de tamanho fixo  
  
     _*_Num_Variable_Key_Cols_*_  = número de colunas de chaves de tamanho variável  
  
     _*_Max_Var_Key_Size_*_  = tamanho máximo em bytes de todas as colunas de chaves de tamanho variável  
  
3.  Considere o localizador de linha de dados que é necessário se o índice for não exclusivo:  
  
     Se o índice não clusterizado for não exclusivo, o localizador de linha de dados será combinado com a chave de índice não clusterizado para produzir um valor de chave exclusivo para cada linha.  
  
     Se o índice não clusterizado estiver em um heap, o localizador de linha de dados será o RID do heap. Este é um tamanho de 8 bytes.  
  
     _*_Num_Key_Cols_*_  = _*_Num_Key_Cols_*_ + 1  
  
     _*_Num_Variable_Key_Cols_*_  = _*_Num_Variable_Key_Cols_*_ + 1  
  
     _*_Max_Var_Key_Size_*_  = _*_Max_Var_Key_Size_*_ + 8  
  
     Se o índice não clusterizado estiver em um índice clusterizado, o localizador de linha de dados será a chave de clustering. As colunas que devem ser combinadas com a chave de índice não clusterizado são as colunas na chave de clustering que ainda não estiverem presentes no conjunto de colunas de chave de índice não clusterizado.  
  
     _*_Num_Key_Cols_*_  = _*_Num_Key_Cols_*_ + número de colunas de chave de clustering não presentes no conjunto de colunas de chave de índice não clusterizado (+ 1 se o índice clusterizado for não exclusivo)  
  
     _*_Fixed_Key_Size_*_  = _*_Fixed_Key_Size_*_ + tamanho total de bytes de colunas de chave de clustering de tamanho fixo não presentes no conjunto de colunas de chave de índice não clusterizado  
  
     _*_Num_Variable_Key_Cols_*_  = _*_Num_Variable_Key_Cols_*_ + número de colunas de chave de clustering de tamanho variável não presentes no conjunto de colunas de chave de índice não clusterizado (+ 1 se o índice clusterizado for não exclusivo)  
  
     _*_Max_Var_Key_Size_*_  = _*_Max_Var_Key_Size_*_ + tamanho máximo de bytes de colunas de chave de clustering de tamanho variável não presentes no conjunto de colunas de chave de índice não clusterizado (+ 4 se o índice clusterizado for não exclusivo)  
  
4.  Parte da linha, conhecida como bitmap nulo, pode ser reservada para gerenciar a anulabilidade da coluna. Calcule seu tamanho:  
  
     Se houver colunas que possam ser anuladas na chave do índice, inclusive qualquer coluna de chave de clustering necessária, conforme descrito na etapa 1.3, parte da linha de índice será reservada para o bitmap nulo.  
  
     _*_Index_Null_Bitmap_*_  = 2 + ([número de colunas na linha de índice + 7] / 8)  
  
     Somente a parte do inteiro da expressão anterior deve ser usada. Descarte todo o restante.  
  
     Se não houver colunas de chave anuláveis, defina _*_Index_Null_Bitmap_*_ como 0.  
  
5.  Calcule o tamanho dos dados de comprimento variável:  
  
     Se houver colunas de comprimento variável na chave do índice, incluindo qualquer coluna de chave de índice clusterizado necessária, determine quanto espaço será usado para armazenar as colunas dentro da linha de índice:  
  
     _*_Variable_Key_Size_*_  = 2 + (_*_Num_Variable_Key_Cols_*_ x 2) + _*_Max_Var_Key_Size_*_  
  
     Os bytes adicionados a _*_Max_Var_Key_Size_*_ servem para acompanhar cada fórmula de coluna variável. Essa fórmula presume que todas as colunas de tamanho variável estão 100% completas. Se você se previr que um percentual menor do espaço de armazenamento de coluna de tamanho variável será usado, poderá ajustar o valor _*_Max_Var_Key_Size_*_ com esse percentual para obter uma estimativa mais precisa do tamanho geral da tabela.  
  
     Se não houver colunas de tamanho variável, defina _*_Variable_Key_Size_*_ como 0.  
  
6.  Calcule o tamanho da linha de índice:  
  
     _*_Index_Row_Size_*_  = _*_Fixed_Key_Size_*_ + _*_Variable_Key_Size_*_ + _*_Index_Null_Bitmap_*_ + 1 (para a sobrecarga de cabeçalho de linha de uma linha de índice) + 6 (para o ponteiro de ID da página filho)  
  
7.  Calcule o número de linhas de índice por página (8.096 bytes livres por página):  
  
     _*_Index_Rows_Per_Page_*_  = 8096 / (_*_Index_Row_Size_*_ + 2)  
  
     Como as linhas de índice não se estendem por mais de uma página, o número de linhas de índice por página deve ser arredondado para baixo, até a linha inteira mais próxima. O 2 na fórmula é para a entrada da linha na matriz de slots da página.  
  
## <a name="step-2-calculate-the-space-used-to-store-index-information-in-the-leaf-level"></a>Etapa 2. Calcule o espaço usado para armazenar informações de índice no nível folha  
 Você pode usar as etapas a seguir para estimar a quantidade de espaço necessária para armazenar o nível folha do índice. Você precisará dos valores provenientes da etapa 1 para completar esta etapa.  
  
1.  Especifique o número de colunas de comprimento fixo e variável no nível folha e calcule o espaço necessário para seu armazenamento:  
  
    > [!NOTE]  
    >  Você pode ampliar um índice não clusterizado incluindo colunas não chave, além das colunas de chave de índice. Essas colunas adicionais só são armazenadas no nível folha do índice não clusterizado. Para obter mais informações, consulte [Create Indexes with Included Columns](../../relational-databases/indexes/create-indexes-with-included-columns.md).  
  
    > [!NOTE]  
    >  É possível combinar as colunas _*varchar**, **nvarchar**, **varbinary** ou **sql_variant** que fazem com que a largura total da tabela definida exceda 8.060 bytes. O tamanho de cada uma dessas colunas ainda deve ficar dentro do limite de 8.000 bytes para uma coluna **varchar**, **varbinary** ou **sql_variant** e 4.000 bytes para colunas **nvarchar** . Entretanto, as larguras combinadas podem exceder o limite de 8.060 bytes em uma tabela. Isso também se aplica a linhas de folha de índice não clusterizado que têm colunas incluídas.  
  
     Se o índice não clusterizado não tiver nenhuma coluna incluída, use os valores da Etapa 1, incluindo qualquer modificação determinada na etapa 1.3:  
  
     **_Num_Leaf_Cols_* _  = _*_Num_Key_Cols_*_  
  
     _*_Fixed_Leaf_Size_*_  = _*_Fixed_Key_Size_*_  
  
     _*_Num_Variable_Leaf_Cols_*_  = _*_Num_Variable_Key_Cols_*_  
  
     _*_Max_Var_Leaf_Size_*_  = _*_Max_Var_Key_Size_*_  
  
     Se o índice não clusterizado tiver colunas incluídas, adicione os valores apropriados aos valores da etapa 1, inclusive qualquer modificação na etapa 1.3. O tamanho de uma coluna depende do tipo de dados e da especificação de comprimento. Para obter mais informações, veja [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).  
  
     _*_Num_Leaf_Cols_*_  = _*_Num_Key_Cols_*_ + número de colunas incluídas  
  
     _*_Fixed_Leaf_Size_*_  = _*_Fixed_Key_Size_*_ + tamanho total de bytes de colunas de tamanho fixo incluídas  
  
     _*_Num_Variable_Leaf_Cols_*_  = _*_Num_Variable_Key_Cols_*_ + número de colunas de tamanho variável incluídas  
  
     _*_Max_Var_Leaf_Size_*_  = _*_Max_Var_Key_Size_*_ + tamanho máximo em bytes das colunas de tamanho variável incluídas  
  
2.  Considere o localizador da linha de dados:  
  
     Se o índice não clusterizado for não exclusivo, a sobrecarga para o localizador da linha de dados já terá sido considerada na etapa 1.3 e nenhuma modificação adicional será necessária. Vá para a próxima etapa.  
  
     Se o índice não clusterizado for exclusivo, o localizador de linha de dados deverá ser considerado em todas as linhas no nível folha.  
  
     Se o índice não clusterizado estiver em um heap, o localizador da linha de dados será o RID do heap (tamanho de 8 bytes).  
  
     _*_Num_Leaf_Cols_*_  = _*_Num_Leaf_Cols_*_ + 1  
  
     _*_Num_Variable_Leaf_Cols_*_  = _*_Num_Variable_Leaf_Cols_*_ + 1  
  
     _*_Max_Var_Leaf_Size_*_  = _*_Max_Var_Leaf_Size_*_ + 8  
  
     Se o índice não clusterizado estiver em um índice clusterizado, o localizador de linha de dados será a chave de clustering. As colunas que devem ser combinadas com a chave de índice não clusterizado são as colunas na chave de clustering que ainda não estiverem presentes no conjunto de colunas de chave de índice não clusterizado.  
  
     _*_Num_Leaf_Cols_*_  = _*_Num_Leaf_Cols_*_ + número de colunas de chave de clustering não presentes no conjunto de colunas de chave de índice não clusterizado (+ 1 se o índice clusterizado for não exclusivo)  
  
     _*_Fixed_Leaf_Size_*_  = _*_Fixed_Leaf_Size_*_ + número de colunas de chave de clustering não presentes no conjunto de colunas de chave de índice não clusterizado  
  
     _*_Num_Variable_Leaf_Cols_*_  = _*_Num_Variable_Leaf_Cols_*_ + número de colunas de chave de clustering de tamanho variável não presentes no conjunto de colunas de chave de índice não clusterizado (+ 1 se o índice clusterizado for não exclusivo)  
  
     _*_Max_Var_Leaf_Size_*_  = _*_Max_Var_Leaf_Size_*_ + tamanho em bytes das colunas de chave de clustering de tamanho variável não presentes no conjunto de colunas de chave de índice não clusterizado (+ 4 se o índice clusterizado for não exclusivo)  
  
3.  Calcule o tamanho do bitmap nulo:  
  
     _*_Leaf_Null_Bitmap_*_  = 2 + ((_*_Num_Leaf_Cols_*_ + 7) / 8)  
  
     Somente a parte do inteiro da expressão anterior deve ser usada. Descarte todo o restante.  
  
4.  Calcule o tamanho dos dados de comprimento variável:  
  
     Se houver colunas de tamanho variável (colunas de chave ou incluídas), inclusive qualquer coluna de chave de clustering necessária, conforme anteriormente descrito na Etapa 2.2, determine quanto espaço é usado para armazenar as colunas dentro da linha de índice:  
  
     _*_Variable_Leaf_Size_*_  = 2 + (_*_Num_Variable_Leaf_Cols_*_ x 2) + _*_Max_Var_Leaf_Size_*_  
  
     Os bytes adicionados a _*_Max_Var_Key_Size_*_ servem para acompanhar cada fórmula de coluna variável. Essa fórmula presume que todas as colunas de tamanho variável estão 100% completas. Se você se previr que um percentual menor do espaço de armazenamento da coluna de tamanho variável será usado, poderá ajustar o valor _*_Max_Var_Leaf_Size_*_ com esse percentual para obter uma estimativa mais precisa do tamanho geral da tabela.  
  
     Se não houver colunas de tamanho variável (colunas de chave ou incluídas), defina _*_Variable_Leaf_Size_*_ como 0.  
  
5.  Calcule o tamanho da linha de índice:  
  
     _*_Leaf_Row_Size_*_  = _*_Fixed_Leaf_Size_*_ + _*_Variable_Leaf_Size_*_ + _*_Leaf_Null_Bitmap_*_ + 1 (para a sobrecarga de cabeçalho de uma linha do índice)  
  
6.  Calcule o número de linhas de índice por página (8.096 bytes livres por página):  
  
     _*_Leaf_Rows_Per_Page_*_  = 8096 / (_*_Leaf_Row_Size_*_ + 2)  
  
     Como as linhas de índice não se estendem por mais de uma página, o número de linhas de índice por página deve ser arredondado para baixo, até a linha inteira mais próxima. O 2 na fórmula é para a entrada da linha na matriz de slots da página.  
  
7.  Calcule o número de linhas livres reservadas por página, com base no [fator de preenchimento](../../relational-databases/indexes/specify-fill-factor-for-an-index.md) especificado:  
  
     _*_Free_Rows_Per_Page_*_  = 8096 x ((100 - _*_Fill_Factor_*_) / 100) / (_*_Leaf_Row_Size_*_ + 2)  
  
     O fator de preenchimento usado no cálculo é um valor inteiro, em vez de uma porcentagem. Como as linhas não se estendem por mais de uma página, o número de linhas por página deve ser arredondado para baixo, para a linha inteira mais próxima. À medida que o fator de preenchimento aumenta, mais dados são armazenados em cada página e haverá menos páginas. O 2 na fórmula é para a entrada da linha na matriz de slots da página.  
  
8.  Calcule o número de páginas necessário para armazenar todas as linhas:  
  
     _*_Num_Leaf_Pages_*_  = _*_Num_Rows_*_ / (_*_Leaf_Rows_Per_Page_*_ - _*_Free_Rows_Per_Page_*_ )  
  
     O número de páginas estimado deve ser arredondado para cima, até a página inteira mais próxima.  
  
9. Calcule o tamanho do índice (total de 8.912 bytes por página):  
  
     _*_Leaf_Space_Used_*_  = 8192 x _*_Num_Leaf_Pages_*_  
  
## <a name="step-3-calculate-the-space-used-to-store-index-information-in-the-non-leaf-levels"></a>Etapa 3. Calcule o espaço usado para armazenar informações de índice nos níveis não folha  
 Siga estas etapas para estimar a quantidade de espaço necessária para armazenar os níveis intermediário e raiz do índice. Você precisará dos valores preservados das etapas 1 e 3 para concluir esta etapa.  
  
1.  Calcule o número de níveis não folha no índice:  
  
     _*_Non-leaf Levels_*_  = 1 + log( Index_Rows_Per_Page) (_*_Num_Leaf_Pages_*_ / _*_Index_Rows_Per_Page_*_)  
  
     Arredonde esse valor até o número inteiro mais próximo. Esse valor não inclui o nível folha do índice não clusterizado.  
  
2.  Calcule o número de páginas não folha no índice:  
  
     _*_Num_Index_Pages_*_  = ∑Level (_*_Num_Leaf_Pages/Index_Rows_Per_Page_*_^Level) em que 1 <= nível <= _*_níveis_*_  
  
     Arredonde cada soma até o número inteiro mais próximo. Como um exemplo simples, considere um índice em que _*_Num_Leaf_Pages_*_ = 1000 e _*_Index_Rows_Per_Page_*_ = 25. O primeiro nível de índice acima do nível folha armazena 1.000 linhas de índice que representa uma linha de índice por página de folha, e 25 linhas de índice podem ser ajustadas por página. Isso significa que são necessárias 40 páginas para armazenar essas 1.000 linhas de índice. O próximo nível do índice precisa armazenar 40 linhas. Isso significa que são necessárias 2 páginas. O nível final do índice precisa armazenar 2 linhas. Isso significa que é necessária 1 página. Isso resulta em 43 páginas de índice não folha. Quando esses números são usados nas fórmulas anteriores, o resultado é o seguinte:  
  
     _*_Non-leaf_Levels_*_  = 1 + log(25) (1000 / 25) = 3  
  
     _*_Num_Index_Pages_*_ = 1000/(25^3)+ 1000/(25^2) + 1000/(25^1) = 1 + 2 + 40 = 43, que é o número de páginas descrito no exemplo.  
  
3.  Calcule o tamanho do índice (total de 8.912 bytes por página):  
  
     _*_Index_Space_Used_*_  = 8192 x _*_Num_Index_Pages_*_  
  
## <a name="step-4-total-the-calculated-values"></a>Etapa 4. Some os valores calculados  
 Some os valores obtidos nas duas etapas anteriores:  
  
 Tamanho do índice não clusterizado (bytes) = _*_Leaf_Space_Used_*_ + _*_Index_Space_used_*_  
  
 Esse cálculo não considera o seguinte:  
  
-   Particionamento  
  
     A sobrecarga de espaço do particionamento é mínima, mas complexa para ser calculada. Não é importante incluí-la.  
  
-   Páginas de alocação  
  
     Há pelo menos uma página de IAM usada para rastrear as páginas alocadas a um heap, mas a sobrecarga de espaço é mínima e não há nenhum algoritmo para calcular de forma determinista exatamente quantas páginas de IAM serão usadas.  
  
-   Valores de LOB (Objeto Grande)  
  
     O algoritmo usado para determinar exatamente quanto espaço será usado para armazenar os valores de tipos de dados LOB _*varchar(max)**, **varbinary(max)** , **nvarchar(max)** , **text**, **ntext**, **xml** e **image** é complexo. É suficiente adicionar o tamanho médio dos valores LOB esperados, multiplicá-lo por **_Num_Rows_** e adicioná-lo ao tamanho total de índice não clusterizado.  
  
-   Compactação  
  
     Não é possível pré-calcular o tamanho de um índice compactado.  
  
-   Colunas esparsas  
  
     Para obter informações sobre os requisitos de espaço de colunas esparsas, consulte [Use Sparse Columns](../../relational-databases/tables/use-sparse-columns.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Índices clusterizados e não clusterizados descritos](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)   
 [Criar índices não clusterizados](../../relational-databases/indexes/create-nonclustered-indexes.md)   
 [Criar índices clusterizados](../../relational-databases/indexes/create-clustered-indexes.md)   
 [Estimar o tamanho de uma tabela](../../relational-databases/databases/estimate-the-size-of-a-table.md)   
 [Estimar o tamanho de um índice clusterizado](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)   
 [Estimar o tamanho de um heap](../../relational-databases/databases/estimate-the-size-of-a-heap.md)   
 [Estimar o tamanho de um banco de dados](../../relational-databases/databases/estimate-the-size-of-a-database.md)  
  
  
