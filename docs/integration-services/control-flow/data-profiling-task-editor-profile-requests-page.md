---
title: Editor de Tarefa Criação de Perfil de Dados (Página de Solicitações de Perfil) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataprofilingtask.profilerequests.f1
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: c72acb3d-380e-436e-8041-ed364eddfabd
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a13799d353fcf1e1dff1999009cc2f1e8dcedc76
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71294176"
---
# <a name="data-profiling-task-editor-profile-requests-page"></a>Data Profiling Task Editor (Profile Requests Page)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Use a página **Solicitações de Perfil** do **Editor da Tarefa Criação de Perfil de Dados** para selecionar e configurar os perfis que deseja computar. Em uma tarefa Criação de Perfil de Dados simples, você pode calcular várias perfis para várias colunas ou combinações de colunas em várias tabelas ou exibições.  
  
 Para obter mais informações sobre como usar a Tarefa Criação de Perfil de Dados, consulte [Configuração da Tarefa Criação de Perfil de Dados](../../integration-services/control-flow/setup-of-the-data-profiling-task.md). Para obter mais informações sobre como usar o Visualizador de Perfil de Dados para analisar a saída da Tarefa Criação de Perfil de Dados, consulte [Visualizador de Perfil de Dados](../../integration-services/control-flow/data-profile-viewer.md).  
  
 **Para abrir a página Solicitações de Perfil do Editor da Tarefa Criação de Perfil de Dados**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém a tarefa Criação de Perfil de Dados.  
  
2.  Na guia **Fluxo de Controle** , clique duas vezes na tarefa Criação de Perfil de Dados.  
  
3.  No **Editor da Tarefa Criação de Perfil de Dados**, clique em **Solicitações de Perfil**.  
  
## <a name="using-the-requests-pane"></a>Usando o painel de solicitações  
 O painel de solicitações é o painel exibido no topo da página. Esse painel lista todos os perfis configurados para a tarefa Criação de Perfil Dados atual. Se nenhum perfil foi configurado, o painel de solicitações ficará vazio. Para adicionar um novo perfil, clique em uma área vazia embaixo da coluna **Tipo de Perfil** e selecione o tipo de perfil da lista. Para configurar um perfil, selecione o perfil no painel de solicitações e depois defina as propriedades do perfil no painel **Propriedades da Solicitação** .  
  
### <a name="requests-pane-options"></a>Opções do painel de solicitações  
 O painel de solicitações tem as seguintes opções:  
  
 **Exibir**  
 Selecione se deseja visualizar todos os perfis configurados para a tarefa ou somente um dos perfis.  
  
 As colunas no painel de solicitações foram alteradas com base na **Exibição** selecionada. Para obter mais informações sobre cada uma dessas colunas, consulte a próxima seção, "Colunas do painel de solicitações".  
  
### <a name="requests-pane-columns"></a>Colunas do painel de solicitações  
 As colunas exibidas pelo painel de solicitações dependem da **Exibição** selecionada:  
  
-   Se **Todas as Solicitações**for selecionado, o painel de solicitações terá duas colunas: **Tipo de Perfil** e **ID da Solicitação**.  
  
-   Se desejar exibir um dos cinco perfis de coluna, o painel de solicitações terá quatro colunas: **Tipo de Perfil**, **Tabela ou Exibição**, **Coluna** e **ID da Solicitação**.  
  
-   Se optar por exibir um perfil Chave Candidata, o painel de solicitações terá quatro colunas: **Tipo de Perfil**, **Tabela ou Exibição**, **Colunas de Chave**e **ID da Solicitação**.  
  
-   Se você optar por exibir um perfil Dependência Funcional, o painel de solicitações terá cinco colunas: **Tipo de Perfil**, **Tabela ou Exibição**, **Colunas Determinantes**, **Coluna Dependente**, e **ID da Solicitação**.  
  
-   Se você optar por exibir um perfil Inclusão de Valor, o painel de solicitações terá seis colunas: **Tipo de Perfil**, **Tabela Lateral de Subconjunto ou Exibição**, **Tabela Lateral de Superconjunto ou Exibição**, **Colunas Laterais de Subconjunto**, **Colunas Laterais de Superconjunto**e **ID da Solicitação**.  
  
 As seções a seguir descrevem cada dessas colunas.  
  
#### <a name="columns-common-to-all-views"></a>Colunas comuns a todas as exibições  
 **Tipo de Perfil**  
 Selecione um perfil de dados das opções seguintes:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Solicitação do Perfil Chave de Candidato**|Compute um perfil Chave de Candidato.<br /><br /> Este perfil informa se uma coluna ou conjunto de colunas é uma chave, ou uma chave aproximada, para a tabela selecionada. Este perfil também pode ajudar a identificar problemas em seus dados, como valores em duplicata em uma possível coluna de chave.|  
|**Solicitação do Perfil Distribuição de Comprimento de Coluna**|Computa um perfil Distribuição de Comprimento da Coluna.<br /><br /> O perfil Distribuição de Comprimento de Coluna informa todos os comprimentos distintos de valores de cadeia de caracteres na coluna selecionada e a porcentagem de linhas na tabela que cada comprimento representa. Este perfil pode ajudar a identificar problemas em seus dados, como valores que não são válidos. Por exemplo, você cria o perfil de uma coluna com códigos de estados dos Estados Unidos com dois caracteres e descobre valores maiores que dois caracteres.|  
|**Solicitação do Perfil Razão Nula de Coluna**|Computa um perfil Razão Nula de Coluna.<br /><br /> O perfil Razão Nula de Coluna informa a porcentagem de valores nulos na coluna selecionada. Este perfil pode ajudar a identificar problemas em seus dados, como uma inesperada razão alta de valores nulos em uma coluna. Por exemplo, você cria um perfil de uma coluna de Zip/Código Postal e descobre uma porcentagem alta e inaceitável de códigos ausentes.|  
|**Solicitação do Perfil Padrão de Coluna**|Computa um Perfil Padrão de Coluna.<br /><br /> O perfil Padrão de Coluna informa um conjunto de expressões regulares que cobrem a porcentagem especificada de valores em uma coluna de cadeia de caracteres. Esse perfil pode ajudar a identificar problemas em seus dados, como cadeias de caracteres inválidos. Este perfil também pode sugerir expressões regulares que podem ser usadas no futuro para validar novos valores. Por exemplo, um perfil de padrão de uma coluna de Código Postal dos Estados Unidos pode produzir as expressões regulares: \d{5}-\d{4}, \d{5} e \d{9}. Se você vir outras expressões regulares, seus dados provavelmente conterão valores inválidos ou que estão em um formato incorreto.|  
|**Solicitação do Perfil Estatísticas de Coluna**|Selecione esta opção para computar um perfil Estatísticas de Coluna usando as configurações padrão para todas as colunas aplicáveis na tabela ou exibição selecionada.<br /><br /> Um perfil Estatísticas de Coluna informa estatísticas como mínimo, máximo, média e desvio padrão para colunas numéricas, além de mínimo e máximo para colunas **datetime** . Esse perfil pode ajudar a identificar problemas em seus dados, como datas inválidas. Por exemplo, você cria o perfil de uma coluna de datas de histórico e descobre uma data máxima no futuro.|  
|**Solicitação do Perfil Distribuição de Valor**|Computa um perfil Distribuição de Valor da Coluna.<br /><br /> Um perfil Distribuição de Valor de Coluna informa todos os valores distintos na coluna selecionada e a porcentagem de linhas na tabela que cada valor representa. Esse perfil também pode informar valores que representam mais que uma porcentagem especificada na tabela. O perfil também pode ajudar a identificar problemas em seus dados, como um número incorreto de valores distintos em uma coluna. Por exemplo, você cria o perfil de uma coluna que contém estados dos Estados Unidos e descobre mais que 50 valores distintos.|  
|**Solicitação do Perfil Dependência Funcional**|Compute um perfil Dependência Funcional.<br /><br /> Um perfil Dependência Funcional informa até que ponto os valores em uma coluna (a coluna dependente) dependem dos valores em outra coluna ou conjunto de colunas (a coluna determinante). Este perfil também pode ajudar a identificar problemas em seus dados, como valores inválidos. Por exemplo, você cria o perfil da dependência entre uma coluna que contém Códigos Postais dos Estados Unidos e uma coluna que contém estados dos Estados Unidos. O mesmo Código Postal sempre deve ter o mesmo estado, mas o perfil descobre violações desta dependência.|  
|**Solicitação do Perfil Inclusão de Valor**|Compute um perfil Inclusão de Valor.<br /><br /> O perfil Inclusão de Valor computa a sobreposição nos valores entre duas colunas ou conjuntos de colunas. Esse perfil também pode determinar se uma coluna ou conjunto de colunas é apropriado para servir como uma chave estrangeira entre as tabelas selecionadas. Esse perfil também pode ajudar a identificar problemas em seus dados, como valores inválidos. Por exemplo, você cria um perfil com a coluna ID_do_produto de uma tabela Vendas e descobre que a coluna contém valores não encontrados na coluna ID_do_produto da tabela Produtos.|  
  
 **RequestID**  
 Exibe o identificador da solicitação. Normalmente, não é necessário alterar o valor gerado automaticamente.  
  
#### <a name="columns-common-to-all-individual-profiles"></a>Colunas comuns a todos os perfis individuais  
 **Gerenciador de Conexões**  
 Exibe o gerenciador de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)] que se conecta ao banco de dados de origem.  
  
 **Request ID**  
 Exibe um identificador da solicitação. Normalmente, não é necessário alterar o valor gerado automaticamente.  
  
#### <a name="columns-common-to-the-five-individual-column-profiles"></a>Colunas comuns aos cinco perfis de colunas individuais  
 **Tabela ou Exibição**  
 Exibe a tabela ou exibição que contêm a coluna selecionada.  
  
 **Coluna**  
 Exibe a coluna selecionada para a criação de perfil.  
  
#### <a name="columns-specific-to-the-candidate-key-profile"></a>Colunas específicas ao perfil Chave de Candidato  
 **Tabela ou Exibição**  
 Exibe a tabela ou exibição que contêm as colunas selecionadas.  
  
 **Colunas de Chave**  
 Exibe as colunas selecionadas para a criação de perfil.  
  
#### <a name="columns-specific-to-the-functional-dependency-profile"></a>Colunas específicas ao perfil Dependência Funcional  
 **Tabela ou Exibição**  
 Exibe a tabela ou exibição que contêm as colunas selecionadas.  
  
 **Colunas Determinantes**  
 Exibe as colunas selecionadas para a criação de perfil como coluna ou colunas determinantes. No exemplo no qual o código postal dos Estados Unidos determina o estado nos Estados Unidos, a coluna determinante seria a coluna Código Postal.  
  
 **Dependent column**  
 Exibe as colunas selecionadas para a criação de perfil como coluna dependente. No exemplo no qual o código postal dos Estados Unidos determina o estado nos Estados Unidos, a coluna dependente seria a coluna com os estados.  
  
#### <a name="columns-specific-to-the-value-inclusion-profile"></a>Colunas específicas ao perfil Inclusão de Valor  
 **Tabela Lateral de Subconjunto ou Exibição**  
 Exibe a tabela ou exibição que contêm a coluna ou colunas selecionadas como colunas laterais de subconjunto.  
  
 **Tabela Lateral de Superconjunto ou Exibição**  
 Exibe a tabela ou exibição que contêm a coluna ou colunas selecionadas como colunas laterais de superconjunto.  
  
 **Colunas Laterais de Subconjunto**  
 Exibe a coluna ou colunas selecionadas para a criação de perfil como colunas laterais de subconjunto. No exemplo no qual você deseja verificar se os valores em uma coluna com estados dos Estados Unidos estão em uma tabela de referência com códigos de estados dos Estados Unidos de dois caracteres, a coluna de subconjunto é a coluna com os estados na tabela de origem.  
  
 **Colunas Laterais de Superconjunto**  
 Exibe a coluna ou colunas selecionadas para a criação de perfil como colunas laterais de superconjunto. No exemplo no qual você deseja verificar se os valores em uma coluna com estados dos Estados Unidos estão em uma tabela de referência com códigos de estados dos Estados Unidos de dois caracteres, a coluna de superconjunto é a coluna com os códigos dos estados na tabela de referência.  
  
## <a name="using-the-request-properties-pane"></a>Usando o painel Propriedades de Solicitação  
 O painel **Propriedades de Solicitação** é exibido debaixo do painel de solicitações. Esse painel exibe as opções para o perfil selecionado no painel de solicitações.  
  
> [!NOTE]  
>  Após selecionar um **Tipo de Perfil**, é necessário selecionar o campo **ID da Solicitação** para exibir as propriedades da solicitação de perfil no painel **Propriedades de Solicitação** .  
  
 Essas opções variam com base no perfil selecionado. Para obter mais informações sobre as opções para tipos de perfil individual, consulte os seguintes tópicos:  
  
-   [Opções da solicitação de perfil Chave de Candidato &#40;tarefa Criação de Perfil de Dados&#41;](../../integration-services/control-flow/candidate-key-profile-request-options-data-profiling-task.md)  
  
-   [Opções da solicitação do perfil Razão Nula de Coluna &#40;Tarefa Criação de Perfil de Dados&#41;](../../integration-services/control-flow/column-null-ratio-profile-request-options-data-profiling-task.md)  
  
-   [Opções da solicitação do perfil Estatísticas de Coluna &#40;Tarefa Criação de Perfil de Dados&#41;](../../integration-services/control-flow/column-statistics-profile-request-options-data-profiling-task.md)  
  
-   [Opções de solicitação do perfil Distribuição de Valor de Coluna &#40;Tarefa Criação de Perfil de Dados&#41;](../../integration-services/control-flow/column-value-distribution-profile-request-options-data-profiling-task.md)  
  
-   [Opções da solicitação de perfil Distribuição de Tamanho de Coluna &#40;Tarefa Criação de Perfil de Dados&#41;](../../integration-services/control-flow/column-length-distribution-profile-request-options-data-profiling-task.md)  
  
-   [Opções da solicitação do perfil Padrão de Coluna &#40;Tarefa Criação de Perfil de Dados&#41;](../../integration-services/control-flow/column-pattern-profile-request-options-data-profiling-task.md)  
  
-   [Opções da solicitação do perfil Dependência Funcional &#40;Tarefa Criação de Perfil de Dados&#41;](../../integration-services/control-flow/functional-dependency-profile-request-options-data-profiling-task.md)  
  
-   [Opções da solicitação do perfil Inclusão de Valor &#40;Tarefa Criação de Perfil de Dados&#41;](../../integration-services/control-flow/value-inclusion-profile-request-options-data-profiling-task.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Editor da tarefa Criação de Perfil de Dados &#40;Página Geral&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [Formulário de Perfil Rápido de Tabela Única &#40;Tarefa Criação de Perfil de Dados&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  
