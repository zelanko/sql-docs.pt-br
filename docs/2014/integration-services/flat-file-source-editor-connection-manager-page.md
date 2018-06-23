---
title: Editor de origem do arquivo (página Gerenciador de Conexão) simples | Microsoft Docs
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
- sql12.dts.designer.flatfilesourceadapter.connection.f1
helpviewer_keywords:
- Flat File Source Editor
ms.assetid: 2efd6baa-ed75-4f3f-b667-514024cebdb8
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 72cf4b3ee9dbcedb7a8f917328a0bdb715ba575a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007310"
---
# <a name="flat-file-source-editor-connection-manager-page"></a>Editor de Fonte de Arquivo Simples (página Gerenciador de Conexões)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Fonte de Arquivo Simples** para selecionar o gerenciador de conexões que a fonte do arquivo simples usará. A fonte de Arquivo Simples lê dados de um arquivo de texto, que pode estar em formato de largura delimitada, fixa ou mista.  
  
 Uma fonte de Arquivo Simples pode usar um dos seguintes tipos de gerenciadores de conexões:  
  
-   Um gerenciador de conexões de Arquivo Simples se a fonte for um arquivo simples. Para obter mais informações, consulte [Flat File Connection Manager](connection-manager/file-connection-manager.md).  
  
-   Um gerenciador de conexões de Vários Arquivos Simples se a fonte corresponder a vários arquivos simples e a tarefa Fluxo de Dados estiver dentro de um contêiner de loop, como o contêiner de Loop For. Em cada loop do contêiner, a fonte de Arquivo Simples carrega dados do nome de arquivo seguinte fornecido pelo gerenciador de conexões de Vários Arquivos Simples. Para obter mais informações, consulte [Gerenciador de conexões de vários arquivos simples](connection-manager/multiple-flat-files-connection-manager.md).  
  
 Para saber mais sobre a fonte de Arquivo Simples, consulte [Flat File Source](data-flow/flat-file-source.md).  
  
## <a name="options"></a>Opções  
 **Flat file connection manager**  
 Selecione um gerenciador de conexões na lista ou crie um novo gerenciador de conexões clicando em **Novo**.  
  
 **Nova**  
 Crie um novo gerenciador de conexões, usando a caixa de diálogo **Editor de Gerenciador de Conexões de Arquivo Simples** .  
  
 **Reter valores nulos da origem como valores nulos no fluxo de dados**  
 Especifique se os valores nulos devem ser mantidos na extração dos dados. O valor padrão dessa propriedade é **false**. Quando o valor é f`alse`, a fonte de Arquivo Simples substitui valores nulos dos dados de fonte por valores padrão apropriados para cada coluna, como cadeias de caracteres vazias, no caso de colunas de cadeia de caracteres, e zero, no caso de colunas numéricas.  
  
 **Visualização**  
 Visualize os resultados usando a caixa de diálogo **Exibição de Dados** . A visualização pode exibir até 200 linhas.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de origem de arquivo simples &#40;página colunas&#41;](../../2014/integration-services/flat-file-source-editor-columns-page.md)   
 [Editor de origem de arquivo simples &#40;página de saída de erro&#41;](../../2014/integration-services/flat-file-source-editor-error-output-page.md)   
 [Gerenciador de Conexões de Arquivos Simples](connection-manager/file-connection-manager.md)  
  
  