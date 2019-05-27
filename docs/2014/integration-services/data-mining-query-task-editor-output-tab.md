---
title: Editor de tarefa de consulta de mineração de dados (guia saída) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dmquerytask.output.f1
helpviewer_keywords:
- Data Mining Query Task Editor
ms.assetid: 62f9e015-6fe0-4396-ad90-3ad51bf00025
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: db02b92ffead56451e72c7a1d564c2c9956d2ecc
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66059782"
---
# <a name="data-mining-query-task-editor-output-tab"></a>Editor da Tarefa Consulta de Mineração de Dados (guia Saída)
  Use a guia **Saída** da caixa de diálogo **Editor da Tarefa Consulta de Mineração de Dados** para especificar o destino da consulta de previsão.  
  
 Para saber mais sobre como implementar a mineração de dados em pacotes, consulte [Tarefa Consulta de mineração de dados](control-flow/data-mining-query-task.md) e [Soluções de mineração de dados](../analysis-services/data-mining/data-mining-solutions.md).  
  
## <a name="general-options"></a>Opções gerais  
 **Nome**  
 Forneça um nome exclusivo para a tarefa Consulta de Mineração de Dados. Esse nome é usado como rótulo no ícone de tarefa.  
  
> [!NOTE]  
>  Os nomes das tarefas devem ser exclusivos em um pacote.  
  
 **Descrição**  
 Digite uma descrição para a tarefa Consulta de Mineração de Dados.  
  
## <a name="output-tab-options"></a>Opções da guia Saída  
 **Conexão**  
 Selecione um gerenciador de conexões na lista ou clique em **Novo** para criar um novo gerenciador de conexões.  
  
 **Nova**  
 Crie um novo gerenciador de conexões. Só podem ser usados os tipos de gerenciador de conexões ADO.NET e OLE DB.  
  
 **Tabela de saída**  
 Especifique a tabela na qual a consulta de previsão deve gravar seus resultados.  
  
 **Ignorar e recriar tabela de saída**  
 Indique se a consulta de previsão deve substituir o conteúdo na tabela de destino, ignorando e, em seguida, recriando a tabela.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor da Tarefa Consulta de Mineração de Dados &#40;Guia Modelo de Mineração&#41;](../../2014/integration-services/data-mining-query-task-editor-mining-model-tab.md)   
 [Editor da Tarefa Consulta de Mineração de Dados &#40;Guia Consulta&#41;](../../2014/integration-services/data-mining-query-task-editor-query-tab.md)   
 [Designer de Mineração de dados](../analysis-services/data-mining/data-mining-designer.md)  
  
  
