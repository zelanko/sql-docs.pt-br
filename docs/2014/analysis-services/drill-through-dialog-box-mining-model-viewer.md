---
title: Drill-Through a caixa de diálogo (Visualizador do modelo de mineração) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.drillthrough.f1
ms.assetid: 42b78399-143d-4f44-90e0-b545ffb79e10
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d26fcb3d26570adafe340f190e7a91c82fd2ef3a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62731545"
---
# <a name="drill-through-dialog-box-mining-model-viewer"></a>Caixa de diálogo Extrair Detalhes (Visualizador do modelo de mineração)
  Ao exibir um modelo de mineração usando a guia **Visualizador do Modelo de Mineração** do Designer de Mineração de Dados, é possível detalhar os dados de caso, contanto que o modelo tenha o detalhamento habilitado. Além disso, se a estrutura de mineração subjacente tiver o detalhamento habilitado, também será possível ver colunas na estrutura de mineração, mesmo se essas colunas não tiverem sido incluídas no modelo de mineração. Na lista de colunas, as colunas da estrutura têm o rótulo “Structure.” como prefixo.  
  
> [!NOTE]  
>  Não é possível habilitar o detalhamento em uma estrutura de mineração existente. Em vez disso, você deve recriar a estrutura de mineração e habilitar o detalhamento durante o processo de criação.  
  
 Para obter informações sobre como acessar os dados de caso de cada visualizador de modelo de mineração que dá suporte ao detalhamento, **consulte** [Detalhar dados do caso com base em um modelo de mineração](data-mining/drill-through-to-case-data-from-a-mining-model.md).  
  
## <a name="options"></a>Opções  
 **Casos classificados em**  
 Exibe a definição da regra, o conjunto de itens e o cluster contidos no nó selecionado.  
  
 **Lista de colunas**  
 Exibe as colunas no modelo, seguida pelas colunas da estrutura.  
  
 **Observação** As colunas da estrutura são exibidas somente se o detalhamento estiver habilitado na estrutura de mineração e se você tiver selecionado a opção **Colunas do Modelo e da Estrutura**. Além disso, você deve ter permissões de detalhamento no modelo de mineração e na estrutura de mineração para exibir as colunas.  
  
 Colunas de estrutura que não estão incluídas no modelo aparecem como **estrutura.\< nome da coluna >**.  
  
> [!NOTE]  
>  É possível clicar com o botão direito do mouse em qualquer lugar da grade da coluna e selecionar **Copiar Tudo** para copiar os dados do detalhamento, no formato delimitado por tabulação, para a Área de transferência. Os dados copiados incluem apenas os dados de caso, não a definição de nó.  
  
 **Reproduzir**  
 Clique no botão de seta verde para atualizar os dados.  
  
## <a name="see-also"></a>Consulte também  
 [Consultas de detalhamento &#40;Mineração de dados&#41;](data-mining/drillthrough-queries-data-mining.md)   
 [Visualizadores do modelo de mineração &#40; Designer do modelo de mineração de dados &#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Tarefas e instruções do visualizador do modelo de mineração](data-mining/mining-model-viewer-tasks-and-how-tos.md)  
  
  
