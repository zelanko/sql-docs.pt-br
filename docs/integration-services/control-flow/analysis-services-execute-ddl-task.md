---
title: Tarefa Executar DDL do Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.asexecuteddltask.f1
- sql13.dts.designer.asexecuteddltask.general.f1
- sql13.dts.designer.asexecuteddltask.ddl.f1
helpviewer_keywords:
- Analysis Services Execute DDL task
- DDL
ms.assetid: 7f25c8c6-b601-41f2-9553-be0a2ee0751a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a160e61e390f58dc640a5d1da265cdb77d5d9be1
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71294340"
---
# <a name="analysis-services-execute-ddl-task"></a>Tarefa Executar DDL do Analysis Services

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  A tarefa Executar DLL do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] executa instruções DDL (linguagem de definição de dados) que podem criar, descartar ou alterar modelos de mineração e objetos multidimensionais, como cubos e dimensões. Por exemplo, uma instrução DDL pode criar uma partição no cubo **Adventure Works** ou excluir uma dimensão do [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)], o exemplo de banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] incluído no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 A tarefa Executar DDL do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa um gerenciador de conexões do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para se conectar a uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou a um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Para obter mais informações, consulte [Analysis Services Connection Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md).  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui um número de tarefas que desempenham outras operações de business intelligence, como processamento de objetos analíticos e execução de consultas de previsão de mineração de dados.  
  
 Para obter mais informações sobre tarefas de business intelligence relacionadas, clique em um dos tópicos a seguir:  
  
-   [Tarefa Processamento do Analysis Services](../../integration-services/control-flow/analysis-services-processing-task.md)  
  
-   [Tarefa Consulta de Mineração de Dados](../../integration-services/control-flow/data-mining-query-task.md)  
  
## <a name="ddl-statements"></a>Instruções DDL  
 As instruções DDL são representadas como instruções no ASSL (Analysis Services Scripting Language) do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e são enquadradas em um comando XMLA (XML for Analysis).  
  
-   O ASSL é usado para definir e descrever uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e os bancos de dados e objetos de banco de dados que ela contém. Para obter mais informações, consulte [Linguagem de script do Analysis Services &#40;ASSL para XMLA&#41;](/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla).  
  
-   O XMLA é uma linguagem de comandos usada para enviar comandos de ação, como Criar, Alterar ou Processar para uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para obter mais informações, consulte [Referência do XMLA &#40;XML for Analysis&#41;](/bi-reference/xmla/xml-for-analysis-xmla-reference).  
  
 Se o código DDL for armazenado em um arquivo separado, a tarefa Executar DDL do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usará um gerenciador de conexões de arquivo para especificar o caminho do arquivo. Para obter mais informações, consulte [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md).  
  
 Como as instruções DDL podem conter senhas e outras informações confidenciais, um pacote que contém uma ou mais tarefas Executar DDL do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] deve usar o nível de proteção de pacote **EncryptAllWithUserKey** ou **EncryptAllWithPassword**. Para obter mais informações, consulte [Integration Services &#40;SSIS&#41; Pacotes](../../integration-services/integration-services-ssis-packages.md).  
  
### <a name="ddl-examples"></a>Exemplos de DDL  
 As três instruções de DDL a seguir foram geradas por script de objetos no [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)], o banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] incluído no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 A instrução DDL a seguir exclui a dimensão **Promoção** .  
  
```  
<Delete xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
    <Object>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
        <DimensionID>Dim Promotion</DimensionID>  
    </Object>  
</Delete>  
  
```  
  
 A instrução de DDL a seguir processa o cubo do [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] .  
  
```  
<Batch xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
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
<Create xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
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
<Delete xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
    <Object>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
        <DimensionID>Dim Promotion</DimensionID>  
    </Object>  
</Delete>  
  
```  
  
 A instrução de DDL a seguir processa o cubo do [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] .  
  
```  
<Batch xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
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
<Create xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
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
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Página Expressões](../../integration-services/expressions/expressions-page.md)  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-analysis-services-execute-ddl-task"></a>Configuração programática da Tarefa Executar DDL do Analysis Services  
 Para obter mais informações sobre como definir essas propriedades programaticamente, clique no tópico a seguir:  
  
-   <xref:Microsoft.DataTransformationServices.Tasks.DTSProcessingTask.ASExecuteDDLTask>  
  
## <a name="analysis-services-execute-ddl-task-editor-general-page"></a>Editor da Tarefa Executar DDL do Analysis Services (página Geral)
  Use a página **Geral** da caixa de diálogo **Editor da Tarefa Executar DDL do Analysis Services** para nomear e descrever a tarefa Executar DDL do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
### <a name="options"></a>Opções  
 **Nome**  
 Forneça um nome exclusivo para a tarefa Executar DDL do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Esse nome é usado como rótulo no ícone de tarefa.  
  
> [!NOTE]  
>  Os nomes das tarefas devem ser exclusivos em um pacote.  
  
 **Descrição**  
 Digite uma descrição para a tarefa Executar DDL do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
## <a name="analysis-services-execute-ddl-task-editor-ddl-page"></a>Editor da Tarefa Executar DDL do Analysis Services (Página DDL)
  Use a página **DDL** da caixa de diálogo **Editor da Tarefa Executar DDL do Analysis Services** para especificar uma conexão com um projeto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou um banco de dados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e para fornecer informações sobre a origem das instruções DDL (linguagem de definição de dados).  
  
### <a name="static-options"></a>Opções estáticas  
 **Conexão**  
 Selecione um projeto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou um gerenciador de conexões [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] na lista ou clique em \<**Nova conexão...** > e use a caixa de diálogo **Adicionar Gerenciador de Conexões do Analysis Services** para criar uma nova conexão.  
  
 **Tópicos relacionados:** [Referência da interface do usuário da caixa de diálogo Adicionar Gerenciador de Conexões do Analysis Services](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md), [Gerenciador de Conexão do Analysis Services](../../integration-services/connection-manager/analysis-services-connection-manager.md)  
  
 **SourceType**  
 Especifique a origem da instrução DDL. As opções desta propriedade estão listadas na seguinte tabela:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Direct Input**|Define a origem da instrução DDL armazenada na caixa de texto **SourceDirect** . A seleção deste valor exibe as opções dinâmicas na seção a seguir.|  
|**File Connection**|Define a origem para um arquivo que contém a instrução DDL. A seleção deste valor exibe as opções dinâmicas na seção a seguir.|  
|**Variável**|Define a origem para uma variável. A seleção deste valor exibe as opções dinâmicas na seção a seguir.|  
  
### <a name="dynamic-options"></a>Opções dinâmicas  
  
#### <a name="sourcetype--direct-input"></a>SourceType = Entrada Direta  
 **Origem**  
 Digite as instruções DDL ou clique nas reticências **(...)** e digite as instruções na caixa de diálogo **Instruções DDL**.  
  
#### <a name="sourcetype--file-connection"></a>SourceType = File Connection  
 **Origem**  
 Selecione uma conexão de Arquivo na lista ou clique em \<**Nova conexão...** > e use a caixa de diálogo **Adicionar Gerenciador de Conexões de Arquivos** para criar uma nova conexão.  
  
 **Tópicos relacionados:** [Gerenciador de Conexão de Arquivo](../../integration-services/connection-manager/file-connection-manager.md)  
  
#### <a name="sourcetype--variable"></a>SourceType = Variable  
 **Origem**  
 Selecione uma variável na lista ou clique em \<**Nova variável...** > e use a caixa de diálogo **Adicionar Variável** para criar uma nova variável.  
  
 **Tópicos relacionados:** [Variáveis do SSIS &#40;Integration Services&#41;](../../integration-services/integration-services-ssis-variables.md)  
  
