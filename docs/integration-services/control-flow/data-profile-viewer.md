---
title: Visualizador de Perfil de Dados | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.dataprofileviewer.f1
helpviewer_keywords:
- Data Profile Viewer [Integration Services]
- Data Profiling task [Integration Services], output viewer
ms.assetid: b9043428-ce26-45bb-910c-588d07579565
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4c4924ee6dd1c053119f7ceaf97cd1dbd4d7e95f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71294224"
---
# <a name="data-profile-viewer"></a>Visualizador de Perfil de Dados

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Exibir e analisar os perfis de dados são a próxima etapa no processo de criação de perfil de dados. Esses perfis podem ser exibidos depois que você executar a tarefa Criação de Perfil de Dados dentro de um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e computá-los. Para obter mais informações sobre como configurar e executar a tarefa Criação de Perfil de Dados, consulte [Configuração da Tarefa Criação de Perfil de Dados](../../integration-services/control-flow/setup-of-the-data-profiling-task.md).  
  
> [!IMPORTANT]  
>  O arquivo de saída pode conter dados confidenciais sobre seu banco de dados e os dados contidos no banco de dados. Para obter sugestões sobre como tornar esse arquivo mais seguro, consulte [Acesso aos arquivos usados por pacotes](../../integration-services/security/security-overview-integration-services.md#files).  
  
## <a name="data-profiles"></a>Perfis de dados  
 Para exibir os perfis, configure a tarefa Criação de Perfil de Dados para enviar a saída a um arquivo e use o Visualizador de Perfil de Dados de maneira autônoma. Para abrir o Visualizador de Perfil de Dados, execute um dos procedimentos a seguir.  
  
-   Clique com o botão direito do mouse na tarefa **Criação de Perfil de Dados** no Designer de [!INCLUDE[ssIS](../../includes/ssis-md.md)] e clique em **Editar**. Clique em **Abrir o Visualizador de Perfil** na página **Geral** de **Editor da Tarefa Criação de Perfil de Dados**.  
  
-   Na pasta *\<unidade>* :\Arquivos de Programas (x86) | Arquivos de Programas\Microsoft SQL Server\110\DTS\Binn, execute o DataProfileViewer.exe.  
  
 O visualizador usa vários painéis para exibir os perfis solicitados e os resultados computados, com detalhes e capacidade de busca opcionais:  
  
 Painel**Perfis**  
 O painel **Perfis** exibe os perfis que foram solicitados na tarefa Perfil de Dados. Para exibir os resultados computados do perfil, selecione o perfil no painel **Perfis** e os resultados serão exibidos nos outros painéis do visualizador.  
  
 Painel**Resultados**  
 O painel **Resultados** usa apenas uma linha para resumir os resultados computados do perfil. Por exemplo, ao solicitar um **Perfil de Distribuição de Comprimento de Coluna**, essa linha incluirá os dados de comprimento máximo e mínimo, além da contagem da linha. Em muitos perfis, é possível selecionar essa linha no painel **Resultados** para ver detalhes adicionais no painel **Detalhes** (opcional).  
  
 Painel**Detalhes**  
 Para muitos tipos de perfil, o painel **Detalhes** exibe informações adicionais sobre os resultados de perfil selecionados no painel **Resultados** . Por exemplo, se você solicitar um **Perfil de Distribuição de Comprimento de Coluna**, o painel **Detalhes** exibirá todos os comprimentos de coluna encontrados. O painel também exibe o número e a porcentagem de linhas nas quais o valor de coluna tem esse comprimento de coluna.  
  
 Para os três tipos de perfil que são computados em mais de uma coluna (Perfil Chave de Candidato, Dependência Funcional e Inclusão de Valor), o painel **Detalhes** exibe as violações da relação esperada. Por exemplo, se você solicitar um Perfil Chave de Candidato, o painel Detalhes exibirá valores duplicados que violam a exclusividade da chave candidata.  
  
 Se a fonte de dados usada para computar o perfil estiver disponível, você poderá clicar duas vezes em uma linha no painel **Detalhes** para ver as linhas de dados correspondentes no painel **Busca Detalhada** .  
  
 Painel**Busca Detalhada**  
 Clique duas vezes em uma linha no painel **Detalhes** para ver as linhas de dados correspondentes no painel **Busca Detalhada** quando as seguintes condições forem verdadeiras:  
  
-   A fonte de dados usada para computar o perfil está disponível.  
  
-   Você tem permissão para exibir os dados.  
  
 Para conectar ao banco de dados de origem para uma solicitação de busca detalhada, o Visualizador de Perfil de Dados usa a Autenticação do Windows e as credenciais do usuário atual. O Visualizador de Perfil de Dados não usa as informações de conexão armazenadas no pacote que executou a tarefa Criação de Perfil de Dados.  
  
> [!IMPORTANT]  
>  O recurso de busca detalhada que está disponível no Visualizador de Perfil de Dados envia consultas ao vivo à fonte de dados original. Essas consultas podem ter um impacto negativo no desempenho do servidor.  
>   
>  Se você fizer uma busca detalhada em um arquivo de saída que não foi criado recentemente, as consultas de busca detalhada poderão retornar um conjunto diferente de linhas daquelas nas quais a saída original foi calculada.  
  
 Para obter mais informações sobre a interface do usuário do Visualizador de Perfil de Dados, consulte [Ajuda de F1 do Visualizador de Perfil de Dados](../../integration-services/control-flow/data-profile-viewer-f1-help.md).  
  
## <a name="data-profile-viewer-f1-help"></a>Ajuda de F1 do Visualizador de Perfil de Dados
  Use o Visualizador de Perfil de Dados para exibir a saída da tarefa Criação de Perfil de Dados.  
  
 Para obter mais informações sobre como usar o Visualizador de Perfil de Dados, consulte [Visualizador de Perfil de Dados](../../integration-services/control-flow/data-profile-viewer.md). Para obter mais informações sobre como usar a tarefa Criação de Perfil de Dados, que cria a saída para análise no Visualizador de Perfil de Dados, consulte [Configuração da tarefa Criação de Perfil de Dados](../../integration-services/control-flow/setup-of-the-data-profiling-task.md).  
  
### <a name="static-options"></a>Opções estáticas  
 **Abrir**  
 Clique para buscar o arquivo salvo que contém a saída da tarefa Criação de Perfil de Dados.  
  
 Painel**Perfis**  
 Expanda a árvore no painel **Perfis** para ver os perfis incluídos na saída. Selecione um perfil para exibir os seus resultados.  
  
 Painel**Mensagens**  
 Exibe mensagens de estado.  
  
 Painel**Busca Detalhada**  
 Exibe as linhas de dados que correspondem a um valor na saída, se a fonte de dados usada pela tarefa Criação de Perfil de dados estiver disponível.  
  
 Por exemplo, se estiver exibindo a saída de um perfil Distribuição de Valor de Coluna para uma coluna Estado dos Estados Unidos da América, o painel **Distribuição de Valor Detalhado** pode conter uma linha para "WA". Clique duas vezes na linha do painel **Distribuição de Valor Detalhado** para ver as linhas de dados nas quais o valor da coluna de estado é “WA” no painel de busca detalhada.  
  
### <a name="dynamic-options"></a>Opções dinâmicas  
  
#### <a name="profile-type--column-length-distribution-profile"></a>Tipo de Perfil = Perfil de Distribuição de Comprimento de Coluna  
  
##### <a name="column-length-distribution-profile---column-pane"></a>Perfil de Distribuição de Tamanho de Coluna – painel \<coluna>  
 **Comprimento Mínimo**  
 Exibe o comprimento mínimo de valores nesta coluna.  
  
 **Comprimento Máximo**  
 Exibe o comprimento máximo de valores nesta coluna.  
  
 **Ignorar Espaços à Esquerda**  
 Exibe se este perfil foi calculado com um valor **IgnoreLeadingSpaces** de True ou False. Esta propriedade foi definida na página **Solicitações de Perfil** do Editor de Tarefa Criação de Perfil de Dados.  
  
 **Ignorar Espaços à Direita**  
 Exibe se este perfil foi calculado com um valor **IgnoreTrailingSpaces** de True ou False. Esta propriedade foi definida na página **Solicitações de Perfil** do Editor de Tarefa Criação de Perfil de Dados.  
  
 **Contagem de Linhas**  
 Exibe o número de linhas na tabela ou exibição.  
  
##### <a name="detailed-length-distribution-pane"></a>Painel Distribuição de Comprimento Detalhado  
 **Comprimento**  
 Exibe os comprimentos de coluna localizados na coluna perfilada.  
  
 **Count**  
 Exibe o número de linhas nas quais o valor da coluna cujo perfil está sendo criado tem o tamanho mostrado na coluna **Tamanho** .  
  
 **Percentual**  
 Exibe o percentual de linhas nas quais o valor da coluna cujo perfil está sendo criado tem o tamanho exibido na coluna **Tamanho** .  
  
#### <a name="profile-type--column-null-ratio-profile"></a>Tipo de Perfil = Perfil de Razão Nula de Coluna  
  
##### <a name="column-null-ratio-profile---column-pane"></a>Perfil de Razão Nula de Coluna – painel \<coluna>  
 **Contagem Nula**  
 Exibe o número de linhas nas quais a coluna perfilada tem um valor nulo.  
  
 **Porcentagem Nula**  
 Exibe a porcentagem de linhas nas quais a coluna cujo perfil está sendo criado tem um valor nulo  
  
 **Contagem de Linhas**  
 Exibe o número de linhas na tabela ou exibição.  
  
#### <a name="profile-type--column-pattern-profile"></a>Tipo de Perfil = Perfil Padrão de Coluna  
  
##### <a name="column-pattern-profile---column-pane"></a>Perfil de Padrão de Coluna – painel \<coluna>  
 **Contagem de Linhas**  
 Exibe o número de linhas na tabela ou exibição.  
  
##### <a name="pattern-distribution-pane"></a>Painel Distribuição de Padrão  
 **Padrão**  
 Exibe os padrões computados para a coluna cujo perfil está sendo criado.  
  
 **Percentual**  
 Exibe o percentual de linhas cujos valores correspondem ao padrão exibido na coluna **Padrão** .  
  
#### <a name="profile-type--column-statistics-profile"></a>Tipo de Perfil = Perfil de Estatísticas da Coluna  
  
##### <a name="column-statistics-profile---column-pane"></a>Perfil de Estatísticas da Coluna – painel \<coluna>  
 **Mínimo**  
 Exibe o valor mínimo localizado na coluna cujo perfil está sendo criado.  
  
 **Máximo**  
 Exibe o valor máximo localizado na coluna cujo perfil está sendo criado.  
  
 **Mean**  
 Exibe a média dos valores encontrados na coluna cujo perfil está sendo criado.  
  
 **Desvio Padrão**  
 Exibe o desvio padrão dos valores encontrados na coluna cujo perfil está sendo criado.  
  
#### <a name="profile-type--column-value-distribution-profile"></a>Tipo de Perfil = Perfil de Distribuição de Valor da Coluna  
  
##### <a name="column-value-distribution-profile---column-pane"></a>Perfil de Distribuição de Valor da Coluna – painel \<coluna>  
 **Número de Valores Distintos**  
 Exibe a contagem de valores distintos encontrados na coluna cujo perfil está sendo criado.  
  
 **Contagem de Linhas**  
 Exibe o número de linhas na tabela ou exibição.  
  
##### <a name="detailed-value-distribution-pane"></a>Painel Distribuição de Valor Detalhado  
 **Valor**  
 Exibe os valores distintos encontrados na coluna cujo perfil está sendo criado.  
  
 **Count**  
 Exibe o número de linhas nas quais a coluna cujo perfil está sendo criado tem o valor exibido na coluna **Valor** .  
  
 **Percentual**  
 Exibe o percentual de linhas nas quais a coluna cujo perfil está sendo criado tem o valor exibido na coluna **Valor** .  
  
#### <a name="profile-type--candidate-key-profile"></a>Tipo de Perfil = Perfil-Chave de Candidato  
  
##### <a name="candidate-key-profile---table-pane"></a>Perfil-Chave de Candidato – painel \<tabela>  
 **Colunas de Chave**  
 Exibe as colunas que foram selecionadas para criação de perfil como chave candidata.  
  
 **Intensidade de Chave**  
 Exibe a intensidade (em porcentagem) da coluna da chave candidata ou da combinação de colunas. Uma intensidade de chave inferior a 100% indica que existem valores em duplicata.  
  
##### <a name="key-violations-pane"></a>Painel Violações de Chave  
 **\<column1>, \<column2>, etc.**  
 Exibe os valores em duplicata encontrados na coluna cujo perfil está sendo criado.  
  
 **Count**  
 Exibe o número de linhas nas quais a coluna especificada tem o valor exibido na primeira coluna.  
  
#### <a name="profile-type--functional-dependency-profile"></a>Tipo de Perfil = Perfil de Dependência Funcional  
  
##### <a name="functional-dependency-profile-pane"></a>Painel do perfil de Dependência Funcional  
 **Colunas Determinantes**  
 Exibe a coluna ou colunas selecionadas como coluna ou colunas determinantes. No exemplo no qual o mesmo Código Postal dos Estados Unidos deveria ter sempre o mesmo estado, a coluna Código Postal é a coluna determinante.  
  
 **Colunas Dependentes**  
 Exibe a coluna ou colunas selecionadas como coluna ou colunas dependentes. No exemplo no qual o mesmo Código Postal dos Estados Unidos deveria ter sempre o mesmo estado, a coluna Estado é a coluna dependente.  
  
 **Intensidade de Dependência Funcional**  
 Exibe a intensidade (em porcentagem) da dependência funcional entre colunas. Uma intensidade de chave inferior a 100% indica que há casos nos quais o valor determinante não determina o valor dependente. No exemplo no qual o mesmo Código Postal dos Estados Unidos deveria ter sempre o mesmo estado, isso provavelmente indica que alguns valores de estado são inválidos  
  
##### <a name="functional-dependency-violations-pane"></a>Painel Violações de Dependência Funcional  
  
> [!NOTE]  
>  Uma porcentagem alta de valores errôneos nos dados poderia conduzir a resultados inesperados de um perfil Dependência Funcional. Por exemplo, 90% das linhas têm um valor de “WI” em Estado para um valor de Código Postal de "98052". O perfil informa linhas que contêm o valor de estado correto de "WA" como violações.  
  
 **\<nome de coluna determinante>**  
 Exibe o valor da coluna determinante ou combinação de colunas na instância de uma violação de dependência funcional.  
  
 **\<nome de coluna dependente>**  
 Exibe o valor da coluna dependente na instância de uma violação de dependência funcional.  
  
 **Contagem de Suporte**  
 Exibe o número de linhas nas quais o valor de coluna determinante determina a coluna dependente.  
  
 **Contagem de Violação**  
 Exibe o número de linhas nas quais o valor de coluna determinante não determina a coluna dependente (Essas são as linhas nas quais o valor dependente é o valor exibido na coluna **\<dependent column name>** .)  
  
 **Percentual de Suporte**  
 Exibe a porcentagem de linhas nas quais a coluna determinante determina a coluna dependente.  
  
#### <a name="profile-type--value-inclusion-profile"></a>Tipo de Perfil = Perfil de Inclusão de Valor  
  
##### <a name="value-inclusion-profile-pane"></a>Painel do Perfil de Inclusão de Valor  
 **Colunas Laterais de Subconjunto**  
 Exibe a coluna ou combinação de colunas cujo perfil foi criado para determinar se elas estão nas colunas do superconjunto.  
  
 **Colunas Laterais de Superconjunto**  
 Exibe a coluna ou combinação de colunas cujo perfil foi criado para determinar se elas incluem os valores nas colunas do subconjunto.  
  
 **Intensidade de Inclusão**  
 Exibe a intensidade (em porcentagem) da sobreposição entre colunas. Uma intensidade de chave inferior a 100% indica que há casos nos quais o valor do subconjunto não está localizado entre os valores do superconjunto.  
  
##### <a name="inclusion-violations-pane"></a>Painel Violações de Inclusão  
 **\<column1>, \<column2>, etc.**  
 Exibe os valores na coluna de subconjunto ou colunas que não foram localizadas na coluna ou colunas do superconjunto.  
  
 **Count**  
 Exibe o número de linhas nas quais a coluna especificada tem o valor exibido na primeira coluna.  
  
