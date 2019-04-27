---
title: Opções de solicitação de perfil de distribuição de valor de coluna (Tarefa Criação de Perfil de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: c1e5f5de-04f5-4d00-a9f0-55817186bdf9
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5a79ba9f2ff211ed4bf56e749acba7f1d4601643
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62832421"
---
# <a name="column-value-distribution-profile-request-options-data-profiling-task"></a>Opções de solicitação do perfil Distribuição de Valor de Coluna (tarefa Criação de Perfil de Dados)
  Use o painel **Propriedades da Solicitação** da página **Solicitações de Perfil** para definir as opções da **Solicitação de Perfil de Distribuição de Valor de Coluna** selecionada no painel de solicitações. Um Perfil de Distribuição de Valor de Coluna reporta todos os valores distintos na coluna selecionada e a porcentagem de linhas na tabela que cada valor representa. O perfil também pode informar valores que representam mais que uma porcentagem especificada de linhas na tabela. O perfil também pode ajudar a identificar problemas em seus dados, como um número incorreto de valores distintos em uma coluna. Por exemplo, você cria um perfil para uma coluna Estado dos Estados Unidos da América e descobre mais de 50 valores distintos.  
  
> [!NOTE]  
>  As opções descritas neste tópico são exibidas na página **Solicitações de Perfil** do **Editor da Tarefa Criação de Perfil de Dados**. Para obter mais informações sobre essa página do editor, consulte [Editor da Tarefa Criação de Perfil de Dados &#40;Página Solicitações de perfil&#41;](data-profiling-task-editor-profile-requests-page.md).  
  
 Para obter mais informações sobre como usar a Tarefa Criação de Perfil de Dados, consulte [Configuração da Tarefa Criação de Perfil de Dados](data-profiling-task.md). Para obter mais informações sobre como usar o Visualizador de Perfil de Dados para analisar a saída da Tarefa Criação de Perfil de Dados, consulte [Visualizador de Perfil de Dados](data-profile-viewer.md).  
  
## <a name="request-properties-options"></a>Opções de Propriedades da Solicitação  
 Em uma **Solicitação de Perfil de Distribuição de Valor de Coluna**, o painel **Propriedades da Solicitação** exibe os seguintes grupos de opções:  
  
-   **Dados**que incluem as opções **TableOrView** e **Column**  
  
-   **Geral**  
  
-   **Opções**  
  
### <a name="data-options"></a>Opções de dados  
 **ConnectionManager**  
 Selecione o gerente de conexões do [!INCLUDE[vstecado](../../includes/vstecado-md.md)] que usa o Provedor de Dados .NET para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) para conexão com o banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contém a tabela ou a exibição que você deseja analisar.  
  
 **TableOrView**  
 Selecione a tabela ou exibição existente que contêm a coluna para a qual será criado um perfil.  
  
 Para obter mais informações, consulte a seção "Opções TableOrView" neste tópico.  
  
 **Column**  
 Selecione a coluna existente para a qual um perfil será criado. Selecione **(\*)** para analisar todas as colunas.  
  
 Para obter mais informações, consulte a seção “Opções Column” neste tópico.  
  
#### <a name="tableorview-options"></a>Opções TableOrView  
 **Esquema**  
 Especifica o esquema ao qual a tabela selecionada pertence. Esta opção é somente leitura.  
  
 **Table**  
 Exibe o nome da tabela selecionada. Esta opção é somente leitura.  
  
#### <a name="column-options"></a>Opções de Coluna  
 **IsWildCard**  
 Especifica se o curinga **(\*)** foi selecionado. Esta opção será definida como **True** se você tiver selecionado **(\*)** para analisar todas as colunas. Será **Falso** se você selecionou uma coluna individual para a criação de um perfil. Esta opção é somente leitura.  
  
 **ColumnName**  
 Exibe o nome da coluna selecionada. Esta opção estará em branco se você tiver selecionado **(\*)** para analisar todas as colunas. Esta opção é somente leitura.  
  
 **StringCompareOptions**  
 Selecione as opções para comparação de valores da cadeia de caracteres. As opções dessa propriedade são listadas na tabela a seguir. O valor padrão desta opção é **Padrão**.  
  
> [!NOTE]  
>  Se o curinga **(\*)** for usado para **ColumnName**, **CompareOptions** será somente leitura e será definido como **Padrão**.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Default**|Classifica e compara dados com base na ordenação da coluna na tabela de origem.|  
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
 **ValueDistributionOption**  
 Especifique se deseja computar a distribuição para todos os valores de coluna. O valor padrão desta opção é **FrequentValues**.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**AllValues**|A distribuição é computada para todos os valores de coluna.|  
|**FrequentValues**|A distribuição é computada somente para valores cuja frequência excede o valor mínimo especificado em **FrequentValueThreshold**. Os valores que não estiverem dentro do **FrequentValueThreshold** serão excluídos do relatório de saída.|  
  
 **FrequentValueThreshold**  
 Especifique o limite (um valor entre 0 e 1) a partir do qual o valor de coluna deve ser informado. Esta opção é desabilitada se **AllValues** for selecionado como **ValueDistributionOption**. O valor padrão desta opção é 0.001.  
  
## <a name="see-also"></a>Consulte também  
 [Editor da tarefa Criação de Perfil de Dados &#40;Página Geral&#41;](../general-page-of-integration-services-designers-options.md)   
 [Formulário de Perfil Rápido de Tabela Única &#40;Tarefa Criação de Perfil de Dados&#41;](single-table-quick-profile-form-data-profiling-task.md)  
  
  
