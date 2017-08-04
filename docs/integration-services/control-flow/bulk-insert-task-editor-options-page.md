---
title: "Em massa Editor da tarefa de inserção (página Opções) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.bulkinserttask.options.f1
helpviewer_keywords:
- Bulk Insert Task Editor
ms.assetid: b3702811-3eb8-4b28-9190-5ae7a1a7bb6f
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1a714027caa6581a56d9f22da84c48d469e80cb1
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="bulk-insert-task-editor-options-page"></a>Editor da Tarefa Inserção em Massa (página de Opções)
  Use a página **Opções** da caixa de diálogo **Editor da Tarefa Inserção em Massa** para definir as propriedades da operação de inserção em massa. A tarefa Inserção em Massa copia uma grande quantidade de dados em uma exibição ou tabela do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para saber mais sobre como trabalhar com inserções em massa, consulte [Tarefa Inserção em Massa](../../integration-services/control-flow/bulk-insert-task.md) e [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md).  
  
## <a name="options"></a>Opções  
 **CodePage**  
 Especifique a página de código dos dados no arquivo de dados.  
  
 **DataFileType**  
 Especifique o valor do tipo de dados a ser usado na operação de carregamento.  
  
 **BatchSize**  
 Especifique o número de linhas em um lote. O padrão é todo o arquivo de dados. Se você definir **BatchSize** para zero, os dados serão carregados em um único lote.  
  
 **LastRow**  
 Especifique a última linha a ser copiada.  
  
 **FirstRow**  
 Especifique a primeira linha da qual começar a copiar.  
  
 **Opções**  
 |Termo|Definição|  
|----------|----------------|  
|**Verificar restrições**|Selecione para verificar as restrições de tabelas e colunas.|  
|**Manter nulos**|Selecione para reter valores nulos durante a operação de inserção em massa, em vez de inserir qualquer valor padrão para colunas vazias.|  
|**Habilitar inserção de identidade**|Selecione para inserir valores existentes em uma coluna de identidade.|  
|**Bloqueio de tabela**|Selecione para bloquear a tabela durante a inserção em massa.|  
|**Acionadores**|Selecione para acionar qualquer inserção, atualização ou exclusão de gatilhos na tabela.|  
  
 **SortedData**  
 Especifique a cláusula ORDER BY na instrução de inserção em massa. O nome da coluna que você fornece deve ser uma coluna válida na tabela de destino. O padrão é **false**. Isto significa que os dados não são classificados por uma cláusula ORDER BY.  
  
 **MaxErrors**  
 Especifique o número máximo de erros que podem ocorrer antes que a operação de inserção em massa seja cancelada. Um valor de 0 indica que um número infinito de erros é permitido.  
  
> [!NOTE]  
>  Cada linha que não pode ser importada pela operação de carregamento em massa é contada como um erro.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor da tarefa inserção em massa &#40; Página geral &#41;](../../integration-services/control-flow/bulk-insert-task-editor-general-page.md)   
 [Editor da tarefa inserção em massa &#40; Página de Conexão &#41;](../../integration-services/control-flow/bulk-insert-task-editor-connection-page.md)   
 [Página expressões](../../integration-services/expressions/expressions-page.md)   
 [Fluxo de controle](../../integration-services/control-flow/control-flow.md)  
  
  
