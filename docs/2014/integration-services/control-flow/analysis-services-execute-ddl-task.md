---
title: Tarefa Executar DDL do Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.asexecuteddltask.f1
helpviewer_keywords:
- Analysis Services Execute DDL task
- DDL
ms.assetid: 7f25c8c6-b601-41f2-9553-be0a2ee0751a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 19da5b920b31791eacaf362819ce731d2822c0c4
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50148101"
---
# <a name="analysis-services-execute-ddl-task"></a>Tarefa Executar DDL do Analysis Services
  A tarefa Executar DLL do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] executa instruções DDL (linguagem de definição de dados) que podem criar, descartar ou alterar modelos de mineração e objetos multidimensionais, como cubos e dimensões. Por exemplo, uma instrução DDL pode criar uma partição no cubo **Adventure Works** ou excluir uma dimensão do [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)], o exemplo de banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] incluído no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 A tarefa Executar DDL do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa um gerenciador de conexões do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para se conectar a uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou a um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Para obter mais informações, consulte [Analysis Services Connection Manager](../connection-manager/analysis-services-connection-manager.md).  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui um número de tarefas que desempenham outras operações de business intelligence, como processamento de objetos analíticos e execução de consultas de previsão de mineração de dados.  
  
 Para obter mais informações sobre tarefas de business intelligence relacionadas, clique em um dos tópicos a seguir:  
  
-   [Tarefa Processamento do Analysis Services](analysis-services-processing-task.md)  
  
-   [Tarefa Consulta de Mineração de Dados](data-mining-query-task.md)  
  
## <a name="ddl-statements"></a>Instruções DDL  
 As instruções DDL são representadas como instruções no ASSL (Analysis Services Scripting Language) do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e são enquadradas em um comando XMLA (XML for Analysis).  
  
-   O ASSL é usado para definir e descrever uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e os bancos de dados e objetos de banco de dados que ela contém. Para obter mais informações, consulte [Analysis Services Scripting Language &#40;ASSL&#41; referência](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla).  
  
-   O XMLA é uma linguagem de comandos usada para enviar comandos de ação, como Criar, Alterar ou Processar para uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para obter mais informações, consulte [Referência do XMLA &#40;XML for Analysis&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-xmla-reference).  
  
 Se o código DDL for armazenado em um arquivo separado, a tarefa Executar DDL do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usará um gerenciador de conexões de arquivo para especificar o caminho do arquivo. Para obter mais informações, consulte [File Connection Manager](../connection-manager/file-connection-manager.md).  
  
 Como as instruções DDL podem conter senhas e outras informações confidenciais, um pacote que contém uma ou mais tarefas Executar DDL do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] deve usar o nível de proteção de pacote `EncryptAllWithUserKey` ou `EncryptAllWithPassword`. Para obter mais informações, consulte [Integration Services &#40;SSIS&#41; Pacotes](../integration-services-ssis-packages.md).  
  
### <a name="ddl-examples"></a>Exemplos de DDL  
 As três instruções de DDL a seguir foram geradas por script de objetos no [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)], o banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] incluído no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 A instrução DDL a seguir exclui a dimensão **Promoção** .  
  
```  
<Delete xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
    <Object>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
        <DimensionID>Dim Promotion</DimensionID>  
    </Object>  
</Delete>  
  
```  
  
 A instrução de DDL a seguir processa o cubo do [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] .  
  
```  
<Batch xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  <Parallel>  
    <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
      <Object>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      </Object>  
      <Type>ProcessFull</Type>  
      <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
    </Process>  
  </Parallel>  
</Batch>  
  
```  
  
 A instrução DDL a seguir cria o modelo de mineração **Previsão** .  
  
```  
<Create xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
    <ParentObject>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
        <MiningStructureID>Forecasting</MiningStructureID>  
    </ParentObject>  
    <ObjectDefinition>  
        <MiningModel xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
            <ID>Forecasting</ID>  
            <Name>Forecasting</Name>  
            <Algorithm>Microsoft_Time_Series</Algorithm>  
            <AlgorithmParameters>  
                <AlgorithmParameter>  
                    <Name>PERIODICITY_HINT</Name>  
                    <Value xsi:type="xsd:string">{12}</Value>  
                </AlgorithmParameter>  
            </AlgorithmParameters>  
            <Columns>  
                <Column>  
                    <ID>Amount</ID>  
                    <Name>Amount</Name>  
                    <SourceColumnID>Amount</SourceColumnID>  
                    <Usage>Predict</Usage>  
                </Column>  
                <Column>  
                    <ID>Model Region</ID>  
                    <Name>Model Region</Name>  
                    <SourceColumnID>Model Region</SourceColumnID>  
                    <Usage>Key</Usage>  
                </Column>  
                <Column>  
                    <ID>Quantity</ID>  
                    <Name>Quantity</Name>  
                    <SourceColumnID>Quantity</SourceColumnID>  
                    <Usage>Predict</Usage>  
                </Column>  
                <Column>  
                    <ID>Time Index</ID>  
                    <Name>Time Index</Name>  
                    <SourceColumnID>Time Index</SourceColumnID>  
                    <Usage>Key</Usage>  
                </Column>  
            </Columns>  
            <Collation>Latin1_General_CS_AS_KS</Collation>  
        </MiningModel>  
    </ObjectDefinition>  
</Create>  
  
```  
  
 As três instruções de DDL a seguir foram geradas por script de objetos no [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)], o banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] incluído no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 A instrução DDL a seguir exclui a dimensão **Promoção** .  
  
```  
<Delete xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
    <Object>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
        <DimensionID>Dim Promotion</DimensionID>  
    </Object>  
</Delete>  
  
```  
  
 A instrução de DDL a seguir processa o cubo do [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] .  
  
```  
<Batch xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  <Parallel>  
    <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
      <Object>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      </Object>  
      <Type>ProcessFull</Type>  
      <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
    </Process>  
  </Parallel>  
</Batch>  
  
```  
  
 A instrução DDL a seguir cria o modelo de mineração **Previsão** .  
  
```  
<Create xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
    <ParentObject>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
        <MiningStructureID>Forecasting</MiningStructureID>  
    </ParentObject>  
    <ObjectDefinition>  
        <MiningModel xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
            <ID>Forecasting</ID>  
            <Name>Forecasting</Name>  
            <Algorithm>Microsoft_Time_Series</Algorithm>  
            <AlgorithmParameters>  
                <AlgorithmParameter>  
                    <Name>PERIODICITY_HINT</Name>  
                    <Value xsi:type="xsd:string">{12}</Value>  
                </AlgorithmParameter>  
            </AlgorithmParameters>  
            <Columns>  
                <Column>  
                    <ID>Amount</ID>  
                    <Name>Amount</Name>  
                    <SourceColumnID>Amount</SourceColumnID>  
                    <Usage>Predict</Usage>  
                </Column>  
                <Column>  
                    <ID>Model Region</ID>  
                    <Name>Model Region</Name>  
                    <SourceColumnID>Model Region</SourceColumnID>  
                    <Usage>Key</Usage>  
                </Column>  
                <Column>  
                    <ID>Quantity</ID>  
                    <Name>Quantity</Name>  
                    <SourceColumnID>Quantity</SourceColumnID>  
                    <Usage>Predict</Usage>  
                </Column>  
                <Column>  
                    <ID>Time Index</ID>  
                    <Name>Time Index</Name>  
                    <SourceColumnID>Time Index</SourceColumnID>  
                    <Usage>Key</Usage>  
                </Column>  
            </Columns>  
            <Collation>Latin1_General_CS_AS_KS</Collation>  
        </MiningModel>  
    </ObjectDefinition>  
</Create>  
  
```  
  
## <a name="configuration-of-the-analysis-services-execute-ddl-task"></a>Configuração da Tarefa Executar DDL do Analysis Services  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique em um dos seguintes tópicos:  
  
-   [Editor da Tarefa Executar DDL do Analysis Services &#40;Página Geral&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor da Tarefa Executar DDL do Analysis Services &#40;Página DDL&#41;](../analysis-services-execute-ddl-task-editor-ddl-page.md)  
  
-   [Página Expressões](../expressions/expressions-page.md)  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-analysis-services-execute-ddl-task"></a>Configuração programática da Tarefa Executar DDL do Analysis Services  
 Para obter mais informações sobre como definir essas propriedades programaticamente, clique no tópico a seguir:  
  
-   <xref:Microsoft.DataTransformationServices.Tasks.DTSProcessingTask.ASExecuteDDLTask>  
  
  
