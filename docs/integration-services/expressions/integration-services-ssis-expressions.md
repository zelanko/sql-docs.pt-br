---
title: Expressões do SSIS (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], expressions
- Integration Services packages, expressions
- SQL Server Integration Services packages, expressions
- expressions [Integration Services], packages
- SSIS packages, expressions
ms.assetid: 26d2e242-7f60-4fa9-a70d-548a80eee667
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 60789eddd79f591996d6b1b4b18b36320f7813f6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68080722"
---
# <a name="integration-services-ssis-expressions"></a>Expressões do SSIS (Integration Services)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Uma expressão é uma combinação de símbolos (identificadores, literais, funções e operadores) gera um único valor de dados. Expressões simples podem ser uma única constante, variável ou função. Na maioria das vezes, as expressões são complexas, usando diversos operadores e funções e consultando diversas colunas e variáveis. No [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], as expressões podem ser usadas para definir condições para instruções CASE, criar e atualizar valores em colunas de dados, atribuir valores às variáveis, atualizar ou preencher propriedades em tempo de execução, definir restrições em restrições de precedência e fornecem as expressões usadas pelo contêiner Loop For.  
  
 As expressões têm base em uma linguagem de expressão e no avaliador de expressão. O avaliador de expressão analisa a expressão e determina se ela segue as regras da linguagem de expressão. Para obter mais informações sobre a sintaxe de expressão e os literais e identificadores com suporte, consulte os tópicos a seguir.  
  
-   [Sintaxe &#40;SSIS&#41;](../../integration-services/expressions/syntax-ssis.md)  
  
-   [Literais &#40;SSIS&#41;](../../integration-services/expressions/numeric-string-and-boolean-literals.md)  
  
-   [Identificadores &#40;SSIS&#41;](../../integration-services/expressions/identifiers-ssis.md)  
  
## <a name="components-that-use-expressions"></a>Componentes que usam expressões  
 Os seguintes elementos no [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] podem usar expressões:  
  
-   A transformação de Divisão Condicional implementa uma estrutura de decisão com base em expressões para direcionar linhas de dados a destinos diferentes. As expressões usadas em uma transformação de Divisão Condicional devem avaliar para **true** ou **false**. Por exemplo, linhas que atendem a condição na expressão " Column1 > Column2" podem ser direcionadas para uma saída diferente.  
  
-   A transformação Coluna Derivada usa valores criados usando expressões para preencher novas colunas em um fluxo de dados ou atualizar colunas existentes. Por exemplo, a expressão Column1 + "ABC" pode ser usada para atualizar um valor ou criar um novo valor com a cadeia de caracteres concatenada.  
  
-   Variáveis usam uma expressão para definir seu valor. Por exemplo, GETDATE() define o valor da variável como a data atual.  
  
-   As restrições de precedência podem usar expressões para especificar as condições que determinam se a tarefa ou contêiner restrito em um pacote é executado. Expressões usadas em uma restrição de precedência devem avaliar para **true** ou **false**. Por exemplo, a expressão \@A > \@B compara duas variáveis definidas pelo usuário para determinar se a tarefa restrita é executada.  
  
-   O contêiner Loop For pode usar expressões para construir a inicialização, avaliação e instruções de incremento usadas pela estrutura de looping. Por exemplo, a expressão \@Counter = 1 inicializa o contador de loop.  
  
 As expressões também podem ser usadas para atualizar os valores de propriedades de pacotes, contêineres como Loop For e Loop Foreach, tarefas, gerenciadores de conexões no nível de pacote e projeto, provedores de log e enumeradores Foreach. Por exemplo, ao usar uma expressão de propriedade, a cadeia de caracteres “Localhost.AdventureWorks” pode ser atribuída à propriedade ConnectionName da tarefa Executar SQL. Para obter mais informações, consulte [Usar expressões de propriedade em pacotes](../../integration-services/expressions/use-property-expressions-in-packages.md).  
  
## <a name="icon-markers-for-expressions"></a>Marcadores de ícone para expressões  
 No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], um marcador de ícone especial é exibido ao lado de gerenciadores de conexões, variáveis e tarefas com expressões definidas. A propriedade **HasExpressions** está disponível em todos os objetos SSIS que dão suporte a expressões, com a exceção de variáveis. A propriedade permite que você identifique facilmente quais objetos têm expressões.  
  
## <a name="expression-builder"></a>Construtor de Expressões  
 O construtor de expressões é uma ferramenta gráfica para criação de expressões. Está disponível nas caixas de diálogo **Editor de Transformação de Divisão Condicional**, **Editor de Transformação de Colunas Derivadas** e na caixa de diálogo **Construtor de Expressões** , é uma ferramenta gráfica para construir expressões.  
  
 O construtor de expressões fornece pastas que contêm elementos específicos do pacote e pastas que contêm funções, conversões de tipo e operadores fornecidos pela linguagem de expressão. Os elementos específicos do pacote incluem variáveis de sistema e variáveis definidas pelo usuário. Nas caixas de diálogo **Editor de Transformação de Divisão Condicional** e **Editor de Transformação de Coluna Derivada** , você também pode exibir colunas de dados. Para construir expressões para as transformações, é possível arrastar itens das pastas para a coluna **Condição** ou **Expressão** ou pode digitar a expressão diretamente na coluna. O construtor de expressão soma elementos de sintaxe necessários automaticamente como o prefixo \@ em nomes de variável.  
  
> [!NOTE]  
>  Os nomes das variáveis do sistema e das variáveis definidas pelo usuário diferenciam maiúsculas de minúsculas.  
  
 As variáveis possuem escopo e a pasta **Variáveis** no construtor de expressão lista apenas as variáveis que estão no escopo e disponíveis para uso. Para obter mais informações, consulte [Variáveis do SSIS &#40;Integration Services&#41;](../../integration-services/integration-services-ssis-variables.md).  
  
## <a name="related-tasks"></a>Related Tasks  
 [Usar uma expressão em um componente de fluxo de dados](https://msdn.microsoft.com/library/9181b998-d24a-41fb-bb3c-14eee34f910d)  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Artigo técnico, [Exemplos de expressões SSIS](https://go.microsoft.com/fwlink/?LinkId=220761), em social.technet.microsoft.com  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
  
  
