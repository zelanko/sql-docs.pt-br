---
title: Editor da tarefa Executar SQL (página conjunto de resultados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executesqltask.resultset.f1
helpviewer_keywords:
- Execute SQL Task Editor
ms.assetid: d27000c8-8d91-4e1c-b45e-bca9a3c12f6d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d84f7fe551d83f609b2ffc3da92b51eb36b9a595
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66058973"
---
# <a name="execute-sql-task-editor-result-set-page"></a>Editor da Tarefa Executar SQL (página Conjunto de Resultados)
  Use a página **Conjunto de Resultados** da caixa de diálogo **Editor da Tarefa Executar SQL** para mapear o resultado da instrução SQL para variáveis novas ou já existentes. As opções dessa caixa de diálogo serão desabilitadas se o **ResultSet** na página Geral for definido como **Nenhum**.  
  
 Para obter mais informações, consulte [Tarefa Executar SQL](control-flow/execute-sql-task.md) e [Conjuntos de resultados na tarefa Executar SQL](../../2014/integration-services/result-sets-in-the-execute-sql-task.md).  
  
## <a name="options"></a>Opções  
 **Nome do Resultado**  
 Depois que você adicionar um conjunto de resultados de conjunto de mapeamento clicando em **Adicionar**, forneça um nome exclusivo para o resultado. Dependendo do tipo de conjunto de resultados, é necessário usar nomes de resultado específicos.  
  
 Se o tipo de conjunto de resultados for **Linha única**, será possível usar o nome de uma coluna retornado pela consulta ou o número que representam a posição de uma coluna na lista de colunas de uma coluna retornada pela consulta.  
  
 Se o tipo de conjunto de resultados for **Conjunto de resultados completo** ou **XML**, será necessário usar 0 como o nome de conjunto de resultados.  
  
 **Tópicos Relacionados**: [Conjuntos de resultados na tarefa Executar SQL](../../2014/integration-services/result-sets-in-the-execute-sql-task.md)  
  
 **Nome da Variável**  
 Mapeie o conjunto de resultados para uma variável selecionando uma variável ou clique em \<**Nova variável...**> para adicionar uma nova variável usando a caixa de diálogo **Adicionar Variável**.  
  
 **Adicionar**  
 Clique para adicionar um mapeamento de conjunto de resultados.  
  
 **Remover**  
 Selecione um mapeamento de conjunto de resultados na lista e clique em **Remover**.  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services referência de erro e mensagem](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor da tarefa Executar SQL &#40;página Geral&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor da tarefa Executar SQL &#40;página mapeamento de parâmetro&#41;](../../2014/integration-services/execute-sql-task-editor-parameter-mapping-page.md)   
 [Referência do Transact-SQL &#40;Mecanismo de Banco de Dados&#41;](/sql/t-sql/language-reference)  
  
  
