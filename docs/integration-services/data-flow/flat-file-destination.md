---
title: Simples de destino do arquivo | Microsoft Docs
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
- sql13.dts.designer.flatfiledest.f1
helpviewer_keywords:
- flat files
- Flat File destination
- text file writing [Integration Services]
- destinations [Integration Services], Flat File
ms.assetid: e0d6e356-8db4-48aa-ba66-029397f98f61
caps.latest.revision: 49
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 78a0ec526f83dcab8d7358ef5a51f1f6ccfd0a04
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="flat-file-destination"></a>Destino de arquivo simples
  O destino de Arquivo Simples grava dados em um arquivo de texto. O arquivo de texto pode ser em formato delimitado, de largura fixa, largura fixa com delimitador de linha ou com imperfeição à direita.  
  
 Você pode configurar o destino de arquivo simples das seguintes formas:  
  
-   Forneça um bloco de texto que é inserido no arquivo antes de qualquer dado ser escrito. O texto pode fornecer informações como cabeçalhos de coluna.  
  
-   Especifique se os dados devem ser substituídos em um arquivo de destino que tenha o mesmo nome.  
  
 Esse destino utiliza um gerente de conexões de arquivo simples para acessar o arquivo de texto. Ao definir propriedades no gerenciador de conexões de arquivo simples que o arquivo simples usa, você pode especificar como o destino do arquivo simples formata e escreve o arquivo de texto. Quando você configura o gerenciador de conexões de arquivo simples, você especifica informações sobre o arquivo e sobre cada coluna do arquivo. Por exemplo, pode-se especificar os caracteres que delimitam colunas e linhas no arquivo e especificar o tipo de dados e o comprimento de cada coluna. Para obter mais informações, consulte [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
 O destino de arquivo simples inclui a propriedade personalizada Header. Essa propriedade pode ser atualizada por uma expressão de propriedade quando o pacote é carregado. Para obter mais informações, consulte [Expressões do Integration Services &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md), [Usar expressões de propriedade em pacotes](../../integration-services/expressions/use-property-expressions-in-packages.md) e [Propriedades personalizadas de arquivo simples](../../integration-services/data-flow/flat-file-custom-properties.md).  
  
 Esse destino tem uma saída. Não dá suporte a uma saída de erro.  
  
## <a name="configuration-of-the-flat-file-destination"></a>Configuração do destino de Arquivo Simples  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor de Fonte de Arquivo Simples** , clique em um dos seguintes tópicos:  
  
-   [Editor de Destino de Arquivo Simples &#40;Página Gerenciador de Conexões&#41;](../../integration-services/data-flow/flat-file-destination-editor-connection-manager-page.md)  
  
-   [Editor de Destino de Arquivo Simples &#40;Página Mapeamentos&#41;](../../integration-services/data-flow/flat-file-destination-editor-mappings-page.md)  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas de arquivo simples](../../integration-services/data-flow/flat-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
 Para obter informações sobre como definir as propriedades do componente de fluxo de dados, consulte [Definir as propriedades de um componente de fluxo de dados](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Consulte também  
 [Fonte de Arquivo Simples](../../integration-services/data-flow/flat-file-source.md)   
 [Fluxo de Dados](../../integration-services/data-flow/data-flow.md)  
  
  
