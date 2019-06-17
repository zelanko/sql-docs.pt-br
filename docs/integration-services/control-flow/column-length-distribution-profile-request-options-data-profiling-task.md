---
title: Opções de solicitação do perfil Distribuição de Comprimento de Coluna (tarefa Criação de Perfil de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: 1a4de41f-f38d-40ea-ba1b-6c0ef67ea52a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1307ae8e5fdc81a0c42d17899fb9ea0fa3a1e2f7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65727895"
---
# <a name="column-length-distribution-profile-request-options-data-profiling-task"></a>Opções de solicitação do perfil Distribuição de Comprimento de Coluna (tarefa Criação de Perfil de Dados)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Use o painel **Propriedades da Solicitação** da página **Solicitações de Perfil** para definir as opções da **Solicitação de Perfil de Distribuição de Comprimento de Coluna** selecionada no painel de solicitações. Um Perfil de Distribuição de Comprimento de Coluna reporta todos os comprimentos distintos de valores de cadeia de caracteres na coluna selecionada e a porcentagem de linhas na tabela que cada comprimento representa. Esse perfil pode ajudá-lo a identificar problemas em seus dados, como valores inválidos. Por exemplo, você cria o perfil de uma coluna com códigos de estados dos Estados Unidos com dois caracteres e descobre valores maiores que dois caracteres.  
  
> [!NOTE]  
>  As opções descritas neste tópico são exibidas na página **Solicitações de Perfil** do **Editor da Tarefa Criação de Perfil de Dados**. Para obter mais informações sobre essa página do editor, consulte [Editor da Tarefa Criação de Perfil de Dados &#40;Página Solicitações de perfil&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md).  
  
 Para obter mais informações sobre como usar a Tarefa Criação de Perfil de Dados, consulte [Configuração da Tarefa Criação de Perfil de Dados](../../integration-services/control-flow/setup-of-the-data-profiling-task.md). Para obter mais informações sobre como usar o Visualizador de Perfil de Dados para analisar a saída da Tarefa Criação de Perfil de Dados, consulte [Visualizador de Perfil de Dados](../../integration-services/control-flow/data-profile-viewer.md).  
  
## <a name="request-properties-options"></a>Opções de Propriedades da Solicitação  
 Em uma **Solicitação de Perfil de Distribuição de Comprimento de Coluna**, o painel **Propriedades da Solicitação** exibe os seguintes grupos de opções:  
  
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
 Especifique o esquema ao qual a tabela selecionada pertence. Esta opção é somente leitura.  
  
 **Table**  
 Exibe o nome da tabela selecionada. Esta opção é somente leitura.  
  
#### <a name="column-options"></a>Opções de Coluna  
 **IsWildCard**  
 Especifica se o curinga **(\*)** foi selecionado. Esta opção será definida como **True** se você tiver selecionado **(\*)** para analisar todas as colunas. Será **Falso** se você selecionou uma coluna individual para a criação de um perfil. Esta opção é somente leitura.  
  
 **ColumnName**  
 Exibe o nome da coluna selecionada. Esta opção estará em branco se você tiver selecionado **(\*)** para analisar todas as colunas. Esta opção é somente leitura.  
  
 **StringCompareOptions**  
 Esta opção não se aplica ao Perfil de Distribuição de Comprimento de Coluna.  
  
### <a name="general-options"></a>Opções gerais  
 **RequestID**  
 Digite um nome descritivo para identificar esta solicitação de perfil. Normalmente, não é necessário alterar o valor gerado automaticamente.  
  
### <a name="options"></a>Opções  
 **IgnoreLeadingSpaces**  
 Indique se espaços à esquerda devem ser ignorados quando o perfil comparar valores da cadeia de caracteres. O valor padrão desta opção é **False**.  
  
 **IgnoreTrailingSpaces**  
 Indique se espaços à direita devem ser ignorados quando o perfil comparar valores da cadeia de caracteres. O valor padrão desta opção é **Verdadeiro**.  
  
## <a name="see-also"></a>Consulte Também  
 [Editor da tarefa Criação de Perfil de Dados &#40;Página Geral&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [Formulário de Perfil Rápido de Tabela Única &#40;Tarefa Criação de Perfil de Dados&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  
