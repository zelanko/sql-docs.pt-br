---
title: Tarefa Criação de Perfil de Dados | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: control-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.dataprofilingtask.f1
helpviewer_keywords:
- Data Profiling task [Integration Services], about Data Profiling task
- data profiling
- profiling data
ms.assetid: 248ce233-4342-42c5-bf26-f4387ea152cf
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f13b87b12f22b05984574a41b4b74d9ef1c748cf
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="data-profiling-task"></a>Tarefa Criação de Perfil de Dados
  A tarefa Criação de Perfil de Dados computa vários perfis ajudam a familiarizar-se com uma fonte de dados e a identificar problemas nos dados que precisam ser corrigidos.  
  
 É possível usar a tarefa Criação de perfil de dados dentro de um pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para criar perfil de dados armazenado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e identificar possíveis problemas com a qualidade dos dados.  
  
> [!NOTE]  
>  Este tópico descreve apenas os recursos e os requisitos da tarefa Criação de Perfil de Dados. Para obter um passo a passo de como usar a tarefa Criação de Perfil de Dados, consulte a seção [Tarefa e Visualizador de Criação de Perfil de Dados](../../integration-services/control-flow/data-profiling-task-and-viewer.md).  
  
## <a name="requirements-and-limitations"></a>Requisitos e limitações  
 A tarefa Criação de Perfil de Dados funciona apenas com dados armazenados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa tarefa não funciona com fontes de dados de terceiros ou baseadas em arquivo.  
  
 Além disso, para executar um pacote que contém a tarefa Criação de Perfil de Dados, você deve usar uma conta que tem permissões de leitura/gravação, inclusive permissões CREATE TABLE, no banco de dados tempdb.  
  
## <a name="data-profiler-viewer"></a>Visualizador do Criador de Perfil de Dados  
 Após usar a tarefa para computar perfis de dados e salvá-los em um arquivo, você pode usar o Visualizador de Perfil de Dados autônomo para examinar a saída de perfil. O Visualizador de perfil de dados também suporta o recurso de extração de detalhes para ajudá-lo a entender problemas com a qualidade dos dados identificados no resultado do perfil. Para obter mais informações, consulte [Visualizador de Perfil de Dados](../../integration-services/control-flow/data-profile-viewer.md).  
  
> [!IMPORTANT]  
>  O arquivo de saída pode conter dados confidenciais sobre seu banco de dados e os dados contidos no banco de dados. Para obter sugestões sobre como tornar esse arquivo mais seguro, consulte [Acesso aos arquivos usados por pacotes](../../integration-services/security/security-overview-integration-services.md#files).  
>   
>  O recurso de busca detalhada que está disponível no Visualizador de Perfil de Dados envia consultas ao vivo à fonte de dados original.  
  
## <a name="available-profiles"></a>Perfis disponíveis  
 A tarefa Criação de perfil de dados pode computar oito perfis de dados diferentes. Cinco desses perfis analisam colunas individuais e os três restantes analisam diversas colunas ou relações entre colunas e tabelas.  
  
 Os cinco perfis a seguir analisam colunas individuais.  
  
|Perfis que analisam colunas individuais|Description|  
|----------------------------------------------|-----------------|  
|Perfil Distribuição de Comprimento de Coluna|Reporta todos os comprimentos de valores de cadeia de caracteres na coluna selecionada e a porcentagem de linhas na tabela que cada comprimento representa.<br /><br /> Este perfil o ajuda a identificar problemas em seus dados, como valores que não são válidos. Por exemplo, você cria o perfil de uma coluna com códigos de estados dos Estados Unidos que devem ter dois caracteres e descobre valores maiores que dois caracteres.|  
|Perfil Razão Nula de Coluna|Informa a porcentagem de valores nulos na coluna selecionada.<br /><br /> Este perfil o ajuda a identificar problemas em seus dados, como uma razão alta de valores nulos inesperada em uma coluna. Por exemplo, você cria um perfil de uma coluna de Zip/Código Postal e descobre uma porcentagem alta e inaceitável de códigos ausentes.|  
|Perfil Padrão de Coluna|Informa um conjunto de expressões regulares que cobrem a porcentagem especificada de valores em uma coluna de cadeia de caracteres.<br /><br /> Este perfil o ajuda a identificar problemas em seus dados, como cadeias de caracteres que não são válidas. Este perfil também pode sugerir expressões regulares que podem ser usadas no futuro para validar novos valores. Por exemplo, um perfil de padrão de uma coluna CEP dos Estados Unidos pode produzir as expressões regulares: \d{5}-\d{4}, \d{5} e \d{9}. Se você vir outras expressões regulares, seus dados provavelmente conterão valores inválidos ou que estão em um formato incorreto.|  
|Perfil Estatísticas de Coluna|Informa estatísticas como mínimo, máximo, média e desvio padrão para colunas numéricas, além de mínimo e máximo para colunas **datetime** .<br /><br /> Este perfil o ajuda a identificar problemas em seus dados, como datas inválidas. Por exemplo, você cria o perfil de uma coluna de datas de histórico e descobre uma data máxima no futuro.|  
|Perfil Distribuição de Valor de Coluna|Reporta todos os valores distintos na coluna selecionada e a porcentagem de linhas na tabela que cada valor representa. Também pode informar valores que representam mais que uma porcentagem especificada de linhas na tabela.<br /><br /> Este perfil o ajuda a identificar problemas em seus dados, como um número incorreto ou valores distintos em uma coluna. Por exemplo, você cria o perfil de uma coluna que supostamente contém estados dos Estados Unidos e descobre mais de 50 valores distintos.|  
  
 Os três perfis a seguir analisam diversas colunas ou relações entre colunas e tabelas.  
  
|Perfis que analisam diversas colunas|Description|  
|--------------------------------------------|-----------------|  
|Perfil-chave de candidato|Informa se uma coluna ou conjunto de colunas é uma chave, ou uma chave aproximada, para a tabela selecionada.<br /><br /> Este perfil também o ajuda a identificar problemas em seus dados, como valores duplicados em uma possível coluna chave.|  
|Perfil Dependência Funcional|Informa até que ponto os valores em uma coluna (a coluna dependente) dependem dos valores em outra coluna ou conjunto de colunas (a coluna determinante).<br /><br /> Este perfil também o ajuda a identificar problemas em seus dados, como valores inválidos. Por exemplo, você cria o perfil da dependência entre uma coluna que contém CEPs dos Estados Unidos e uma coluna que contém estados dos Estados Unidos. O mesmo Código Postal sempre deve ter o mesmo estado, mas o perfil descobre violações desta dependência.|  
|Perfil de inclusão de valor|Computa a sobreposição nos valores entre duas colunas ou conjuntos de colunas. Este perfil pode determinar se uma coluna ou conjunto de colunas é apropriado para servir como uma chave estrangeira entre as tabelas selecionadas.<br /><br /> Este perfil também o ajuda a identificar problemas em seus dados, como valores inválidos. Por exemplo, você cria um perfil com a coluna ID_do_produto de uma tabela Vendas e descobre que a coluna contém valores não encontrados na coluna ID_do_produto da tabela Produtos.|  
  
## <a name="prerequisites-for-a-valid-profile"></a>Pré-requisitos para um perfil válido  
 Um perfil não é válido a menos que você selecione tabelas e colunas que não estejam vazias e as colunas contenham tipos de dados válidos para o perfil.  
  
### <a name="valid-data-types"></a>Tipos de dados válidos  
 Alguns dos perfis disponíveis têm importância apenas para determinados tipos de dados. Por exemplo, computar um perfil de padrão da coluna para uma coluna que contém valores numéricos ou **datetime** não tem importância. Portanto, esse perfil não é válido.  
  
|Perfil|Tipos de dados válidos*|  
|-------------|------------------------|  
|ColumnStatisticsProfile|Colunas de tipo numérico ou **datetime** (sem **mean** nem **stddev** na coluna **datetime** )|  
|ColumnNullRatioProfile|Todas as colunas**|  
|ColumnValueDistributionProfile|Colunas do tipo **integer** , do tipo **char** e do tipo **datetime**|  
|ColumnLengthDistributionProfile|Colunas do tipo **char** |  
|ColumnPatternProfile|Colunas do tipo **char** |  
|CandidateKeyProfile|Colunas do tipo **integer** , do tipo **char** e do tipo **datetime**|  
|FunctionalDependencyProfile|Colunas do tipo **integer** , do tipo **char** e do tipo **datetime**|  
|InclusionProfile|Colunas do tipo **integer** , do tipo **char** e do tipo **datetime**|  
  
 \* Na tabela anterior de tipos de dados válidos, os tipos **integer**, **char**, **datetime**e **numeric** incluem os seguintes tipos de dados específicos:  
  
 Entre os tipos de número inteiro estão **bit**, **tinyint**, **smallint**, **int**e **bigint**.  
  
 Tipos de caracteres incluem **char**, **nchar**, **varchar**e **nvarchar** , mas não incluem **varchar(max)** nem **nvarchar(max)**.  
  
 Entre os tipos de data e hora estão **datetime**, **smalldatetime**e **timestamp**.  
  
 Tipos numéricos incluem tipos **integer** (exceto **bit**), **money**, **smallmoney**, **decimal**, **float**, **real**e **numeric**.  
  
 \*\* **image**, **text**, **XML**, **udt**e **variant** em perfis que não sejam o Perfil Razão Nula de Coluna.  
  
### <a name="valid-tables-and-columns"></a>Tabelas e colunas válidas  
 Se a tabela ou coluna estiver vazia, a Criação de perfis de dados executará as seguintes ações:  
  
-   Quando a tabela ou exibição selecionada estiver vazia, a tarefa de Criação de perfis de dados não computará nenhum perfil.  
  
-   Quando todos os valores na coluna selecionada forem nulos, a tarefa de Criação de perfis de dados computará somente o perfil de razão nula da coluna. A tarefa não computa o perfil de Distribuição de comprimento da coluna, o perfil de Padrão da coluna, o perfil de Estatísticas da coluna ou o perfil de Distribuição de valor da coluna.  
  
## <a name="features-of-the-data-profiling-task"></a>Recursos da tarefa de Criação de perfis de dados  
 A tarefa de Criação de perfis de dados tem as seguintes opções de configuração convenientes:  
  
-   **Colunas curinga** Ao configurar uma solicitação de perfil, a tarefa aceita o caractere curinga **(\*)** no lugar do nome da coluna. Isto simplifica a configuração e facilita o descobrimento das características de dados pouco conhecidos. Quando a tarefa executar, ela criará perfis de toda coluna que tiver um tipo de dados apropriado.  
  
-   **Perfil Rápido** You can select Perfil Rápido to configure the task quickly. Um Perfil Rápido cria um perfil de uma tabela ou exibição usando todos os perfis e configurações padrão.  
  
## <a name="custom-logging-messages-available-on-the-data-profililng-task"></a>Mensagens de log personalizadas disponíveis na tarefa Criação de Perfil de Dados  
 A tabela a seguir lista as entradas de log personalizadas para a tarefa Criação de Perfil de Dados. Para obter mais informações, consulte [Log do SSIS &#40;Integration Services&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
|Entrada de log|Description|  
|---------------|-----------------|  
|**DataProfilingTaskTrace**|Fornece informações descritivas sobre o status da tarefa. As mensagens incluem as seguintes informações:<br /><br /> Solicitações de processamento inicial<br /><br /> Início da consulta<br /><br /> Query End<br /><br /> Concluir solicitação de computação|  
  
## <a name="output-and-its-schema"></a>Saída e seu esquema  
 A tarefa Criação de Perfil de Dados produz os perfis selecionados em XML que é estruturado de acordo com o esquema DataProfile.xsd. É possível especificar se a saída deste XML será salva em um arquivo ou em uma variável de pacote. Você pode exibir esse esquema online em [http://schemas.microsoft.com/sqlserver/2008/DataDebugger/](http://schemas.microsoft.com/sqlserver/2008/DataDebugger/). Na página da Web, você pode salvar uma cópia local do esquema. Em seguida, será possível exibir a cópia local do esquema no Microsoft [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ou em outro editor de esquemas, em um editor XML ou em um editor de texto como o Bloco de Notas.  
  
 Com relação às informações sobre a qualidade de dados, o esquema pode ser útil para:  
  
-   Trocar informações de qualidade de dados dentro e entre organizações.  
  
-   Construir ferramentas personalizadas que trabalhem com informações de qualidade de dados.  
  
 O namespace de destino é identificado no esquema como [http://schemas.microsoft.com/sqlserver/2008/DataDebugger/](http://schemas.microsoft.com/sqlserver/2008/DataDebugger/).  
  
## <a name="output-in-the-conditional-workflow-of-a-package"></a>Saída no fluxo de trabalho condicional de um pacote  
 Os componentes de criação de perfil de dados, não incluem funcionalidade interna pronta para implementar lógica condicional no fluxo de trabalho do pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , com base na saída da tarefa de Criação de Perfil de Dados. Porém, você pode adicionar facilmente esta lógica, com uma quantidade mínima de programação, em uma tarefa de Script. Este código poderia efetuar uma consulta XPath contra a saída da XML e salvar o resultado em uma variável de pacote. Restrições de precedência que conectam a tarefa Script a tarefas subsequentes, podem usar uma expressão para determinar o fluxo de trabalho. Por exemplo, a tarefa Script detecta que a porcentagem de valores nulos em uma coluna excede um certo limite. Quando esta condição for verdade, você poderia querer interromper o pacote e resolver o problema antes de continuar.  
  
## <a name="configuration-of-the-data-profiling-task"></a>Configuração da tarefa Criação de Perfil de Dados  
 Você configura a tarefa de Criação de perfil de dados usando o **Editor de tarefa Criação de perfil de dados**. O editor tem duas páginas:  
  
 [Página Geral](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)  
 Na página **Geral** , você especifica o arquivo ou a variável de saída. É possível também selecionar **Perfil Rápido** para configurar rapidamente a tarefa para computar os perfis usando as configurações padrão. Para obter mais informações, consulte [Formulário de Perfil Rápido de Tabela Única &#40;Tarefa Criação de Perfil de Dados&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md).  
  
 [Página de Solicitações de perfil](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md)  
 Na página **Solicitações de Perfil** , você especifica a fonte de dados e seleciona e configura os perfis de dados que quer computar. Para obter mais informações sobre os vários perfis que podem ser configurados, consulte os tópicos a seguir:  
  
-   [Opções da solicitação de perfil Chave de Candidato &#40;tarefa Criação de Perfil de Dados&#41;](../../integration-services/control-flow/candidate-key-profile-request-options-data-profiling-task.md)  
  
-   [Opções da solicitação de perfil Distribuição de Tamanho de Coluna &#40;Tarefa Criação de Perfil de Dados&#41;](../../integration-services/control-flow/column-length-distribution-profile-request-options-data-profiling-task.md)  
  
-   [Opções da solicitação do perfil Razão Nula de Coluna &#40;Tarefa Criação de Perfil de Dados&#41;](../../integration-services/control-flow/column-null-ratio-profile-request-options-data-profiling-task.md)  
  
-   [Opções da solicitação do perfil Padrão de Coluna &#40;Tarefa Criação de Perfil de Dados&#41;](../../integration-services/control-flow/column-pattern-profile-request-options-data-profiling-task.md)  
  
-   [Opções da solicitação do perfil Estatísticas de Coluna &#40;Tarefa Criação de Perfil de Dados&#41;](../../integration-services/control-flow/column-statistics-profile-request-options-data-profiling-task.md)  
  
-   [Opções de solicitação do perfil Distribuição de Valor de Coluna &#40;Tarefa Criação de Perfil de Dados&#41;](../../integration-services/control-flow/column-value-distribution-profile-request-options-data-profiling-task.md)  
  
-   [Opções da solicitação do perfil Dependência Funcional &#40;Tarefa Criação de Perfil de Dados&#41;](../../integration-services/control-flow/functional-dependency-profile-request-options-data-profiling-task.md)  
  
-   [Opções da solicitação do perfil Inclusão de Valor &#40;Tarefa Criação de Perfil de Dados&#41;](../../integration-services/control-flow/value-inclusion-profile-request-options-data-profiling-task.md)  
  
  
