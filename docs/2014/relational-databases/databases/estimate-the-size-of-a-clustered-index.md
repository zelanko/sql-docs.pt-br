---
title: Estimar o tamanho de um índice clusterizado | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- space allocation [SQL Server], index size
- size [SQL Server], tables
- disk space [SQL Server], indexes
- predicting table size [SQL Server]
- table size [SQL Server]
- estimating table size
- space [SQL Server], indexes
- clustered indexes, table size
- nonclustered indexes [SQL Server], table size
- designing databases [SQL Server], estimating size
- calculating table size
ms.assetid: 2b5137f8-98ad-46b5-9aae-4c980259bf8d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fe7b988590de54a3cb02aa540b244e1f56f3ba24
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66054133"
---
# <a name="estimate-the-size-of-a-clustered-index"></a>Estimar o tamanho de um índice clusterizado
  Você pode usar as seguintes etapas para estimar a quantidade de espaço exigida para armazenar dados em um índice clusterizado:  
  
1.  Calcule o espaço usado para armazenar dados no nível folha do índice clusterizado.  
  
2.  Calcule o espaço usado para armazenar as informações de índice para o índice clusterizado.  
  
3.  Some os valores calculados.  
  
## <a name="step-1-calculate-the-space-used-to-store-data-in-the-leaf-level"></a>Etapa 1. Calcular o espaço usado para armazenar dados no nível folha  
  
1.  Especifique o número de linhas que estarão presentes na tabela:  
  
     ***Num_Rows***  = número de linhas na tabela  
  
2.  Especifique o número de colunas de comprimento fixo e variável e calcule o espaço necessário para o seu armazenamento:  
  
     Calcule o espaço que cada um desses grupos de colunas ocupa dentro da linha de dados. O tamanho de uma coluna depende do tipo de dados e da especificação de comprimento.  
  
     ***Num_Cols***  = número total de colunas (comprimento fixo e tamanho variável)  
  
     ***Fixed_Data_Size***  = tamanho total em bytes de todas as colunas de tamanho fixo  
  
     ***Num_Variable_Cols***  = número de colunas de tamanho variável  
  
     ***Max_Var_Size***  = tamanho máximo em bytes de todas as colunas de comprimento variável  
  
3.  Se o índice clusterizado for do tipo não exclusivo, explique a coluna do *indicador de exclusividade* :  
  
     O identificador de exclusividade é uma coluna de comprimento variável que permite valor nulo. Ele será não nulo e terá 4 bytes de tamanho em linhas com valores de chave não exclusivos. Esse valor faz parte da chave de índice e é necessário para garantir que cada linha tenha um valor de chave exclusivo.  
  
     ***Num_Cols***  = ***Num_Cols*** + 1  
  
     ***Num_Variable_Cols***  = ***Num_Variable_Cols*** + 1  
  
     ***Max_Var_Size***  = ***Max_Var_Size*** + 4  
  
     Essas modificações assumem que todos os valores serão do tipo não exclusivo.  
  
4.  Parte da linha, conhecida como bitmap nulo, é reservada para gerenciar a nulabilidade da coluna. Calcule seu tamanho:  
  
     ***Null_Bitmap***  = 2 + ((***Num_Cols*** + 7) / 8)  
  
     Somente a parte de inteiro da expressão anterior deve ser usada; descarte todo o restante.  
  
5.  Calcule o tamanho dos dados de comprimento variável:  
  
     Se houver colunas de comprimento variável na tabela, determine quanto espaço será usado para armazenar as colunas dentro da linha:  
  
     ***Variable_Data_Size***  = 2 + (***Num_Variable_Cols*** x 2) + ***Max_Var_Size***  
  
     Os bytes adicionados a ***Max_Var_Size*** são para acompanhar cada coluna de variáveis. Essa fórmula presume que todas as colunas de comprimento variável estão 100% completas. Se você prevê que um percentual menor do espaço de armazenamento da coluna de tamanho variável será usada, poderá ajustar o valor ***Max_Var_Size*** de acordo com esse percentual para obter uma estimativa mais precisa do tamanho geral da tabela.  
  
    > [!NOTE]  
    >  Você pode combinar as colunas `varchar`, `nvarchar`, `varbinary` ou `sql_variant` que fazem com que a largura total definida da tabela exceda 8.060 bytes. O comprimento de cada uma dessas colunas ainda deve ficar dentro do limite de 8.000 bytes para uma coluna `varchar`, `varbinary` ou `sql_variant` e de 4.000 bytes para colunas `nvarchar`. Entretanto, as larguras combinadas podem exceder o limite de 8.060 bytes em uma tabela.  
  
     Se não houver colunas de tamanho variável, defina ***Variable_Data_Size*** como 0.  
  
6.  Calcule o tamanho total da linha:  
  
     ***Row_Size***  = ***Fixed_Data_Size*** + ***Variable_Data_Size*** + ***Null_Bitmap*** + 4  
  
     O valor 4 é a sobrecarga de cabeçalho de uma linha de dados.  
  
7.  Calcule o número de linhas por página (8.096 bytes livres por página):  
  
     ***Rows_Per_Page***  = 8096 / (***Row_Size*** + 2)  
  
     Como as linhas não se estendem por mais de uma página, o número de linhas por página deve ser arredondado para baixo, para a linha inteira mais próxima. O valor 2 na fórmula é para a entrada da linha na matriz de slot da página.  
  
8.  Calcule o número de linhas livres reservadas por página, com base no [fator de preenchimento](../indexes/specify-fill-factor-for-an-index.md) especificado:  
  
     ***Free_Rows_Per_Page***  = 8096 x ((100 - ***Fill_Factor***) / 100) / (***Row_Size*** + 2)  
  
     O fator de preenchimento usado no cálculo é um valor inteiro, em vez de uma porcentagem. Como as linhas não se estendem por mais de uma página, o número de linhas por página deve ser arredondado para baixo, para a linha inteira mais próxima. À medida que o fator de preenchimento aumenta, mais dados são armazenados em cada página e haverá menos páginas. O valor 2 na fórmula é para a entrada da linha na matriz de slot da página.  
  
9. Calcule o número de páginas necessário para armazenar todas as linhas:  
  
     ***Num_Leaf_Pages***  = ***Num_Rows*** / (***Rows_Per_Page*** - ***Free_Rows_Per_Page***)  
  
     O número de páginas estimado deve ser arredondado para cima, até a página inteira mais próxima.  
  
10. Calcule a quantidade de espaço necessária para armazenar os dados no nível folha (total de 8.192 bytes por página):  
  
     ***Leaf_space_used***  = 8192 x ***Num_Leaf_Pages***  
  
## <a name="step-2-calculate-the-space-used-to-store-index-information"></a>Etapa 2. Calcular o espaço usado para armazenar as informações de índice  
 Você pode usar as seguintes etapas para estimar a quantidade de espaço necessária para armazenar os níveis superiores do índice:  
  
1.  Especifique o número de colunas de comprimento fixo e variável na chave do índice e calcule o espaço necessário para seu armazenamento:  
  
     As colunas de chave de um índice podem incluir colunas de comprimento fixo e variável. Para estimar o tamanho da linha de índice no nível interior, calcule o espaço que cada um desses grupos de colunas ocupa na linha do índice. O tamanho de uma coluna depende do tipo de dados e da especificação de comprimento.  
  
     ***Num_Key_Cols***  = número total de colunas de chaves (tamanho fixo e tamanho variável)  
  
     ***Fixed_Key_Size***  = tamanho total em bytes de todas as colunas de chaves de tamanho fixo  
  
     ***Num_Variable_Key_Cols***  = número de colunas de chaves de tamanho variável  
  
     ***Max_Var_Key_Size***  = tamanho máximo em bytes de todas as colunas de chaves de tamanho variável  
  
2.  Explique qualquer indicador de exclusividade, caso o índice seja do tipo não exclusivo:  
  
     O identificador de exclusividade é uma coluna de comprimento variável que permite valor nulo. Ele será não nulo e com 4 bytes de tamanho em linhas com valores de chave não exclusivos. Esse valor faz parte da chave de índice e é necessário para garantir que cada linha tenha um valor de chave exclusivo.  
  
     ***Num_Key_Cols***  = ***Num_Key_Cols*** + 1  
  
     ***Num_Variable_Key_Cols***  = ***Num_Variable_Key_Cols*** + 1  
  
     ***Max_Var_Key_Size***  = ***Max_Var_Key_Size*** + 4  
  
     Essas modificações assumem que todos os valores serão do tipo não exclusivo.  
  
3.  Calcule o tamanho do bitmap nulo:  
  
     Se houver colunas que permitem valor nulo na chave de índice, parte da linha do índice será reservada para o bitmap nulo. Calcule seu tamanho:  
  
     ***Index_Null_Bitmap***  = 2 + ([número de colunas na linha de índice + 7] / 8)  
  
     Somente a parte do inteiro da expressão anterior deve ser usada. Descarte todo o restante.  
  
     Se não houver colunas de chave anuláveis, defina ***Index_Null_Bitmap*** como 0.  
  
4.  Calcule o tamanho dos dados de comprimento variável:  
  
     Se houver colunas de comprimento variável no índice, determine quanto espaço será usado para armazenar as colunas dentro da linha do índice:  
  
     ***Variable_Key_Size***  = 2 + (***Num_Variable_Key_Cols*** x 2) + ***Max_Var_Key_Size***  
  
     Os bytes adicionados a ***Max_Var_Key_Size*** são para acompanhamento de cada coluna de comprimento variável. Essa fórmula presume que todas as colunas de comprimento variável estão 100% completas. Se você se previr que um percentual menor do espaço de armazenamento de coluna de tamanho variável será usado, poderá ajustar o valor ***Max_Var_Key_Size*** com esse percentual para obter uma estimativa mais precisa do tamanho geral da tabela.  
  
     Se não houver colunas de tamanho variável, defina ***Variable_Key_Size*** como 0.  
  
5.  Calcule o tamanho da linha de índice:  
  
     ***Index_Row_Size***  = ***Fixed_Key_Size*** + ***Variable_Key_Size*** + ***Index_Null_Bitmap*** + 1 (para a sobrecarga de cabeçalho de linha de uma linha de índice) + 6 (para o ponteiro de ID da página filho)  
  
6.  Calcule o número de linhas de índice por página (8.096 bytes livres por página):  
  
     ***Index_Rows_Per_Page***  = 8096 / (***Index_Row_Size*** + 2)  
  
     Como as linhas de índice não se estendem por mais de uma página, o número de linhas de índice por página deve ser arredondado para baixo, até a linha inteira mais próxima. O 2 na fórmula é para a entrada da linha na matriz de slots da página.  
  
7.  Calcule o número de níveis no índice:  
  
     ***Non-leaf Levels*** = 1 + log Index_Rows_Per_Page (***Num_Leaf_Pages*** / ***Index_Rows_Per_Page***)  
  
     Arredonde esse valor até o número inteiro mais próximo. Esse valor não inclui o nível folha do índice clusterizado.  
  
8.  Calcule o número de páginas não folha no índice:  
  
     ***Num_Index_Pages =*** ∑ Level ***(Num_Leaf_Pages / (Index_Rows_Per_Page***<sup>nível</sup>***))***  
  
     em que 1 <= Level <= ***Non-leaf_Levels***  
  
     Arredonde cada soma até o número inteiro mais próximo. Como um exemplo simples, considere um índice em que ***Num_Leaf_Pages*** = 1000 e ***Index_Rows_Per_Page*** = 25. O primeiro nível de índice acima do nível folha armazena 1.000 linhas de índice que representa uma linha de índice por página de folha, e 25 linhas de índice podem ser ajustadas por página. Isso significa que são necessárias 40 páginas para armazenar essas 1.000 linhas de índice. O próximo nível do índice precisa armazenar 40 linhas. Isso significa que são necessárias 2 páginas. O nível final do índice precisa armazenar 2 linhas. Isso significa que é necessária 1 página. Isso resulta em 43 páginas de índice não folha. Quando esses números são usados nas fórmulas anteriores, o resultado é o seguinte:  
  
     ***Non-leaf_Levels***  = 1 + log25 (1000 / 25) = 3  
  
     ***Num_Index_Pages*** = 1000 /(25<sup>3</sup>) + 1000 / (25<sup>2</sup>) + 1000 / (25<sup>1</sup>) = 1 + 2 + 40 = 43, que é o número de páginas descrito no exemplo.  
  
9. Calcule o tamanho do índice (total de 8.912 bytes por página):  
  
     ***Index_Space_Used***  = 8192 x ***Num_Index_Pages***  
  
## <a name="step-3-total-the-calculated-values"></a>Etapa 3. Some os valores calculados  
 Some os valores obtidos nas duas etapas anteriores:  
  
 Tamanho do índice clusterizado (bytes) = ***Leaf_Space_Used*** + ***Index_Space_used***  
  
 Esse cálculo não considera o seguinte:  
  
-   Particionamento  
  
     A sobrecarga de espaço do particionamento é mínima, mas complexa para ser calculada. Não é importante incluí-la.  
  
-   Páginas de alocação  
  
     Há pelo menos uma página de IAM usada para rastrear as páginas alocadas a um heap, mas a sobrecarga de espaço é mínima e não há nenhum algoritmo para calcular de forma determinista exatamente quantas páginas de IAM serão usadas.  
  
-   Valores de LOB (Objeto Grande)  
  
     O algoritmo para determinar exatamente quanto espaço será usado armazenar os valores `varchar(max)`, `varbinary(max)`, `nvarchar(max)`, `text`, `ntext`, `xml` e `image` dos tipos de dados LOB é complexo. É suficiente adicionar o tamanho médio dos valores LOB esperados, multiplicá-lo por ***Num_Rows***e adicioná-lo ao tamanho total de índice clusterizado.  
  
-   Compactação  
  
     Não é possível pré-calcular o tamanho de um índice compactado.  
  
-   Colunas esparsas  
  
     Para obter informações sobre os requisitos de espaço de colunas esparsas, consulte [Use Sparse Columns](../tables/use-sparse-columns.md).  
  
## <a name="see-also"></a>Consulte também  
 [Índices clusterizados e não clusterizados descritos](../indexes/clustered-and-nonclustered-indexes-described.md)   
 [Estimar o tamanho de uma tabela](estimate-the-size-of-a-table.md)   
 [Criar índices clusterizados](../indexes/create-clustered-indexes.md)   
 [Criar índices não clusterizados](../indexes/create-nonclustered-indexes.md)   
 [Estimar o tamanho de um índice não clusterizado](estimate-the-size-of-a-nonclustered-index.md)   
 [Estimar o tamanho de um heap](estimate-the-size-of-a-heap.md)   
 [Estimar o tamanho de um banco de dados](estimate-the-size-of-a-database.md)  
  
  
