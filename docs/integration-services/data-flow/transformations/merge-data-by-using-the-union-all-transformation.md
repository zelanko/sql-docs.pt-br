---
title: "Mesclar dados por meio da transforma&#231;&#227;o Unir Tudo | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "mesclando conjuntos de dados [Integration Services]"
  - "mesclando entradas [Integration Services]"
  - "combinando conjuntos de dados"
  - "transformação Unir Tudo"
  - "conjuntos de dados [Serviços de Integração], mesclagem"
ms.assetid: 78304403-a81c-4101-b87e-ec80ddfdac98
caps.latest.revision: 22
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 22
---
# Mesclar dados por meio da transforma&#231;&#227;o Unir Tudo
  Para adicionar e configurar uma transformação Union All, o pacote já deve incluir pelo menos uma tarefa de Fluxo de Dados e duas fontes de dados.  
  
 A transformação Union All combina várias entradas. A primeira entrada que é conectada à transformação é a entrada de referência e as entradas conectadas em seguida são as entradas secundárias. A saída inclui as colunas da entrada de referência.  
  
### Para combinar entradas em um fluxo de dados  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], clique duas vezes no pacote no Gerenciador de Soluções para abri-lo no Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)], e clique na guia **Fluxo de Dados**.  
  
2.  Da **Caixa de Ferramentas**, arraste a transformação Union All para a superfície de design da guia **Fluxo de Dados**.  
  
3.  Conecte a transformação Union All para o fluxo de dados arrastando um conector de uma fonte de dados ou uma transformação anterior para a transformação Union All.  
  
4.  Clique duas vezes na transformação Union All.  
  
5.  No **Editor da Transformação Union All**, mapeie uma coluna de uma entrada para uma coluna na lista **Nome da Coluna de Saída** clicando uma linha e selecionando uma coluna na lista de entrada. Selecione **\<ignore>** na lista de entrada para ignorar o mapeamento da coluna.  
  
    > [!NOTE]  
    >  O mapeamento entre duas colunas requer que seus metadados tenham correspondência.  
  
    > [!NOTE]  
    >  As colunas em uma entrada secundária que não são mapeadas para colunas de referência, são definidas com valores nulos na saída.  
  
6.  Opcionalmente, modifique os nomes de colunas na coluna **Nome da Coluna de Saída**.  
  
7.  Repetir as etapas 5 e 6 para cada coluna em cada entrada.  
  
8.  Clique em **OK**.  
  
9. Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## Consulte também  
 [Transformação Unir Tudo](../../../integration-services/data-flow/transformations/union-all-transformation.md)   
 [Transformações do Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Caminhos do Integration Services](../../../integration-services/data-flow/integration-services-paths.md)   
 [Tarefa de Fluxo de Dados](../../../integration-services/control-flow/data-flow-task.md)  
  
  