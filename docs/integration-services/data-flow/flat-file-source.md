---
title: Origem do arquivo simples | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.flatfilesource.f1
- sql13.dts.designer.flatfilesourceadapter.connection.f1
- sql13.dts.designer.flatfilesourceadapter.columns.f1
- sql13.dts.designer.flatfilesourceadapter.errorhandling.f1
helpviewer_keywords:
- sources [Integration Services], Flat File
- text file reading [Integration Services]
- flat files
- Flat File source
ms.assetid: 4a64f7f3-f25d-4db0-93b3-a29496030e58
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 0f8f9bd1a31fd395daea280a4718f87e12c774de
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67941492"
---
# <a name="flat-file-source"></a>Fonte de Arquivo Simples

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  A fonte de Arquivo Simples lê dados de um arquivo de texto. O arquivo de texto pode ser delimitado, ter largura fixa ou formato misto.  
  
-   O formato delimitado usa delimitadores de coluna e linha para definir colunas e linhas.  
  
-   O formato de largura fixa utiliza a largura para definir colunas e linhas. Esse formato também inclui um caractere para preenchimento de campos na capacidade máxima de sua largura.  
  
-   O formato irregular à direita utiliza largura para definir todas as colunas, exceto a última, que é delimitada pelo delimitador de linha.  
  
 Você pode configurar a fonte de Arquivo Simples das seguintes formas:  
  
-   Adicione uma coluna à saída de transformação que contém o nome do arquivo de texto do qual a fonte de Arquivo Simples extrai os dados.  
  
-   Especifique se a fonte de Arquivo Simples interpreta cadeias de caracteres de comprimento zero em colunas com valores nulos.  
  
    > [!NOTE]  
    >  O gerenciador de conexões de Arquivo Simples que a fonte de Arquivo Simples utiliza deve ser configurado para usar um formato delimitado para interpretar cadeias de caracteres de comprimento zero como nulas. Se o gerenciador de conexões usar largura fixa ou formatos à direita irregulares, os dados que consistem em espaços não poderão ser interpretados como valores nulos.  
  
 As colunas na saída da origem Arquivo Simples incluem a propriedade FastParse. FastParse indica se a coluna usa as rotinas de análise mais rápidas, mas sem distinção de localidade, que são fornecidas pelo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , ou as rotinas de análise padrão com distinção de localidade. Para obter mais informações, consulte [Fast Parse](https://msdn.microsoft.com/library/6688707d-3c5b-404e-aa2f-e13092ac8d95) e [Standard Parse](https://msdn.microsoft.com/library/dfe835b1-ea52-4e18-a23a-5188c5b6f013).  
  
 Colunas de saída também incluem a propriedade UseBinaryFormat. Use esta propriedade para implementar o suporte a dados binários, como dados com o formato decimal compactado, em arquivos. Por padrão, UseBinaryFormat é definido como **false**. Se quiser usar um formato binário, defina UseBinaryFormat como **true** e o tipo de dados na coluna de saída como **DT_BYTES**. Ao fazer isso, a fonte de Arquivo Simples ignora a conversão de dados e transfere os dados para a coluna de saída como estão. Você pode usar uma transformação, como Colunas Derivadas ou Conversão de Dados para converter os dados **DT_BYTES** em um tipo de dados diferente ou pode escrever scripts personalizados em uma transformação de scripts para interpretar os dados. Você também pode escrever um componente de fluxo de dados personalizado para interpretar os dados. Para obter mais informações sobre que tipo de dados você pode converter **DT_BYTES**, consulte [Converter &#40;Expressão SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 Essa fonte utiliza um gerenciador de conexões de arquivos simples para acessar o arquivo de texto. Definindo propriedades no gerenciador de conexões de arquivos simples, você pode fornecer informações sobre o arquivo e cada coluna nele contido, e especificar como a fonte de Arquivo Simples deverá tratar os dados no arquivo de texto. Por exemplo, você pode especificar os caracteres que delimitam colunas e linhas no arquivo e o tipo de dados e o comprimento de cada coluna. Para obter mais informações, consulte [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
 Essa fonte tem uma saída e uma saída de erro.  
  
## <a name="configuration-of-the-flat-file-source"></a>Configuração da origem Arquivo Simples  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas de arquivo simples](../../integration-services/data-flow/flat-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter detalhes sobre como definir as propriedades de um componente de fluxo de dados, consulte [Definir as propriedades de um componente de fluxo de dados](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="flat-file-source-editor-connection-manager-page"></a>Editor de Fonte de Arquivo Simples (página Gerenciador de Conexões)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Fonte de Arquivo Simples** para selecionar o gerenciador de conexões que a fonte do arquivo simples usará. A fonte de Arquivo Simples lê dados de um arquivo de texto, que pode estar em formato de largura delimitada, fixa ou mista.  
  
 Uma fonte de Arquivo Simples pode usar um dos seguintes tipos de gerenciadores de conexões:  
  
-   Um gerenciador de conexões de Arquivo Simples se a fonte for um arquivo simples. Para obter mais informações, consulte [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
-   Um gerenciador de conexões de Vários Arquivos Simples se a fonte corresponder a vários arquivos simples e a tarefa Fluxo de Dados estiver dentro de um contêiner de loop, como o contêiner de Loop For. Em cada loop do contêiner, a fonte de Arquivo Simples carrega dados do nome de arquivo seguinte fornecido pelo gerenciador de conexões de Vários Arquivos Simples. Para obter mais informações, consulte [Gerenciador de conexões de vários arquivos simples](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md).  
  
### <a name="options"></a>Opções  
 **Flat file connection manager**  
 Selecione um gerenciador de conexões na lista ou crie um novo gerenciador de conexões clicando em **Novo**.  
  
 **Nova**  
 Crie um novo gerenciador de conexões, usando a caixa de diálogo **Editor de Gerenciador de Conexões de Arquivo Simples** .  
  
 **Reter valores nulos da origem como valores nulos no fluxo de dados**  
 Especifique se os valores nulos devem ser mantidos na extração dos dados. O valor padrão dessa propriedade é **false**. Quando o valor é f**alse**, a fonte de Arquivo Simples substitui valores nulos dos dados de origem por valores padrão apropriados para cada coluna, como cadeias de caracteres vazias, no caso de colunas de cadeia de caracteres, e zero, no caso de colunas numéricas.  
  
 **Visualização**  
 Visualize os resultados usando a caixa de diálogo **Exibição de Dados** . A visualização pode exibir até 200 linhas.  
  
## <a name="flat-file-source-editor-columns-page"></a>Editor de Fonte de Arquivo Simples (página Colunas)
  Use o nó **Colunas** da caixa de diálogo **Editor de Fonte de Arquivo Simples** para mapear uma coluna de saída para cada coluna externa (fonte).  
  
> [!NOTE]  
>  A propriedade **FileNameColumnName** da fonte de Arquivo Simples e a propriedade **FastParse** de suas colunas de saída não estão disponíveis no **Editor de Fonte de Arquivo Simples**, mas pode ser definida por meio do **Editor Avançado**. Para obter mais informações sobre estas propriedades, consulte a seção Fonte de Arquivo Simples em [Flat File Custom Properties](../../integration-services/data-flow/flat-file-custom-properties.md).  
  
### <a name="options"></a>Opções  
 **Colunas Externas Disponíveis**  
 Exiba a lista de colunas externas disponíveis na fonte de dados. Você não pode usar esta tabela para adicionar ou excluir colunas.  
  
 **Coluna Externa**  
 Exiba as colunas externas (fonte) na ordem em que serão lidas pela tarefa. É possível alterar esta ordem desmarcando as colunas selecionadas na tabela e selecionando as colunas externas da lista em uma ordem diferente.  
  
 **Coluna de Saída**  
 Forneça um nome exclusivo para cada coluna de saída. O padrão é o nome da coluna externa (origem) selecionada; porém, é possível escolher qualquer nome descritivo exclusivo. O nome fornecido será exibido no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
## <a name="flat-file-source-editor-error-output-page"></a>Editor de Fonte de Arquivo Simples (página Saída de Erro)
  Use a página **Saída de Erro** da caixa de diálogo **Editor de Fonte de Arquivo Simples** para selecionar opções de tratamento de erros e definir propriedades nas colunas de saída de erros.\  
  
### <a name="options"></a>Opções  
 **Entrada/Saída**  
 Exibe o nome da fonte de dados.  
  
 **Coluna**  
 Exibe as colunas externas (fonte) selecionadas na página **Gerenciador de Conexões** da caixa de diálogo **Editor de Fonte de Arquivo Simples**.  
  
 **Erro**  
 Especifique o que deve acontecer quando ocorre um erro: ignorar a falha, redirecionar a linha ou causar falha no componente.  
  
 **Tópicos relacionados:** [Tratamento de erro em dados](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **Truncation**  
 Especifique o que deve acontecer quando ocorre um truncamento: ignorar a falha, redirecionar a linha ou causar falha do componente.  
  
 **Descrição**  
 Exiba a descrição do erro.  
  
 **Definir este valor para células selecionadas**  
 Especifique o que deve acontecer a todas as células selecionadas quando ocorre um erro ou um truncamento: ignorar a falha, redirecionar a linha ou causar a falha no componente.  
  
 **Aplicar**  
 Aplique a opção de tratamento de erros às células selecionadas.  
  
## <a name="see-also"></a>Consulte Também  
 [Destino de arquivo simples](../../integration-services/data-flow/flat-file-destination.md)   
 [Fluxo de Dados](../../integration-services/data-flow/data-flow.md)  
  
  
