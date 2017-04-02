---
title: "Editor de Transforma&#231;&#227;o Agrupamento Difuso (guia Gerenciador de Conex&#245;es) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.fuzzygroupingtransformation.connection.f1"
helpviewer_keywords: 
  - "Editor de Transformação Agrupamento Difuso"
ms.assetid: 47b1446d-5331-473c-9cb5-a98b1f55bf5f
caps.latest.revision: 27
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 27
---
# Editor de Transforma&#231;&#227;o Agrupamento Difuso (guia Gerenciador de Conex&#245;es)
  Use a guia **Gerenciador de Conexões** da caixa de diálogo **Editor de Transformação Agrupamento Difuso** para selecionar uma conexão existente ou criar uma nova.  
  
> [!NOTE]  
>  O servidor especificado pela conexão deve estar executando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. A transformação Agrupamento Difuso cria objetos de dados temporários no tempdb que podem ser tão grandes quanto a entrada completa para a transformação. A execução da transformação emite, em seu decorrer, consultas de servidor contra esses objetos temporários. Isso pode afetar o desempenho global de servidor.  
  
 Para saber mais sobre a transformação Agrupamento Difuso, consulte [Fuzzy Grouping Transformation](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md).  
  
## Opções  
 **gerenciador de conexões OLE DB**  
 Selecione um gerenciador de conexões OLE DB existente usando a caixa de listagem ou crie uma nova conexão usando o botão **Novo**.  
  
 **Nova**  
 Crie uma nova conexão usando a caixa de diálogo **Configurar Gerenciador de Conexões OLE DB**.  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Identificar linhas de dados semelhantes por meio da transformação Agrupamento Difuso](../../../integration-services/data-flow/transformations/identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation.md)  
  
  