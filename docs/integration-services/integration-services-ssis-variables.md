---
title: Variáveis do SSIS (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 973e5e1449205d5e72abfa03068db3c8c3e98f87
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71296159"
---
# <a name="integration-services-ssis-variables"></a>Variáveis do SSIS (Integration Services)

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  As variáveis armazenam valores que um pacote [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e seus contêineres, tarefas e manipuladores de eventos podem usar em tempo de execução. Os scripts na tarefa Script e o componente de Script também podem usar variáveis. As restrições de precedência que colocam em sequência tarefas e contêineres em um fluxo de trabalho podem usar variáveis quando suas definições de restrições incluem expressões.  
  
 Você pode usar variáveis em pacotes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para as seguintes finalidades:  
  
-   Atualizar propriedades de elementos do pacote em tempo de execução. Por exemplo, você pode definir o número de executáveis simultâneos permitido por um contêiner Loop Foreach dinamicamente.  
  
-   Incluir uma tabela de pesquisa na memória. Por exemplo, um pacote pode executar uma tarefa Executar SQL que carrega uma variável com valores de dados.  
  
-   Carregar variáveis com valores de dados e usá-las para especificar um critério de pesquisa em uma cláusula WHERE. Por exemplo, o script em uma tarefa de Script pode atualizar o valor de uma variável usada por uma instrução Transact-SQL em uma tarefa Executar SQL.  
  
-   Carregar uma variável com um valor inteiro e usar o valor para controlar o loop dentro de um fluxo de controle do pacote. Por exemplo, você pode usar uma variável na expressão de avaliação de um contêiner Loop For para controlar a iteração.  
  
-   Preencher valores de parâmetro para instruções Transact-SQL em tempo de execução. Por exemplo, um pacote pode executar uma tarefa Executar SQL e usar variáveis para definir os parâmetros em uma instrução Transact-SQL dinamicamente.  
  
-   Criar expressões que incluem valores de variáveis. Por exemplo, a transformação Coluna Derivada pode popular uma coluna com o resultado obtido pela multiplicação de um valor de variável pelo valor de uma coluna.  
  
## <a name="system-and-user-defined-variables"></a>Variáveis de sistema e definidas pelo usuário  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] dá suporte a dois tipos de variáveis: variáveis definidas pelo usuário e variáveis de sistema. As variáveis definidas pelo usuário são definidas por desenvolvedores de pacote e as variáveis de sistema são definidas pelo [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Você pode criar tantas variáveis definidas pelo usuário quantas forem exigidas por um pacote, mas não pode criar variáveis de sistema adicionais.  
  
 Todas as variáveis, as do sistema e as definidas pelo usuário, podem ser usadas nas associações de parâmetro que a tarefa Executar SQL usa para mapear variáveis para parâmetros em instruções SQL. Para obter mais informações, consulte [Tarefa Executar SQL](../integration-services/control-flow/execute-sql-task.md) e [Parâmetros e códigos de retorno na Tarefa Executar SQL](https://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663).  
  
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
  
 Um conjunto diferente de variáveis de sistema está disponível para tipos de contêiner diferentes. Para obter mais informações sobre as variáveis de sistema usadas por pacotes e seus elementos, consulte [System Variables](../integration-services/system-variables.md).  
  
 Para obter mais informações sobre situações reais de uso de variáveis, consulte [Usar variáveis em pacotes](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
## <a name="properties-of-variables"></a>Propriedades de variáveis  
 Você pode configurar variáveis definidas pelo usuário configurando as seguintes propriedades na janela **Variáveis** ou na janela **Propriedades** . Determinadas propriedades só estão disponíveis na janela Propriedades.  
  
> [!NOTE]  
>  A única opção configurável em variáveis de sistema é especificar se elas geram um evento quando alteram o valor.  
  
 **Description**    
 Especifica a descrição da variável.  
  
 **EvaluateAsExpression**    
 Quando a propriedade é definida como **Verdadeira**, a expressão fornecida é usada para definir o valor da variável.  
  
 **Expressão**    
 Especifica a expressão que é atribuída à variável.  
  
 **Nome**    
 Especifica o nome da variável.  
  
 **Namespace**  
 O [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] fornece dois namespaces, **User** e **System**. Por padrão, as variáveis personalizadas ficam no namespace **Usuário** e as variáveis de sistema no namespace **System** . Você pode criar namespaces adicionais para variáveis definidas pelo usuário e alterar o nome do namespace **Usuário** , mas não pode alterar o nome do namespace **Sistema** , adicionar variáveis no namespace **Sistema** ou atribuir variáveis de sistema para um namespace diferente.  
  
**RaiseChangedEvent**  
 Quando a propriedade é definida como **True**, o evento **OnVariableValueChanged** é gerado quando o valor da variável é alterado.  
  
 **ReadOnly (somente-leitura)**  
 Quando a propriedade é definida como **False**, a variável é leitura\gravação.  
  
**Escopo**    
 > [!NOTE]  
>  Você pode alterar as configurações dessa propriedade clicando em **Mover Variável** na janela **Variáveis** .  
  
 Uma variável é criada no escopo de um pacote ou no escopo de um contêiner, tarefa ou manipulador de eventos do pacote. Como o contêiner do pacote está no topo da hierarquia de contêineres, as variáveis com escopo de pacote funcionam como variáveis globais e podem ser usadas por todos os contêineres do pacote. Da mesma maneira, as variáveis definidas no escopo de um contêiner, como o contêiner Loop For, podem ser usadas por todas as tarefas ou contêineres no contêiner Loop For.  
  
 Se um pacote executar outros pacotes usando a tarefa Executar Pacote, as variáveis definidas no escopo do pacote de chamada ou da tarefa Executar Pacote poderão se tornar disponíveis para o pacote chamado usando o tipo de configuração Variável do Pacote Pai. Para obter mais informações, consulte [Package Configurations](../integration-services/packages/package-configurations.md).  
  
**IncludeInDebugDump**  
 Indique se o valor da variável está incluído nos arquivos de despejo de depuração.  
  
 Para variáveis definidas pelo usuário e variáveis de sistema, o valor padrão para a opção **InclueInDebugDump** é **true**.  
  
 Porém, para variáveis definidas pelo usuário, o sistema redefine a opção **IncludeInDebugDump** como **false** quando as condições seguintes são cumpridas:  
  
-   Se a propriedade de variável **EvaluateAsExpression** é definida como **true**, o sistema redefine a opção **IncludeInDebugDump** como **false**.  
  
     Para incluir o texto da expressão como o valor da variável nos arquivos de despejo de depuração, defina a opção **IncludeInDebugDump** como **true**.  
  
-   Se o tipo de dados da variável for alterado para uma cadeia de caracteres, o sistema redefinirá a opção **IncludeInDebugDump** como **false**.  
  
 Quando o sistema redefine a opção **IncludeInDebugDump** como **false**, o valor selecionado pelo usuário pode ser substituído.  
  
**Value**    
O valor de uma variável definida pelo usuário pode ser literal ou uma expressão. O valor de uma variável não pode ser nulo. As variáveis têm os seguintes valores padrão:

| Tipo de dados | Valor padrão |
|---|---|
| Boolean | Falso |
| Tipos de dados numéricos e binários | 0 (zero) |
| Tipos de dados char e cadeia de caracteres | (cadeia de caracteres vazia) |
| Objeto | System.Object |
| | |

Uma variável tem opções para definir o valor da variável e o tipo de dados do valor. As duas propriedades devem ser compatíveis: por exemplo, o uso de um valor de cadeia de caracteres com um tipo de dados inteiro não é válido.  
  
 Se a variável for configurada para avaliar como uma expressão, você deve fornecer uma expressão. Em tempo de execução, a expressão é avaliada e a variável é definida para o resultado da avaliação. Por exemplo, se uma variável usar a expressão `DATEPART("month", GETDATE())` , o valor da variável será o número equivalente do mês da data atual. A expressão deve ser uma expressão válida que usa a sintaxe gramatical da expressão [!INCLUDE[ssIS](../includes/ssis-md.md)] . Quando uma expressão é usada com variáveis, ela pode usar literais e os operadores e funções que a gramática da expressão fornece, mas não pode referenciar as colunas de um fluxo de dados no pacote. O comprimento máximo de uma expressão é de 4000 caracteres. Para obter mais informações, consulte [Expressões do Integration Services &#40;SSIS&#41;](../integration-services/expressions/integration-services-ssis-expressions.md).  
  
**ValueType**    
 > [!NOTE]  
>  O valor da propriedade é exibido na coluna **Tipo de dados** na janela **Variáveis** .  
  
 Especifica o tipo de dados do valor da variável.  

## <a name="scenarios-for-using-variables"></a>Cenários para o uso de variáveis  
 As variáveis são usadas de muitos modos diferentes em pacotes [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Você provavelmente perceberá que o desenvolvimento do pacote não progride muito antes de você adicionar uma variável definida pelo usuário ao seu pacote para implementar a flexibilidade e a capacidade gerenciamento exigida por sua solução. Dependendo da situação, as variáveis do sistema também são usadas normalmente.  
  
 **Expressões de Propriedade** Use variáveis para fornecer valores nas expressões de propriedade que definem as propriedades de pacotes e objetos de pacote. Por exemplo, a expressão, `SELECT * FROM @varTableName` inclui a variável `varTableName` que atualiza a instrução SQL executada por uma tarefa Executar SQL. A expressão, `DATEPART("d", GETDATE()) == 1? @[User::varPackageFirst]:@[User::varPackageOther]`", atualiza o pacote executado pela tarefa Executar Pacote, executando o pacote especificado na variável `varPackageFirst` no primeiro dia do mês e executando o pacote especificado na variável `varPackageOther` nos outros dias. Para obter mais informações, consulte [Usar expressões de propriedade em pacotes](../integration-services/expressions/use-property-expressions-in-packages.md).  
  
 **Expressões de Fluxo de Dados** Use variáveis para fornecer valores nas expressões que as transformações Coluna Derivada e Divisão Condicional usam para preencher colunas ou direcionar as linhas de dados para diferentes saídas de transformação. Por exemplo, a expressão, `@varSalutation + LastName`, junta o valor na variável `VarSalutation` e a coluna `LastName` . A expressão, `Income < @HighIncome`, direciona as linhas de dados nas quais o valor da coluna `Income` é menor que o valor na variável `HighIncome` para uma saída. Para obter mais informações, consulte [Transformação Coluna Derivada](../integration-services/data-flow/transformations/derived-column-transformation.md), [Transformação Divisão Condicional](../integration-services/data-flow/transformations/conditional-split-transformation.md) e [Expressões do Integration Services &#40;SSIS&#41;](../integration-services/expressions/integration-services-ssis-expressions.md).  
  
 **Expressões de Restrição de Precedência** Fornece valores para usar em restrições de precedência para determinar se o executável de uma restrição executa. As expressões pode ser usadas junto com uma saída de execução (êxito, falha, conclusão) ou no lugar de uma saída de execução. Por exemplo, se a expressão, `@varMax > @varMin`, for avaliada como **true**, o executável será executado. Para obter mais informações, consulte [Adicionar expressões a restrições de precedência](https://msdn.microsoft.com/library/5574d89a-a68e-4b84-80ea-da93305e5ca1).  
  
 **Parâmetros e Códigos de Retorno** Fornecem valores para parâmetros de entrada ou armazenam os valores de parâmetros de saída e códigos de retorno. Isso é feito mapeando as variáveis para parâmetros e valores de retorno. Por exemplo, se você definir a variável `varProductId` como 23 e executar a instrução SQL, `SELECT * from Production.Product WHERE ProductID = ?`, a consulta recuperará o produto com um `ProductID` de 23. Para obter mais informações, consulte [Tarefa Executar SQL](../integration-services/control-flow/execute-sql-task.md) e [Parâmetros e códigos de retorno na Tarefa Executar SQL](https://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663).  
  
 **Expressões Loop For** Fornece valores a serem usados na inicialização, avaliação e expressões de atribuição do Loop For. Por exemplo, se a variável `varCount` for 2 e a `varMaxCount` for 10, a expressão de inicialização será `@varCount`, a expressão de avaliação será  `@varCount < @varMaxCount`e a expressão de atribuição será `@varCount =@varCount +1`e o loop será repetido 8 vezes. Para obter mais informações, consulte [Contêiner Loop For](../integration-services/control-flow/for-loop-container.md).  
  
 **Configurações de Variável do Pacote Pai** Passa valores de pacotes pai para pacotes filho. Os pacotes filho podem acessar variáveis no pacote pai usando configurações de variáveis do pacote pai. Por exemplo, se o pacote filho precisar usar a mesma data que o pacote pai, o pacote filho poderá definir uma configuração de variável de pacote pai que especifica uma variável definida pela função GETDATE no pacote pai. Para obter mais informações, consulte [Tarefa Executar Pacote](../integration-services/control-flow/execute-package-task.md) e [Configurações de pacote](../integration-services/packages/package-configurations.md).  
  
 **Tarefa Script e Componente Script** Fornece uma lista de variáveis somente leitura e de leitura/gravação à tarefa Script ou ao componente Script, atualiza as variáveis de leitura/gravação dentro do script e usa os valores atualizados dentro ou fora do script. Por exemplo, no código, `numberOfCars = CType(Dts.Variables("NumberOfCars").Value, Integer)`, a variável do script `numberOfCars` é atualizada pelo valor na variável, `NumberOfCars`. Para obter mais informações, consulte [Usando variáveis na tarefa Script](../integration-services/extending-packages-scripting/task/using-variables-in-the-script-task.md).  

## <a name="add-a-variable"></a>Adicionar uma variável  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o pacote do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] com o qual você deseja trabalhar.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  No Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] , defina o escopo da variável, seguindo uma das ações:  
  
    -   Para definir o escopo para o pacote, clique na superfície de design da guia **Fluxo de Controle** .  
  
    -   Para definir o escopo a um manipulador de eventos, selecione um executável e um manipulador de eventos na superfície de design da guia **Manipulador de Eventos** .  
  
    -   Para definir o escopo para uma tarefa ou contêiner, na superfície de design da guia **Fluxo de Controle** ou **Manipulador de Eventos** , clique na tarefa ou no contêiner.  
  
4.  No menu **SSIS** , clique em **Variáveis**. Além disso, você pode exibir a janela **Variáveis** mapeando o comando View.Variables para uma combinação de teclas de sua escolha na página **Teclado** da caixa de diálogo **Opções** .  
  
5.  Na janela **Variáveis** , clique no ícone **Adicionar Variável** . A nova variável é adicionada à lista.  
  
6.  Se desejar, clique no ícone **Opções de Grade** , selecione as colunas adicionais a serem exibidas na caixa de diálogo **Opções de Grade Variáveis** e clique em **OK**.  
  
7.  Como opção, define as propriedades de variáveis. Para obter mais informações, consulte [Definir as propriedades de uma variável definida pelo usuário](https://msdn.microsoft.com/library/f98ddbec-f668-4dba-a768-44ac3ae0536f).  
  
8.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  

### <a name="add-variable-dialog-box"></a>Caixa de diálogo Adicionar Variável
Use a caixa de diálogo **Adicionar Variável** para especificar as propriedades de uma nova variável.  
  
#### <a name="options"></a>Opções  
 **Contêiner**  
 Selecione um contêiner na lista. O contêiner define o escopo da variável. O contêiner pode ser o pacote ou um executável no pacote.  
  
 **Nome**  
 Digite o nome da variável.  
  
 **Namespace**  
 Especifique o namespace da variável. Por padrão, variáveis definidas pelo usuário estão no namespace **User** .  
  
 **Tipo de valor**  
 Selecione um tipo de dados.  
  
 **Valor**  
 Digite um valor. É necessário que o valor seja compatível com o tipo de dados especificado na opção **Tipo de valor** .  
  
 **Somente leitura**  
 Selecione para que a variável seja do tipo somente leitura.  
   
## <a name="delete-a-variable"></a>Excluir uma variável  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique com o botão direito do mouse no pacote para abri-lo.  
  
3.  No menu **SSIS** , clique em **Variáveis**. Além disso, você pode exibir a janela **Variáveis** mapeando o comando View.Variables para uma combinação de teclas de sua escolha na página **Teclado** da caixa de diálogo **Opções** .  
  
4.  Selecione a variável a ser excluída e clique em **Excluir Variável**.  
  
     Se você não vir a variável na janela Variáveis, clique em **Opções de Grade** e selecione **Mostrar variáveis de todos os escopos**.  
  
5.  Se a caixa de diálogo **Confirmar Exclusão de Variáveis** abrir, clique em **Sim** para confirmar.  
  
6.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## <a name="change-the-scope-of-a-variable"></a>Alterar o escopo de uma variável  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique com o botão direito do mouse no pacote para abri-lo.  
  
3.  No menu **SSIS** , clique em **Variáveis**. Além disso, você pode exibir a janela **Variáveis** mapeando o comando View.Variables para uma combinação de teclas de sua escolha na página **Teclado** da caixa de diálogo **Opções** .  
  
4.  Selecione a variável e clique em **Mover Variável**.  
  
     Se você não vir a variável na janela Variáveis, clique em **Opções de Grade** e selecione **Mostrar variáveis de todos os escopos**.  
  
5.  Na caixa de diálogo **Selecionar Novo Escopo** , selecione o pacote ou um contêiner, tarefa ou manipulador de eventos no pacote, para alterar o escopo variável.  
  
6.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  

## <a name="set-the-properties-of-a-user-defined-variable"></a>Definir as propriedades de uma variável definida pelo usuário
 Para definir as propriedades de uma variável definida pelo usuário no [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], você pode usar um dos seguintes recursos:  
  
-   Janela Variáveis.  
  
-   Janela Propriedades. A janela **Propriedades** lista propriedades para configurar variáveis não disponíveis na janela **Variáveis** : Description, EvaluateAsExpression, Expression, ReadOnly, ValueType e IncludeInDebugDump.  
  
> [!NOTE]  
>  O [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] também fornece um conjunto de variáveis do sistema cujas propriedades não podem ser atualizadas, com a exceção da propriedade RaiseChangedEvent.  
  
### <a name="set-expressions-on-variables"></a>Definir expressões em variáveis  
  
 Quando você usa a janela **Propriedades** para definir as expressões em uma variável definida pelo usuário:  
  
-   O valor de uma variável pode ser definido pela propriedade Value ou Expression. Por padrão, a propriedade EvaluateAsExpression está definida como **False** e o valor da variável é definido pela propriedade Value. Para usar uma expressão para definir o valor, você deve definir antes EvaluateAsExpression como **True**e fornecer uma expressão na propriedade Expression. A propriedade Value é definida automaticamente como o resultado de avaliação da expressão.  
  
-   A propriedade ValueType contém o tipo de dados do valor na propriedade Value. Quando Value é definido por uma expressão, ValueType é atualizado automaticamente para um tipo de dados compatível com o resultado da avaliação da expressão. Por exemplo, se Value contiver 0 e a propriedade ValueType contiver **Int32** e você definir Expression como GETDATE(), Value conterá a data e hora atuais e ValueType será definido como **DateTime**.  
  
-   A janela **Propriedades** para a variável fornece acesso à caixa de diálogo **Construtor de Expressões** . É possível usar essa ferramenta para criar, validar e avaliar expressões. Para obter mais informações, consulte [Construtor de Expressões](../integration-services/expressions/expression-builder.md) e [Expressões do Integration Services &#40;SSIS&#41;](../integration-services/expressions/integration-services-ssis-expressions.md).  
  
 Quando você usa a janela **Variáveis** para definir as expressões em uma variável definida pelo usuário:  
  
-   Para usar uma expressão para definir um valor de variável, primeiro confirme que o tipo de dados da variável é compatível com o resultado da avaliação da expressão e, em seguida, forneça uma expressão na coluna **Expressão** da janela **Variáveis** . A propriedade EvaluateAsExpression na janela **Propriedades** é automaticamente definida como **True**.  
  
-   Quando você atribui uma expressão a uma variável, um marcador de ícone especial é exibido ao lado da variável. Esse marcador de ícone especial também é exibido ao lado de gerenciadores de conexões e tarefas que têm expressões definidas neles.  
  
-   A janela **Variáveis** para a variável fornece acesso à caixa de diálogo **Construtor de Expressões** . É possível usar essa ferramenta para criar, validar e avaliar expressões. Para obter mais informações, consulte [Construtor de Expressões](../integration-services/expressions/expression-builder.md) e [Expressões do Integration Services &#40;SSIS&#41;](../integration-services/expressions/integration-services-ssis-expressions.md).  
  
 Na janela **Variáveis** e **Propriedades**, se você atribuir uma expressão à variável e **EvaluateAsExpression** for definido como **True**, você não poderá alterar o tipo de dados da variável.  
  
### <a name="set-the-namespace-and-name-properties"></a>Definir as propriedades Namespace e Name
  
 Os valores das propriedades **Name** e **Namespace** devem começar com uma letra de caractere alfabético, conforme definido pelo Unicode Standard 2.0 ou um sublinhado (_). Os caracteres subsequentes podem ser letras ou números conforme definido no padrão Unicode Standard 2.0 ou o sublinhado (\_).  
  
### <a name="set-variable-properties-in-the-variables-window"></a>Definir as propriedades de variáveis na janela Variáveis   
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique com o botão direito do mouse no pacote para abri-lo.  
  
3.  No menu **SSIS** , clique em **Variáveis**.  
  
     Além disso, você pode exibir a janela **Variáveis** mapeando o comando View.Variables para uma combinação de teclas de sua escolha na página **Teclado** da caixa de diálogo **Opções** .  
  
4.  Opcionalmente, na janela **Variáveis** , clique em **Opções de Grade**e selecione as colunas para serem exibidas na janela **Variáveis** e selecione os filtros para serem aplicados na lista de variáveis.  
  
5.  Selecione a variável na lista e atualize os valores nas colunas **Nome**, **Tipo de Dados**, **Valor**, **Namespace**, **Gerar Evento de Alteração**, **Descrição,** e **Expressão** .  
  
6.  Selecione a variável na lista e, em seguida, clique **Mover Variável** para alterar o escopo.  
  
7.  Para salvar o pacote atualizado, no menu **Arquivo** , clique em **Salvar Itens Selecionados**.  
  
### <a name="set-variable-properties-in-the-properties-window"></a>Definir as propriedades de variáveis na janela Propriedades  

1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique com o botão direito do mouse no pacote para abri-lo.  
  
3.  No menu **Exibir** , clique em **Janela Propriedades**.  
  
4.  No Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] , clique na guia **Explorador de Pacotes** e expanda o nó do Pacote.  
  
5.  Para modificar variáveis com escopo no pacote, expanda o nó Variáveis; caso contrário, expanda os Manipuladores de Evento ou os nós Executáveis até que localize o nó Variáveis que contém a variável que deseja modificar.  
  
6.  Clique na variável cujas propriedades você deseja modificar.  
  
7.  Na janela **Propriedades** , atualize as propriedades da variável de leitura/escrita. Algumas propriedades são de leitura/somente leitura para variáveis definidas pelo usuário.  
  
     Para obter mais informações sobre as propriedades, consulte [Integration Services &#40;SSIS&#41; Variables](../integration-services/integration-services-ssis-variables.md).  
  
8.  Para salvar o pacote atualizado, no menu **Arquivo** , clique em **Salvar Itens Selecionados**.  

## <a name="update-a-variable-dynamically-with-configurations"></a>Atualizar uma variável dinamicamente com configurações  
 Para atualizar dinamicamente as variáveis, é possível criar configurações para as variáveis, implantar as configurações com o pacote e atualizar os valores da variável no arquivo de configuração ao implantar os pacotes. Em tempo de execução, o pacote usa os valores de variável atualizados. Para obter mais informações, consulte [Criar configurações de pacote](../integration-services/packages/create-package-configurations.md).  

## <a name="related-tasks"></a>Related Tasks  
 [Usar os valores de variáveis e parâmetros em um pacote filho](../integration-services/packages/legacy-package-deployment-ssis.md#child)  
  
 [Mapear parâmetros de consulta para variáveis em um componente de fluxo de dados](../integration-services/data-flow/map-query-parameters-to-variables-in-a-data-flow-component.md)  
