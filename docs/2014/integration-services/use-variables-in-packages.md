---
title: Usar variáveis em pacotes | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- user-defined variables [Integration Services]
- variables [Integration Services], use scenarios
- system variables [Integration Services]
ms.assetid: 7742e92d-46c5-4cc4-b9a3-45b688ddb787
author: janinezhang
ms.author: janinez
ms.openlocfilehash: ddf6086306d24c4f92dfef2b9f4522dc2002733f
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972586"
---
# <a name="use-variables-in-packages"></a>Usar variáveis em pacotes
  Variáveis são adições úteis e flexíveis aos pacotes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ; elas podem fornecer comunicação entre objetos no pacote e entre pacotes pai e filho. As variáveis também podem ser usadas em expressões e scripts.  
  
## <a name="user-defined-variables-and-system-variables"></a>Variáveis definidas pelo usuário e pelo sistema  
 O [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] oferece variáveis de sistema e suporta variáveis definidas pelo usuário. Ao criar um novo pacote, adicione um contêiner ou uma tarefa a um pacote ou crie um manipulador de eventos, o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] inclui um conjunto de variáveis do sistema para o contêiner. Variáveis do sistema contêm informações úteis sobre um pacote, contêiner, tarefa ou manipulador de eventos. Por exemplo, no tempo de execução a variável do sistema **Nome do computador** contém o nome do computador no qual o pacote está sendo executado e **Hora Inicial** a hora que a execução do pacote começou. As variáveis de sistema são somente leitura. Para obter mais informações, consulte [Variáveis de sistema](system-variables.md).  
  
 É possível criar variáveis definidas pelo usuário e usá-las em pacotes. Variáveis definidas pelo usuário podem ser usadas de diversas formas no [!INCLUDE[ssIS](../includes/ssis-md.md)]: em scripts; nas expressões usadas pelas restrições de precedência, no contêiner Loop For, na transformação Coluna Derivada e na transformação Divisão Condicional; e nas expressões de propriedade que atualizam os valores da propriedade.  
  
 Por exemplo, é possível usar uma variável definida pelo usuário na condição de avaliação para o contêiner Loop For. Também é possível mapear o valor de coleção do enumerador em um contêiner Loop Foreach para uma variável, e se uma tarefa Executar SQL usar uma instrução SQL com parâmetro, você poderá mapear os parâmetros para a instrução para variáveis. Para obter mais informações, consulte [Variáveis do SSIS &#40;Integration Services&#41;](integration-services-ssis-variables.md).  
  
## <a name="variables-usage-scenarios"></a>Cenários de uso de variáveis  
 As variáveis são usadas de muitos modos diferentes em pacotes [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Você provavelmente perceberá que o desenvolvimento do pacote não progride muito antes de você adicionar uma variável definida pelo usuário ao seu pacote para implementar a flexibilidade e a capacidade gerenciamento exigida por sua solução. Dependendo da situação, as variáveis do sistema também são usadas normalmente.  
  
 **Expressões de Propriedade** Use variáveis para fornecer valores nas expressões de propriedade que definem as propriedades de pacotes e objetos de pacote. Por exemplo, a expressão, `SELECT * FROM @varTableName` inclui a variável `varTableName` que atualiza a instrução SQL executada por uma tarefa Executar SQL. A expressão, `DATEPART("d", GETDATE()) == 1? @[User::varPackageFirst]:@[User::varPackageOther]`", atualiza o pacote executado pela tarefa Executar Pacote, executando o pacote especificado na variável `varPackageFirst` no primeiro dia do mês e executando o pacote especificado na variável `varPackageOther` nos outros dias. Para obter mais informações, consulte [Usar expressões de propriedade em pacotes](expressions/use-property-expressions-in-packages.md).  
  
 **Expressões de Fluxo de Dados** Use variáveis para fornecer valores nas expressões que as transformações Coluna Derivada e Divisão Condicional usam para preencher colunas ou direcionar as linhas de dados para diferentes saídas de transformação. Por exemplo, a expressão, `@varSalutation + LastName`, junta o valor na variável `VarSalutation` e a coluna `LastName` . A expressão, `Income < @HighIncome`, direciona as linhas de dados nas quais o valor da coluna `Income` é menor que o valor na variável `HighIncome` para uma saída. Para obter mais informações, consulte [Transformação Coluna Derivada](data-flow/transformations/derived-column-transformation.md), [Transformação Divisão Condicional](data-flow/transformations/conditional-split-transformation.md) e [Expressões do Integration Services &#40;SSIS&#41;](expressions/integration-services-ssis-expressions.md).  
  
 **Expressões de Restrição de Precedência** Fornece valores para usar em restrições de precedência para determinar se o executável de uma restrição executa. As expressões pode ser usadas junto com uma saída de execução (êxito, falha, conclusão) ou no lugar de uma saída de execução. Por exemplo, se a expressão, `@varMax > @varMin`, avaliar para `true`, o executável será executado. Para obter mais informações, consulte [Adicionar expressões a restrições de precedência](control-flow/precedence-constraints.md).  
  
 **Parâmetros e Códigos de Retorno** Fornecem valores para parâmetros de entrada ou armazenam os valores de parâmetros de saída e códigos de retorno. Isso é feito mapeando as variáveis para parâmetros e valores de retorno. Por exemplo, se você definir a variável `varProductId` como 23 e executar a instrução SQL, `SELECT * from Production.Product WHERE ProductID = ?`, a consulta recuperará o produto com um `ProductID` de 23. Para obter mais informações, consulte [Tarefa Executar SQL](control-flow/execute-sql-task.md) e [Parâmetros e códigos de retorno na Tarefa Executar SQL](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md).  
  
 **Expressões Loop For** Fornece valores a serem usados na inicialização, avaliação e expressões de atribuição do Loop For. Por exemplo, se a variável `varCount` for 2 e a `varMaxCount` for 10, a expressão de inicialização será `@varCount`, a expressão de avaliação será  `@varCount < @varMaxCount`e a expressão de atribuição será `@varCount =@varCount +1`e o loop será repetido 8 vezes. Para obter mais informações, consulte [Contêiner Loop For](control-flow/for-loop-container.md).  
  
 **Configurações de Variável do Pacote Pai** Passa valores de pacotes pai para pacotes filho. Os pacotes filho podem acessar variáveis no pacote pai usando configurações de variáveis do pacote pai. Por exemplo, se o pacote filho precisar usar a mesma data que o pacote pai, o pacote filho poderá definir uma configuração de variável de pacote pai que especifica uma variável definida pela função GETDATE no pacote pai. Para obter mais informações, consulte [Tarefa Executar Pacote](control-flow/execute-package-task.md) e [Configurações de pacote](../../2014/integration-services/package-configurations.md).  
  
 **Tarefa Script e Componente Script** Fornece uma lista de variáveis somente leitura e de leitura/gravação à tarefa Script ou ao componente Script, atualiza as variáveis de leitura/gravação dentro do script e usa os valores atualizados dentro ou fora do script. Por exemplo, no código, `numberOfCars = CType(Dts.Variables("NumberOfCars").Value, Integer)`, a variável do script `numberOfCars` é atualizada pelo valor na variável, `NumberOfCars`. Para obter mais informações, consulte [Usando variáveis na tarefa Script](control-flow/script-task.md).  
  
## <a name="configurations-and-variables"></a>Configurações e Variáveis  
 Para atualizar dinamicamente as variáveis, é possível criar configurações para as variáveis, implantar as configurações com o pacote e atualizar os valores da variável no arquivo de configuração ao implantar os pacotes. Em tempo de execução, o pacote usa os valores de variável atualizados. Para obter mais informações, consulte [Criar configurações de pacote](../../2014/integration-services/create-package-configurations.md).  
  
### <a name="to-add-modify-and-delete-user-defined-variables"></a>Para adicionar, modificar e excluir variáveis definidas pelo usuário  
  
-   [Adicionar, excluir, alterar o escopo de uma variável definida pelo usuário em um pacote](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)  
  
-   [Definir as propriedades de uma variável definida pelo usuário](../../2014/integration-services/set-the-properties-of-a-user-defined-variable.md)  
  
  
