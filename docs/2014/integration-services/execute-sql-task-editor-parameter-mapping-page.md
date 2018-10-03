---
title: Editor da tarefa SQL (página mapeamento de parâmetros) executar | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executesqltask.parametermapping.f1
helpviewer_keywords:
- Execute SQL Task Editor
ms.assetid: 8ebe020a-7921-46b2-8823-398748f379b2
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 867ecaedcdcbafb972ccd289b5257fc73b353a5a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48092366"
---
# <a name="execute-sql-task-editor-parameter-mapping-page"></a>Editor da Tarefa Executar SQL (página Mapeamento de Parâmetros)
  Use a página **Mapeamento de Parâmetros** da caixa de diálogo **Editor da Tarefa Executar SQL** para mapear as variáveis para os parâmetros na instrução SQL.  
  
 Para saber mais sobre essa tarefa, consulte [Tarefa Executar SQL](control-flow/execute-sql-task.md) e [Parâmetros e códigos de retorno na Tarefa Executar SQL](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md).  
  
## <a name="options"></a>Opções  
 **Nome da Variável**  
 Depois de adicionar um mapeamento de parâmetros clicando em **Adicionar**, selecione uma variável de sistema ou definida pelo usuário na lista ou clique em \<**Nova variável...**> para adicionar uma nova variável usando a caixa de diálogo **Adicionar Variável**.  
  
 **Tópicos relacionados:** [Variáveis do Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md)  
  
 **Direção**  
 Selecione a direção do parâmetro. Mapeie cada variável para um parâmetro de entrada, parâmetro de saída ou um código de retorno.  
  
 **Tipo de Dados**  
 Selecione o tipo de dados do parâmetro. A lista de tipos de dados disponíveis é específica para o provedor selecionado no gerenciador de conexões usado pela tarefa.  
  
 **Nome do parâmetro**  
 Forneça um nome de parâmetro.  
  
 Dependendo do tipo de gerenciador de conexões usado pela tarefa, você deve usar números ou nomes de parâmetro. Alguns tipos de gerenciadores de conexões exigem que o primeiro caractere do nome do parâmetro seja o sinal \@, nomes específicos como \@Param1, ou nomes de coluna como nomes de parâmetro.  
  
 **Tópicos relacionados:** [Parâmetros e códigos de retorno na Tarefa Executar SQL](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md)  
  
 **Tamanho do Parâmetro**  
 Informe o tamanho dos parâmetros com comprimento variável, como cadeias de caracteres e campos binários.  
  
 Esta configuração garante que o provedor aloque espaço suficiente para obter valores de parâmetro de comprimento variável.  
  
 **Adicionar**  
 Clique para adicionar um mapeamento de parâmetros.  
  
 **Remover**  
 Selecione um mapeamento de parâmetros na lista e clique em **Remover**.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [SQL Editor da tarefa executar &#40;página geral&#41;](general-page-of-integration-services-designers-options.md)   
 [SQL Editor da tarefa executar &#40;página conjunto de resultados&#41;](../../2014/integration-services/execute-sql-task-editor-result-set-page.md)   
 [Referência do Transact-SQL &#40;Mecanismo de Banco de Dados&#41;](/sql/t-sql/language-reference)  
  
  
