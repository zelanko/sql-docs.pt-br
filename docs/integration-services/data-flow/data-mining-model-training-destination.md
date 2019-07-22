---
title: Destino de treinamento do modelo de mineração de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataminingmodeltrainingdest.f1
- sql13.dts.designer.dmmtrainingtransformation.connection.f1
- sql13.dts.designer.dmmtrainingtransformation.columns.f1
helpviewer_keywords:
- destinations [Integration Services], Data Mining Model Training
- Data Mining Model Training destination
- mining models [Analysis Services], training
- training mining models
ms.assetid: 6bc8cbe2-46af-4f7b-93d6-86779313c9d7
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 6a148af7be04bba6bdf5c16ca7e85e94f1a0de31
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68049444"
---
# <a name="data-mining-model-training-destination"></a>Destino de treinamento do modelo de mineração de dados

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Um destino de treinamento de modelos de mineração de dados treina modelos de mineração de dados ao passar os dados que o destino recebe pelos algoritmos de modelo de mineração de dados. Vários modelos de mineração de dados poderão ser treinados por um destino se os modelos forem criados na mesma estrutura de mineração de dados. Para obter mais informações, consulte [Mining Structure Columns](../../analysis-services/data-mining/mining-structure-columns.md) e [Mining Model Columns](../../analysis-services/data-mining/mining-model-columns.md).  
  
## <a name="configuration-of-the-data-mining-model-training-destination"></a>Configuração do destino Treinamento de Modelo de Mineração de Dados  
 Se uma coluna de nível de caso da estrutura de destino e os modelos criados na estrutura tiverem o tipo de conteúdo KEY TIME ou KEY SEQUENCE, os dados de entrada deverão ser classificados nessa coluna. Por exemplo, os modelos criados pelo algoritmo do Microsoft Time Series utilizam o tipo de conteúdo KEY TIME. Se os dados de entrada não forem classificados, o processamento do modelo poderá falhar. Se os dados exigirem a classificação, você poderá usar uma transformação do tipo Classificação antecipadamente no fluxo de dados para classificá-los. Esse requisito não se aplica a colunas com o tipo de conteúdo KEY. Para obter mais informações, consulte [Tipos de Conteúdo &#40; mineração de dados&#41;](../../analysis-services/data-mining/content-types-data-mining.md) e [Transformação Sort](../../integration-services/data-flow/transformations/sort-transformation.md).  
  
> [!NOTE]  
>  A entrada para o destino Treinamento de Modelo de Mineração de Dados deve ser classificada. Para classificar os dados, você pode incluir um upstream de destino do tipo Classificação a partir do destino Treinamento de Modelo de Mineração de Dados no fluxo de dados. Para obter mais informações, consulte [Sort Transformation](../../integration-services/data-flow/transformations/sort-transformation.md).  
  
 Este destino tem uma entrada e nenhuma saída.  
  
 O destino Treinamento de Modelo de Mineração de Dados utiliza um gerenciador de conexões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que se conecta ao projeto ou à instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que contém a estrutura de mineração e os modelos de mineração treinados pelo destino. Para obter mais informações, consulte [Analysis Services Connection Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md).  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas do destino Treinamento do Modelo de Mineração de Dados](../../integration-services/data-flow/data-mining-model-training-destination-custom-properties.md)  
  
 Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades de um componente de fluxo de dados](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="data-mining-model-training-editor-connection-tab"></a>Editor de Treinamento de Modelo de Mineração de Dados (guia Conexão)
  Use a página **Conexão** da caixa de diálogo **Editor de Treinamento do Modelo de Mineração de Dados** para selecionar um modelo de mineração para treinar.  
  
### <a name="options"></a>Opções  
 **Gerenciador de conexões**  
 Selecione na lista de conexões existentes do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou crie uma nova conexão do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando o botão **Novo** como descrito abaixo.  
  
 **Nova**  
 Crie uma nova conexão usando a caixa de diálogo **Adicionar Gerenciador de Conexões do Analysis Services** .  
  
 **Estrutura de mineração**  
 Selecione na lista de estruturas de mineração disponíveis ou crie uma estrutura nova clicando em **Novo**.  
  
 **Nova**  
 Crie uma estrutura e modelo de mineração novos usando o **Assistente de Mineração de Dados**.  
  
 **Modelos de mineração**  
 Exiba a lista de modelos de mineração associada com a estrutura de mineração selecionada.  
  
## <a name="data-mining-model-training-editor-columns-tab"></a>Editor de Treinamento de Modelo de Mineração de Dados (guia Colunas)
  Use a página **Colunas** da caixa de diálogo do **Editor de Treinamento do Modelo de Mineração de Dados** para mapear colunas de entrada para colunas na estrutura de mineração.  
  
## <a name="options"></a>Opções  
 **Colunas de Entrada Disponíveis**  
 Exiba a lista das colunas de entrada disponíveis. Arraste colunas de entrada para mapeá-las para as colunas de estrutura de mineração.  
  
 **Colunas da estrutura de mineração**  
 Exiba a lista de colunas de estrutura de mineração. Arraste colunas de estrutura de mineração para mapeá-las para as colunas de entrada disponíveis.  
  
 **Coluna de Entrada**  
 Exibir colunas de entrada selecionadas na tabela acima. Para alterar ou remover uma seleção de mapeamento, use a lista de **Colunas de Entrada Disponíveis**.  
  
 **Colunas da estrutura de mineração**  
 Exiba cada coluna de destino disponível, seja mapeada ou não.  
  
