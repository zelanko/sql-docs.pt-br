---
title: Comparar dados de cadeia de caracteres | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- comparing string data
- comparison options [Integration Services]
- locales [Integration Services]
- converting string data
- string comparisons
ms.assetid: 93aeb5bd-e208-46b7-8979-dea2dcd37d4c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8de2ce3e407de132869138a54d5a17559b6308bc
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58270703"
---
# <a name="comparing-string-data"></a>comparando dados de cadeia de caracteres
  Comparações de cadeia de caracteres são uma parte importante de muitas das transformações realizadas pelo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]e as comparações de cadeia de caracteres também são usadas na avaliação de expressões em variáveis e expressões de propriedade. Por exemplo, a transformação de Classificação compara valores em um conjunto de dados para classificar dados em ordem crescente ou decrescente.  
  
## <a name="configuring-transformations-for-string-comparisons"></a>Configurando transformações para comparações de cadeias de caracteres  
 As transformações Classificação, Agregação, Agrupamento Difuso e Pesquisa Difusa podem ser personalizadas para alterar a maneira que as cadeias de caracteres são comparadas no nível da coluna. Por exemplo, é possível especificar que uma comparação ignore caixas altas e baixas, o que significa que os caracteres maiúsculos e minúsculos são tratados da mesma forma.  
  
 As seguintes transformações usam expressões que podem incluir comparações de cadeias de caracteres.  
  
-   A transformação Divisão Condicional pode usar comparações de cadeia de caracteres em expressões para determinar para qual saída enviar a linha de dados. Para obter mais informações, consulte [Conditional Split Transformation](../../integration-services/data-flow/transformations/conditional-split-transformation.md).  
  
-   A transformação de Coluna Derivada pode usar comparações de cadeias de caracteres em expressões para gerar novos valores de coluna. Para obter mais informações, consulte [Derived Column Transformation](../../integration-services/data-flow/transformations/derived-column-transformation.md).  
  
 Variáveis, mapeamentos de variáveis e restrições de precedência também usam expressões que podem incluir comparações de cadeias de caracteres. Para obter mais informações sobre expressões, consulte [Integration Services &#40;SSIS&#41; Expressões](../../integration-services/expressions/integration-services-ssis-expressions.md).  
  
## <a name="processing-during-string-comparison"></a>Processando durante a comparação de cadeias de caracteres  
 Dependendo dos dados e da configuração da transformação, o seguinte processamento pode ocorrer durante a comparação dos dados da cadeia de caracteres:  
  
-   Convertendo dados em Unicode. Se os dados de origem ainda não forem Unicode, eles serão convertidos automaticamente para Unicode antes da comparação ocorrer.  
  
-   Usando a localidade para aplicar regras específicas de localidades para interpretar data, hora, dados decimais e ordem de classificação.  
  
-   Aplicando opções de comparação no nível de coluna para alterar a sensibilidade das comparações.  
  
## <a name="converting-string-data-to-unicode"></a>Convertendo os dados da cadeia de caracteres para Unicode  
 Dependendo das operações que a transformação realiza e a configuração da transformação, os dados da cadeia de caracteres podem ser convertidos no tipo de dados DT_WSTR, que é uma representação Unicode dos caracteres da cadeia de caracteres.  
  
 Os dados de cadeias de caracteres que têm o tipo DT_STR são convertidos em Unicode por meio do uso da página de código da coluna. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] dá suporte a páginas de código no nível de coluna, e cada coluna pode ser convertida por meio de uma página de código diferente.  
  
 Na maioria dos casos, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pode identificar a página de código correta da origem de dados. Por exemplo, no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é possível definir uma ordenação nos níveis do banco de dados e da coluna. A página de código é derivada de uma ordenação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], que pode ser uma ordenação do Windows ou do SQL.  
  
 Se o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornecer uma página de código inesperada ou se o pacote acessar uma origem de dados usando um provedor que não fornece informações suficientes para determinar a página de código correta, você poderá especificar uma página de código padrão na origem OLE DB e no destino OLE DB. As páginas de código padrão são usadas em vez das páginas de código fornecidas pelo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Os arquivos não têm páginas de código. Ao invés disso, os gerenciadores de conexões de Arquivo Simples e de Vários Arquivos Simples usados por um pacote para conectar aos dados de arquivo incluem uma propriedade para especificar a página de código do arquivo. A página de código pode ser definida apenas no nível de arquivo, não no nível da coluna.  
  
## <a name="setting-locale"></a>Configuração de localidade  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] não usa a página de código para inscrever regras específicas de localidades para classificar dados ou interpretar data, hora e dados decimais. Em vez disso, a transformação lê a localidade definida pela propriedade LocaleId no componente de fluxo de dados, tarefa de Fluxo de Dados, contêiner ou pacote. Por padrão, a localidade de uma transformação é herdada de sua tarefa de Fluxo de Dados, que, por sua vez, herda do pacote. Se a tarefa de Fluxo de Dados estiver em um contêiner como o Loop For, ela herdará sua localidade do contêiner.  
  
 Também é possível especificar uma localidade para o gerenciamento de conexões de Arquivo Simples e um gerenciador de conexões de Vários Arquivos Simples.  
  
## <a name="setting-comparison-options"></a>Definindo opções de comparação  
 A localidade fornece as regras básicas para comparar dados de cadeia de caracteres. Por exemplo, a localidade especifica a posição de classificação de cada letra no alfabeto. No entanto, essas regras podem não ser suficientes para as comparações que algumas transformações realizam e o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] oferece suporte a um conjunto de opções de comparação avançadas que vão além das regras de comparação de uma localidade. Estas opções de comparação são definidas no nível da coluna. Por exemplo, um das opções de comparação permite que você ignore caracteres de não espaçamento. O efeito dessa opção é ignorar diacríticos como o acento, que torna "a" e "á" idênticos para fins de comparação.  
  
 A seguinte tabela descreve as opções de comparação e um estilo de classificação.  
  
|Opção de comparação|Descrição|  
|-----------------------|-----------------|  
|Ignora maiúsculas e minúsculas|Especifica se a comparação faz distinção entre letras maiúsculas e minúsculas. Se esta opção for definida, a comparação de cadeia de caracteres ignorará a distinção entre letras maiúsculas e minúsculas. Por exemplo, "ABC" torna-se igual a "abc".|  
|Ignora o tipo kana|Especifica se a comparação distingue os dois tipos de caracteres de kana japoneses: hiragana e katakana. Se esta opção for definida, a comparação de cadeia de caracteres ignorará o tipo de kana usado.|  
|Ignora largura do caractere|Especifica se a comparação faz distinção entre um caractere de byte único e o mesmo caractere representado como um caractere de byte duplo. Se esta opção for definida, a comparação de cadeia de caracteres tratará representações de byte único e representações de byte duplo do mesmo caractere como idênticas.|  
|Ignora caracteres de não espaçamento|Especifica se a comparação distingue entre caracteres de espaço e sinais diacríticos. Se esta opção for definida, a comparação ignorará os sinais diacríticos. Por exemplo, "å" é igual a "a".|  
|Ignora símbolos|Especifica se a comparação faz distinção entre caracteres de letra e símbolos como caracteres de espaço em branco, pontuação, símbolos monetários e matemáticos. Se esta opção estiver definida, a comparação de cadeia de caracteres ignorará símbolos. Por exemplo, " Nova Iorque" se torna igual a "Nova Iorque" e "* ABC" é o mesmo que "ABC" '.|  
|Classificar pontuação como símbolos|Especifica se a comparação classifica todos os símbolos de pontuação, menos o hífen e o apóstrofo, antes dos caracteres alfanuméricos. Por exemplo, se esta opção for definida, ".ABC" será classificada antes de "ABC."|  
  
 As transformações Classificação, Agregar, Agrupamento Difuso e Pesquisa Difusa incluem estas opções para comparar dados.  
  
 O sinalizador de comparação **FullySensitive** é exibido na caixa de diálogo **Editor Avançado** para as transformações Agrupamento Difuso e Pesquisa Difusa. Selecionar o sinalizador de comparação **FullySensitive** significa que todas as opções de comparação se aplicam.  
  
## <a name="see-also"></a>Consulte Também  
 [Tipos de dados do Integration Services](../../integration-services/data-flow/integration-services-data-types.md)   
 [Análise rápida](https://msdn.microsoft.com/library/6688707d-3c5b-404e-aa2f-e13092ac8d95)   
 [Análise padrão](https://msdn.microsoft.com/library/dfe835b1-ea52-4e18-a23a-5188c5b6f013)  
  
  
