---
title: Opções da solicitação do perfil Dependência Funcional (Tarefa Criação de Perfil de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: 6eb853aa-8016-490c-be4f-06ab8d7f5021
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 8ec1e724c607a8805b9654f8ade077ab078e4eae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67988196"
---
# <a name="functional-dependency-profile-request-options-data-profiling-task"></a>Opções da solicitação do perfil Dependência Funcional (tarefa Criação de Perfil de Dados)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Use o painel **Propriedades da Solicitação** da página **Solicitações de Perfil** para definir as opções da **Solicitação de Perfil de Dependência Funcional** selecionada no painel de solicitações. Um perfil de Dependência Funcional informa até que ponto os valores em uma coluna (a coluna dependente) dependem dos valores em outra coluna ou conjunto de colunas (a coluna determinante). Esse perfil também pode ajudá-lo a identificar problemas em seus dados, como valores inválidos. Por exemplo, você perfila a dependência entre uma coluna Código Postal e uma coluna estado dos Estados Unidos. Nesse perfil, o mesmo Código Postal deve sempre ter o mesmo estado, mas o perfil descobre violações da dependência.  
  
> [!NOTE]  
>  As opções descritas neste tópico são exibidas na página **Solicitações de Perfil** do **Editor da Tarefa Criação de Perfil de Dados**. Para obter mais informações sobre essa página do editor, consulte [Editor da Tarefa Criação de Perfil de Dados &#40;Página Solicitações de perfil&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md).  
  
 Para obter mais informações sobre como usar a Tarefa Criação de Perfil de Dados, consulte [Configuração da Tarefa Criação de Perfil de Dados](../../integration-services/control-flow/setup-of-the-data-profiling-task.md). Para obter mais informações sobre como usar o Visualizador de Perfil de Dados para analisar a saída da Tarefa Criação de Perfil de Dados, consulte [Visualizador de Perfil de Dados](../../integration-services/control-flow/data-profile-viewer.md).  
  
## <a name="understanding-the-selection-of-determinant-and-dependent-columns"></a>Compreendendo a seleção de colunas determinantes e dependentes  
 Uma **Solicitação de Perfil de Dependência Funcional** computa o grau no qual a coluna lateral determinante ou grupo de colunas (especificados na propriedade **DeterminantColumns** ) determina o valor da coluna lateral dependente (especificada na propriedade **DependentColumn** ). Por exemplo, uma coluna estado dos Estados Unidos deveria ser funcionalmente dependente em uma coluna Código Postal dos Estados Unidos. Ou seja, se o Código Postal (coluna determinante) for 98052, o estado (coluna dependente) deve ser sempre Washington.  
  
 Para o lado determinante, é possível especificar uma coluna ou um conjunto de colunas na propriedade **DeterminantColumns** . Por exemplo, considere uma tabela de amostra com as colunas A, B e C. Sendo assim, as seguintes seleções são feitas para a propriedade **DeterminantColumns** :  
  
-   Ao selecionar o curinga **(\*)** , a tarefa Criação de Perfil de Dados testa cada coluna como lado determinante da dependência.  
  
-   Ao selecionar o curinga **(\*)** e outra(s) coluna(s), a tarefa Criação de Perfil de Dados testa cada combinação de colunas como lado determinante da dependência. Por exemplo, considere uma tabela de exemplo com as colunas A, B e C. Se forem especificados **(\*)** e a coluna C como valor da propriedade **DeterminantColumns**, a tarefa Criação de Perfil de Dados testará as combinações (A, C) e (B, C) como lado determinante da dependência.  
  
 Para o lado dependente, é possível especificar uma única coluna ou o curinga **(\*)** na propriedade **DependentColumn**. Quando você seleciona o curinga **(\*)** , a tarefa Criação de Perfil de Dados testa a coluna lateral ou conjunto de colunas determinante com relação a cada coluna.  
  
> [!NOTE]  
>  Se selecionar **(\*)** , essa opção poderá resultar em um grande número de computações e diminuir o desempenho da tarefa. Entretanto, se a tarefa encontrar um subconjunto que atenda ao limite de uma dependência funcional, a tarefa não analisará combinações adicionais. Por exemplo, na tabela de exemplo descrita acima, se a tarefa determinar que a coluna C é uma coluna determinante, a tarefa não continuará analisando os candidatos compostos.  
  
## <a name="request-properties-options"></a>Opções de Propriedades da Solicitação  
 Para uma **Solicitação de Perfil de Dependência Funcional**, o painel **Propriedades da Solicitação** exibe os seguintes grupos de opções:  
  
-   **Dados**que incluem as opções **DeterminantColumns** e **DependentColumn**  
  
-   **Geral**  
  
-   **Opções**  
  
### <a name="data-options"></a>Opções de dados  
 **ConnectionManager**  
 Selecione o gerente de conexões do [!INCLUDE[vstecado](../../includes/vstecado-md.md)] que usa o Provedor de Dados .NET para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) para conexão com o banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contém a tabela ou a exibição que você deseja analisar.  
  
 **TableOrView**  
 Selecione a tabela ou exibição cujo perfil deseja criar.  
  
 **DeterminantColumns**  
 Selecione a coluna determinante ou conjunto de colunas. Ou seja, selecione a coluna ou conjunto de colunas cujos valores determinam o valor da coluna dependente.  
  
 Para obter mais informações, consulte as seções "Compreendendo a seleção de colunas determinantes e dependentes" “Opções DeterminantColumns e DependentColumn” neste tópico.  
  
 **DependentColumn**  
 Selecione a coluna dependente. Ou seja, selecione a coluna cujo valor é determinado pelo valor da coluna lateral ou conjunto de colunas laterais determinantes.  
  
 Para obter mais informações, consulte as seções "Compreendendo a seleção de colunas determinantes e dependentes" “Opções DeterminantColumns e DependentColumn” neste tópico.  
  
#### <a name="determinantcolumns-and-dependentcolumn-options"></a>Opções de DeterminantColumns e DependentColumn  
 As opções a seguir são apresentadas para cada coluna selecionada para criação de perfil em **DeterminantColumns** e em **DependentColumn**.  
  
 Para obter mais informações, consulte a seção "Compreendendo a seleção de colunas determinantes e dependentes" anteriormente neste tópico.  
  
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
|**Default**|Classifica e compara dados com base na ordenação da coluna na tabela de origem.|  
|**BinarySort**|Classifica e compara dados com base nos padrões de bit definidos para cada caractere. A ordem de classificação binária faz distinção entre maiúsculas e minúsculas e acentuação. Binário é também a ordem de classificação mais rápida.|  
|**DictionarySort**|Classifica e compara dados com base nas regras de classificação e comparação, conforme definidas em dicionários do idioma ou alfabeto associado.|  
  
 Se **DictionarySort**for selecionado, também é possível selecionar qualquer combinação das opções relacionadas na tabela a seguir. Por padrão, nenhuma destas opções adicionais está selecionada.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**IgnoreCase**|Especifica se a comparação faz distinção entre letras maiúsculas e minúsculas. Se esta opção for definida, a comparação de cadeia de caracteres ignorará a distinção entre letras maiúsculas e minúsculas. Por exemplo, "ABC" torna-se igual a "abc".|  
|**IgnoreNonSpace**|Especifica se a comparação distingue entre caracteres de espaço e sinais diacríticos. Se esta opção for definida, a comparação ignorará os sinais diacríticos. Por exemplo, "Ã¥" é igual a "a".|  
|**IgnoreKanaType**|Especifica se a comparação distingue os dois tipos de caracteres de kana japoneses: hiragana e katakana. Se esta opção for definida, a comparação de cadeia de caracteres ignorará o tipo de kana usado.|  
|**IgnoreWidth**|Especifica se a comparação faz distinção entre um caractere de byte único e o mesmo caractere representado como um caractere de byte duplo. Se esta opção for definida, a comparação de cadeia de caracteres tratará representações de byte único e representações de byte duplo do mesmo caractere como idênticas.|  
  
### <a name="general-options"></a>Opções gerais  
 **RequestID**  
 Digite um nome descritivo para identificar esta solicitação de perfil. Normalmente, não é necessário alterar o valor gerado automaticamente.  
  
### <a name="options"></a>Opções  
 **ThresholdSetting**  
 Especifique a configuração de limite. O valor padrão dessa propriedade é **Especificado**.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Nenhum**|Nenhum limite é especificado. A força de dependência funcional é informada independentemente do seu valor.|  
|**Especificado**|Use o limite especificado em **FDStrengthThreshold**. A força de dependência funcional só será informada se for superior ao limite.|  
|**Exact**|Nenhum limite é especificado. A força de dependência funcional só será informada se a dependência funcional entre as colunas selecionadas for exata.|  
  
 **FDStrengthThreshold**  
 Especifique o limite (usando um valor entre 0 e 1) a partir do qual a força de dependência funcional deve ser informada. O valor padrão dessa propriedade é 0,95. Esta opção é habilitada somente quando **Especificado** é selecionado como **ThresholdSetting**.  
  
 **MaxNumberOfViolations**  
 Especifique o número máximo de violações de dependência funcional a ser informado na saída. O valor padrão dessa propriedade é 100. Esta opção é desabilitada quando **Exato** é selecionado como **ThresholdSetting**.  
  
## <a name="see-also"></a>Consulte Também  
 [Editor da tarefa Criação de Perfil de Dados &#40;Página Geral&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [Formulário de Perfil Rápido de Tabela Única &#40;Tarefa Criação de Perfil de Dados&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  
