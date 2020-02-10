---
title: 'Tarefa 9: adicionando a transformação unir tudo para combinar registros corretos e corrigidos | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 24ba466d-a7d3-49e7-9111-b348399c9e58
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 93b160b6e513ad866126df8b401b82ee1270be84
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65489645"
---
# <a name="task-9-adding-union-all-transform-to-combine-correct-and-corrected-records"></a>Tarefa 9: Adicionando a Transformação Unir Tudo para combinar registros corretos e corrigidos
  Nesta tarefa, você adiciona a Transformação Unir Tudo ao fluxo de dados. A transformação Union All combina várias entradas em apenas uma saída. No cenário, isso combina registros Corretos e Corrigidos em um fluxo.  
  
1.  Arraste e solte **unir todas as** transformações da seção **comum** da **caixa de ferramentas do SSIS** para a guia fluxo de **dados** e coloque-as em **escolher os registros corretos e corrigidos**.  
  
2.  Clique com o botão direito do mouse em **Union All** Transform na guia **fluxo de dados** e clique em **renomear**. Digite **combinar registros corretos e corrigidos**e pressione **Enter**.  
  
     ![Combinar Registros Corretos e Corrigidos](../../2014/tutorials/media/et-addinguattocombinecacrecords-01.jpg "Combinar Registros Corretos e Corrigidos")  
  
3.  Conectar **selecione registros corretos e corrigidos** para **combinar os registros corretos e corrigidos** na guia **fluxo de dados** usando o conector azul. Você deverá ver a caixa de diálogo **seleção de saída de entrada** .  
  
4.  Na caixa de diálogo **saída de entrada** , selecione **corrigir** para **saída** e clique em **OK**.  
  
     ![Caixa de diálogo Seleção de Saída e Entrada](../../2014/tutorials/media/et-addinguattocombinecacrecords-02.jpg "Caixa de diálogo Seleção de Saída e Entrada")  
  
5.  Mova o conector intitulado **correto** para a esquerda arrastando e soltando o ponto no final do conector para a esquerda.  
  
     ![Conectar Corrigir a Combinar Corretos e Corrigidos](../../2014/tutorials/media/et-addinguattocombinecacrecords-03.jpg "Conectar Corrigir a Combinar Corretos e Corrigidos")  
  
6.  Se você selecionar **escolher correção de registros corretos e corrigidos** , você verá outro conector azul. Arraste esse conector azul para **combinar os registros corretos e corrigidos**.  
  
     ![Conectar Corrigido a Combinar Corretos e Corrigidos](../../2014/tutorials/media/et-addinguattocombinecacrecords-04.jpg "Conectar Corrigido a Combinar Corretos e Corrigidos")  
  
7.  Esse **conector** deve ter o título **corrigido**. Como você tem apenas duas condições **corretas** e **corrigidas**, e uma condição já foi usada, a caixa de diálogo de **seleção de saída de entrada** não é exibida desta vez. Se os conectores se sobrepuserem, mova um deles para esquerda e o outro para direita arrastando o conector para a esquerda ou direita.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 10: Adicionando a Transformação Grupo Difuso para identificar duplicatas](../../2014/tutorials/task-10-adding-fuzzy-group-transform-to-identify-duplicates.md)  
  
  
