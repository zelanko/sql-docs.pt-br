---
title: Caixa de diálogo Drill-through (Visualizador do modelo de mineração) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.drillthrough.f1
ms.assetid: 42b78399-143d-4f44-90e0-b545ffb79e10
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c065e36dd20646312d04379ea61b96d37a47a262
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66081491"
---
# <a name="drill-through-dialog-box-mining-model-viewer"></a>Caixa de diálogo Extrair Detalhes (Visualizador do modelo de mineração)
  Ao exibir um modelo de mineração usando a guia **Visualizador do Modelo de Mineração** do Designer de Mineração de Dados, é possível detalhar os dados de caso, contanto que o modelo tenha o detalhamento habilitado. Além disso, se a estrutura de mineração subjacente tiver o detalhamento habilitado, também será possível ver colunas na estrutura de mineração, mesmo se essas colunas não tiverem sido incluídas no modelo de mineração. Na lista de colunas, as colunas da estrutura têm o rótulo “Structure.” como prefixo.  
  
> [!NOTE]  
>  Não é possível habilitar o detalhamento em uma estrutura de mineração existente. Em vez disso, você deve recriar a estrutura de mineração e habilitar o detalhamento durante o processo de criação.  
  
 Para obter informações sobre como acessar os dados de caso de cada visualizador de modelo de mineração que dá suporte ao detalhamento, **consulte** [Detalhar dados do caso com base em um modelo de mineração](data-mining/drill-through-to-case-data-from-a-mining-model.md).  
  
## <a name="options"></a>Opções  
 **Casos Classificados em**  
 Exibe a definição da regra, o conjunto de itens e o cluster contidos no nó selecionado.  
  
 **Lista de colunas**  
 Exibe as colunas no modelo, seguida pelas colunas da estrutura.  
  
 **Observação** As colunas da estrutura são exibidas somente se o detalhamento estiver habilitado na estrutura de mineração e se você tiver selecionado a opção **Colunas do Modelo e da Estrutura**. Além disso, você deve ter permissões de detalhamento no modelo de mineração e na estrutura de mineração para exibir as colunas.  
  
 As colunas de estrutura que não estão incluídas no modelo aparecem como **estrutura\< . nome da coluna>**.  
  
> [!NOTE]  
>  É possível clicar com o botão direito do mouse em qualquer lugar da grade da coluna e selecionar **Copiar Tudo** para copiar os dados do detalhamento, no formato delimitado por tabulação, para a Área de transferência. Os dados copiados incluem apenas os dados de caso, não a definição de nó.  
  
 **Reproduzir**  
 Clique no botão de seta verde para atualizar os dados.  
  
## <a name="see-also"></a>Consulte Também  
 [Consultas de detalhamento &#40;mineração de dados&#41;](data-mining/drillthrough-queries-data-mining.md)   
 [Visualizadores de modelo de mineração &#40;designer de modelo de mineração de dados&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Tarefas e instruções do visualizador do modelo de mineração](data-mining/mining-model-viewer-tasks-and-how-tos.md)  
  
  
