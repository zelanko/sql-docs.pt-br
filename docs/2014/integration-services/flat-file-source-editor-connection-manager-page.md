---
title: Editor de fonte de arquivo simples (página Gerenciador de conexões) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.flatfilesourceadapter.connection.f1
helpviewer_keywords:
- Flat File Source Editor
ms.assetid: 2efd6baa-ed75-4f3f-b667-514024cebdb8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d3c729faa93cf445e7e0aff46fa94258bc7ea7a4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66058687"
---
# <a name="flat-file-source-editor-connection-manager-page"></a>Editor de Fonte de Arquivo Simples (página Gerenciador de Conexões)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Fonte de Arquivo Simples** para selecionar o gerenciador de conexões que a fonte do arquivo simples usará. A fonte de Arquivo Simples lê dados de um arquivo de texto, que pode estar em formato de largura delimitada, fixa ou mista.  
  
 Uma fonte de Arquivo Simples pode usar um dos seguintes tipos de gerenciadores de conexões:  
  
-   Um gerenciador de conexões de Arquivo Simples se a fonte for um arquivo simples. Para obter mais informações, consulte [Flat File Connection Manager](connection-manager/file-connection-manager.md).  
  
-   Um gerenciador de conexões de Vários Arquivos Simples se a fonte corresponder a vários arquivos simples e a tarefa Fluxo de Dados estiver dentro de um contêiner de loop, como o contêiner de Loop For. Em cada loop do contêiner, a fonte de Arquivo Simples carrega dados do nome de arquivo seguinte fornecido pelo gerenciador de conexões de Vários Arquivos Simples. Para obter mais informações, consulte [Gerenciador de conexões de vários arquivos simples](connection-manager/multiple-flat-files-connection-manager.md).  
  
 Para saber mais sobre a fonte de Arquivo Simples, consulte [Flat File Source](data-flow/flat-file-source.md).  
  
## <a name="options"></a>Opções  
 **Gerenciador de conexões de arquivos simples**  
 Selecione um gerenciador de conexões na lista ou crie um novo gerenciador de conexões clicando em **Novo**.  
  
 **Novo**  
 Crie um novo gerenciador de conexões, usando a caixa de diálogo **Editor de Gerenciador de Conexões de Arquivo Simples** .  
  
 **Reter valores nulos da origem como valores nulos no fluxo de dados**  
 Especifique se os valores nulos devem ser mantidos na extração dos dados. O valor padrão dessa propriedade é **false**. Quando o valor é f`alse`, a fonte de Arquivo Simples substitui valores nulos dos dados de fonte por valores padrão apropriados para cada coluna, como cadeias de caracteres vazias, no caso de colunas de cadeia de caracteres, e zero, no caso de colunas numéricas.  
  
 **Visualizar**  
 Visualize os resultados usando a caixa de diálogo **Exibição de Dados** . A visualização pode exibir até 200 linhas.  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services referência de erro e mensagem](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de fonte de arquivo simples &#40;página colunas&#41;](../../2014/integration-services/flat-file-source-editor-columns-page.md)   
 [Editor de fonte de arquivo simples &#40;página saída de erro&#41;](../../2014/integration-services/flat-file-source-editor-error-output-page.md)   
 [Gerenciador de conexões de arquivos simples](connection-manager/file-connection-manager.md)  
  
  
