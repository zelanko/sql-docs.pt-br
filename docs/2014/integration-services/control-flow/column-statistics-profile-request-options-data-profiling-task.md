---
title: Opções da solicitação do perfil Estatísticas de Coluna (tarefa Criação de Perfil de Dados) | Microsoft Docs
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
ms.assetid: 87205984-507a-49f3-b27c-36a0075c234d
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: e50abc86092a2d39f6fdb40ab9776063be3e71ea
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118720"
---
# <a name="column-statistics-profile-request-options-data-profiling-task"></a>Opções da solicitação do perfil Estatísticas de Coluna (tarefa Criação de Perfil de Dados)
  Use o painel **Propriedades da Solicitação** da página **Solicitações de Perfil** para definir as opções da **Solicitação de Perfil de Estatísticas de Coluna** selecionada no painel de solicitações. Um perfil de Estatísticas de Coluna informa estatísticas como mínimo, máximo, média e desvio padrão para colunas numéricas, além de mínimo e máximo para colunas `datetime`. Este perfil pode ajudá-lo a identificar problemas em seus dados, como datas inválidas. Por exemplo, você cria o perfil de uma coluna de datas de histórico e descobre uma data máxima no futuro.  
  
> [!NOTE]  
>  As opções descritas neste tópico são exibidas na página **Solicitações de Perfil** do **Editor da Tarefa Criação de Perfil de Dados**. Para obter mais informações sobre essa página do editor, consulte [Editor da Tarefa Criação de Perfil de Dados &#40;Página Solicitações de perfil&#41;](data-profiling-task-editor-profile-requests-page.md).  
  
 Para obter mais informações sobre como usar a Tarefa Criação de Perfil de Dados, consulte [Configuração da Tarefa Criação de Perfil de Dados](data-profiling-task.md). Para obter mais informações sobre como usar o Visualizador de Perfil de Dados para analisar a saída da Tarefa Criação de Perfil de Dados, consulte [Visualizador de Perfil de Dados](data-profile-viewer.md).  
  
## <a name="request-properties-options"></a>Opções de Propriedades da Solicitação  
 Para uma **Solicitação de Perfil de Estatísticas de Coluna**, o painel **Propriedades da Solicitação** exibe os seguintes grupos de opções:  
  
-   **Dados**que incluem as opções **TableOrView** e **Column**  
  
-   **Geral**  
  
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
 Esta opção não é aplicável ao Perfil de Estatísticas de Coluna.  
  
### <a name="general-options"></a>Opções gerais  
 **RequestID**  
 Digite um nome descritivo para identificar esta solicitação de perfil. Normalmente, não é necessário alterar o valor gerado automaticamente.  
  
## <a name="see-also"></a>Consulte também  
 [Editor da tarefa de criação de perfil dados &#40;página geral&#41;](../general-page-of-integration-services-designers-options.md)   
 [Formulário de Perfil Rápido de Tabela Única &#40;Tarefa Criação de Perfil de Dados&#41;](single-table-quick-profile-form-data-profiling-task.md)  
  
  