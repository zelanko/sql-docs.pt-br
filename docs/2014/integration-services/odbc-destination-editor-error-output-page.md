---
title: Editor de destino ODBC (página saída de erro) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.odbcdest.errorhandling.f1
ms.assetid: 0a743f8d-2a51-4296-9976-8104f5ca22d3
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 82853123767237314edac1e301723724628439d9
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965036"
---
# <a name="odbc-destination-editor-error-output-page"></a>Editor de Destinos ADO NET (página Saída de Erro)
  Use a página **Saída de Erro** da caixa de diálogo **Editor de Destino ODBC** para selecionar as opções para tratamento de erros.  
  
 Para obter mais informações sobre o destino ODBC, consulte [ODBC Destination](data-flow/odbc-destination.md).  
  
 **Para abrir a página Saída de Erro do Editor de Destino ODBC**  
  
## <a name="task-list"></a>Lista de Tarefas  
  
-   No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], abra o pacote [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] que tem o destino ODBC.  
  
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
  
### <a name="description"></a>Descrição  
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
  
## <a name="see-also"></a>Consulte Também  
 [Editor de destinos ODBC &#40;página Gerenciador de conexões&#41;](../../2014/integration-services/odbc-destination-editor-connection-manager-page.md)   
 [Editor de Destinos ODBC &#40;Página Mapeamentos&#41;](../../2014/integration-services/odbc-destination-editor-mappings-page.md)  
  
  
