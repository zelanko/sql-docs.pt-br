---
title: Editor de origem do ADO NET (página saída de erro) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.adonetsource.erroroutput.f1
ms.assetid: 4dd9d129-a95c-4d3a-bbbf-e84a39089950
caps.latest.revision: 13
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d593b46462f8ca4e4c02431d234ae2aa4f29c197
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37259062"
---
# <a name="ado-net-source-editor-error-output-page"></a>Editor de Origem ADO NET (Página Saída de Erro)
  Use a página **Saída de Erro** da caixa de diálogo **Editor de Origem ADO NET** para selecionar as opções de manipulação de erros e definir as propriedades nas colunas de saída de erros.  
  
 Para obter mais informações sobre a origem ADO NET, consulte [ADO NET Source](data-flow/ado-net-source.md).  
  
 **Para abrir a página Saída de Erro**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que tenha a origem ADO NET.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes na origem ADO NET.  
  
3.  No **Editor de Origem ADO NET**, clique em **Saída de Erro**.  
  
## <a name="options"></a>Opções  
 **Entrada/Saída**  
 Exibe o nome da fonte de dados.  
  
 **Coluna**  
 Exiba as colunas externas (origem) que você selecionou na página **Gerenciador de Conexões** da caixa de diálogo **Editor de Origem ADO NET** .  
  
 **Erro**  
 Especifique o que deve acontecer quando ocorre um erro: ignorar a falha, redirecionar a linha ou causar falha no componente.  
  
 **Tópicos Relacionados:** [Tratamento de erros em dados](data-flow/error-handling-in-data.md)  
  
 **Truncation**  
 Especifique o que deve acontecer quando ocorre um truncamento: ignorar a falha, redirecionar a linha ou causar falha do componente.  
  
 **Descrição**  
 Exiba a descrição do erro.  
  
 **Definir este valor para células selecionadas**  
 Especifique o que deve acontecer a todas as células selecionadas quando ocorre um erro ou um truncamento: ignorar a falha, redirecionar a linha ou causar a falha no componente.  
  
 **Aplicar**  
 Aplique a opção de tratamento de erros às células selecionadas.  
  
## <a name="see-also"></a>Consulte também  
 [Editor de origem do ADO NET &#40;página do Gerenciador de Conexão&#41;](../../2014/integration-services/ado-net-source-editor-connection-manager-page.md)   
 [Editor de origem do ADO NET &#40;página de colunas&#41;](../../2014/integration-services/ado-net-source-editor-columns-page.md)   
 [Gerenciador de conexões ADO.NET](connection-manager/ado-net-connection-manager.md)  
  
  
