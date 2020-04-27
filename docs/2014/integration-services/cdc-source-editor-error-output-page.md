---
title: Editor de origem CDC (página saída de erro) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.cdcsource.errorhandling.f1
ms.assetid: 8a4c2cb8-fd2f-4c45-824f-b93473a8981e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d3bf33d52b380e1ac05864c6e7402567b42df54a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66061037"
---
# <a name="cdc-source-editor-error-output-page"></a>Editor de Origem CDC (página Saída de Erro)
  Use a página **Saída de Erro** da caixa de diálogo **Editor de Origem CDC** para selecionar as opções para tratamento de erros.  
  
 Para obter mais informações sobre a origem CDC, consulte [CDC Source](data-flow/cdc-source.md).  
  
## <a name="task-list"></a>Lista de Tarefas  
 **Para abrir a página Saída de Erro do Editor de Origem CDC**  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], abra o pacote [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] que tem a origem CDC.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes na origem CDC.  
  
3.  No **Editor de Origem CDC**, clique em **Saída de Erro**.  
  
## <a name="options"></a>Opções  
 **Entrada/Saída**  
 Exibe o nome da fonte de dados.  
  
 **Coluna**  
 Exiba as colunas externas (origem) selecionadas na página **Gerenciador de Conexões** da caixa de diálogo **CDC Source Editor (Editor de Origem CDC)** .  
  
 **Erro**  
 Selecione como a origem CDC deve tratar erros em um fluxo: ignorar a falha, redirecionar a linha ou causar falha no componente.  
  
 **Truncation**  
 Selecione como a origem CDC deve tratar o truncamento em um fluxo: ignorar a falha, redirecionar a linha ou causar falha no componente.  
  
 **Descrição**  
 Não usado.  
  
 **Definir este valor para células selecionadas**  
 Selecione como a origem CDC trata todas as células selecionadas quando ocorre um erro ou um truncamento: ignorar a falha, redirecionar a linha ou causar a falha no componente.  
  
 **Aplicar**  
 Aplique as opções de tratamento de erros às células selecionadas.  
  
## <a name="error-handling-options"></a>Opções de tratamento de erros  
 Você usa as opções a seguir para configurar como a origem CDC trata erros e truncamentos.  
  
 **Falha no Componente**  
 A tarefa Fluxo de Dados falha quando ocorre um erro ou um truncamento. Esse é o comportamento padrão.  
  
 **Ignorar Falha**  
 O erro ou truncamento é ignorado e a linha de dados é direcionada para a saída da origem CDC.  
  
 **Redirecionar fluxo**  
 O erro ou a linha de dados de truncamento é direcionada para a saída do erro da origem CDC. Neste caso, o tratamento de erro da origem CDC é usado. Para obter mais informações, consulte [CDC Source](data-flow/cdc-source.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Editor de origem CDC &#40;página do Gerenciador de conexões&#41;](../../2014/integration-services/cdc-source-editor-connection-manager-page.md)   
 [Editor de Origem CDC &#40;página Colunas&#41;](../../2014/integration-services/cdc-source-editor-columns-page.md)  
  
  
