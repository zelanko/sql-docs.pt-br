---
title: Editor de origem ODBC (página saída de erro) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.odbcsource.errorhandling.f1
ms.assetid: b2f6866c-db07-4cb3-9f38-889f8d2b03e6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b19a94e71eaef45184c1777ce299809b2b2d7f8d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66057124"
---
# <a name="odbc-source-editor-error-output-page"></a>Editor de Origem ODBC (página Saída de Erro)
  Use a página **Saída de Erro** da caixa de diálogo **Editor de Origem ODBC** para selecionar as opções para tratamento de erros.  
  
 Para obter mais informações sobre a origem ODBC, consulte [CDC Source](data-flow/cdc-source.md).  
  
## <a name="task-list"></a>Lista de Tarefas  
 **Para abrir a página Saída de Erro do Editor de Origem ODBC**  
  
-   No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], abra o pacote [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] que tem a fonte ODBC.  
  
-   Na guia **Fluxo de Dados** , clique duas vezes na fonte ODBC.  
  
-   No **Editor de Origem ODBC**, clique em **Saída de Erro**.  
  
## <a name="options"></a>Opções  
  
### <a name="inputoutput"></a>Entrada/Saída  
 Exibe o nome da fonte de dados.  
  
### <a name="column"></a>Coluna  
 Não usado.  
  
### <a name="error"></a>Erro  
 Selecione como a origem ODBC deve tratar erros em um fluxo: ignorar a falha, redirecionar a linha ou causar falha no componente.  
  
### <a name="truncation"></a>Truncation  
 Selecione como a origem ODBC deve tratar o truncamento em um fluxo: ignorar a falha, redirecionar a linha ou causar falha no componente.  
  
### <a name="description"></a>Descrição  
 Não usado.  
  
### <a name="set-this-value-to-selected-cells"></a>Definir este valor para células selecionadas  
 Selecione como a origem ODBC trata todas as células selecionadas quando ocorre um erro ou um truncamento: ignorar a falha, redirecionar a linha ou causar a falha no componente.  
  
### <a name="apply"></a>Aplicar  
 Aplique as opções de tratamento de erros às células selecionadas.  
  
## <a name="error-handling-options"></a>Opções de tratamento de erros  
 Você usa as opções a seguir para configurar como a origem ODBC trata erros e truncamentos.  
  
### <a name="fail-component"></a>Falha no Componente  
 A tarefa Fluxo de Dados falha quando ocorre um erro ou um truncamento. Esse é o comportamento padrão.  
  
### <a name="ignore-failure"></a>Ignorar Falha  
 O erro ou o truncamento é ignorado.  
  
### <a name="redirect-flow"></a>Redirecionar fluxo  
 A linha que está causando o erro ou o truncamento é direcionada para a saída do erro da origem ODBC. Para obter mais informações, consulte [ODBC Source](data-flow/odbc-source.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Editor de origem ODBC &#40;página Gerenciador de conexões&#41;](../../2014/integration-services/odbc-source-editor-connection-manager-page.md)   
 [Editor de Origem ODBC &#40;Página Colunas&#41;](../../2014/integration-services/odbc-source-editor-columns-page.md)  
  
  
