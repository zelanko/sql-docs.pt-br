---
title: Processamento de requisitos e considerações (mineração de dados) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d4228f5ae90f7fdd2510787b6fca6ad10f7302e4
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="processing-requirements-and-considerations-data-mining"></a>Requisitos e considerações de processamento (mineração de dados)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Este tópico descreve algumas considerações técnicas para lembrar ao processar objetos de mineração de dados. Para obter uma explicação geral do que é processamento e como isso se aplica à mineração de dados, consulte [Processando objetos de Data Mining](../../analysis-services/data-mining/processing-data-mining-objects.md).  
  
 [Consultas em repositório relacional](#bkmk_QueryReqs)  
  
 [Processando estruturas de mineração](#bkmk_ProcessStructures)  
  
 [Processando os modelos de mineração](#bkmk_ProcessModels)  
  
##  <a name="bkmk_QueryReqs"></a> Consultas no repositório relacional durante o processamento  
 Para a mineração de dados, o processamento tem três fases: consultar a fonte de dados, determinar estatísticas brutas e usar a definição e o algoritmo do modelo para treinar o modelo de mineração.  
  
 O servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] emite consultas para o banco de dados que fornece os dados brutos. Esse banco de dados pode ser uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ou uma versão anterior do mecanismo de banco de dados do SQL Server. Quando você processa uma estrutura de mineração de dados, os dados da fonte são transferidos para a estrutura de mineração e mantidos no disco em um novo formato compactado. Nem todas as colunas da fonte de dados são processadas; apenas as colunas incluídas na estrutura de mineração, de acordo com as associações.  
  
 Usando esses dados, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cria um índice de todas as colunas de dados discretos e dados, e cria um índice à parte para as colunas contínuas. É emitida uma consulta para cada tabela aninhada a fim de criar o índice, e uma consulta adicional por tabela aninhada é gerada para processar relações entre cada par de tabela aninhada e de tabela de casos. O motivo para a criação de várias consultas é processar um repositório de dados multidimensional interno especial. Você pode limitar o número de consultas que o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] envia para o repositório relacional definindo a propriedade de servidor **DatabaseConnectionPoolMax**. Para obter mais informações, consulte [Propriedades OLAP](../../analysis-services/server-properties/olap-properties.md).  
  
 Quando você processa um modelo, ele não relê os dados da fonte de dados. Em vez disso, ele obtém o resumo dos dados da estrutura de mineração. Com o uso do cubo criado, junto com o cache do índice e os dados de caso em cache, o servidor cria threads independentes para treinar os modelos.  
  
 Para obter mais informações sobre as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que dão suporte ao processamento paralelo de modelo, consulte [recursos compatíveis com as edições do SQL Server 2012](http://go.microsoft.com/fwlink/?linkid=232473) (http://go.microsoft.com/fwlink/?linkid=232473).  
  
##  <a name="bkmk_ProcessStructures"></a> Processando estruturas de mineração  
 Uma estrutura de mineração pode ser processada junto com todos os modelos dependentes, ou separadamente. Processar uma estrutura de mineração separadamente de modelos pode ser útil quando é esperado que alguns modelos levem muito tempo para processar e você deseja adiar essa operação.  
  
 Para obter mais informações, consulte [Processar uma estrutura de mineração](../../analysis-services/data-mining/process-a-mining-structure.md).  
  
 Se você estiver preocupado em conservar espaço no disco rígido, observe que a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] retém caches de estrutura de mineração localmente. Ou seja, ela grava todos os dados de treinamento no seu disco rígido local. Se não quiser que seus dados sejam armazenados em cache, poderá alterar o padrão configurando a propriedade <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> na estrutura de mineração como **ClearAfterProcessing**. Isso destruirá o cache após o processamento dos modelos. No entanto, também desabilitará a análise na estrutura de mineração. Para obter mais informações, consulte [Consultas de detalhamento &#40;Mineração de dados&#41;](../../analysis-services/data-mining/drillthrough-queries-data-mining.md).  
  
 Além disso, se limpar o cache, não poderá usar o conjunto de testes de validação, se houver definido um, e a definição da partição do conjunto de testes será perdida. Para obter mais informações sobre como usar conjuntos de dados de controle, consulte [Conjuntos de dados de teste e treinamento](../../analysis-services/data-mining/training-and-testing-data-sets.md).  
  
##  <a name="bkmk_ProcessModels"></a> Processando os modelos de mineração  
 Você pode processar um modelo de mineração separadamente de sua estrutura de mineração associada ou pode processar todos os modelos que estão baseados na estrutura, junto com a estrutura.  
  
 Para obter mais informações, consulte [Processar um modelo de mineração](../../analysis-services/data-mining/process-a-mining-model.md).  
  
 Porém, no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], você não pode selecionar vários modelos de mineração para processar com a estrutura. Se você precisar controlar quais modelos são processados, terá que selecioná-los individualmente ou usar XMLA ou DMX para processar modelos em série.  
  
## <a name="when-reprocessing-is-required"></a>Quando o reprocessamento é necessário  
 Você deve processar os modelos [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] definidos antes de poder começar a trabalhar com eles. Também deve processar novamente os modelos de mineração sempre que mudar a estrutura do modelo de mineração, atualizar os dados de treinamento, alterar um modelo de mineração existente ou adicionar um novo modelo de mineração à estrutura.  
  
 Os modelos de mineração também são processados nestes cenários:  
  
 **Implantação de um projeto**: dependendo das configurações do projeto e do estado atual do projeto, os modelos de mineração no projeto são geralmente processados completamente quando o projeto é implantado.  
  
 Ao iniciar a implantação, o processamento começa automaticamente, a menos que exista uma versão processada anteriormente no servidor [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e não houve mudanças na estrutura. É possível implantar um projeto selecionando **Implantar solução** na lista suspensa ou pressionando a tecla F5. É possível  
  
 Para obter mais informações sobre como definir propriedades de implantação no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que controlam como os modelos de mineração são implantados, consulte [Implantação de soluções de Data Mining](../../analysis-services/data-mining/deployment-of-data-mining-solutions.md).  
  
 **Movendo um modelo de mineração**: quando você move um modelo de mineração usando o comando EXPORT, somente a definição do modelo é exportada, incluindo o nome da estrutura de mineração que é esperada que forneça dados ao modelo.  
  
 Reprocessando requisitos para os cenários a seguir usando os comandos EXPORT e IMPORT:  
  
-   A estrutura de mineração existe na instância de destino e a estrutura de mineração está em um estado não processado.  
  
     A estrutura e o modelo devem ser reprocessados.  
  
-   A estrutura de mineração existe na instância de destino e a estrutura de mineração foi processada. Somente o modelo de mineração foi exportado.  
  
     O modelo pode ser usado sem processamento.  
  
-   A definição de estrutura de mineração também foi exportada usando a palavra-chave WITH DEPENDENCIES.  
  
     A estrutura e o modelo devem ser reprocessados.  
  
 Para obter mais informações, consulte [Exportar e importar objetos de Data Mining](../../analysis-services/data-mining/export-and-import-data-mining-objects.md).  
  
## <a name="see-also"></a>Consulte também  
 [Estruturas de mineração & #40; Analysis Services – mineração de dados & #41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Estruturas de mineração & #40; Analysis Services – mineração de dados & #41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Processar um modelo multidimensional &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)  
  
  
