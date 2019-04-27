---
title: Editor de transformação de pesquisa (página geral) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.lookuptransformation.general.f1
ms.assetid: 4bd15e48-0feb-4f95-be91-5df58105dbfb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4aa5b08a35a2eaf0d82b79145ecacde9d50579ee
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62767298"
---
# <a name="lookup-transformation-editor-general-page"></a>Editor da Transformação Pesquisa (página Geral)
  Use a página **Geral** da caixa de diálogo Editor da Transformação Pesquisa para selecionar o modo de cache, selecionar o tipo de conexão e especificar como lidar com as linhas com entradas sem-correspondência.  
  
 Para saber mais sobre a transformação Pesquisa, consulte [Lookup Transformation](data-flow/transformations/lookup-transformation.md).  
  
## <a name="options"></a>Opções  
 **Cache cheio**  
 Gere e carregue o conjunto de dados de referência no cache antes de executar a transformação Pesquisa.  
  
 **Cache parcial**  
 Gere o conjunto de dados de referência durante a execução da transformação Pesquisa. Carregue as linhas com entradas com correspondência no conjunto de dados de referência e as linhas com entradas sem-correspondência no conjunto de dados no cache.  
  
 **Não cache**  
 Gere o conjunto de dados de referência durante a execução da transformação Pesquisa. Nenhum dado é carregado no cache.  
  
 **Gerenciador de conexões do cache**  
 Configure a transformação Pesquisa para usar um Gerenciador de conexão de cache. Esta opção estará disponível somente se a opção Cache cheio for selecionada.  
  
 **Gerenciador de conexões OLE DB**  
 Configure a transformação Pesquisa para usar um Gerenciador de conexões OLE DB.  
  
 **Especificar como lidar com linhas com entradas sem-correspondência**  
 Selecione uma opção para lidar com as linhas que não correspondem a pelo menos uma entrada no conjunto de dados de referência.  
  
 Ao selecionar **Redirecionar linhas para uma saída sem-correspondência**, as linhas serão redirecionadas a uma saída sem-correspondência e serão tratadas como erros. A opção **Erro** na página **Saída de Erro** da caixa de diálogo **Editor da Transformação Pesquisa** não estará disponível.  
  
 Ao selecionar uma opção na caixa de listas **Especificar como lidar com linhas com entradas sem-correspondência** , as linhas serão tratadas como erros. A opção **Erro** na página **Saída de Erro** estará disponível.  
  
## <a name="external-resources"></a>Recursos externos  
 Entrada de blog, [Lookup cache modes](https://go.microsoft.com/fwlink/?LinkId=219518) (em inglês) em blogs.msdn.com  
  
## <a name="see-also"></a>Consulte também  
 [Cache Connection Manager](connection-manager/cache-connection-manager.md)   
 [Editor de Transformação Pesquisa &#40;Página Conexão&#41;](../../2014/integration-services/lookup-transformation-editor-connection-page.md)   
 [Editor de Transformação Pesquisa &#40;Guia Colunas&#41;](../../2014/integration-services/lookup-transformation-editor-columns-page.md)   
 [Editor de Transformação Pesquisa &#40;Página Avançado&#41;](../../2014/integration-services/lookup-transformation-editor-advanced-page.md)   
 [Editor de Transformação Pesquisa &#40;Página Saída de Erro&#41;](../../2014/integration-services/lookup-transformation-editor-error-output-page.md)  
  
  
