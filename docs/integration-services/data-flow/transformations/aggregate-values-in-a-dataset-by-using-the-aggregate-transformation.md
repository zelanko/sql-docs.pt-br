---
title: "Agregar valores em um conjunto de dados usando a transformação agregação | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Aggregate transformation [Integration Services]
- aggregate values [Integration Services]
- datasets [Integration Services], aggregate values
ms.assetid: 01b81c0f-d5e0-483b-81b2-73800a6945ac
caps.latest.revision: 48
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8b4e99dd830e0722fa5717f8749ef7f4dc152be0
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="aggregate-values-in-a-dataset-by-using-the-aggregate-transformation"></a>Agregar valores em um conjunto de dados por meio da transformação Agregação
  Para adicionar e configurar uma transformação de Agregação, o pacote já deve incluir pelo menos uma tarefa de Fluxo de Dados e uma origem.  
  
### <a name="to-aggregate-values-in-a-dataset"></a>Para agregar valores em um conjunto de dados  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Dados** e na **Caixa de Ferramentas**, arraste a transformação Agregação para a superfície de design.  
  
4.  Conecte a transformação Agregação ao fluxo de dados arrastando um conector da fonte ou transformação anterior para a transformação Agregação.  
  
5.  Clique duas vezes na transformação.  
  
6.  Na caixa de diálogo **Editor da Transformação Agregação** , clique na guia **Agregações** .  
  
7.  Na lista **Colunas de Entrada Disponíveis** , marque a caixa de seleção ao lado das colunas nas quais deseja agregar os valores. As colunas selecionadas aparecem na tabela.  
  
    > [!NOTE]  
    >  É possível selecionar uma coluna diversas vezes, aplicando diversas transformações à coluna. Para identificar exclusivamente as agregações, um número é anexado ao nome padrão do alias de saída da coluna.  
  
8.  Como opção, modifique o valor nas colunas **Alias de Saída** .  
  
9. Para alterar a operação de agregação padrão, **Agrupar por**selecione uma operação diferente na lista **Operação** .  
  
10. Para alterar a comparação padrão, selecione os sinalizadores de comparação individuais listados na coluna **Sinalizadores de Comparação** . Por padrão, uma comparação ignora a diferença entre maiúsculas e minúsculas, tipo kana, caracteres sem-espaçamento e largura do caractere.  
  
11. Como opção, para a agregação **Distinção de contagem** , especifique um número exato de valores distintos na coluna **Chaves de Distinção de Contagem** ou selecione uma contagem aproximada na coluna **Escala de Distinção de Contagem** .  
  
    > [!NOTE]  
    >  O fornecimento do número de valores distintos, exato ou aproximado, melhora o desempenho, pois a transformação pode alocar antecipadamente uma quantidade da memória para fazer seu trabalho.  
  
12. Como opção, clique em **Avançado** e atualize o nome da saída da transformação Agregação. Se as agregações incluirem uma operação **Group By** , você poderá selecionar uma contagem aproximada de valores de chave de agrupamento na coluna **Escala de Chaves** ou especifique um número exato de valores de chave de agrupamento na coluna **Chaves** .  
  
    > [!NOTE]  
    >  O fornecimento do número de valores distintos, exato ou aproximado, melhora o desempenho, pois a transformação pode alocar antecipadamente uma quantidade da memória para fazer seu trabalho.  
  
    > [!NOTE]  
    >  As opções **Escala de Chaves** e **Chaves** são mutuamente exclusivas. Se você digitar valores em ambas as colunas, o valor maior em **Escala de Chaves** ou **Chaves** será usado.  
  
13. Como opção, clique na guia **Avançado** e defina os atributos que se aplicam à otimização de todas as operações realizadas pela transformação Agregação.  
  
14. Clique em **OK**.  
  
15. Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## <a name="see-also"></a>Consulte também  
 [Transformação agregação](../../../integration-services/data-flow/transformations/aggregate-transformation.md)   
 [Transformações do Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Caminhos do Integration Services](../../../integration-services/data-flow/integration-services-paths.md)   
 [Tarefa de fluxo de dados](../../../integration-services/control-flow/data-flow-task.md)  
  
  
