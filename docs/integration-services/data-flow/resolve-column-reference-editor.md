---
title: "Resolver Editor de referência de coluna | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.resolvereferences.preview.F1
- sql13.dts.designer.resolvereferences.mapper.F1
ms.assetid: bb3ee33c-79c4-4c76-a82f-71581b4a60f1
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f2ff8a97d45d75c3e93d4aa3111b653c9612b889
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="resolve-column-reference-editor"></a>Resolver editor de referência de coluna
  Quando um caminho de entrada é desconectado ou se houver qualquer coluna não mapeada no caminho, um ícone de erro será exibido ao lado do caminho de dados correspondente. Para simplificar a resolução de erros de referência de coluna, o editor resolver referências permite vincular colunas de saída não mapeadas com colunas de entrada não mapeadas para todos os caminhos da árvore de execução. O editor Resolver Referências também realçará os caminhos para indicar quais caminhos estão sendo resolvidos.  
  
> [!NOTE]  
>  É possível editar um componente até mesmo quando seu caminho de entrada é desconectado  
  
 Depois que todas as referências a coluna foram resolvidas, se não houver erros de caminho de dados, nenhum ícone de erro será exibido ao lado dos caminhos de dados.  
  
## <a name="options"></a>Opções  
 **Colunas de saída não mapeadas (origem)**    
 Colunas do caminho upstream que não estão mapeadas no momento  
  
**Colunas mapeadas (origem)**    
 Colunas do caminho upstream que estão mapeadas para colunas do caminho downstream  
  
**Colunas mapeadas (destino)**    
 Colunas do caminho upstream que estão mapeadas para colunas do caminho downstream  
  
**Colunas de entrada não mapeadas (destino)**    
 Colunas do caminho downstream que não estão mapeadas no momento  
  
**Excluir Colunas de Entrada Não Mapeadas**  
 Selecione Excluir Colunas de Entrada Não Mapeadas para ignorar colunas não mapeadas no destino do caminho de dados. O botão Visualizar Alterações exibe uma lista das alterações que ocorrerão quando você pressionar o botão OK.  
  
  
