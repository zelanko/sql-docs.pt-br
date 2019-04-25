---
title: Criar uma coluna calculada no Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 705428d2c2a6671452a1d95e06e500f4860574e0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62472298"
---
# <a name="create-a-calculated-column"></a>Criar uma coluna calculada
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Colunas calculadas permitem adicionar novos dados a seu modelo. Em vez de colar ou importar valores na coluna, você deve criar uma fórmula DAX que define os valores de nível de linha da coluna. Os valores em cada linha de uma coluna calculada são calculados e preenchidos quando você cria uma fórmula válida e, em seguida, clica em ENTER. A coluna calculada pode ser então adicionada a um relatório ou aplicativo de análise da mesma maneira que qualquer outra coluna de dados. Este artigo descreve como criar uma nova coluna calculada usando a barra de fórmulas DAX no designer de modelo.  
  
#### <a name="to-create-a-new-calculated-column"></a>Para criar uma nova coluna calculada  
  
1.  No designer de modelo, na Exibição de Dados, selecione a tabela à qual você quer adicionar uma coluna calculada, clique no menu **Coluna** e clique em **Adicionar Coluna**.  
  
     **Adicionar Coluna** é realçado na coluna vazia mais à direita, e o cursor se move para a barra de fórmulas.  
  
     Para criar uma nova coluna entre duas colunas existentes, clique com o botão direito do mouse em uma coluna existente e clique em **Inserir Coluna**.  
  
2.  Na barra de fórmulas, siga um destes procedimentos:  
  
    -   Digite um sinal de igual seguido por uma fórmula.  
  
    -   Digite um sinal de igual, seguido por uma função DAX, seguida por argumentos e parâmetros, conforme exigido pela função.  
  
    -   Clique no botão de função (**fx**) e, na caixa de diálogo **Inserir Função** , selecione uma categoria e uma função, e clique em **OK**. Na barra de fórmulas, digite os argumentos e os parâmetros restantes conforme exigido pela função.  
  
3.  Pressione ENTER para aceitar a fórmula.  
  
     A coluna inteira é preenchida com a fórmula, e um valor é calculado para cada linha.  
  
> [!TIP]  
>  É possível usar a opção AutoCompletar Fórmula DAX no meio de uma fórmula existente com funções aninhadas. O texto pouco antes do ponto de inserção é usado para exibir valores na lista suspensa, e todo o texto depois do ponto de inserção permanece inalterado.  
  
## <a name="see-also"></a>Consulte também  
 [Colunas calculadas](../../analysis-services/tabular-models/ssas-calculated-columns.md)   
 [Medidas](../../analysis-services/tabular-models/measures-ssas-tabular.md)  
  
  
