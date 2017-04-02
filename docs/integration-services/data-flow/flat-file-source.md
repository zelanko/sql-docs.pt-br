---
title: "Fonte de Arquivo Simples | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.flatfilesource.f1"
helpviewer_keywords: 
  - "origens [Integration Services], arquivo simples"
  - "leitura de arquivo de texto [Integration Services]"
  - "arquivos simples"
  - "Fonte de Arquivo Simples"
ms.assetid: 4a64f7f3-f25d-4db0-93b3-a29496030e58
caps.latest.revision: 50
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 50
---
# Fonte de Arquivo Simples
  A fonte de Arquivo Simples lê dados de um arquivo de texto. O arquivo de texto pode ser delimitado, ter largura fixa ou formato misto.  
  
-   O formato delimitado usa delimitadores de coluna e linha para definir colunas e linhas.  
  
-   O formato de largura fixa utiliza a largura para definir colunas e linhas. Esse formato também inclui um caractere para preenchimento de campos na capacidade máxima de sua largura.  
  
-   O formato irregular à direita utiliza largura para definir todas as colunas, exceto a última, que é delimitada pelo delimitador de linha.  
  
 Você pode configurar a fonte de Arquivo Simples das seguintes formas:  
  
-   Adicione uma coluna à saída de transformação que contém o nome do arquivo de texto do qual a fonte de Arquivo Simples extrai os dados.  
  
-   Especifique se a fonte de Arquivo Simples interpreta cadeias de caracteres de comprimento zero em colunas com valores nulos.  
  
    > [!NOTE]  
    >  O gerenciador de conexões de Arquivo Simples que a fonte de Arquivo Simples utiliza deve ser configurado para usar um formato delimitado para interpretar cadeias de caracteres de comprimento zero como nulas. Se o gerenciador de conexões usar largura fixa ou formatos à direita irregulares, os dados que consistem em espaços não poderão ser interpretados como valores nulos.  
  
 As colunas na saída da origem Arquivo Simples incluem a propriedade FastParse. FastParse indica se a coluna usa as rotinas de análise mais rápidas, mas sem distinção de localidade, que são fornecidas pelo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], ou as rotinas de análise padrão com distinção de localidade. Para obter mais informações, consulte [Fast Parse](../Topic/Fast%20Parse.md) e [Standard Parse](../Topic/Standard%20Parse.md).  
  
 Colunas de saída também incluem a propriedade UseBinaryFormat. Use esta propriedade para implementar o suporte a dados binários, como dados com o formato decimal compactado, em arquivos. Por padrão, UseBinaryFormat é definido como **false**. Se quiser usar um formato binário, defina UseBinaryFormat como **true** e o tipo de dados na coluna de saída como **DT_BYTES**. Ao fazer isso, a fonte de Arquivo Simples ignora a conversão de dados e transfere os dados para a coluna de saída como estão. Você pode usar uma transformação, como Colunas Derivadas ou Conversão de Dados para converter os dados **DT_BYTES** em um tipo de dados diferente ou pode escrever scripts personalizados em uma transformação de scripts para interpretar os dados. Você também pode escrever um componente de fluxo de dados personalizado para interpretar os dados. Para obter mais informações sobre que tipo de dados você pode converter **DT_BYTES**, consulte [Converter &#40;Expressão SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 Essa fonte utiliza um gerenciador de conexões de arquivos simples para acessar o arquivo de texto. Definindo propriedades no gerenciador de conexões de arquivos simples, você pode fornecer informações sobre o arquivo e cada coluna nele contido, e especificar como a fonte de Arquivo Simples deverá tratar os dados no arquivo de texto. Por exemplo, você pode especificar os caracteres que delimitam colunas e linhas no arquivo e o tipo de dados e o comprimento de cada coluna. Para obter mais informações, consulte [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
 Essa fonte tem uma saída e uma saída de erro.  
  
## Configuração da origem Arquivo Simples  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor de Fonte de Arquivo Simples**, clique em um dos seguintes tópicos:  
  
-   [Editor de Fonte de Arquivo Simples &#40;Página Gerenciador de Conexões&#41;](../../integration-services/data-flow/flat-file-source-editor-connection-manager-page.md)  
  
-   [Editor de Fonte de Arquivo Simples &#40;Página Colunas&#41;](../../integration-services/data-flow/flat-file-source-editor-columns-page.md)  
  
-   [Editor de Fonte de Arquivo Simples &#40;Página Saída de Erro&#41;](../../integration-services/data-flow/flat-file-source-editor-error-output-page.md)  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../Topic/Common%20Properties.md)  
  
-   [Propriedades personalizadas de arquivo simples](../../integration-services/data-flow/flat-file-custom-properties.md)  
  
## Tarefas relacionadas  
 Para obter detalhes sobre como definir as propriedades de um componente de fluxo de dados, consulte [Definir as propriedades de um componente de fluxo de dados](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## Consulte também  
 [Destino de arquivo simples](../../integration-services/data-flow/flat-file-destination.md)   
 [Fluxo de Dados](../../integration-services/data-flow/data-flow.md)  
  
  