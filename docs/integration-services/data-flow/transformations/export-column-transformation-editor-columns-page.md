---
title: "Editor de Transforma&#231;&#227;o Exportar Colunas (p&#225;gina Colunas) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.fileextractortransformation.columns.f1"
helpviewer_keywords: 
  - "Editor de Transformação Exportar Colunas"
ms.assetid: b659a5c2-5509-4b5b-9c82-136c971d5c7f
caps.latest.revision: 28
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 28
---
# Editor de Transforma&#231;&#227;o Exportar Colunas (p&#225;gina Colunas)
  Use a página **Colunas** da caixa de diálogo **Exportar Editor de Transformação Colunas** para especificar as colunas no fluxo de dados a serem extraídas para arquivos. Você pode especificar se a transformação Exportar Coluna acrescenta dados a um arquivo ou substitui um arquivo existente.  
  
 Para saber mais sobre a transformação Exportar Coluna, consulte [Export Column Transformation](../../../integration-services/data-flow/transformations/export-column-transformation.md).  
  
## Opções  
 **Extrair Coluna**  
 Selecione na lista de colunas de entrada que contêm dados de texto ou de imagem. Todas as linhas devem ter definições para **Extrair Coluna** e **Coluna de Caminho de Arquivos**.  
  
 **Coluna de Caminho de Arquivos**  
 Selecione na lista de colunas de entrada que contêm caminhos e nomes de arquivo. Todas as linhas devem ter definições para **Extrair Coluna** e **Coluna de Caminho de Arquivos**.  
  
 **Permitir Acréscimo**  
 Especifique se a transformação acrescenta dados a arquivos existentes. O padrão é **false**.  
  
 **Forçar Truncamento**  
 Especifique se a transformação exclui o conteúdo dos arquivos existentes antes de gravar dados. O padrão é **false**.  
  
 **Gravar BOM**  
 Especifique se deve ser gravada uma BOM (marca de ordem de byte) no arquivo. Uma BOM só será gravada se os dados forem do tipo **DT_NTEXT** ou DT_WSTR e não estiverem anexados a um arquivo de dados existente.  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Exportar Editor de Transformação Colunas &#40;Página Saída de Erro&#41;](../../../integration-services/data-flow/transformations/export-column-transformation-editor-error-output-page.md)  
  
  