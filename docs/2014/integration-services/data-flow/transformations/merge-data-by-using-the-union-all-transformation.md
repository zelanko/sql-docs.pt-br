---
title: Mesclar dados por meio da transformação Unir Tudo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- merging datasets [Integration Services]
- merging inputs [Integration Services]
- combining datasets
- Union All transformation
- datasets [Integration Services], merging
ms.assetid: 78304403-a81c-4101-b87e-ec80ddfdac98
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5b113a2ca169ebc1f49a522d51800b09b9a30343
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37221806"
---
# <a name="merge-data-by-using-the-union-all-transformation"></a>Mesclar dados por meio da transformação Unir Tudo
  Para adicionar e configurar uma transformação Union All, o pacote já deve incluir pelo menos uma tarefa de Fluxo de Dados e duas fontes de dados.  
  
 A transformação Union All combina várias entradas. A primeira entrada que é conectada à transformação é a entrada de referência e as entradas conectadas em seguida são as entradas secundárias. A saída inclui as colunas da entrada de referência.  
  
### <a name="to-combine-inputs-in-a-data-flow"></a>Para combinar entradas em um fluxo de dados  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], clique duas vezes no pacote no Gerenciador de Soluções para abri-lo no Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , e clique na guia **Fluxo de Dados** .  
  
2.  Da **Caixa de Ferramentas**, arraste a transformação Union All para a superfície de design da guia **Fluxo de Dados** .  
  
3.  Conecte a transformação Union All para o fluxo de dados arrastando um conector de uma fonte de dados ou uma transformação anterior para a transformação Union All.  
  
4.  Clique duas vezes na transformação Union All.  
  
5.  No **Editor da Transformação Union All**, mapeie uma coluna de uma entrada para uma coluna na lista **Nome da Coluna de Saída** clicando uma linha e selecionando uma coluna na lista de entrada. Selecione **\<ignore>** na lista de entrada para ignorar o mapeamento da coluna.  
  
    > [!NOTE]  
    >  O mapeamento entre duas colunas requer que seus metadados tenham correspondência.  
  
    > [!NOTE]  
    >  As colunas em uma entrada secundária que não são mapeadas para colunas de referência, são definidas com valores nulos na saída.  
  
6.  Opcionalmente, modifique os nomes de colunas na coluna **Nome da Coluna de Saída** .  
  
7.  Repetir as etapas 5 e 6 para cada coluna em cada entrada.  
  
8.  Clique em **OK**.  
  
9. Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## <a name="see-also"></a>Consulte também  
 [Union All Transformation](union-all-transformation.md)   
 [Transformações do Integration Services](integration-services-transformations.md)   
 [Caminhos do Integration Services](../integration-services-paths.md)   
 [Tarefa de fluxo de dados] ((.. /.. /Control-Flow/Data-Flow-Task.MD)  
  
  
