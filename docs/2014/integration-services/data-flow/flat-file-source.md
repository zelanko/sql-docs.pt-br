---
title: Origem do arquivo simples | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.flatfilesource.f1
helpviewer_keywords:
- sources [Integration Services], Flat File
- text file reading [Integration Services]
- flat files
- Flat File source
ms.assetid: 4a64f7f3-f25d-4db0-93b3-a29496030e58
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6338c7a306f163f786f2c1e7d44ae4dbc66504ec
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58380134"
---
# <a name="flat-file-source"></a>Fonte de Arquivo Simples
  A fonte de Arquivo Simples lê dados de um arquivo de texto. O arquivo de texto pode ser delimitado, ter largura fixa ou formato misto.  
  
-   O formato delimitado usa delimitadores de coluna e linha para definir colunas e linhas.  
  
-   O formato de largura fixa utiliza a largura para definir colunas e linhas. Esse formato também inclui um caractere para preenchimento de campos na capacidade máxima de sua largura.  
  
-   O formato irregular à direita utiliza largura para definir todas as colunas, exceto a última, que é delimitada pelo delimitador de linha.  
  
 Você pode configurar a fonte de Arquivo Simples das seguintes formas:  
  
-   Adicione uma coluna à saída de transformação que contém o nome do arquivo de texto do qual a fonte de Arquivo Simples extrai os dados.  
  
-   Especifique se a fonte de Arquivo Simples interpreta cadeias de caracteres de comprimento zero em colunas com valores nulos.  
  
    > [!NOTE]  
    >  O gerenciador de conexões de Arquivo Simples que a fonte de Arquivo Simples utiliza deve ser configurado para usar um formato delimitado para interpretar cadeias de caracteres de comprimento zero como nulas. Se o gerenciador de conexões usar largura fixa ou formatos à direita irregulares, os dados que consistem em espaços não poderão ser interpretados como valores nulos.  
  
 As colunas na saída da origem Arquivo Simples incluem a propriedade FastParse. FastParse indica se a coluna usa as rotinas de análise mais rápidas, mas sem distinção de localidade, que são fornecidas pelo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , ou as rotinas de análise padrão com distinção de localidade. Para obter mais informações, consulte [Fast Parse](../fast-parse.md) e [Standard Parse](../standard-parse.md).  
  
 Colunas de saída também incluem a propriedade UseBinaryFormat. Use esta propriedade para implementar o suporte a dados binários, como dados com o formato decimal compactado, em arquivos. Por padrão, UseBinaryFormat é definido `false`. Se você quiser usar um formato binário, defina UseBinaryFormat como `true` e o tipo de dados na coluna de saída para `DT_BYTES`. Ao fazer isso, a fonte de Arquivo Simples ignora a conversão de dados e transfere os dados para a coluna de saída como estão. Você pode usar uma transformação, como Colunas Derivadas ou Conversão de Dados para lançar os dados `DT_BYTES` a um tipo de dados diferente ou pode escrever scripts personalizados em uma transformação de scripts para interpretar os dados. Você também pode escrever um componente de fluxo de dados personalizado para interpretar os dados. Para obter mais informações sobre quais tipos de dados você podem converter `DT_BYTES` para ver [conversão &#40;expressão do SSIS&#41;](../expressions/cast-ssis-expression.md).  
  
 Essa fonte utiliza um gerenciador de conexões de arquivos simples para acessar o arquivo de texto. Definindo propriedades no gerenciador de conexões de arquivos simples, você pode fornecer informações sobre o arquivo e cada coluna nele contido, e especificar como a fonte de Arquivo Simples deverá tratar os dados no arquivo de texto. Por exemplo, você pode especificar os caracteres que delimitam colunas e linhas no arquivo e o tipo de dados e o comprimento de cada coluna. Para obter mais informações, consulte [Flat File Connection Manager](../connection-manager/file-connection-manager.md).  
  
 Essa fonte tem uma saída e uma saída de erro.  
  
## <a name="configuration-of-the-flat-file-source"></a>Configuração da origem Arquivo Simples  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor de Fonte de Arquivo Simples**, clique em um dos seguintes tópicos:  
  
-   [Editor de Fonte de Arquivo Simples &#40;Página Gerenciador de Conexões&#41;](../flat-file-source-editor-connection-manager-page.md)  
  
-   [Editor de Fonte de Arquivo Simples &#40;Página Colunas&#41;](../flat-file-source-editor-columns-page.md)  
  
-   [Editor de Fonte de Arquivo Simples &#40;Página Saída de Erro&#41;](../flat-file-source-editor-error-output-page.md)  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../common-properties.md)  
  
-   [Propriedades personalizadas de arquivo simples](flat-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter detalhes sobre como definir as propriedades de um componente de fluxo de dados, consulte [Definir as propriedades de um componente de fluxo de dados](set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Consulte também  
 [Destino de arquivo simples](flat-file-destination.md)   
 [Fluxo de Dados](data-flow.md)  
  
  
