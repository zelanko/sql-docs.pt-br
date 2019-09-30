---
title: Derivar valores de coluna por meio da transformação Coluna Derivada | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- columns [Integration Services]
- derived columns
- columns [Integration Services], values
- Derived Column transformation
ms.assetid: 28b07746-fc6f-42b2-b741-9de6fac3f29c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8a8b9d523f3c0edd3a642caba8efc2396267e141
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71291488"
---
# <a name="derive-column-values-by-using-the-derived-column-transformation"></a>Derivar valores de coluna por meio da transformação Coluna Derivada

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Para adicionar e configurar uma transformação Coluna Derivada, o pacote já deve incluir pelo menos uma tarefa de Fluxo de Dados e uma origem.  
  
 A transformação de Coluna Derivada usa expressões para atualizar os valores de colunas existentes ou adicionar valores a novas colunas. Ao optar por adicionar valores a novas colunas, a caixa de diálogo **Editor de Transformação Coluna Derivada** avalia a expressão e define apropriadamente os metadados das colunas. Por exemplo, se uma expressão concatena duas colunas – cada uma com o tipo de dados DT_WSTR e um comprimento de 50 – com um espaço entre os dois valores de coluna, a nova coluna terá o tipo de dados DT_WSTR e um comprimento de 101. É possível atualizar o tipo de dados de colunas novas. O único requisito é que o tipo de dados seja compatível com os dados inseridos. Por exemplo, a caixa de diálogo **Editor de Transformação Coluna Derivada** gera um erro de validação ao atribuir um valor de dados a uma coluna com um tipo de dados Integer. Dependendo do tipo de dados selecionado, é possível especificar o comprimento, a precisão, a escala e a página de código da coluna.  
  
### <a name="to-derive-column-values"></a>Para derivar valores de coluna  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Dados** e, na **Caixa de Ferramentas**, arraste a transformação Coluna Derivada para a superfície de design.  
  
4.  Conecte a transformação de Coluna Derivada ao fluxo de dados arrastando um conector da fonte ou da transformação anterior para a transformação de Coluna Derivada.  
  
5.  Clique duas vezes na transformação de Coluna Derivada.  
  
6.  Na caixa de diálogo **Editor de Transformação Coluna Derivada** , crie as expressões para usar como condições arrastando variáveis, colunas, funções e operadores para a coluna **Expressão** na grade. Como alternativa, é possível digitar a expressão na coluna **Expressão** .  
  
    > [!NOTE]  
    >  Se a expressão não for válida, o texto da expressão será realçado e uma Dica de Ferramenta na coluna descreverá os erros.  
  
7.  Na lista **Coluna Derivada**, selecione **\<adicionar como uma nova coluna>** para gravar o resultado da avaliação da expressão em uma nova coluna ou selecione uma coluna existente para atualizar com o resultado da avaliação.  
  
     Se você optar por usar uma nova coluna, a caixa de diálogo **Editor de Transformação Coluna Derivada** avaliará a expressão e atribuirá um tipo de dados à coluna, dependendo do tipo de dados, tamanho, precisões, escala e página de código.  
  
8.  Se estiver usando uma nova coluna, selecione um tipo de dados na lista **Tipo de Dados** . Dependendo do tipo de dados selecionado, atualize, opcionalmente, os valores nas colunas **Tamanho**, **Precisão**, **Escala**e **Página de Código** . Metadados de colunas existentes não podem ser alterados.  
  
9. Opcionalmente, modifique os valores na coluna **Nome da Coluna Derivada** .  
  
10. Para configurar a saída de erro, clique em **Configurar Saída de Erro**. Para obter mais informações, consulte [Debugging Data Flow](../../../integration-services/troubleshooting/debugging-data-flow.md).  
  
11. Clique em **OK**.  
  
12. Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## <a name="see-also"></a>Consulte Também  
 [Derived Column Transformation](../../../integration-services/data-flow/transformations/derived-column-transformation.md)   
 [Tipos de dados do Integration Services](../../../integration-services/data-flow/integration-services-data-types.md)   
 [Transformações do Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Caminhos do Integration Services](../../../integration-services/data-flow/integration-services-paths.md)   
 [Tarefa de Fluxo de Dados](../../../integration-services/control-flow/data-flow-task.md)   
 [Expressões do Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md)  
  
  
