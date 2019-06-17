---
title: Variáveis do SSIS (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- variables [Integration Services], passing between packages
- user-defined variables [Integration Services]
- scope [Integration Services]
- system variables [Integration Services]
- variables [Integration Services]
- variables [Integration Services], about variables
- values [Integration Services]
ms.assetid: c1e81ad6-628b-46d4-9b09-d2866517b6ca
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b824129d1687dce8471800f79d106328b9ee36f6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62892263"
---
# <a name="integration-services-ssis-variables"></a>Variáveis do SSIS (Integration Services)
  As variáveis armazenam valores que um pacote do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e seus contêineres, tarefas e manipuladores de eventos podem usar em tempo de execução. Os scripts na tarefa Script e o componente de Script também podem usar variáveis. As restrições de precedência que colocam em sequência tarefas e contêineres em um fluxo de trabalho podem usar variáveis quando suas definições de restrições incluem expressões.  
  
 Você pode usar variáveis em pacotes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para as seguintes finalidades:  
  
-   Atualizar propriedades de elementos do pacote em tempo de execução. Por exemplo, você pode definir o número de executáveis simultâneos permitido por um contêiner Loop Foreach dinamicamente.  
  
-   Incluir uma tabela de pesquisa na memória. Por exemplo, um pacote pode executar uma tarefa Executar SQL que carrega uma variável com valores de dados.  
  
-   Carregar variáveis com valores de dados e usá-las para especificar um critério de pesquisa em uma cláusula WHERE. Por exemplo, o script em uma tarefa de Script pode atualizar o valor de uma variável usada por uma instrução Transact-SQL em uma tarefa Executar SQL.  
  
-   Carregar uma variável com um valor inteiro e usar o valor para controlar o loop dentro de um fluxo de controle do pacote. Por exemplo, você pode usar uma variável na expressão de avaliação de um contêiner Loop For para controlar a iteração.  
  
-   Preencher valores de parâmetro para instruções Transact-SQL em tempo de execução. Por exemplo, um pacote pode executar uma tarefa Executar SQL e usar variáveis para definir os parâmetros em uma instrução Transact-SQL dinamicamente.  
  
-   Criar expressões que incluem valores de variáveis. Por exemplo, a transformação Coluna Derivada pode popular uma coluna com o resultado obtido pela multiplicação de um valor de variável pelo valor de uma coluna.  
  
## <a name="system-and-user-defined-variables"></a>Variáveis de sistema e definidas pelo usuário  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] dá suporte a dois tipos de variáveis: variáveis definidas pelo usuário e variáveis de sistema. As variáveis definidas pelo usuário são definidas por desenvolvedores de pacote e as variáveis de sistema são definidas pelo [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Você pode criar tantas variáveis definidas pelo usuário quantas forem exigidas por um pacote, mas não pode criar variáveis de sistema adicionais.  
  
 Todas as variáveis, as do sistema e as definidas pelo usuário, podem ser usadas nas associações de parâmetro que a tarefa Executar SQL usa para mapear variáveis para parâmetros em instruções SQL. Para obter mais informações, consulte [Tarefa Executar SQL](control-flow/execute-sql-task.md) e [Parâmetros e códigos de retorno na Tarefa Executar SQL](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md).  
  
> [!NOTE]  
>  Os nomes das variáveis de sistema e das variáveis definidas pelo usuário diferenciam maiúsculas de minúsculas.  
  
 Você pode criar variáveis definidas pelo usuário para todos os tipos de contêineres do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] : pacotes, contêineres Loop Foreach, contêineres Loop For, contêineres de Sequência, tarefas e manipuladores de eventos. Variáveis definidas pelo usuário são membros da coleção de Variáveis do contêiner.  
  
 Se você cria o pacote usando o Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] , pode ver os membros das coleções de Variáveis nas pastas **Variáveis** da guia **Explorador de Pacotes** do Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] . As pastas relacionam variáveis definidas pelo usuário e variáveis de sistema.  
  
 Você pode configurar variáveis definidas pelo usuário dos seguintes modos:  
  
-   Forneça um nome e uma descrição para a variável.  
  
-   Especifique um namespace para a variável.  
  
-   Indique se a variável gera um evento quando seu valor é alterado.  
  
-   Indique se a variável é somente leitura ou leitura/gravação.  
  
-   Use o resultado da avaliação de uma expressão para definir o valor da variável.  
  
-   Crie a variável no escopo do pacote ou de um objeto de pacote como uma tarefa.  
  
-   Especifique o valor e o tipo de dados da variável.  
  
 A única opção configurável em variáveis de sistema é especificar se elas geram um evento quando alteram o valor.  
  
 Um conjunto diferente de variáveis de sistema está disponível para tipos de contêiner diferentes. Para obter mais informações sobre as variáveis de sistema usadas por pacotes e seus elementos, consulte [System Variables](system-variables.md).  
  
 Para obter mais informações sobre situações reais de uso de variáveis, consulte [Usar variáveis em pacotes](../../2014/integration-services/use-variables-in-packages.md).  
  
## <a name="variable-properties"></a>Propriedades variáveis  
 Você pode configurar variáveis definidas pelo usuário configurando as seguintes propriedades na janela **Variáveis** ou na janela **Propriedades** . Determinadas propriedades só estão disponíveis na janela Propriedades.  
  
> [!NOTE]  
>  A única opção configurável em variáveis de sistema é especificar se elas geram um evento quando alteram o valor.  
  
 Descrição  
 Especifica a descrição da variável.  
  
 EvaluateAsExpression  
 Quando a propriedade é definida como `True`, a expressão fornecida é usada para definir o valor da variável.  
  
 Expression  
 Especifica a expressão que é atribuída à variável.  
  
 Nome  
 Especifica o nome da variável.  
  
 Namespace  
 O [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] fornece dois namespaces, **User** e **System**. Por padrão, as variáveis personalizadas ficam no namespace **Usuário** e as variáveis de sistema no namespace **System** . Você pode criar namespaces adicionais para variáveis definidas pelo usuário e alterar o nome do namespace **Usuário**, mas não pode alterar o nome do namespace **Sistema**, adicionar variáveis no namespace **Sistema** ou atribuir variáveis de sistema para um namespace diferente.  
  
 RaiseChangedEvent  
 Quando a propriedade é definida como `True`, o evento `OnVariableValueChanged` é gerado quando o valor da variável é alterado.  
  
 ReadOnly (somente-leitura)  
 Quando a propriedade é definida como `False`, a variável é leitura\gravação.  
  
 Scope  
 > [!NOTE]  
>  Você pode alterar as configurações dessa propriedade clicando em **Mover Variável** na janela **Variáveis** .  
  
 Uma variável é criada no escopo de um pacote ou no escopo de um contêiner, tarefa ou manipulador de eventos do pacote. Como o contêiner do pacote está no topo da hierarquia de contêineres, as variáveis com escopo de pacote funcionam como variáveis globais e podem ser usadas por todos os contêineres do pacote. Da mesma maneira, as variáveis definidas no escopo de um contêiner, como o contêiner Loop For, podem ser usadas por todas as tarefas ou contêineres no contêiner Loop For.  
  
 Se um pacote executar outros pacotes usando a tarefa Executar Pacote, as variáveis definidas no escopo do pacote de chamada ou da tarefa Executar Pacote poderão se tornar disponíveis para o pacote chamado usando o tipo de configuração Variável do Pacote Pai. Para obter mais informações, consulte [Package Configurations](../../2014/integration-services/package-configurations.md).  
  
 IncludeInDebugDump  
 Indique se o valor da variável está incluído nos arquivos de despejo de depuração.  
  
 Para variáveis definidas pelo usuário e variáveis do sistema, o valor padrão para o **InclueInDebugDump** opção é `true`.  
  
 No entanto, para variáveis definidas pelo usuário, o sistema redefine a **IncludeInDebugDump** opção `false` quando as seguintes condições forem atendidas:  
  
-   Se o **EvaluateAsExpression** propriedade da variável é definida como `true`, o sistema redefine a **IncludeInDebugDump** opção `false`.  
  
     Para incluir o texto da expressão como o valor da variável nos arquivos de despejo de depuração, defina as **IncludeInDebugDump** opção `true`.  
  
-   Se o tipo de dados da variável é alterado para uma cadeia de caracteres, o sistema redefine a **IncludeInDebugDump** opção `false`.  
  
 Quando o sistema redefine a **IncludeInDebugDump** opção `false`, isso poderá substituir o valor selecionado pelo usuário.  
  
 Valor  
 O valor de uma variável definida pelo usuário pode ser literal ou uma expressão. Uma variável inclui opções para definir o valor da variável e o tipo de dados do valor. As duas propriedades devem ser compatíveis: por exemplo, o uso de um valor de cadeia de caracteres com um tipo de dados inteiro não é válido.  
  
 Se a variável for configurada para avaliar como uma expressão, você deve fornecer uma expressão. Em tempo de execução, a expressão é avaliada e a variável é definida para o resultado da avaliação. Por exemplo, se uma variável usar a expressão `DATEPART("month", GETDATE())` , o valor da variável será o número equivalente do mês da data atual. A expressão deve ser uma expressão válida que usa a sintaxe gramatical da expressão [!INCLUDE[ssIS](../includes/ssis-md.md)] . Quando uma expressão é usada com variáveis, ela pode usar literais e os operadores e funções que a gramática da expressão fornece, mas não pode referenciar as colunas de um fluxo de dados no pacote. O comprimento máximo de uma expressão é de 4000 caracteres. Para obter mais informações, consulte [Expressões do Integration Services &#40;SSIS&#41;](expressions/integration-services-ssis-expressions.md).  
  
 ValueType  
 > [!NOTE]  
>  O valor da propriedade é exibido na coluna **Tipo de dados** na janela **Variáveis** .  
  
 Especifica o tipo de dados do valor da variável.  
  
## <a name="configuring-variables"></a>Configurando variáveis  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)] , consulte [Janela de Variáveis](../../2014/integration-services/variables-window.md).  
  
 Para obter mais informações sobre propriedades variáveis e sobre como definir essas propriedades programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.Variable>.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Adicionar, excluir, alterar o escopo de uma variável definida pelo usuário em um pacote](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)  
  
 [Definir as propriedades de uma variável definida pelo usuário](../../2014/integration-services/set-the-properties-of-a-user-defined-variable.md)  
  
 [Usar os valores de variáveis e parâmetros em um pacote filho](../../2014/integration-services/use-the-values-of-variables-and-parameters-in-a-child-package.md)  
  
 [Mapear parâmetros de consulta para variáveis em um componente de fluxo de dados](data-flow/map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
  
