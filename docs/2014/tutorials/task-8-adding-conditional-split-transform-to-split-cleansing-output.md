---
title: 'Tarefa 8: adicionando transformação de divisão condicional à saída de limpeza de divisão | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: d4ebe420-a4a9-4076-89d3-41abe726fc5c
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 57e8738edf77dae56454baba9ffc1b193146b110
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85006343"
---
# <a name="task-8-adding-conditional-split-transform-to-split-cleansing-output"></a>Tarefa 8: Adicionando a Transformação Divisão Condicional para dividir a saída da limpeza
  Nesta transformação, você adiciona uma Transformação Divisão Condicional ao fluxo de dados. A transformação Divisão Condicional pode rotear linhas para saídas diferentes com base no conteúdo dos dados. Para este tutorial, você usa a coluna saída de **status do registro** da transformação limpeza DQS. Apenas os registros corretos ou corrigidos serão carregados no servidor MDS neste tutorial. Portanto, você verifica se o **status do registro** está **correto** ou **corrigido**e combina os registros antes de carregar os registros para o MDS.  
  
1.  Arraste e solte **a transformação de divisão condicional** da seção **comum** na caixa de **Ferramentas do SSIS** para a guia fluxo de **dados** em **limpar dados do fornecedor**.  
  
2.  Clique com o botão direito do mouse em **divisão condicional**e clique em **renomear**. Digite **escolher os registros corretos e corrigidos** e pressione **Enter**.  
  
3.  Conecte os **dados do fornecedor de limpeza** e escolha os **registros corretos e corrigidos** usando o conector azul.  
  
     ![Limpar dados do fornecedor-> escolha corrigir & corrigido](../../2014/tutorials/media/et-addingcsttosplitcleansingoutput-01.jpg "Limpar Dados de Fornecedor -> Escolher Correto & Corrigido")  
  
4.  Clique duas vezes em **escolher os registros corretos e corrigidos** na guia **fluxo de dados** .  
  
5.  Altere o **nome de saída padrão** na parte inferior da tela para **corrigir**.  
  
6.  Expanda **colunas** no **painel superior esquerdo**.  
  
     ![Editor de Transformação Divisão Condicional](../../2014/tutorials/media/et-addingcsttosplitcleansingoutput-02.jpg "Editor de Transformação Divisão Condicional")  
  
7.  Arraste e solte o **status do registro** para a coluna **condição** .  
  
8.  Digite **= = "corrigido"** ao lado de **[status do registro]** para a coluna **condição** .  
  
9. Clique no **caso 1** na **coluna nome de saída**e altere o nome para **corrigido**.  
  
10. Clique em **OK** para fechar a caixa de diálogo **Editor de transformação Divisão condicional** .  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 9: Adicionando a Transformação Unir Tudo para combinar registros corretos e corrigidos](../../2014/tutorials/task-9-adding-union-all-transform-to-combine-correct-and-corrected-records.md)  
  
  
