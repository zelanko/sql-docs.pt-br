---
description: Literais boolianos, de cadeia de caracteres e numéricos
title: Literais (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 11/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- string literals
- numeric literals [Integration Services]
- Boolean literals
- expressions [Integration Services], literals
- literals [Integration Services]
- mapping literals [Integration Services]
ms.assetid: a980cd52-54ef-4b9c-b00c-e6807cf8e01f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2ae5d096a90d4e755a57842fb9fb242f7d863eee
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88477481"
---
# <a name="numeric-string-and-boolean-literals"></a>Literais boolianos, de cadeia de caracteres e numéricos

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


 Expressões podem incluir literais numérico, de cadeia de caracteres e boolianos. O avaliador de expressão aceita uma variedade de literais numéricos como inteiros, decimais e constantes de ponto flutuante. O avaliador de expressão também dá suporte a sufixos longos e flutuantes, que especificam como o avaliador de expressão trata os valores, e uma notação científica em literais numéricos.  
  
## <a name="numeric-literals"></a>Literais numéricos  
 O avaliador de expressão aceita tipos de dados numéricos integral e não integral. Também dá suporte a identificadores de linhagem (identificadores numéricos exclusivos para elementos de pacote). Identificadores de linhagem são números, mas eles não podem ser usados em operações matemáticas.  
  
 O avaliador de expressão aceita sufixos que você pode usar para indicar como o avaliador de expressão trata o literal numérico. Por exemplo, você pode indicar o inteiro 37 para ser tratado como um tipo de dados inteiro longo, escrevendo 37L ou 37l.  
  
 A tabela a seguir lista sufixos para literais numéricos.  
  
|Sufixo|Descrição|  
|------------|-----------------|  
|L ou l|Um longo literal numérico.|  
|U ou u|Um literal numérico não assinado.|  
|E ou e|O expoente em notação científica|  
  
 A tabela a seguir lista elementos de expressão numérica e suas expressões regulares.  
  
|Elemento Expression|Expressão regular|Descrição|  
|------------------------|------------------------|-----------------|  
|Dígitos expressos como D.|[0-9]|Qualquer dígito.|  
|Notação científica expressa como E.|[Ee][+-]?{D}+|Letras maiúsculas ou minúsculas e, opcionalmente + ou -, e um ou mais dígitos como definido em D.|  
|Sufixo de inteiro expresso como IS.|(([lL]?[uU]?)&#124;([uU]?[lL]?))|Opcionalmente, u e l maiúsculos ou minúsculos ou uma combinação de u e l. U ou u indica um valor sem assinatura. L ou l indica um valor longo.|  
|Sufixo flutuante expresso como FS.|([f&#124;F]&#124;[l&#124;L])|F ou l maiúsculo ou minúsculo. F ou f indica um valor flutuante (tipo de dados DT_R4). L ou l indica um valor longo (tipo de dados DT_R8).|  
|Dígito hexadecimal expresso como H.|[a-fA-F0-9]|Qualquer dígito hexadecimal.|  
  
 A tabela a seguir descreve literais numéricos válidos que usam a linguagem de expressão regular.  
  
|Expressão regular|Descrição|  
|------------------------|-----------------|  
|{D}+{IS}|Um literal numérico integral com pelo menos um dígito (D) e, opcionalmente, o sufixo longo e/ou não assinado (IS).  Exemplos: 457, 785u, 986L e 7945ul.|  
|{D}+{E}{FS}|Um literal numérico não integral com pelo menos um dígito (D), notação científica, e o sufixo flutuante ou longo.  Exemplos: 4E8l, 13e-2f e 5E+L.|  
|{D}*"."{D}+{E}?{FS}|Um literal numérico não integral com um lugar decimal, uma fração decimal com pelo menos um dígito (D), um expoente opcional (E) e um identificador flutuante ou longo (FS). Este literal numérico tem o tipo de dados DT_R4 ou DT_R8.  Exemplos: 6.45E3f, .89E-2l e 1.05E+7F.|  
|{D}+"."{D}*{E}?{FS}|Um literal numérico não integral com pelo menos um dígito significante (D), um lugar decimal, um expoente (E) e um identificador flutuante ou longo (FS). Este literal numérico tem o tipo de dados DT_R4 ou DT_R8.  Exemplos: 1.E-4f, 4.6E6L e 8.365E+2f.|  
|{D}*.{D}+|Um literal numérico não integral com precisão e escala. Tem um lugar decimal e uma fração decimal com pelo menos um dígito (D). Este literal numérico tem o tipo de dados DT_NUMERIC.  Exemplos: .9, 5.8 e 0.346.|  
|{D}+.{D}*|Um literal numérico não integral com precisão e escala. Tem pelo menos um dígito significante (D) e um lugar decimal. Este literal numérico tem o tipo de dados DT_NUMERIC.  Exemplos: 6., 0.2 e 8.0.|  
|#{D}+|Um identificador de linhagem. Consiste no caractere de libra (#) e em pelo menos um dígito (D). Exemplos: #123.|  
|0[xX]{H}+{uU}|Um literal numérico em formato hexadecimal. Inclui um zero, um x maiúsculo ou minúsculo, pelo menos um H maiúsculo, e, opcionalmente, o sufixo não assinado. Exemplos: 0xFF0A e 0X000010000U.|  
  
 Para obter mais informações sobre os tipos de dados que o avaliador de expressão usa, consulte [Tipos de Dados do Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Expressões podem incluir literais numéricos com tipos de dados diferentes. Quando o avaliador de expressão avalia estas expressões, ele converte os dados em tipos compatíveis. Para obter mais informações, consulte [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
 Porém, conversão entre alguns tipos de dados requer uma conversão explícita. O avaliador de expressão fornece o operador cast para executar as conversão de tipo de dados explícita. Para obter mais informações, consulte [Cast &#40;Expressão do SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
### <a name="mapping-numeric-literals-to-integration-services-data-types"></a>Mapeando literais numéricos para tipos de dados do Integration Services  
 O avaliador de expressão executa as seguintes conversões ao avaliar literais numérico:  
  
-   Um literal numérico integral é mapeado para um tipo de dados inteiro como se segue.  
  
    |Sufixo|Tipo de resultado|  
    |------------|-----------------|  
    |Nenhum|DT_I4|  
    |U|DT_UI4|  
    |L|DT_I8|  
    |UL|DT_UI8|  
  
    > **IMPORTANTE:** Se não houver um sufixo longo (L ou l), a avaliador de expressão mapeará os valores assinados para o tipo de dados DT_I4 e os valores não assinados para o tipo de dados DT_UI4, embora o valor cause estouro no tipo de dados.  
  
-   Um literal numérico que inclui um expoente é convertido para o tipo de dados DT_R4 ou DT_R8. Se a expressão incluir o sufixo longo, ela será convertida para DT_R8; se ela incluir o sufixo flutuante, ela será convertida para o tipo de dados DT_R4.  
  
-   Se um literal numérico não integral incluir F ou f, ele será mapeado para o tipo de dados DT_R4. Se incluir L ou l e o número for um inteiro, será mapeado para o tipo de dados DT_I8. Se for um número real, ele será mapeado para o tipo de dados DT_R8. Se incluir o sufixo longo, ele será convertido para o tipo de dados DT_R8.  
  
-   Um literal numérico não integral com precisão e escala é mapeado para o tipo de dados DT_NUMERIC.  
  
## <a name="string-literals"></a>Literais de cadeia de caracteres  
 Literais da cadeia de caracteres devem estar entre aspas. A linguagem de expressão fornece um conjunto de sequências de escape para caracteres normalmente de escape, como caracteres que não são impressos e aspas.  
  
 Um literal de cadeia de caracteres consiste em zero ou mais caracteres entre aspas. Se uma cadeia de caracteres contiver aspa, estes devem ser de escape para que a expressão seja analisada. Qualquer caractere de dois bytes, exceto \x0000, é permitido em uma cadeia de caracteres, porque o caractere \x0000 é o terminador nulo de uma cadeia de caracteres.  
  
 As cadeias de caracteres podem incluir outros caracteres que requerem uma sequência de escape. A tabela a seguir lista sequências de escape para literais de cadeia de caracteres.  
  
|Sequência de escape|Descrição|  
|---------------------|-----------------|  
|\a|Alerta|  
|\b|Backspace|  
|\f|Avanço de formulário|  
|\n|Nova linha|  
|\r|Retorno de carro|  
|\t|Guia horizontal|  
|\v|Guia vertical|  
|\\"|Aspas|  
|\\\|Barra invertida|  
|\xhhhh|Caractere Unicode em notação hexadecimal|  
  
## <a name="boolean-literals"></a>Literais boolianos  
 O avaliador de expressão aceita os literais boolianos habituais: **True** e **False**. O avaliador de expressão não faz distinção entre maiúsculas e minúsculas e qualquer combinação de letras maiúsculas e minúsculas é permitida. Por exemplo, TRUE funciona tão bem quanto True.  
  
> **OBSERVAÇÃO:** Em uma expressão, um literal booliano deve ser delimitado por espaços.  
  
  
