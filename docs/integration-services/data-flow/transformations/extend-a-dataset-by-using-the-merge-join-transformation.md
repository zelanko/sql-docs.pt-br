---
title: "Estender um conjunto de dados usando a transformação mesclar junção | Microsoft Docs"
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
- Merge Join transformation
- datasets [Integration Services], joining
- datasets [Integration Services], extending
- joining datasets [Integration Services]
ms.assetid: 9e512c3c-f89b-45f3-8281-cdb8f35a2b1f
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0a7d7b4a2af89c855a6269d90d94f79465bfad8a
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="extend-a-dataset-by-using-the-merge-join-transformation"></a>Estender um conjunto de dados por meio da transformação Junção de Mesclagem
  Para adicionar e configurar uma ttransformação Junção de Mesclagem, o pacote já deve incluir pelo menos uma tarefa de Fluxo de Dados e dois componentes de fluxo de dados que forneçam entradas para a ttransformação Junção de Mesclagem.  
  
 A ttransformação Junção de Mesclagem requer duas entradas classificadas. Para obter mais informações, consulte [Classificar dados para as transformações Mesclagem e Junção de Mesclagem](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).  
  
### <a name="to-extend-a-dataset"></a>Estender um conjunto de dados  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Dados** e na **Caixa de Ferramentas**, arraste a transformação Junção de Mesclagem para a superfície de design.  
  
4.  Conecte a transformação Junção de Mesclagem ao fluxo de dados arrastando um conector de uma fonte de dados ou transformação anterior para a transformação Junção de Mesclagem.  
  
5.  Clique duas vezes na ttransformação Junção de Mesclagem.  
  
6.  Na caixa de diálogo **Editor da transformação Junção de Mesclagem** , selecione o tipo de junção que deseja usar na lista **Tipo de junção** .  
  
    > [!NOTE]  
    >  Se você selecionar o tipo **Junção externa esquerda** , poderá clicar em **Trocar Entradas** para mudar as entradas e converter a junção externa esquerda para uma junção externa direita.  
  
7.  Arraste as colunas na entrada esquerda para colunas na entrada direita para especificar as colunas de junção. Se as colunas tiverem o mesmo nome, marque a caixa de seleção **Chave de Junção** e a transformação Junção de Mesclagem criará a junção automaticamente.  
  
    > [!NOTE]  
    >  Você pode criar junções somente entre colunas que tem a mesma posição de classificação e as junções devem ser criadas na ordem especificada pela posição de classificação. Se você tentar criar as junções fora da ordem, o **Editor da Transformação Junção de Mesclagem** solicitará que você crie junções adicionais para as posições da ordem de classificação que foram ignoradas.  
  
    > [!NOTE]  
    >  Por padrão, a saída é classificada nas colunas de junção.  
  
8.  Nas entradas esquerda e direita, marque as caixas de seleção de colunas adicionais a serem incluídas na saída. Por padrão, as colunas de junção já estão incluídas.  
  
9. Se preferir, atualize os nomes de colunas de saída na coluna **Alias de Saída** .  
  
10. Clique em **OK**.  
  
11. Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## <a name="see-also"></a>Consulte também  
 [Transformação junção de mesclagem](../../../integration-services/data-flow/transformations/merge-join-transformation.md)   
 [Transformações do Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Caminhos do Integration Services](../../../integration-services/data-flow/integration-services-paths.md)   
 [Tarefa de fluxo de dados](../../../integration-services/control-flow/data-flow-task.md)  
  
  
