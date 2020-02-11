---
title: Criando um modelo de clustering de sequência relacionado (tutorial de mineração de dados intermediário) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1fb4f5bc-1756-45ca-9cd7-411a8c5992a9
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 71db7ba5246e151bbca8a52972a2ba835b80ddb6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62855873"
---
# <a name="creating-a-related-sequence-clustering-model-intermediate-data-mining-tutorial"></a>Criando um modelo de clustering de sequências relacionado (Tutorial de mineração de dados intermediário)
  Por meio da sua exploração do modelo de clustering de sequências, você aprendeu que outros atributos, como Região ou Rendimento, têm um efeito muito forte sobre os modelos e, portanto, para compreender melhor as sequências, será preciso criar um modelo de clustering de sequências relacionado e remover os atributos relacionados aos dados demográficos do cliente.  
  
 Nesta tarefa, você criará uma cópia do modelo de clustering de sequências regional e removerá do modelo qualquer coluna que não esteja diretamente relacionada às sequências.  
  
 O novo modelo conterá todas as mesmas colunas do modelo de mineração em que foi baseado. No entanto, você não precisa remover as colunas da estrutura de mineração, somente especificar que o novo modelo de mineração deverá ignorar as colunas.  
  
### <a name="to-make-a-copy-of-the-sequence-clustering-model"></a>Para fazer uma cópia do modelo de clustering de sequências  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], no designer de mineração de dados, clique na guia **modelos de mineração** .  
  
2.  Clique com o botão direito do mouse no modelo que você deseja copiar e selecione **novo modelo de mineração**.  
  
3.  Na caixa de diálogo **novo modelo de mineração** , digite um nome de modelo e selecione `Sequence Clustering`Microsoft.  
  
     Para este tutorial, digite o nome `Sequence Clustering`.  
  
4.  Clique em **OK**.  
  
### <a name="to-remove-columns-from-the-mining-model"></a>Para remover colunas do modelo de mineração  
  
1.  Na guia **modelo de mineração** , na coluna do novo modelo denominado clustering de sequência, clique na linha do atributo de **grupo renda** e selecione **ignorar**.  
  
2.  Repita essa etapa para a **região**de atributo.  
  
3.  Clique no sinal de adição ao lado do nome da tabela, **v associações Seq itens de linha**, para expandir a tabela e exibir as colunas da tabela aninhada.  
  
     O novo modelo só deve conter as seguintes colunas:  
  
     **Solicitar NumberKey**  
  
     **Chave de número de linha**  
  
     **Previsão de modelo**  
  
### <a name="to-process-the-new-sequence-clustering-model"></a>Para processar o novo modelo de clustering de sequências  
  
1.  Na guia **modelo de mineração** , clique com o botão direito do mouse `Sequence Clustering`no novo modelo chamado e selecione **modelo de processo**.  
  
     Como o novo modelo de mineração simplificado se baseia em uma estrutura que já foi processada, não será preciso reprocessá-la. É possível processar somente o novo modelo de mineração.  
  
2.  Clique em **Sim** para implantar o projeto de Data Mining atualizado no servidor.  
  
3.  Na caixa de diálogo **modelo de mineração de processo** , clique em **executar**.  
  
4.  Clique em **fechar** para fechar a caixa de diálogo **progresso do processo** e clique em **fechar** novamente na caixa de diálogo **processar modelo de mineração** .  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Criando previsões em um modelo de clustering de sequência &#40;tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/create-predictions-on-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Requisitos e considerações de processamento &#40;mineração de dados&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
