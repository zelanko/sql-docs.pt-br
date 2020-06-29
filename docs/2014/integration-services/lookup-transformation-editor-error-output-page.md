---
title: Editor de transformação pesquisa (página saída de erro) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.lookuptransformation.erroroutput.f1
ms.assetid: 15d53bb0-8be1-46fb-b459-04a397e75fac
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0d83ceee2756e217271663a768bcb6be70983dc0
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85440233"
---
# <a name="lookup-transformation-editor-error-output-page"></a>Editor da Transformação Pesquisa (página Saída de Erro)
  Use a página **Saída de Erro** da caixa de diálogo **Editor da Transformação Pesquisa** para especificar as opções de tratamento de erros.  
  
 Para saber mais sobre a transformação Pesquisa, consulte [Lookup Transformation](data-flow/transformations/lookup-transformation.md).  
  
## <a name="options"></a>Opções  
 **Entrada/Saída**  
 Visualize o nome da entrada.  
  
 **Coluna**  
 Não usado.  
  
 **Erro**  
 Especifique que tipo de erro pode ocorrer ao lidar com linhas com entradas sem correspondência no conjunto de dados de referência:  
  
-   Ignorar falha e direcionar linhas para uma saída.  
  
-   Redirecionar linhas para uma saída de erro.  
  
-   Falha no componente.  
  
 Esta opção não estará disponível ao selecionar **Redirecionar linhas para uma saída sem-correspondência** na lista **Especificar como lidar com linhas com entradas sem-correspondência** . Essa lista está na página **Geral** da caixa de diálogo **Editor da Transformação Pesquisa** .  
  
 **Tópicos Relacionados:** [Tratamento de erros em dados](data-flow/error-handling-in-data.md)  
  
 **Truncation**  
 Especifique o que deve acontecer quando ocorrer um truncamento de dados:  
  
-   Ignorar falha.  
  
-   Redirecionar linha.  
  
-   Falha no componente.  
  
 **Descrição**  
 Visualize a descrição da operação.  
  
 **Definir células selecionadas com esse valor**  
 Especifique o que deve acontecer com todas as células selecionadas quando ocorrer um erro ou truncamento:  
  
-   Ignorar falha.  
  
-   Redirecionar linha.  
  
-   Falha no componente.  
  
 **Aplicar**  
 Aplique a opção de tratamento de erros às células selecionadas.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
