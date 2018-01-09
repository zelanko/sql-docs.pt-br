---
title: Criar uma coluna calculada | Microsoft Docs
ms.custom: 
ms.date: 04/10/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.as.daxref.CreataCalculatedColumn.f1
ms.assetid: 59440510-2d76-41dc-9b55-edc15259f9da
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7ea39808f7b85ac0d51297492183d11d9ac61287
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="create-a-calculated-column"></a>Criar uma coluna calculada
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]Colunas calculadas permitem adicionar novos dados a seu modelo. Em vez de colar ou importar valores para a coluna, você cria uma fórmula DAX que define os valores do nível de linha da coluna. Os valores em cada linha de uma coluna calculada são calculados e preenchidos quando você cria uma fórmula válida e, em seguida, clica em ENTER. A coluna calculada pode ser então adicionada a um relatório ou aplicativo de análise da mesma maneira que qualquer outra coluna de dados. Este tópico descreve como criar uma nova coluna calculada usando a barra de fórmulas DAX no designer modelo.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Colunas calculadas](../../analysis-services/tabular-models/ssas-calculated-columns.md)   
 [Medidas](../../analysis-services/tabular-models/measures-ssas-tabular.md)  
  
  
