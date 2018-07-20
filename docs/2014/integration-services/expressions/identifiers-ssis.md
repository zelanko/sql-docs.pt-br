---
title: Identificadores (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- regular identifiers [Integration Services]
- variables [Integration Services], expressions
- identifiers [Integration Services]
- expressions [Integration Services], variables
- lineage identifiers
- columns [Integration Services], identifiers
- names [Integration Services]
- expressions [Integration Services], identifiers
- qualified identifiers [Integration Services]
ms.assetid: 56af984d-88b4-4db8-b6a2-6b07315a699e
caps.latest.revision: 44
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 322a91c77eaac5433cada0cfef056e1688020dc6
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39083998"
---
# <a name="identifiers-ssis"></a>Identificadores (SSIS)
  Em expressões, identificadores são colunas e variáveis, que estão disponíveis para a operação. Expressões podem usar identificadores regulares e qualificados.  
  
## <a name="regular-identifiers"></a>Identificadores regulares  
 Um identificador regular é um identificador que não precisa de nenhum qualificador adicional. Por exemplo, **MiddleName**, uma coluna na tabela **Contatos** do banco de dados **AdventureWorks** , é um identificador regular.  
  
 A nomeação de identificadores regulares deve seguir estas regras:  
  
-   O primeiro caractere do nome deve ser uma letra como definido pelo Unicode Standard 2.0, ou um caractere de sublinhado (_).  
  
-   Os caracteres subsequentes podem ser letras ou números conforme definido no Unicode Standard 2.0, o sublinhado (_), \@, $ e caracteres #.  
  
> [!IMPORTANT]  
>  Espaços inseridos e caracteres especiais, diferentes daqueles listados, não são válidos em identificadores regulares. Para usar espaços e caracteres especiais, você deve usar um identificador qualificado em vez de um identificador regular.  
  
## <a name="qualified-identifiers"></a>Identificadores qualificados  
 Um identificador qualificado é um identificador que é delimitado por parênteses. Um identificador pode exigir um delimitador porque o nome do identificador inclui espaços ou porque o nome do identificador não começa com uma letra ou o caractere de sublinhado. Por exemplo, o nome da coluna **Middle Name** deve ser qualificado por colchetes e escrito desta forma [Middle Name] em uma expressão.  
  
 Se o nome do identificador incluir espaços ou se o nome não for um nome de identificador regular válido, o identificador deverá ser qualificado. O avaliador de expressão usa os colchetes de abertura e fechando ([]) para qualificar identificadores. Os colchetes são colocados na primeira e na última posição da cadeia de caracteres. Por exemplo, o identificador 5$> se torna [5$>]. Podem ser usados colchetes com nomes de coluna, nomes de variável e nomes de função.  
  
 Se você construir expressões que usam as caixas de diálogo [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, identificadores regulares serão automaticamente colocados entre colchetes. Porém, os colchetes só serão exigidos se o nome incluir caracteres inválidos. Por exemplo, a coluna chamada **MiddleName** é válida sem colchetes.  
  
 Você não pode fazer referência a nomes de coluna que incluem colchetes em expressões. Por exemplo, o nome da coluna **Column[1]** não pode ser usado em uma expressão. Para usar a coluna em uma expressão, ela deve ser renomeada para a um nome sem colchetes.  
  
## <a name="lineage-identifiers"></a>identificadores de linhagem  
 Expressões podem usar identificadores de linhagem para fazer referência a colunas. Os identificadores de linhagem são atribuídos automaticamente quando você criar o pacote pela primeira vez. Você pode exibir o identificador de linhagem para uma coluna na guia **Propriedades da Coluna** da caixa de diálogo **Editor Avançado** no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer.  
  
 Se você recorrer a uma coluna utilizando seu identificador de linhagem, o identificador deverá incluir o prefixo de caractere libra (#). Por exemplo, uma coluna com o identificador de linhagem 147 deve ser referenciado como #147.  
  
 Se uma expressão for analisada com sucesso, o avaliador de expressão substituirá os identificadores de linhagem por nomes de coluna na caixa de diálogo.  
  
## <a name="unique-column-names"></a>Nomes de coluna exclusivos  
 Vários componentes usados em um pacote podem expor colunas com o mesmo nome. Se estas colunas forem usadas em expressões, a ambiguidade delas deve ser resolvida antes que as expressões possam ser analisadas com sucesso. O avaliador de expressão aceita a notação pontilhada por identificar a fonte da coluna. Por exemplo, duas colunas chamadas **Age** se tornam **FlatFileSource.Age** e **OLEDBSource.Age**que indicam que as fontes delas são FlatFileSource ou OLEDBSource. O analisador trata o nome totalmente qualificado como um único nome de coluna.  
  
 Nomes de componente de fonte e nomes de coluna estão separadamente qualificados. Os exemplos a seguir mostram o uso válido de colchetes em uma notação pontilhada:  
  
-   O nome do componente de origem inclui espaços.  
  
    ```  
    [MySo urce].Age  
    ```  
  
-   O primeiro caractere no nome de coluna não é válido.  
  
    ```  
    MySource.[#Age]  
    ```  
  
-   Os nomes do componente de origem e da coluna contêm caracteres inválidos.  
  
    ```  
    [MySource?].[#Age]  
    ```  
  
> [!IMPORTANT]  
>  Se ambos os elementos na notação pontilhada estiverem entre colchetes, o avaliador de expressão interpretará o par como um único identificador, não como uma combinação origem-coluna.  
  
## <a name="variables-in-expressions"></a>Variáveis em expressões  
 Variáveis, quando referenciadas em expressões, devem incluir o \@ prefixo. Por exemplo, o **contador** variável é referenciada usando \@contador. O \@ caractere não é parte do nome da variável; só identifica a variável para o avaliador de expressão. Se você construir expressões usando a caixa de diálogo caixas que [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer fornece, o \@ caractere é adicionado automaticamente ao nome da variável. Não é válido para incluir espaços entre o \@ caractere e o nome da variável.  
  
 Nomes de variável seguem as mesmas regras que esses para outros identificadores regulares:  
  
-   O primeiro caractere do nome deve ser uma letra como definido pelo Unicode Standard 2.0, ou um caractere de sublinhado (_).  
  
-   Os caracteres subsequentes podem ser letras ou números conforme definido no Unicode Standard 2.0, o sublinhado (_), \@, $ e caracteres #.  
  
 Se um nome de variável contiver caracteres diferente daqueles listados, a variável deverá ser colocada entre colchetes. Por exemplo, os nomes de variável com espaços devem ser colocados entre colchetes. O colchete de abertura segue o \@ caractere. Por exemplo, o **My Name** variável é referenciada como \@[My Name]. Ele não é válido para incluir espaços entre o nome de variável e os colchetes.  
  
> [!NOTE]  
>  Os nomes das variáveis do sistema e das variáveis definidas pelo usuário diferenciam maiúsculas de minúsculas.  
  
## <a name="unique-variable-names"></a>Nomes de variável exclusivos  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] aceita variáveis personalizadas e fornece um conjunto de variáveis de sistema. Por padrão, as variáveis personalizadas pertencem ao namespace **User** e as variáveis do sistema pertencem ao namespace **System** . Você pode criar namespaces adicionais para variáveis personalizadas e atualizar os nomes de namespace para se adequar às necessidades de seu aplicativo. O construtor de expressão lista variáveis em escopo em todos os namespaces.  
  
 Todas as variáveis têm escopo e pertencem a um namespace. Uma variável tem o escopo do pacote ou o escopo de um contêiner ou uma tarefa no pacote. O construtor de expressão no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer lista só as variáveis em escopo. Para obter mais informações, consulte [Variáveis do Integration Services &#40;SSIS&#41;](../integration-services-ssis-variables.md) e [Usar variáveis em pacotes](../use-variables-in-packages.md).  
  
 Variáveis usadas em expressões devem ter nomes exclusivos para o avaliador de expressão avaliar a expressão corretamente. Se um pacote usar várias variáveis com o mesmo nome, seus namespaces deverão ser diferentes. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece um operador de resolução de namespace, que consiste em dois dois-pontos (::), para qualificar uma variável com seu namespace. Por exemplo, a expressão a seguir usa duas variáveis denominadas **Count**; uma que pertence ao namespace **User** e uma que pertence ao namespace **MyNamespace** .  
  
```  
@[User::Count] > @[MyNamespace::Count]  
```  
  
> [!IMPORTANT]  
>  Você deve colocar entre colchetes a combinação de namespace e nome de variável qualificado para que o avaliador de expressão reconheça a variável.  
  
 Se o valor de **contagem** na **usuário** namespace for 10 e o valor de **contagem** na **MyNamespace** é 2, a expressão será avaliada como `true` porque o avaliador de expressão reconhece duas variáveis diferentes.  
  
 Se os nomes de variável não forem exclusivos, nenhum erro acontecerá. Em vez disso, o avaliador de expressão utiliza somente uma instância e retorna um resultado incorreto. Por exemplo, a expressão a seguir pretendia comparar os valores (10 e 2) para dois separado **contagem** variáveis, mas a expressão é avaliada como `false` porque o avaliador de expressão usa a mesma instância das  **Contagem de** variável duas vezes.  
  
```  
@Count > @Count  
```  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Artigo técnico, [SSIS Expression Cheat Sheet](http://go.microsoft.com/fwlink/?LinkId=217683), em pragmaticworks.com  
  
  
