---
title: Formulário de Perfil Rápido de Tabela Única (Tarefa Criação de Perfil de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataprofilingtask.quickprofile.f1
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: d2fac9ce-730e-474e-961a-69406b633778
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1adcb5703b2f05282d564bca3eba43012d14e3a1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47599817"
---
# <a name="single-table-quick-profile-form-data-profiling-task"></a>Single Table Quick Profile Form (Data Profiling Task)
  Use o **Formulário de Perfil Rápido de Tabela Única** para configurar a tarefa Criação de Perfil de Dados para criar um perfil de uma tabela ou exibição única usando as configurações padrão.  
  
 Para obter mais informações sobre como usar a Tarefa Criação de Perfil de Dados, consulte [Configuração da Tarefa Criação de Perfil de Dados](../../integration-services/control-flow/setup-of-the-data-profiling-task.md). Para obter mais informações sobre como usar o Visualizador de Perfil de Dados para analisar a saída da Tarefa Criação de Perfil de Dados, consulte [Visualizador de Perfil de Dados](../../integration-services/control-flow/data-profile-viewer.md).  
  
## <a name="options"></a>Opções  
 **Conexão**  
 Selecione um gerenciador de conexões do [!INCLUDE[vstecado](../../includes/vstecado-md.md)] que usa o Provedor de Dados .NET para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) para se conectar com o banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contém a tabela ou a exibição que você deseja analisar.  
  
 **Tabela ou Exibição**  
 Selecione uma tabela ou exibição existente no banco de dados com o qual o gerenciador de conexões selecionado se conecta.  
  
 **Computar**  
 Selecione quais perfis devem ser computados.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Perfil Razão Nula de Coluna**|Compute um perfil Razão Nula de Coluna usando as configurações padrão para todas as colunas aplicáveis na tabela ou exibição selecionada.<br /><br /> Este perfil informa a porcentagem de valores nulos na coluna selecionada. Este perfil pode ajudar a identificar problemas em seus dados, como uma inesperada razão alta de valores nulos em uma coluna. Para obter mais informações sobre as configurações para este perfil, consulte [Opções da solicitação do perfil Razão Nula de Coluna &#40;Tarefa Criação de Perfil de Dados&#41;](../../integration-services/control-flow/column-null-ratio-profile-request-options-data-profiling-task.md).|  
|**Perfil Estatísticas de Coluna**|Compute um perfil Estatísticas de Coluna usando as configurações padrão para todas as colunas aplicáveis na tabela ou exibição selecionada.<br /><br /> Este perfil informa estatísticas como mínimo, máximo, média e desvio padrão para colunas numéricas, além de mínimo e máximo para colunas **datetime** . Este perfil pode ajudá-lo a identificar problemas em seus dados, como datas inválidas. Para obter mais informações sobre as configurações para este perfil, consulte [Opções da solicitação do perfil de Estatísticas de Coluna &#40;Tarefa Criação de Perfil de Dados&#41;](../../integration-services/control-flow/column-statistics-profile-request-options-data-profiling-task.md).|  
|**Perfil Distribuição de Valor de Coluna**|Compute um perfil Distribuição de Valor de Coluna usando as configurações padrão para todas as colunas aplicáveis na tabela ou exibição selecionada.<br /><br /> Este perfil informa todos os valores distintos na coluna selecionada e a porcentagem de linhas na tabela que cada valor representa. O perfil também pode informar valores que representam mais que uma porcentagem especificada de linhas na tabela. O perfil também pode ajudar a identificar problemas em seus dados, como um número incorreto de valores distintos em uma coluna. Para obter mais informações sobre esse perfil, consulte [Opções da solicitação de perfil de Distribuição de Valor de Coluna &#40;Tarefa Criação de Perfil de Dados&#41;](../../integration-services/control-flow/column-value-distribution-profile-request-options-data-profiling-task.md).|  
|**Perfil Distribuição de Comprimento de Coluna**|Compute um perfil Distribuição de Comprimento de Coluna usando as configurações padrão para todas as colunas aplicáveis na tabela ou exibição selecionada.<br /><br /> O perfil Distribuição de Comprimento de Coluna informa todos os comprimentos distintos de valores de cadeia de caracteres na coluna selecionada e a porcentagem de linhas na tabela que cada comprimento representa. Este perfil pode ajudar a identificar problemas em seus dados, como valores que não são válidos. Para obter mais informações sobre as configurações desse perfil, consulte [Opções da solicitação de perfil de Distribuição de Comprimento de Coluna &#40;Tarefa Criação de Perfil de Dados&#41;](../../integration-services/control-flow/column-length-distribution-profile-request-options-data-profiling-task.md).|  
|**Perfil Padrão de Coluna**|Compute um perfil Padrão de Coluna usando as configurações padrão para todas as colunas aplicáveis na tabela ou exibição selecionada.<br /><br /> Este perfil informa um conjunto de expressões regulares que cobrem os valores em uma coluna de cadeia de caracteres. Este perfil pode ajudar a identificar problemas em seus dados, como cadeias de caracteres inválidas. Este perfil também pode sugerir expressões regulares que podem ser usadas no futuro para validar novos valores. Para obter mais informações sobre as configurações desse perfil, consulte [Opções da solicitação de perfil de Comprimento de Coluna &#40;Tarefa Criação de Perfil de Dados&#41;](../../integration-services/control-flow/column-pattern-profile-request-options-data-profiling-task.md).|  
|**Perfil-chave de candidato**|Compute um perfil Chave Candidata para combinações de colunas que incluem até o número de colunas especificado em **para até N chaves de coluna**.<br /><br /> Este perfil informa se uma coluna ou conjunto de colunas é apropriado para servir como chave para a tabela selecionada. Este perfil também pode ajudar a identificar problemas em seus dados, como valores em duplicata em uma possível coluna de chave. Para obter mais informações sobre as configurações desse perfil, consulte [Opções da solicitação de perfil de Chave de Candidato &#40;Tarefa Criação de Perfil de Dados&#41;](../../integration-services/control-flow/candidate-key-profile-request-options-data-profiling-task.md).|  
|**para até N chaves de coluna**|Selecione o número máximo de colunas para testar em possíveis combinações como uma chave para a tabela ou exibição. O valor padrão é 1. O valor máximo é 1000. Por exemplo, selecionando três testes de combinações de chave de uma coluna, de duas colunas e de três colunas.|  
|**Perfil Dependência Funcional**|Compute um perfil Dependência Funcional para combinações de coluna determinante que incluem até o número de colunas especificado em **para até N colunas como determinantes**.<br /><br /> Este perfil informa até que ponto os valores em uma coluna (a coluna dependente) dependem dos valores em outra coluna ou conjunto de colunas (a coluna determinante). Este perfil também pode ajudar a identificar problemas em seus dados, como valores inválidos. Para obter mais informações sobre as configurações desse perfil, consulte [Opções da solicitação de perfil de Dependência Funcional &#40;Tarefa Criação de Perfil de Dados&#41;](../../integration-services/control-flow/functional-dependency-profile-request-options-data-profiling-task.md).|  
|**para até N colunas como determinantes**|Selecione o número máximo de colunas para testar em possíveis combinações como as colunas determinantes. O valor padrão é 1. O valor máximo é 1000. Por exemplo, selecionando dois testes de combinações nas quais as combinações de coluna única e de coluna dupla são as colunas determinantes da outra coluna (dependente).|  
  
> [!NOTE]  
>  O tipo de perfil Valor Inclusão não está disponível no **Formulário de Perfil Rápido de Tabela Única**.  
  
## <a name="see-also"></a>Consulte Também  
 [Editor da tarefa Criação de Perfil de Dados &#40;Página Geral&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [Editor da tarefa Criação de Perfil de Dados &#40;Página Solicitações de Perfil&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md)  
  
  
