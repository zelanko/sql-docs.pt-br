---
title: Criando um modelo (Tutorial de mineração de dados intermediário) de Clustering de sequências relacionado | Microsoft Docs
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
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56035107"
---
# <a name="creating-a-related-sequence-clustering-model-intermediate-data-mining-tutorial"></a>Criando um modelo de clustering de sequências relacionado (Tutorial de mineração de dados intermediário)
  Por meio da sua exploração do modelo de clustering de sequências, você aprendeu que outros atributos, como Região ou Rendimento, têm um efeito muito forte sobre os modelos e, portanto, para compreender melhor as sequências, será preciso criar um modelo de clustering de sequências relacionado e remover os atributos relacionados aos dados demográficos do cliente.  
  
 Nesta tarefa, você criará uma cópia do modelo de clustering de sequências regional e removerá do modelo qualquer coluna que não esteja diretamente relacionada às sequências.  
  
 O novo modelo conterá todas as mesmas colunas do modelo de mineração em que foi baseado. No entanto, você não precisa remover as colunas da estrutura de mineração, somente especificar que o novo modelo de mineração deverá ignorar as colunas.  
  
### <a name="to-make-a-copy-of-the-sequence-clustering-model"></a>Para fazer uma cópia do modelo de clustering de sequências  
  
1.  Na [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], no Designer de mineração de dados, clique em de **modelos de mineração** guia.  
  
2.  Com o modelo que você deseja copiar e, em seguida, selecione o botão direito **novo modelo de mineração**.  
  
3.  No **novo modelo de mineração** caixa de diálogo, digite um nome de modelo e selecione Microsoft `Sequence Clustering`.  
  
     Para este tutorial, digite o nome `Sequence Clustering`.  
  
4.  Clique em **OK**.  
  
### <a name="to-remove-columns-from-the-mining-model"></a>Para remover colunas do modelo de mineração  
  
1.  No **modelo de mineração** guia, na coluna para o novo modelo chamado Clustering de sequências, clique na linha para o **grupo de renda** de atributo e, em seguida, selecione **ignorar**.  
  
2.  Repita essa etapa para o atributo **região**.  
  
3.  Clique no sinal de adição ao lado do nome da tabela, **v Assoc Seq Line Items**, para expandir a tabela e exiba as colunas da tabela aninhada.  
  
     O novo modelo só deve conter as seguintes colunas:  
  
     **Ordem NumberKey**  
  
     **Tecla de número de linha**  
  
     **Modelo de previsão**  
  
### <a name="to-process-the-new-sequence-clustering-model"></a>Para processar o novo modelo de clustering de sequências  
  
1.  No **modelo de mineração** guia, clique no novo modelo chamado `Sequence Clustering`e selecione **modelo de processo**.  
  
     Como o novo modelo de mineração simplificado se baseia em uma estrutura que já foi processada, não será preciso reprocessá-la. É possível processar somente o novo modelo de mineração.  
  
2.  Clique em **Sim** para implantar o projeto de mineração de dados atualizados no servidor.  
  
3.  No **processar modelo de mineração** caixa de diálogo, clique em **executar**.  
  
4.  Clique em **feche** para fechar o **progresso do processo** caixa de diálogo e clique **fechar** novamente no **processar modelo de mineração** caixa de diálogo.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Criando previsões em um modelo de Clustering de sequência &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/create-predictions-on-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Requisitos e considerações de processamento &#40;Mineração de dados&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
