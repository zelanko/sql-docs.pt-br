---
title: Opções da solicitação do perfil Chave de Candidato (Tarefa Criação de Perfil de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: 8632dbc4-4394-4dc7-b19c-f9adeb21ba52
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: ee10aa434e25dd2243133ceaea09921ddf32b000
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007101"
---
# <a name="candidate-key-profile-request-options-data-profiling-task"></a>Opções da solicitação do perfil Chave de Candidato (tarefa Criação de Perfil de Dados)
  Use o painel **Propriedades da Solicitação** da página **Solicitações de Perfil** para definir as opções da **Solicitação de Perfil de Chave de Candidato** selecionada no painel de solicitações. Um perfil Chave de Candidato informa se uma coluna ou conjunto de colunas é uma chave, ou uma chave aproximada, para a tabela selecionada. Esse perfil também pode ajudar a identificar problemas em seus dados, como valores em duplicata em uma possível coluna de chave.  
  
> [!NOTE]  
>  As opções descritas neste tópico são exibidas na página **Solicitações de Perfil** do **Editor da Tarefa Criação de Perfil de Dados**. Para obter mais informações sobre essa página do editor, consulte [Editor da Tarefa Criação de Perfil de Dados &#40;Página Solicitações de perfil&#41;](data-profiling-task-editor-profile-requests-page.md).  
  
 Para obter mais informações sobre como usar a Tarefa Criação de Perfil de Dados, consulte [Configuração da Tarefa Criação de Perfil de Dados](data-profiling-task.md). Para obter mais informações sobre como usar o Visualizador de Perfil de Dados para analisar a saída da Tarefa Criação de Perfil de Dados, consulte [Visualizador de Perfil de Dados](data-profile-viewer.md).  
  
## <a name="understanding-the-selection-of-columns-for-the-keycolumns-property"></a>Compreendendo a seleção de colunas para a propriedade KeyColumns  
 Cada **Solicitação de Perfil de Chave de Candidato** computa a restrição de chave de uma única chave de candidato que consiste de uma única coluna ou de várias colunas:  
  
-   Ao selecionar uma única coluna em **KeyColumns**, a tarefa computa a restrição de chave daquela coluna.  
  
-   Ao selecionar várias colunas em **KeyColumns**, a tarefa computa a restrição de chave da chave composta que consiste de todas as colunas selecionadas.  
  
-   Ao selecionar o caractere curinga, **(\*)**, em **KeyColumns**, a tarefa computa a restrição de chave de cada coluna na tabela ou exibição.  
  
 Por exemplo, considere uma tabela de exemplo com as colunas A, B e C. Sendo assim, as seguintes seleções são feitas para a propriedade **KeyColumns**:  
  
-   Você seleciona (\*) e a coluna C em **KeyColumns**. A tarefa computa a restrição de chave da coluna C e, depois, dos candidatos de chave composta, (A, C) e (B, C).  
  
-   Você seleciona (\*) e (\*) em **KeyColumns**. A tarefa computa a restrição de chave das colunas individuais A, B e C e, depois, dos candidatos de chave composta, (A, B), (A, C) e (B, C).  
  
> [!NOTE]  
>  Se você selecionar (*), essa opção poderá resultar em um grande número de computações e diminuir o desempenho da tarefa. Entretanto, se a tarefa encontrar um subconjunto que atenda ao limite de uma chave, a tarefa não analisará combinações adicionais. Por exemplo, na tabela de exemplo descrita acima, se a tarefa determinar que a coluna C é uma chave, a tarefa não continuará analisando os candidatos de chave compostos.  
  
## <a name="request-properties-options"></a>Opções de Propriedades da Solicitação  
 Para uma **Solicitação de Perfil de Chave de Candidato**, o painel **Propriedades da Solicitação** exibe os seguintes grupos de opções:  
  
-   **Dados**que incluem as opções **TableOrView** e **KeyColumns**  
  
-   **Geral**  
  
-   **Opções**  
  
### <a name="data-options"></a>Opções de dados  
 **ConnectionManager**  
 Selecione o gerente de conexões do [!INCLUDE[vstecado](../../includes/vstecado-md.md)] que usa o Provedor de Dados .NET para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) para conexão com o banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contém a tabela ou a exibição que você deseja analisar.  
  
 **TableOrView**  
 Selecione a tabela ou exibição cujo perfil deseja criar.  
  
 Para obter mais informações, consulte a seção "Opções TableOrView" neste tópico.  
  
 **KeyColumns**  
 Selecione a coluna ou as colunas existentes para criação de perfil. Selecione **(\*)** para analisar todas as colunas.  
  
 Para obter mais informações, consulte a seções "Compreendendo a seleção de colunas para a propriedade KeyColumns " e "Opções KeyColumns " neste tópico.  
  
#### <a name="tableorview-options"></a>Opções TableOrView  
 **Esquema**  
 Especifique o esquema ao qual a tabela selecionada pertence. Esta opção é somente leitura.  
  
 **Table**  
 Exibe o nome da tabela selecionada. Esta opção é somente leitura.  
  
#### <a name="keycolumns-options"></a>Opções de KeyColumns  
 As opções a seguir são apresentadas para cada coluna selecionada para criação de perfil em **KeyColumns**ou para a opção **(\*)**.  
  
 Para obter mais informações, consulte a seção "Compreendendo a seleção de colunas para a propriedade KeyColumns" anteriormente neste tópico.  
  
 **IsWildCard**  
 Especifica se o curinga **(\*)** foi selecionado. Esta opção será definida como **True** se você tiver selecionado **(\*)** para analisar todas as colunas. Será **Falso** se você selecionou uma coluna individual para a criação de um perfil. Esta opção é somente leitura.  
  
 **ColumnName**  
 Exibe o nome da coluna selecionada. Esta opção estará em branco se você tiver selecionado **(\*)** para analisar todas as colunas. Esta opção é somente leitura.  
  
 **StringCompareOptions**  
 Selecione as opções para comparação de valores da cadeia de caracteres. As opções dessa propriedade são listadas na tabela a seguir. O valor padrão desta opção é **Padrão**.  
  
> [!NOTE]  
>  Quando você usar o curinga **(\*)** para **ColumnName**, **CompareOptions** é somente leitura e definido como **Padrão**.  
  
|Valor|Description|  
|-----------|-----------------|  
|**Default**|Classifica e compara dados com base no agrupamento da coluna na tabela de origem.|  
|**BinarySort**|Classifica e compara dados com base nos padrões de bit definidos para cada caractere. A ordem de classificação binária faz distinção entre maiúsculas e minúsculas e acentuação. Binário é também a ordem de classificação mais rápida.|  
|**DictionarySort**|Classifica e compara dados com base nas regras de classificação e comparação, conforme definidas em dicionários do idioma ou alfabeto associado.|  
  
 Se **DictionarySort**for selecionado, também é possível selecionar qualquer combinação das opções relacionadas na tabela a seguir. Por padrão, nenhuma destas opções adicionais está selecionada.  
  
|Valor|Description|  
|-----------|-----------------|  
|**IgnoreCase**|Especifica se a comparação faz distinção entre letras maiúsculas e minúsculas. Se esta opção for definida, a comparação de cadeia de caracteres ignorará a distinção entre letras maiúsculas e minúsculas. Por exemplo, "ABC" torna-se igual a "abc".|  
|**IgnoreNonSpace**|Especifica se a comparação distingue entre caracteres de espaço e sinais diacríticos. Se esta opção for definida, a comparação ignorará os sinais diacríticos. Por exemplo, "å" é igual a "a".|  
|**IgnoreKanaType**|Especifica se a comparação distingue os dois tipos de caracteres de kana japoneses: hiragana e katakana. Se esta opção for definida, a comparação de cadeia de caracteres ignorará o tipo de kana usado.|  
|**IgnoreWidth**|Especifica se a comparação faz distinção entre um caractere de byte único e o mesmo caractere representado como um caractere de byte duplo. Se esta opção for definida, a comparação de cadeia de caracteres tratará representações de byte único e representações de byte duplo do mesmo caractere como idênticas.|  
  
### <a name="general-options"></a>Opções gerais  
 **RequestID**  
 Digite um nome descritivo para identificar esta solicitação de perfil. Normalmente, não é necessário alterar o valor gerado automaticamente.  
  
### <a name="options"></a>Opções  
 **ThresholdSetting**  
 As opções dessa propriedade são listadas na tabela a seguir. O valor padrão dessa propriedade é **Especificado**.  
  
|Valor|Description|  
|-----------|-----------------|  
|**Nenhuma**|Nenhum limite é especificado. A intensidade da chave é informada independentemente de seu valor.|  
|**Especificado**|Um limite é especificado em **KeyStrengthThreshold**. A restrição de chave só será informada se for superior ao limite.|  
|**Exato**|Nenhum limite é especificado. A restrição de chave só será informada se as colunas selecionadas forem uma chave exata.|  
  
 **KeyStrengthThreshold**  
 Especifique o limite (usando um valor entre 0 e 1) a partir do qual a restrição de chave deve ser informada. O valor padrão dessa propriedade é 0,95. Esta opção é habilitada somente quando **Especificado** é selecionado como **KeyStrengthThresholdSetting**.  
  
 **MaxNumberOfViolations**  
 Especifique o número máximo de violações de chave de candidato para informar na saída. O valor padrão dessa propriedade é 100. Esta opção é desabilitada quando **Exato** é selecionada como o **KeyStrengthThresholdSetting**.  
  
## <a name="see-also"></a>Consulte também  
 [Editor da tarefa de criação de perfil dados &#40;página geral&#41;](../general-page-of-integration-services-designers-options.md)   
 [Formulário de Perfil Rápido de Tabela Única &#40;Tarefa Criação de Perfil de Dados&#41;](single-table-quick-profile-form-data-profiling-task.md)  
  
  