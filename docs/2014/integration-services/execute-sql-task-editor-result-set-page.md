---
title: Execute o Editor da tarefa SQL (página do conjunto de resultados) | Microsoft Docs
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
- sql12.dts.designer.executesqltask.resultset.f1
helpviewer_keywords:
- Execute SQL Task Editor
ms.assetid: d27000c8-8d91-4e1c-b45e-bca9a3c12f6d
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: b80d8052fd4492e0da04a65aa17e55f3e960d238
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119157"
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
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [SQL Editor da tarefa executar &#40;página geral&#41;](general-page-of-integration-services-designers-options.md)   
 [SQL Editor da tarefa executar &#40;página mapeamento de parâmetros&#41;](../../2014/integration-services/execute-sql-task-editor-parameter-mapping-page.md)   
 [Referência do Transact-SQL &#40;Mecanismo de Banco de Dados&#41;](/sql/t-sql/language-reference)  
  
  
