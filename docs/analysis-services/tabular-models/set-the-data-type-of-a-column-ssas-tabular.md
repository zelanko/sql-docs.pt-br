---
title: Defina o tipo de dados de uma coluna (SSAS Tabular) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 34e2d508-7b64-4503-a4f0-c6c6ad5f8a44
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 770ce419a167c71914334ea6fa1b3fd397566b34
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="set-the-data-type-of-a-column-ssas-tabular"></a>Definir o tipo de dados de uma coluna (SSAS tabular)
  Quando você importa ou cola dados em um modelo, o designer de modelo detectará automaticamente e aplicará os tipos dos dados. Depois que adicionar dados ao modelo, você poderá modificar manualmente o tipo de dados de uma coluna para alterar o modo como os dados são armazenados. Se você deseja apenas alterar o formato de exibição dos dados sem alterar o modo como são armazenados, faça isso.  
  
### <a name="to-change-the-data-type-or-display-format-for-a-column"></a>Para alterar o tipo de dados ou o formato de exibição de uma coluna  
  
1.  No designer de modelo, selecione a coluna cujo tipo de dados ou formato de exibição você deseja alterar.  
  
2.  Na janela **Propriedades** da coluna, siga um destes procedimentos:  
  
    -   Na propriedade **Formato de Dados** , selecione um formato de dados diferente.  
  
    -   Na propriedade **Tipo de Dados** , selecione um tipo de dados diferente.  
  
## <a name="considerations-when-changing-data-types"></a>Considerações sobre quando alterar os tipos de dados  
 Às vezes, quando você tenta alterar o tipo de dados de uma coluna ou selecionar uma conversão de dados, um destes erros pode ocorrer:  
  
-   Falha ao alterar o tipo de dados  
  
-   Falha ao alterar o tipo de dados de coluna  
  
 Esses erros podem ocorrer até mesmo se o tipo de dados estiver disponível como uma opção na lista suspensa Tipo de dados. Esta seção explica a causa desses erros e como corrigi-los.  
  
### <a name="understanding-automatically-determined-data-types"></a>Entendendo tipos de dados determinados automaticamente  
 Quando você adicionar dados em um modelo, o designer de modelo verificará as colunas de dados para saber quais tipos de dados contém cada coluna. Se os dados dessa coluna estiverem consistentes, o tipo de dados mais preciso será atribuído à coluna.  
  
 No entanto, se você adicionar dados do Excel ou de outra fonte que não imponha o uso de um tipo de dados único em cada coluna, o designer de modelo atribuirá um tipo de dados que acomode todos os valores na coluna. Portanto, se uma coluna contiver números de tipos diferentes, como inteiros, números longos e moeda, o designer de modelo usará um tipo de dados decimal. Como alternativa, se uma coluna misturar números e texto, o designer de modelo usará o tipo de dados de texto. O designer modelo não fornece um tipo de dados semelhante ao tipo de dados Geral disponível no Excel.  
  
 Portanto, se uma coluna contiver números e valores de texto, você não poderá converter a coluna em um tipo de dados numérico.  
  
 Os tipos de dados a seguir estão disponíveis em modelos de semântica de business intelligence:  
  
-   **Texto**  
  
-   **Número Decimal**  
  
-   **Número Inteiro**  
  
-   **Moeda**  
  
-   **TRUE/FALSE**  
  
-   **Data**  
  
 Caso descubra que seus dados têm um tipo de dados errado ou, pelo menos, um tipo diferente do desejado, você terá várias opções:  
  
-   Você pode importar os dados novamente. Para fazer isso, abra a conexão existente com a fonte de dados e importe a coluna novamente. Dependendo do tipo de fonte de dados, você poderá aplicar um filtro durante a importação para remover valores com problema.  
  
-   Você pode criar uma fórmula do DAX em uma coluna calculada para criar um novo valor do tipo de dados desejado. Por exemplo, a função TRUNC pode ser usada para transformar um número decimal em um inteiro ou você pode combinar funções de informações e funções lógicas para testar e converter valores.  
  
### <a name="understanding-data-conversion"></a>Noções básicas sobre a conversão de dados  
 Se ocorrer um erro quando você selecionar uma opção de conversão de dados, talvez o tipo de dados atual da coluna não ofereça suporte à conversão selecionada. Nem todas as conversões são permitidas para todos os tipos de dados. Por exemplo, você só pode alterar uma coluna para um tipo de dados Booliano se o tipo de dados atual da coluna for um número (inteiro ou decimal) ou texto. Portanto, você deve escolher um tipo de dados apropriado para os dados da coluna.  
  
 Depois que você escolher um tipo de dados apropriado, o designer de modelo avisará sobre possíveis alterações nos dados, como truncamento ou imprecisão. Clique em OK para aceitar e alterar os dados para o novo tipo de dados.  
  
 Se houver suporte para tipo de dados, mas o designer de modelo encontrar valores sem suporte no novo tipo de dados, você receberá outro erro e precisará corrigir os valores de dados antes de continuar.  
  
 Para obter informações detalhadas sobre os tipos de dados usados em modelos semânticos de business intelligence, como eles são convertidos implicitamente e como tipos de dados diferentes são usados em fórmulas, consulte [Tipos de dados com suporte &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/data-types-supported-ssas-tabular.md).  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados com suporte &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/data-types-supported-ssas-tabular.md)  
  
  
