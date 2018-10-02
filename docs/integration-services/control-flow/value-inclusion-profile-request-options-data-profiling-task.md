---
title: Opções da solicitação do perfil Inclusão de Valor (Tarefa Criação de Perfil de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: ca94da82-a4c9-4e87-9cba-c2d85bd31f01
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: da5839c81489a278c3e013886ae7b1eeba6834f7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47793525"
---
# <a name="value-inclusion-profile-request-options-data-profiling-task"></a>Opções da solicitação do perfil Inclusão de Valor (tarefa Criação de Perfil de Dados)
  Use o painel **Propriedades da Solicitação** da página **Solicitações de Perfil** para definir as opções da **Solicitação do Perfil de Inclusão de Valor** selecionada no painel de solicitações. Um perfil de Inclusão de Valor computa a sobreposição nos valores entre duas colunas ou conjuntos de colunas. Portanto, esse perfil também pode determinar se uma coluna ou conjunto de colunas é apropriado para servir como uma chave estrangeira entre as tabelas selecionadas. Esse perfil também pode ajudá-lo a identificar problemas em seus dados, como valores inválidos. Por exemplo, você usa um perfil de inclusão de valor para criar um perfil para a coluna ProductID de uma tabela de vendas. O perfil descobre que a coluna contém valores que não são encontrados na coluna ProductID da tabela Produtos.  
  
> [!NOTE]  
>  As opções descritas neste tópico são exibidas na página **Solicitações de Perfil** do **Editor da Tarefa Criação de Perfil de Dados**. Para obter mais informações sobre essa página do editor, consulte [Editor da Tarefa Criação de Perfil de Dados &#40;Página Solicitações de perfil&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md).  
  
 Para obter mais informações sobre como usar a Tarefa Criação de Perfil de Dados, consulte [Configuração da Tarefa Criação de Perfil de Dados](../../integration-services/control-flow/setup-of-the-data-profiling-task.md). Para obter mais informações sobre como usar o Visualizador de Perfil de Dados para analisar a saída da Tarefa Criação de Perfil de Dados, consulte [Visualizador de Perfil de Dados](../../integration-services/control-flow/data-profile-viewer.md).  
  
## <a name="understanding-the-selection-of-columns-for-the-inclusioncolumns-property"></a>Compreendendo a seleção de colunas para a propriedade InclusionColumns  
 Uma **Solicitação de Perfil de Inclusão de Valor** computa se todos os valores em um subconjunto estão presentes no superconjunto. O superconjunto é frequentemente uma tabela de pesquisa ou uma tabela de referência. Por exemplo, a coluna com estados em uma tabela de endereços é a tabela de subconjunto. Cada sigla de estado de dois caracteres nessa coluna também deve ser encontrada na tabela de siglas de estado dos Correios dos Estados Unidos, que é a tabela de superconjunto.  
  
 Quando você usa o curinga (*) como valor da coluna de subconjunto ou superconjunto, a tarefa Criação de Perfil de Dados compara cada coluna com a coluna especificada no outro lado.  
  
> [!NOTE]  
>  Se você selecionar (*), essa opção poderá resultar em um grande número de computações e diminuir o desempenho da tarefa.  
  
## <a name="understanding-the-threshold-settings"></a>Compreendendo as configurações de limite  
 É possível usar duas configurações de limite diferentes para refinar a saída de uma Solicitação do Perfil de Inclusão de Valor.  
  
 Quando um valor diferente de **Nenhum** é especificado para **InclusionThresholdSetting**, o perfil informa a intensidade da inclusão do subconjunto no superconjunto somente sob as seguintes condições:  
  
-   Quando a intensidade de inclusão excede o limite especificado em **InclusionStrengthThreshold**.  
  
-   Quando a intensidade de inclusão tem um valor de 1,0 e **InclusionStrengthThreshold** é definido como **Exato**.  
  
 É possível refinar ainda mais a saída filtrando combinações nas quais a coluna de superconjunto não é uma chave apropriada para a tabela de superconjunto devido a valores não exclusivos. Quando um valor diferente de **Nenhum** é especificado para **SupersetColumnsKeyThresholdSetting**, o perfil informa a intensidade de inclusão do subconjunto no superconjunto somente sob as seguintes condições:  
  
-   Quando a adequação das colunas de superconjunto como uma chave na tabela de superconjunto excede o limite especificado em **SupersetColumnsKeyThreshold**  
  
-   Quando a intensidade de inclusão tem um valor de 1,0 e **SupersetColumnsKeyThreshold** é definido como **Exato**.  
  
## <a name="request-properties-options"></a>Opções de Propriedades da Solicitação  
 Para uma **Solicitação do Perfil de Inclusão de Valor**, o painel **Propriedades da Solicitação** exibe os seguintes grupos de opções:  
  
-   **Dados**que incluem as opções **SubsetTableOrView**, **SupersetTableOrView**e **InclusionColumns**  
  
-   **Geral**  
  
-   **Opções**  
  
### <a name="data-options"></a>Opções de dados  
 **ConnectionManager**  
 Selecione o gerente de conexões do [!INCLUDE[vstecado](../../includes/vstecado-md.md)] que usa o Provedor de Dados .NET para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) para conexão com o banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contém a tabela ou a exibição que você deseja analisar.  
  
 **SubsetTableOrView**  
 Selecione a tabela ou exibição cujo perfil deseja criar.  
  
 Para obter mais informações, consulte a seção "Opções SubsetTableOrView e SupersetTableOrView" neste tópico.  
  
 **SupersetTableOrView**  
 Selecione a tabela ou exibição cujo perfil deseja criar.  
  
 Para obter mais informações, consulte a seção "Opções SubsetTableOrView e SupersetTableOrView" neste tópico.  
  
 **InclusionColumns**  
 Selecione as colunas ou conjuntos de colunas das tabelas de subconjunto e superconjunto.  
  
 Para obter mais informações, consulte a seções "Compreendendo a seleção de colunas para a propriedade InclusionColumns" e "Opções InclusionColumns" anteriormente neste tópico.  
  
#### <a name="subsettableorview-and-supersettableorview-options"></a>Opções de SubsetTableOrView e SupersetTableOrView  
 **Esquema**  
 Especifica o esquema ao qual a tabela selecionada pertence. Esta opção é somente leitura.  
  
 **TableOrView**  
 Exibe o nome da tabela selecionada. Esta opção é somente leitura.  
  
#### <a name="inclusioncolumns-options"></a>Opções de InclusionColumns  
 As opções a seguir são apresentadas para cada conjunto de colunas selecionado para criação de perfil em **InclusionColumns**.  
  
 Para obter mais informações, consulte a seção "Compreendendo a seleção de colunas para a propriedade InclusionColumns" anteriormente neste tópico.  
  
 **IsWildCard**  
 Especifica se o curinga **(\*)** foi selecionado. Esta opção será definida como **True** se você tiver selecionado **(\*)** para analisar todas as colunas. Será **Falso** se você selecionou uma coluna individual para a criação de um perfil. Esta opção é somente leitura.  
  
 **ColumnName**  
 Exibe o nome da coluna selecionada. Esta opção estará em branco se você tiver selecionado **(\*)** para analisar todas as colunas. Esta opção é somente leitura.  
  
 **StringCompareOptions**  
 Selecione as opções para comparação de valores da cadeia de caracteres. As opções dessa propriedade são listadas na tabela a seguir. O valor padrão desta opção é **Padrão**.  
  
> [!NOTE]  
>  Quando você usa o curinga **(\*)** para **ColumnName**, **CompareOptions** é somente leitura e definido como **Default**.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Default**|Classifica e compara dados com base no agrupamento da coluna na tabela de origem.|  
|**BinarySort**|Classifica e compara dados com base nos padrões de bit definidos para cada caractere. A ordem de classificação binária faz distinção entre maiúsculas e minúsculas e acentuação. Binário é também a ordem de classificação mais rápida.|  
|**DictionarySort**|Classifica e compara dados com base nas regras de classificação e comparação, conforme definidas em dicionários do idioma ou alfabeto associado.|  
  
 Se **DictionarySort**for selecionado, também é possível selecionar qualquer combinação das opções relacionadas na tabela a seguir. Por padrão, nenhuma destas opções adicionais está selecionada.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**IgnoreCase**|Especifica se a comparação faz distinção entre letras maiúsculas e minúsculas. Se esta opção for definida, a comparação de cadeia de caracteres ignorará a distinção entre letras maiúsculas e minúsculas. Por exemplo, "ABC" torna-se igual a "abc".|  
|**IgnoreNonSpace**|Especifica se a comparação distingue entre caracteres de espaço e sinais diacríticos. Se esta opção for definida, a comparação ignorará os sinais diacríticos. Por exemplo, "å" é igual a "a".|  
|**IgnoreKanaType**|Especifica se a comparação distingue os dois tipos de caracteres de kana japoneses: hiragana e katakana. Se esta opção for definida, a comparação de cadeia de caracteres ignorará o tipo de kana usado.|  
|**IgnoreWidth**|Especifica se a comparação faz distinção entre um caractere de byte único e o mesmo caractere representado como um caractere de byte duplo. Se esta opção for definida, a comparação de cadeia de caracteres tratará representações de byte único e representações de byte duplo do mesmo caractere como idênticas.|  
  
### <a name="general-options"></a>Opções gerais  
 **RequestID**  
 Digite um nome descritivo para identificar esta solicitação de perfil. Normalmente, não é necessário alterar o valor gerado automaticamente.  
  
### <a name="options"></a>Opções  
 **InclusionThresholdSetting**  
 Selecione a configuração de limite para refinar a saída do perfil. O valor padrão dessa propriedade é **Especificado**. Para obter mais informações, consulte a seção "Compreendendo as configurações de limite" anteriormente neste tópico.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Nenhum**|Nenhum limite é especificado. A intensidade da chave é informada independentemente de seu valor.|  
|**Especificado**|Use o limite especificado em **InclusionStrengthThreshold**. A intensidade de inclusão só será informada se for superior ao limite.|  
|**Exato**|Nenhum limite é especificado. A intensidade de inclusão só será informada se os valores de subconjunto forem completamente incluídos nos valores de superconjunto.|  
  
 **InclusionStrengthThreshold**  
 Especifique o limite (um valor entre 0 e 1) a partir do qual a intensidade de inclusão deve ser informada. O valor padrão dessa propriedade é 0,95. Esta opção é habilitada somente quando **Especificado** é selecionado como **InclusionThresholdSetting**.  
  
 Para obter mais informações, consulte a seção "Compreendendo as configurações de limite" anteriormente neste tópico.  
  
 **SupersetColumnsKeyThresholdSetting**  
 Especifique o limite de superconjunto. O valor padrão dessa propriedade é **Especificado**. Para obter mais informações, consulte a seção "Compreendendo as configurações de limite" anteriormente neste tópico.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Nenhum**|Nenhum limite é especificado. A intensidade de inclusão é informada independentemente da intensidade da chave da coluna de superconjunto.|  
|**Especificado**|Use o limite especificado em **SupersetColumnsKeyThreshold**. A intensidade de inclusão só será informada se a intensidade da chave da coluna de superconjunto for maior que o limite.|  
|**Exato**|Nenhum limite é especificado. A intensidade de inclusão só será informada se as colunas de superconjunto forem uma chave exata na tabela de superconjunto.|  
  
 **SupersetColumnsKeyThreshold**  
 Especifique o limite (um valor entre 0 e 1) a partir do qual a intensidade de inclusão deve ser informada. O valor padrão dessa propriedade é 0,95. Esta opção só é habilitada quando **Especificado** é selecionado como **SupersetColumnsKeyThresholdSetting**.  
  
 Para obter mais informações, consulte a seção "Compreendendo as configurações de limite" anteriormente neste tópico.  
  
 **MaxNumberOfViolations**  
 Especifique o número máximo de violações de inclusão a serem informadas na saída. O valor padrão dessa propriedade é 100. Esta opção é desabilitada quando **Exato** é selecionado como **InclusionThresholdSetting**.  
  
## <a name="see-also"></a>Consulte Também  
 [Editor da tarefa Criação de Perfil de Dados &#40;Página Geral&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [Formulário de Perfil Rápido de Tabela Única &#40;Tarefa Criação de Perfil de Dados&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  
