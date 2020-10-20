---
description: Transformação Exportar Colunas
title: Transformação Exportar Colunas | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.exportcolumntrans.f1
- sql13.dts.designer.fileextractortransformation.columns.f1
- sql13.dts.designer.fileextractortransformation.errorhandling.f1
helpviewer_keywords:
- exporting data
- append options [Integration Services]
- Export Column transformation [Integration Services]
- columns [Integration Services], exporting
- inserting data
- truncate options [Integration Services]
ms.assetid: 678d2dfc-e40c-4fbb-b2cc-42fffc44478a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1cf2f0799896bfaac652e00a7736a0de3d8be97e
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194598"
---
# <a name="export-column-transformation"></a>Transformação Exportar Colunas

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  A transformação Exportar Coluna lê dados em um fluxo de dados e os insere em um arquivo. Por exemplo, se o fluxo de dados contiver informações de produtos, como uma imagem de cada produto, você poderá usar a transformação Exportar Coluna para salvar essas imagens em arquivos.  
  
## <a name="append-and-truncate-options"></a>Opções de anexar e truncar  
 A tabela seguinte descreve como as definições das opções anexar e truncar afetam os resultados.  
  
|Acrescentar|Truncate|O arquivo existe|Resultados|  
|------------|--------------|-----------------|-------------|  
|Falso|Falso|Não|A transformação cria um novo arquivo e grava os dados nele.|  
|True|Falso|Não|A transformação cria um novo arquivo e grava os dados nele.|  
|Falso|True|Não|A transformação cria um novo arquivo e grava os dados nele.|  
|True|True|Não|A transformação falha na validação do tempo de design. Ela não é válida para definir ambas as propriedades como **true**.|  
|Falso|Falso|Sim|Ocorre um erro em tempo de execução. O arquivo existe, mas a transformação não pode ser gravada nele.|  
|Falso|True|Sim|A transformação exclui e recria o arquivo e grava os dados nele.|  
|True|Falso|Sim|A transformação abre o arquivo e grava os dados no final do arquivo.|  
|True|True|Sim|A transformação falha na validação do tempo de design. Ela não é válida para definir ambas as propriedades como **true**.|  
  
## <a name="configuration-of-the-export-column-transformation"></a>Configuração da transformação Exportar Coluna  
 Pode-se configurar a transformação Exportar Coluna com os seguintes procedimentos:  
  
-   Especifique as colunas de dados e as colunas que contêm o caminho dos arquivos onde os dados são gravados.  
  
-   Especificar se a operação de inserção de dados anexa ou trunca arquivos existentes.  
  
-   Especificar se uma BOM (marca de ordem de byte) é gravada no arquivo.  
  
    > [!NOTE]  
    >  Uma BOM só é gravada quando os dados não são anexados a um arquivo existente e eles são do tipo DT_NTEXT.  
  
 A transformação usa pares de colunas de entrada; uma coluna contém um nome de arquivo e a outra contém os dados. Cada linha no conjunto de dados pode especificar um arquivo diferente. Como a transformação processa uma linha, os dados são inseridos no arquivo especificado. No tempo de execução, a transformação cria os arquivos caso eles ainda não existam e, posteriormente, grava os dados nos arquivos. Os dados a serem gravados devem ser do tipo DT_TEXT, DT_NTEXT ou DT_IMAGE. Para obter mais informações, consulte [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md).  
  
 Essa transformação tem uma entrada, uma saída e uma saída de erro.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../set-the-properties-of-a-data-flow-component.md)  
  
-   [Propriedades personalizadas de Transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="export-column-transformation-editor-columns-page"></a>Editor de Transformação Exportar Colunas (página Colunas)
  Use a página **Colunas** da caixa de diálogo **Exportar Editor de Transformação Colunas** para especificar as colunas no fluxo de dados a serem extraídas para arquivos. Você pode especificar se a transformação Exportar Coluna acrescenta dados a um arquivo ou substitui um arquivo existente.  
  
### <a name="options"></a>Opções  
 **Extrair Coluna**  
 Selecione na lista de colunas de entrada que contêm dados de texto ou de imagem. Todas as linhas devem ter definições para **Extrair Coluna** e **Coluna de Caminho de Arquivos**.  
  
 **Coluna de Caminho de Arquivos**  
 Selecione na lista de colunas de entrada que contêm caminhos e nomes de arquivo. Todas as linhas devem ter definições para **Extrair Coluna** e **Coluna de Caminho de Arquivos**.  
  
 **Permitir Acréscimo**  
 Especifique se a transformação acrescenta dados a arquivos existentes. O padrão é **false**.  
  
 **Forçar Truncamento**  
 Especifique se a transformação exclui o conteúdo dos arquivos existentes antes de gravar dados. O padrão é **false**.  
  
 **Gravar BOM**  
 Especifique se deve ser gravada uma BOM (marca de ordem de byte) no arquivo. Uma BOM só será gravada se os dados forem do tipo **DT_NTEXT** ou DT_WSTR e não estiverem anexados a um arquivo de dados existente.  
  
## <a name="export-column-transformation-editor-error-output-page"></a>Exportar Editor de Transformação Colunas (página Saída de Erro)
  Use a página **Saída de Erro** da caixa de diálogo do **Editor de Transformação Exportar Colunas** para especificar como manipular os erros.  
  
### <a name="options"></a>Opções  
 **Entrada/Saída**  
 Visualize o nome da saída. Clique no nome para expandir a exibição a fim de incluir colunas.  
  
 **Coluna**  
 Exiba as colunas de saída que você selecionou na página **Colunas** da caixa de diálogo **Editor de Transformação Exportar Colunas** .  
  
 **Erro**  
 Especifique o que deve acontecer se ocorrer um erro: ignorar a falha, redirecionar a linha ou causar falha do componente.  
  
 **Truncation**  
 Especifique o que deve acontecer se ocorrer um truncamento: ignorar a falha, redirecionar a linha ou causar falha do componente.  
  
 **Descrição**  
 Visualize a descrição da operação.  
  
 **Definir este valor para células selecionadas**  
 Especifique o que deve acontecer a todas as células selecionadas quando ocorre um erro ou um truncamento: ignorar a falha, redirecionar a linha ou causar a falha no componente.  
  
 **Aplicar**  
 Aplique a opção de tratamento de erros às células selecionadas.  
  
