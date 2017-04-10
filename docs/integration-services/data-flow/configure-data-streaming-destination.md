---
title: "Configurar destino do fluxo de dados | Microsoft Docs"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "SQL11.DTS.DESIGNER.DATASTREAMINGDEST.F1"
ms.assetid: bcdbb833-20c8-47ff-a641-bb517f9a1af3
caps.latest.revision: 7
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 7
---
# Configurar destino do fluxo de dados
  Configure o destino de fluxo de dados usando a caixa de diálogo **Editor Avançado para o Destino do Fluxo de Dados**. Abra essa caixa de diálogo clicando duas vezes no componente ou clicando com o botão direito do mouse no componente, no designer de fluxo de dados, e clicando em **Editar**.  
  
 A caixa de diálogo tem três guias: **Propriedades do Componente**, **Colunas de Entrada**, e **Propriedades de Entrada e Saída**.  
  
## Guia Propriedades do Componente  
 Esta guia tem os seguintes campos editáveis:  
  
|Campo|Description|  
|-----------|-----------------|  
|Nome|Nome do componente de destino de streaming de dados no pacote.|  
|ValidateExternalMetadata|Indica se o componente é validado usando fontes de dados externas no momento do design. Se definido como falso, a validação das fontes de dados externas é atrasada até o tempo de execução.|  
|IDColumnName|A exibição gerada pelo Assistente de publicação de feed de dados tem esta coluna de ID adicional. A coluna ID serve como EntityKey para os dados de saída do fluxo de dados quando os dados são consumidos como um feed de OData por outros aplicativos.<br /><br /> O nome padrão para esta coluna é _ID. Você pode especificar um nome diferente para a coluna de ID.|  
  
## Guia Colunas de Entrada  
 No painel superior dessa guia, você deve ver todas as colunas de entrada disponíveis. Selecione as colunas que você deseja incluir na saída deste componente. As colunas selecionadas são exibidas em uma lista no painel inferior. Você pode alterar o nome da coluna de saída, digitando o novo nome no campo **Alias de Saída** na lista.  
  
## Guia Propriedades de Entrada e Saída  
 Semelhante à guia Colunas de Entrada, você pode alterar os nomes das colunas de saída nesta guia. No modo de exibição de árvore à esquerda, expanda **Entrada de Destino do Streaming de Dados** e expanda **Colunas de Entrada**. Clique no nome da coluna de entrada e altere o nome do nome da coluna de saída no painel à direita.  
  
## Consulte também  
 [Destino do Fluxo de Dados](../../integration-services/data-flow/data-streaming-destination.md)   
 [Passo a passo: publicar um Pacote SSIS como um modo SQL](../../integration-services/data-flow/walkthrough-publish-an-ssis-package-as-a-sql-view.md)  
  
  