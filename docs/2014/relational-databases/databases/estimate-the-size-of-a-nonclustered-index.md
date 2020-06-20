---
title: Estimar o tamanho de um índice não clusterizado | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
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
ms.openlocfilehash: 097c0e5568ba17b12f83d09e347eb3bf8b0bd7da
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965963"
---
# <a name="estimate-the-size-of-a-nonclustered-index"></a>Estimar o tamanho de um índice não clusterizado
  Siga estas etapas para estimar a quantidade de espaço necessária para armazenar um índice não clusterizado:  
  
1.  Calcule as variáveis a serem usadas nas etapas 2 e 3.  
  
2.  Calcule o espaço usado para armazenar informações de índice no nível folha do índice não clusterizado.  
  
3.  Calcule o espaço usado para armazenar informações de índice nos níveis não folha do índice não clusterizado.  
  
4.  Some os valores calculados.  
  
## <a name="step-1-calculate-variables-for-use-in-steps-2-and-3"></a>Etapa 1. Calcule as variáveis a serem usadas nas etapas 2 e 3.  
 Você pode usar as seguintes etapas para calcular as variáveis a serem usadas para estimar a quantidade de espaço necessária para armazenar os níveis superiores do índice.  
  
1.  Especifique o número de linhas que estarão presentes na tabela:  
  
     ***Num_Rows***  = número de linhas na tabela  
  
2.  Especifique o número de colunas de comprimento fixo e variável na chave do índice e calcule o espaço necessário para seu armazenamento:  
  
     As colunas de chave de um índice podem incluir colunas de comprimento fixo e variável. Para estimar o tamanho da linha de índice no nível interior, calcule o espaço que cada um desses grupos de colunas ocupa na linha do índice. O tamanho de uma coluna depende do tipo de dados e da especificação de comprimento.  
  
     ***Num_Key_Cols***  = número total de colunas de chaves (tamanho fixo e tamanho variável)  
  
     ***Fixed_Key_Size***  = tamanho total em bytes de todas as colunas de chaves de tamanho fixo  
  
     ***Num_Variable_Key_Cols***  = número de colunas de chaves de tamanho variável  
  
     ***Max_Var_Key_Size***  = tamanho máximo em bytes de todas as colunas de chaves de tamanho variável  
  
3.  Considere o localizador de linha de dados que é necessário se o índice for não exclusivo:  
  
     Se o índice não clusterizado for não exclusivo, o localizador de linha de dados será combinado com a chave de índice não clusterizado para produzir um valor de chave exclusivo para cada linha.  
  
     Se o índice não clusterizado estiver em um heap, o localizador de linha de dados será o RID do heap. Este é um tamanho de 8 bytes.  
  
     ***Num_Key_Cols***  = ***Num_Key_Cols*** + 1  
  
     ***Num_Variable_Key_Cols***  = ***Num_Variable_Key_Cols*** + 1  
  
     ***Max_Var_Key_Size***  = ***Max_Var_Key_Size*** + 8  
  
     Se o índice não clusterizado estiver em um índice clusterizado, o localizador de linha de dados será a chave de clustering. As colunas que devem ser combinadas com a chave de índice não clusterizado são as colunas na chave de clustering que ainda não estiverem presentes no conjunto de colunas de chave de índice não clusterizado.  
  
     ***Num_Key_Cols***  = ***Num_Key_Cols*** + número de colunas de chave de clustering não presentes no conjunto de colunas de chave de índice não clusterizado (+ 1 se o índice clusterizado for não exclusivo)  
  
     ***Fixed_Key_Size***  = ***Fixed_Key_Size*** + tamanho total de bytes de colunas de chave de clustering de tamanho fixo não presentes no conjunto de colunas de chave de índice não clusterizado  
  
     ***Num_Variable_Key_Cols***  = ***Num_Variable_Key_Cols*** + número de colunas de chave de clustering de tamanho variável não presentes no conjunto de colunas de chave de índice não clusterizado (+ 1 se o índice clusterizado for não exclusivo)  
  
     ***Max_Var_Key_Size***  = ***Max_Var_Key_Size*** + tamanho máximo de bytes de colunas de chave de clustering de tamanho variável não presentes no conjunto de colunas de chave de índice não clusterizado (+ 4 se o índice clusterizado for não exclusivo)  
  
4.  Parte da linha, conhecida como bitmap nulo, pode ser reservada para gerenciar a anulabilidade da coluna. Calcule seu tamanho:  
  
     Se houver colunas que possam ser anuladas na chave do índice, inclusive qualquer coluna de chave de clustering necessária, conforme descrito na etapa 1.3, parte da linha de índice será reservada para o bitmap nulo.  
  
     ***Index_Null_Bitmap***  = 2 + ([número de colunas na linha de índice + 7] / 8)  
  
     Somente a parte do inteiro da expressão anterior deve ser usada. Descarte todo o restante.  
  
     Se não houver colunas de chave anuláveis, defina ***Index_Null_Bitmap*** como 0.  
  
5.  Calcule o tamanho dos dados de comprimento variável:  
  
     Se houver colunas de comprimento variável na chave do índice, incluindo qualquer coluna de chave de índice clusterizado necessária, determine quanto espaço será usado para armazenar as colunas dentro da linha de índice:  
  
     ***Variable_Key_Size***  = 2 + (***Num_Variable_Key_Cols*** x 2) + ***Max_Var_Key_Size***  
  
     Os bytes adicionados a ***Max_Var_Key_Size*** servem para acompanhar cada fórmula de coluna variável. Essa fórmula presume que todas as colunas de tamanho variável estão 100% completas. Se você se previr que um percentual menor do espaço de armazenamento de coluna de tamanho variável será usado, poderá ajustar o valor ***Max_Var_Key_Size*** com esse percentual para obter uma estimativa mais precisa do tamanho geral da tabela.  
  
     Se não houver colunas de tamanho variável, defina ***Variable_Key_Size*** como 0.  
  
6.  Calcule o tamanho da linha de índice:  
  
     ***Index_Row_Size***  = ***Fixed_Key_Size*** + ***Variable_Key_Size*** + ***Index_Null_Bitmap*** + 1 (para a sobrecarga de cabeçalho de linha de uma linha de índice) + 6 (para o ponteiro de ID da página filho)  
  
7.  Calcule o número de linhas de índice por página (8.096 bytes livres por página):  
  
     ***Index_Rows_Per_Page***  = 8096 / (***Index_Row_Size*** + 2)  
  
     Como as linhas de índice não se estendem por mais de uma página, o número de linhas de índice por página deve ser arredondado para baixo, até a linha inteira mais próxima. O 2 na fórmula é para a entrada da linha na matriz de slots da página.  
  
## <a name="step-2-calculate-the-space-used-to-store-index-information-in-the-leaf-level"></a>Etapa 2. Calcule o espaço usado para armazenar informações de índice no nível folha  
 Você pode usar as etapas a seguir para estimar a quantidade de espaço necessária para armazenar o nível folha do índice. Você precisará dos valores provenientes da etapa 1 para completar esta etapa.  
  
1.  Especifique o número de colunas de comprimento fixo e variável no nível folha e calcule o espaço necessário para seu armazenamento:  
  
    > [!NOTE]  
    >  Você pode ampliar um índice não clusterizado incluindo colunas não chave, além das colunas de chave de índice. Essas colunas adicionais só são armazenadas no nível folha do índice não clusterizado. Para obter mais informações, consulte [Create Indexes with Included Columns](../indexes/create-indexes-with-included-columns.md).  
  
    > [!NOTE]  
    >  Você pode combinar as colunas `varchar`, `nvarchar`, `varbinary` ou `sql_variant` que fazem com que a largura total definida da tabela exceda 8.060 bytes. O comprimento de cada uma dessas colunas ainda deve ficar dentro do limite de 8.000 bytes para uma coluna `varchar`, `varbinary` ou `sql_variant` e de 4.000 bytes para colunas `nvarchar`. Entretanto, as larguras combinadas podem exceder o limite de 8.060 bytes em uma tabela. Isso também se aplica a linhas de folha de índice não clusterizado que têm colunas incluídas.  
  
     Se o índice não clusterizado não tiver nenhuma coluna incluída, use os valores da Etapa 1, incluindo qualquer modificação determinada na etapa 1.3:  
  
     ***Num_Leaf_Cols***  = ***Num_Key_Cols***  
  
     ***Fixed_Leaf_Size***  = ***Fixed_Key_Size***  
  
     ***Num_Variable_Leaf_Cols***  = ***Num_Variable_Key_Cols***  
  
     ***Max_Var_Leaf_Size***  = ***Max_Var_Key_Size***  
  
     Se o índice não clusterizado tiver colunas incluídas, adicione os valores apropriados aos valores da etapa 1, inclusive qualquer modificação na etapa 1.3. O tamanho de uma coluna depende do tipo de dados e da especificação de comprimento. Para obter mais informações, veja [Tipos de dados &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql).  
  
     ***Num_Leaf_Cols***  = ***Num_Key_Cols*** + número de colunas incluídas  
  
     ***Fixed_Leaf_Size***  = ***Fixed_Key_Size*** + tamanho total de bytes de colunas de tamanho fixo incluídas  
  
     ***Num_Variable_Leaf_Cols***  = ***Num_Variable_Key_Cols*** + número de colunas de tamanho variável incluídas  
  
     ***Max_Var_Leaf_Size***  = ***Max_Var_Key_Size*** + tamanho máximo em bytes das colunas de tamanho variável incluídas  
  
2.  Considere o localizador da linha de dados:  
  
     Se o índice não clusterizado for não exclusivo, a sobrecarga para o localizador da linha de dados já terá sido considerada na etapa 1.3 e nenhuma modificação adicional será necessária. Vá para a próxima etapa.  
  
     Se o índice não clusterizado for exclusivo, o localizador de linha de dados deverá ser considerado em todas as linhas no nível folha.  
  
     Se o índice não clusterizado estiver em um heap, o localizador da linha de dados será o RID do heap (tamanho de 8 bytes).  
  
     ***Num_Leaf_Cols***  = ***Num_Leaf_Cols*** + 1  
  
     ***Num_Variable_Leaf_Cols***  = ***Num_Variable_Leaf_Cols*** + 1  
  
     ***Max_Var_Leaf_Size***  = ***Max_Var_Leaf_Size*** + 8  
  
     Se o índice não clusterizado estiver em um índice clusterizado, o localizador de linha de dados será a chave de clustering. As colunas que devem ser combinadas com a chave de índice não clusterizado são as colunas na chave de clustering que ainda não estiverem presentes no conjunto de colunas de chave de índice não clusterizado.  
  
     ***Num_Leaf_Cols***  = ***Num_Leaf_Cols*** + número de colunas de chave de clustering não presentes no conjunto de colunas de chave de índice não clusterizado (+ 1 se o índice clusterizado for não exclusivo)  
  
     ***Fixed_Leaf_Size***  = ***Fixed_Leaf_Size*** + número de colunas de chave de clustering não presentes no conjunto de colunas de chave de índice não clusterizado  
  
     ***Num_Variable_Leaf_Cols***  = ***Num_Variable_Leaf_Cols*** + número de colunas de chave de clustering de tamanho variável não presentes no conjunto de colunas de chave de índice não clusterizado (+ 1 se o índice clusterizado for não exclusivo)  
  
     ***Max_Var_Leaf_Size***  = ***Max_Var_Leaf_Size*** + tamanho em bytes das colunas de chave de clustering de tamanho variável não presentes no conjunto de colunas de chave de índice não clusterizado (+ 4 se o índice clusterizado for não exclusivo)  
  
3.  Calcule o tamanho do bitmap nulo:  
  
     ***Leaf_Null_Bitmap***  = 2 + ((***Num_Leaf_Cols*** + 7) / 8)  
  
     Somente a parte do inteiro da expressão anterior deve ser usada. Descarte todo o restante.  
  
4.  Calcule o tamanho dos dados de comprimento variável:  
  
     Se houver colunas de comprimento variável na chave de índice, inclusive qualquer coluna de chave de clustering necessária, como anteriormente descrito nas Etapa 2.2, determine quanto espaço é usado para armazenar as colunas dentro da linha de índice:  
  
     ***Variable_Leaf_Size***  = 2 + (***Num_Variable_Leaf_Cols*** x 2) + ***Max_Var_Leaf_Size***  
  
     Os bytes adicionados a ***Max_Var_Key_Size*** servem para acompanhar cada fórmula de coluna variável. Essa fórmula presume que todas as colunas de tamanho variável estão 100% completas. Se você se previr que um percentual menor do espaço de armazenamento da coluna de tamanho variável será usado, poderá ajustar o valor ***Max_Var_Leaf_Size*** com esse percentual para obter uma estimativa mais precisa do tamanho geral da tabela.  
  
     Se não houver colunas de tamanho variável, defina ***Variable_Leaf_Size*** como 0.  
  
5.  Calcule o tamanho da linha de índice:  
  
     ***Leaf_Row_Size***   =  ***Fixed_Leaf_Size***  +  ***Variable_Leaf_Size***  +  ***Leaf_Null_Bitmap*** + 1 (para sobrecarga de cabeçalho de linha de uma linha de índice) + 6 (para o ponteiro de ID de página filho)  
  
6.  Calcule o número de linhas de índice por página (8.096 bytes livres por página):  
  
     ***Leaf_Rows_Per_Page***  = 8.096 / (***Leaf_Row_Size*** + 2)  
  
     Como as linhas de índice não se estendem por mais de uma página, o número de linhas de índice por página deve ser arredondado para baixo, até a linha inteira mais próxima. O 2 na fórmula é para a entrada da linha na matriz de slots da página.  
  
7.  Calcule o número de linhas livres reservadas por página, com base no [fator de preenchimento](../indexes/specify-fill-factor-for-an-index.md) especificado:  
  
     ***Free_Rows_Per_Page***  = 8.096 x ([100 - ***Fill_Factor***] / 100) / (***Leaf_Row_Size*** + 2)  
  
     O fator de preenchimento usado no cálculo é um valor inteiro, em vez de uma porcentagem. Como as linhas não se estendem por mais de uma página, o número de linhas por página deve ser arredondado para baixo, para a linha inteira mais próxima. À medida que o fator de preenchimento aumenta, mais dados são armazenados em cada página e haverá menos páginas. O 2 na fórmula é para a entrada da linha na matriz de slots da página.  
  
8.  Calcule o número de páginas necessário para armazenar todas as linhas:  
  
     ***Num_Leaf_Pages***  = ***Num_Rows*** / (***Leaf_Rows_Per_Page*** - ***Free_Rows_Per_Page***)  
  
     O número de páginas estimado deve ser arredondado para cima, até a página inteira mais próxima.  
  
9. Calcule o tamanho do índice (total de 8.912 bytes por página):  
  
     ***Leaf_Space_Used***  = 8192 x ***Num_Leaf_Pages***  
  
## <a name="step-3-calculate-the-space-used-to-store-index-information-in-the-non-leaf-levels"></a>Etapa 3. Calcule o espaço usado para armazenar informações de índice nos níveis não folha  
 Siga estas etapas para estimar a quantidade de espaço necessária para armazenar os níveis intermediário e raiz do índice. Você precisará dos valores preservados das etapas 1 e 3 para concluir esta etapa.  
  
1.  Calcule o número de níveis não folha no índice:  
  
     ***Níveis não folha*** = 1 + Index_Rows_Per_Page de log (***Num_Leaf_Pages***  /  ***Index_Rows_Per_Page***)  
  
     Arredonde esse valor até o número inteiro mais próximo. Esse valor não inclui o nível folha do índice não clusterizado.  
  
2.  Calcule o número de páginas não folha no índice:  
  
     ***Num_Index_Pages*** = nível de ∑ (***Num_Leaf_Pages/***<sup>nível</sup>de Index_Rows_Per_Page) em que 1 <= nível <= ***níveis***  
  
     Arredonde cada soma até o número inteiro mais próximo. Como um exemplo simples, considere um índice em que ***Num_Leaf_Pages*** = 1000 e ***Index_Rows_Per_Page*** = 25. O primeiro nível de índice acima do nível folha armazena 1.000 linhas de índice que representa uma linha de índice por página de folha, e 25 linhas de índice podem ser ajustadas por página. Isso significa que são necessárias 40 páginas para armazenar essas 1.000 linhas de índice. O próximo nível do índice precisa armazenar 40 linhas. Isso significa que são necessárias 2 páginas. O nível final do índice precisa armazenar 2 linhas. Isso significa que é necessária 1 página. Isso resulta em 43 páginas de índice não folha. Quando esses números são usados nas fórmulas anteriores, o resultado é o seguinte:  
  
     ***Não leaf_Levels*** = 1 + log25 (1000/25) = 3  
  
     ***Num_Index_Pages*** = 1000/(25<sup>3</sup>) + 1000/(25<sup>2</sup>) + 1000/(25<sup>1</sup>) = 1 + 2 + 40 = 43, que é o número de páginas descritas no exemplo.  
  
3.  Calcule o tamanho do índice (total de 8.912 bytes por página):  
  
     ***Index_Space_Used***  = 8192 x ***Num_Index_Pages***  
  
## <a name="step-4-total-the-calculated-values"></a>Etapa 4. Some os valores calculados  
 Some os valores obtidos nas duas etapas anteriores:  
  
 Tamanho do índice não clusterizado (bytes) = ***Leaf_Space_Used*** + ***Index_Space_used***  
  
 Esse cálculo não considera o seguinte:  
  
-   Particionamento  
  
     A sobrecarga de espaço do particionamento é mínima, mas complexa para ser calculada. Não é importante incluí-la.  
  
-   Páginas de alocação  
  
     Há pelo menos uma página de IAM usada para rastrear as páginas alocadas a um heap, mas a sobrecarga de espaço é mínima e não há nenhum algoritmo para calcular de forma determinista exatamente quantas páginas de IAM serão usadas.  
  
-   Valores de LOB (Objeto Grande)  
  
     O algoritmo para determinar exatamente quanto espaço será usado armazenar os valores `varchar(max)`, `varbinary(max)`, `nvarchar(max)`, `text`, `ntext`, `xml` e `image` dos tipos de dados LOB é complexo. É suficiente adicionar o tamanho médio dos valores LOB esperados, multiplicá-lo por ***Num_Rows***e adicioná-lo ao tamanho total de índice não clusterizado.  
  
-   Compactação  
  
     Não é possível pré-calcular o tamanho de um índice compactado.  
  
-   Colunas esparsas  
  
     Para obter informações sobre os requisitos de espaço de colunas esparsas, consulte [Use Sparse Columns](../tables/use-sparse-columns.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Índices clusterizados e não clusterizados descritos](../indexes/clustered-and-nonclustered-indexes-described.md)   
 [Criar índices não clusterizados](../indexes/create-nonclustered-indexes.md)   
 [Criar índices clusterizados](../indexes/create-clustered-indexes.md)   
 [Estimar o tamanho de uma tabela](estimate-the-size-of-a-table.md)   
 [Estimar o tamanho de um índice clusterizado](estimate-the-size-of-a-clustered-index.md)   
 [Estimar o tamanho de um heap](estimate-the-size-of-a-heap.md)   
 [Estimar o tamanho de um banco de dados](estimate-the-size-of-a-database.md)  
  
  
