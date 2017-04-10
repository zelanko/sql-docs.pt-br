---
title: "Identificar linhas de dados semelhantes por meio da transforma&#231;&#227;o Agrupamento Difuso | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "transformação Agrupamento Difuso"
  - "corresponder dados similares [Integration Services]"
  - "linhas de dados similares [Integration Services]"
  - "correspondências difusas"
ms.assetid: ffcb41a6-e23d-49ea-8c32-ac980e3dc495
caps.latest.revision: 23
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 23
---
# Identificar linhas de dados semelhantes por meio da transforma&#231;&#227;o Agrupamento Difuso
  Para adicionar e configurar uma transformação Agrupamento Difuso, o pacote já deve incluir pelo menos uma tarefa de Fluxo de Dados e uma fonte.  
  
### Implementar uma transformação Agrupamento Difuso em um fluxo de dados  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Dados** e, na **Caixa de Ferramentas**, arraste a transformação Agrupamento Difuso para a superfície de design.  
  
4.  Conecte a transformação Agrupamento Difuso ao fluxo de dados arrastando o conector da fonte de dados ou de uma transformação anterior para a transformação Agrupamento Difuso.  
  
5.  Clique duas vezes no transformação Agrupamento Difuso.  
  
6.  Na caixa de diálogo **Editor de Transformação Agrupamento Difuso**, na guia **Gerenciador de Conexões**, selecione um gerenciador de conexões OLE DB que se conecte a um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
    > [!NOTE]  
    >  A transformação requer uma conexão a um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para criar tabelas temporárias e índices.  
  
7.  Clique na guia **Colunas** e, na lista **Colunas de Entrada Disponíveis**, marque a caixa de seleção das colunas de entrada a serem usadas para identificar linhas similares no conjunto de dados.  
  
8.  Marque a caixa de seleção na coluna **Passagem** para identificar as colunas de entrada para passar para a saída de transformação. Colunas de passagem não são incluídas no processo de identificação de linhas duplicadas.  
  
    > [!NOTE]  
    >  As colunas de entrada que são usadas para agrupamento são selecionadas automaticamente como colunas de passagem e não podem ser desmarcadas enquanto estiverem sendo utilizadas para agrupamento.  
  
9. Se preferir, atualize os nomes de colunas de saída na coluna **Alias de Saída**.  
  
10. Se preferir, atualize os nomes de colunas limpas na coluna **OutputAlias do Grupo**.  
  
    > [!NOTE]  
    >  Os nomes padrão de colunas são os nomes das colunas de entrada com um sufixo "_clean".  
  
11. Como alternativa, atualize o tipo de correspondência a ser usada na coluna **Tipo de Correspondência**.  
  
    > [!NOTE]  
    >  Pelo menos uma coluna deve usar correspondência difusa.  
  
12. Especifique o nível mínimo de semelhança das colunas na coluna **Similaridade Mínima**. O valor deve estar entre 0 e 1. Quanto mais próximo de 1 for o valor, mais similares devem ser os valores das colunas de entrada para a formação de um grupo. Uma similaridade mínima de 1 indica uma correspondência exata.  
  
13. Se preferir, atualize os nomes de colunas de similaridade na coluna **Alias de Saída de Similaridade**.  
  
14. Para especificar a manipulação de números em valores de dados, atualize os valores na coluna **Numerais**.  
  
15. Para especificar de que forma a transformação compara os dados de cadeia de caracteres, modifique a seleção padrão de opções de comparação na coluna **Sinalizadores de Comparação**.  
  
16. Clique na guia **Avançado** para modificar os nomes das colunas que a transformação acrescenta à saída para o identificador exclusivo de linha (_key_in), identificador de linhas duplicadas (_key_out) e o valor de similaridade (_score).  
  
17. Como alternativa, ajuste o limite de semelhança movendo a barra deslizante.  
  
18. Se preferir, desmarque as caixas de seleção do delimitadores de token para ignorar delimitadores nos dados.  
  
19. Clique em **OK**.  
  
20. Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## Consulte também  
 [Transformação Agrupamento Difuso](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)   
 [Transformações do Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Caminhos do Integration Services](../../../integration-services/data-flow/integration-services-paths.md)   
 [Tarefa de Fluxo de Dados](../../../integration-services/control-flow/data-flow-task.md)  
  
  