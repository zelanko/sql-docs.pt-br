---
title: "Editor de destino ODBC (página saída de erro) | Microsoft Docs"
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
- sql13.ssis.designer.odbcdest.errorhandling.f1
ms.assetid: 0a743f8d-2a51-4296-9976-8104f5ca22d3
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e0fa59290399f3c3f7fc42b1f74b6a42c573f7d2
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="odbc-destination-editor-error-output-page"></a>Editor de Destinos ADO NET (página Saída de Erro)
  Use a página **Saída de Erro** da caixa de diálogo **Editor de Destino ODBC** para selecionar as opções para tratamento de erros.  
  
 Para obter mais informações sobre o destino ODBC, consulte [ODBC Destination](../../integration-services/data-flow/odbc-destination.md).  
  
 **Para abrir a página Saída de Erro do Editor de Destino ODBC**  
  
## <a name="task-list"></a>Lista de Tarefas  
  
-   No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra o pacote [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] que tem o destino ODBC.  
  
-   Na guia **Fluxo de Dados** , clique duas vezes no destino ODBC.  
  
-   No **Editor de Destino ODBC**, clique em **Saída de Erro**.  
  
## <a name="options"></a>Opções  
  
### <a name="inputoutput"></a>Entrada/Saída  
 Exibe o nome da fonte de dados.  
  
### <a name="column"></a>Coluna  
 Não usado.  
  
### <a name="error"></a>Erro  
 Selecione como o destino ODBC deve tratar erros em um fluxo: ignorar a falha, redirecionar a linha ou causar falha no componente.  
  
### <a name="truncation"></a>Truncation  
 Selecione como o destino ODBC deve tratar truncamento em um fluxo: ignorar a falha, redirecionar a linha ou causar falha no componente.  
  
### <a name="description"></a>Description  
 Exiba uma descrição do erro.  
  
### <a name="set-this-value-to-selected-cells"></a>Definir este valor para células selecionadas  
 Selecione como o destino ODBC trata todas as células selecionadas quando ocorre um erro ou um truncamento: ignorar a falha, redirecionar a linha ou causar a falha no componente.  
  
### <a name="apply"></a>Aplicar  
 Aplique as opções de tratamento de erros às células selecionadas.  
  
## <a name="error-handling-options"></a>Opções de tratamento de erros  
 Você usa as opções a seguir para configurar como o destino ODBC trata erros e truncamentos.  
  
### <a name="fail-component"></a>Falha no Componente  
 A tarefa Fluxo de Dados falha quando ocorre um erro ou um truncamento. Esse é o comportamento padrão.  
  
### <a name="ignore-failure"></a>Ignorar Falha  
 O erro ou o truncamento é ignorado.  
  
### <a name="redirect-flow"></a>Redirecionar fluxo  
 A linha que está causando o erro ou o truncamento é direcionada para a saída do erro do destino ODBC. Para obter mais informações, consulte Destino ODBC.  
  
## <a name="see-also"></a>Consulte também  
 [Editor de destino ODBC &#40; Página Gerenciador de Conexão &#41;](../../integration-services/data-flow/odbc-destination-editor-connection-manager-page.md)   
 [Editor de destino ODBC &#40; Página mapeamentos &#41;](../../integration-services/data-flow/odbc-destination-editor-mappings-page.md)  
  
  
