---
title: Editor de transformação de pesquisa (página Avançado) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.lookuptransformation.advanced.f1
helpviewer_keywords:
- Lookup Transformation Editor
ms.assetid: f3395c65-0320-47f9-8d83-daaa082d8713
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 4982bd1a964e72d6a7e36d88a6f500d2a3ba5d89
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117737"
---
# <a name="lookup-transformation-editor-advanced-page"></a>Editor da Transformação Pesquisa (página Avançado)
  Use a página **Avançado** da caixa de diálogo **Editor da Transformação Pesquisa** para configurar o cache parcial e para modificar a instrução SQL da transformação Pesquisa.  
  
 Para saber mais sobre a transformação Pesquisa, consulte [Lookup Transformation](data-flow/transformations/lookup-transformation.md).  
  
## <a name="options"></a>Opções  
 **Tamanho de cache (32 bits)**  
 Ajuste o tamanho de cache (em megabytes) para computadores de 32 bits. O valor padrão é 5 megabytes.  
  
 **Tamanho de cache (64 bits)**  
 Ajuste o tamanho de cache (em megabytes) para computadores de 64 bits. O valor padrão é 5 megabytes.  
  
 **Ativar cache para linhas com entradas sem-correspondência**  
 Linhas de cache com entradas sem-correspondência no conjunto de dados de referência.  
  
 **Alocação de cache**  
 Especifique o percentual de cache a ser alocado para as linhas com entradas sem-correspondência no conjunto de dados de referência.  
  
 **Modificar instrução SQL**  
 Modifique a instrução SQL usada para gerar o conjunto de dados de referência.  
  
> [!NOTE]  
>  A instrução SQL opcional especificada nesta página substituirá o nome da tabela especificado na página **Conexão** do **Editor da Transformação Pesquisa**. Para obter mais informações, consulte [Lookup Transformation Editor &#40;Connection Page&#41;](../../2014/integration-services/lookup-transformation-editor-connection-page.md).  
  
 **Definir Parâmetros**  
 Mapeie colunas de entrada para parâmetros usando a caixa de diálogo **Definir Parâmetros da Consulta** .  
  
## <a name="external-resources"></a>Recursos externos  
 Entrada de blog, [Lookup cache modes](http://go.microsoft.com/fwlink/?LinkId=219518) (em inglês) em blogs.msdn.com  
  
## <a name="see-also"></a>Consulte também  
 [Editor de transformação pesquisa &#40;página geral&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor de transformação pesquisa &#40;página de Conexão&#41;](../../2014/integration-services/lookup-transformation-editor-connection-page.md)   
 [Editor de Transformação Pesquisa &#40;Guia Colunas&#41;](../../2014/integration-services/lookup-transformation-editor-columns-page.md)   
 [Editor de transformação pesquisa &#40;página de saída de erro&#41;](../../2014/integration-services/lookup-transformation-editor-error-output-page.md)   
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Transformação Pesquisa Difusa](data-flow/transformations/fuzzy-lookup-transformation.md)  
  
  