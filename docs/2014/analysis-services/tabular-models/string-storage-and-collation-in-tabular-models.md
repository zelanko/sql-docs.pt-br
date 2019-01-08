---
title: Armazenamento de cadeia e agrupamento em modelos de tabela | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 8516f0ad-32ee-4688-a304-e705143642ca
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c9bc74d7ac6c1e3fb826e2a1b3ebdc0122fd2720
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53353772"
---
# <a name="string-storage-and-collation-in-tabular-models"></a>Ordenação e armazenamento de cadeia de caracteres em modelos tabulares
  Cadeias de caracteres (valores de texto) são armazenadas em um formato altamente compactado em modelos de tabela; por causa desta compactação, você pode obter resultados inesperados ao recuperar cadeias de caracteres inteiras ou parciais. Além disso, como a localidade e a ordenação são herdadas hierarquicamente do objeto pai mais próximo, se o idioma da cadeia de caracteres não for definido explicitamente, a localidade e a ordenação do pai poderão afetar como cada cadeia de caracteres é armazenada e se ela é exclusiva ou combinada com cadeias de caracteres semelhantes, conforme definido pela ordenação pai.  
  
 Este tópico descreve o mecanismo pelo qual cadeias de caracteres são compactadas e armazenados e também fornece exemplos de como a ordenação e o idioma afetam os resultados de fórmulas de texto em modelos de tabela.  
  
## <a name="storage"></a>Armazenamento  
 Em modelos de tabela, todos os dados são compactados para melhor ajuste na memória. Como consequência, todas as cadeias de caracteres consideradas lexicalmente equivalentes são armazenadas apenas uma vez. A primeira instância da cadeia de caracteres é usada como a representação canônica e, a partir daí, cada cadeia de caracteres equivalente é indexada com o mesmo valor compactado que a primeira ocorrência.  
  
 A pergunta-chave é: o que constitui uma cadeia de caracteres lexicalmente equivalente? Duas cadeias de caracteres serão consideradas lexicalmente equivalentes quando podem ser consideradas como a mesma palavra. Por exemplo, em inglês, quando você procura a palavra **violin** em um dicionário, pode encontrar a entrada **Violin** ou **violin**, dependendo da política editorial do dicionário, mas geralmente considera as duas palavras equivalentes e desconsidera a diferença de capitalização. Em um modelo de tabela, o fator que determina se duas cadeias de caracteres são lexicalmente equivalentes não é a política editorial e nem a preferência do usuário, mas sim a localidade e a ordem de ordenação atribuídos à coluna.  
  
 Portanto, a ordenação e a localidade determinam se letras maiúsculas e minúsculas devem ser tratadas como iguais ou diferentes. Para qualquer palavra específica dentro dessa localidade, a primeira ocorrência da palavra encontrada dentro de uma coluna específica serve como a representação canônica dessa palavra e essa cadeia de caracteres é armazenada em formato descompactado.  Todas as demais cadeias de caracteres são testadas na primeira ocorrência e, se elas corresponderem ao teste de equivalência, serão atribuídas ao valor compactado da primeira ocorrência. Posteriormente, quando os valores compactados são recuperados, eles são representados usando o valor descompactado da primeira ocorrência da cadeia de caracteres.  
  
 Um exemplo o ajudará a esclarecer como isso funciona. A coluna a seguir "Classificação - em inglês" foi extraída de uma tabela que contém informações sobre plantas e árvores. Para cada planta (os nomes das plantas não são mostrados aqui), a coluna de classificação mostra a categoria geral de planta.  
  
|Classificação - em inglês|  
|-------------------------------|  
|trEE|  
|PlAnT|  
|trEE|  
|PlAnT|  
|PlAnT|  
|trEE|  
|PlAnT|  
|trEE|  
|trEE|  
|PlAnT|  
|trEE|  
  
 Talvez os dados sejam de origens diferentes e, portanto, o uso de maiúsculas/minúsculas e acentos era inconsistente, e o banco de dados relacional armazenou essas diferenças como tal. Mas, em geral, os valores são **Plant** ou **Tree**, apenas com diferença em maiúsculas/minúsculas.  
  
 Quando estes valores são carregados em um modelo de tabela que usa a ordenação padrão e a ordem de classificação para inglês americano, maiúsculas/minúsculas não é importante; portanto, apenas dois valores seriam armazenados para a coluna inteira:  
  
|Classificação - em inglês|  
|-------------------------------|  
|trEE|  
|PlAnT|  
  
 Se você usar a coluna **classificação - em inglês**, em seu modelo, onde quer que você exiba a classificação de planta verá não os valores originais, com os vários seu uso de maiusculas e minúsculas, mas somente a primeira instância. A razão é que todas as variantes de maiúsculas e minúsculas de **tree** são consideradas equivalentes nesta ordenação e localidade; portanto, apenas uma cadeia de caracteres foi preservada e a primeira instância dessa cadeia de caracteres que é encontrada pelo sistema é salva.  
  
> [!WARNING]  
>  Você pode optar por definir a cadeia de caracteres que será a primeira a armazenar, de acordo com o que considere correto, mas isso pode ser difícil. Não existe uma maneira simples de determinar previamente a linha que deve ser processada primeiro pelo mecanismo, pois todos os valores são considerados equivalentes. Se você precisar definir o valor padrão, limpe todas as cadeias de caracteres antes de carregar o modelo.  
  
## <a name="locale-and-collation-order"></a>Localidade e ordem de ordenação  
 Ao comparar cadeias de caracteres (valores de texto), o que define a equivalência costuma ser o aspecto cultural de como cadeias de caracteres são interpretadas. Em algumas culturas, um acento ou a capitalização de um caractere pode alterar totalmente o significado da cadeia de caracteres; portanto, tais diferenças em geral são consideradas ao determinar a equivalência de qualquer idioma ou região específica.  
  
 Normalmente, quando você usa seu computador, ele já está configurado para coincidir suas próprias expectativas culturais e o comportamento linguístico; operações de cadeia de caracteres como classificar e comparar valores de texto se comportam da forma esperada. São definidas as configurações que controlam o comportamento específico a um idioma através das configurações **Localidade e Regional** no Windows. Os aplicativos leem essas configurações e alteram o comportamento de forma correspondente. Em alguns casos, um aplicativo pode ter um recurso que lhe permite alterar o comportamento cultural do aplicativo ou o modo no qual as cadeias de caracteres são comparadas.  
  
 Quando você estiver criando um banco de dados modelo de tabela, por padrão o banco de dados herdará estas configurações culturais e linguísticas na forma de um identificador de idioma e ordenação.  
  
-   O identificador de idioma define o conjunto de caracteres que você deseja usar para suas cadeias de caracteres de acordo com sua cultura.  
  
-   A ordenação define a ordenação dos caracteres e sua equivalência.  
  
 É importante observar que um identificador de idioma não só identifica um idioma, mas também o país ou região onde o idioma é usado. Cada identificador de idioma também tem uma especificação de ordenação padrão. Para obter mais informações sobre identificadores de idioma, consulte [IDs de localidade atribuídas pela Microsoft](https://msdn.microsoft.com/goglobal/bb964664.aspx). Você pode usar a coluna LCID Dec para obter a ID correta ao inserir um valor manualmente. Para obter mais informações sobre o conceito SQL de ordenações, consulte [COLLATE &amp;#40;Transact-SQL&amp;#41;](/sql/t-sql/statements/collations). Para obter mais informações sobre os designadores de ordenação e os estilos de comparação para nomes de ordenações do Windows, consulte [Nome de ordenação do Windows &amp;#40;Transact-SQL&amp;#41;](/sql/t-sql/statements/windows-collation-name-transact-sql). O tópico [Nome de ordenação do SQL Server &amp;#40;Transact-SQL&amp;#41;](/sql/t-sql/statements/sql-server-collation-name-transact-sql), mapeia os nomes de ordenação do Windows para os nomes usados para SQL.  
  
 Quando seu banco de dados modelo de tabela for criado, todos os novos objetos no modelo herdarão os atributos de idioma e ordenação do banco de dados. Isto vale para todos os objetos. O caminho de herança começa no objeto, observa o pai de quaisquer atributos de idioma e ordenação a serem herdados e, se nenhum é localizado, continua na parte superior e localiza os atributos de idioma e ordenação em nível de banco de dados. Em outras palavras, se você não especificar os atributos de idioma e ordenação para um objeto, por padrão, o objeto herdará os atributos de seu pai mais próximo.  
  
 Para colunas, os atributos de idioma e ordenação são herdados na criação, de acordo com as seguintes regras:  
  
1.  O objeto de dimensão pai é pesquisado para os atributos de idioma e ordenação. Se ambos os valores existirem, eles serão copiados nos atributos da coluna; se existir apenas um, o outro será inferido a partir de um existente e ambos serão atribuídos; se nenhum existir, passe para a próxima etapa.  
  
2.  O objeto de banco de dados que usa o mesmo processo descrito em Etapa 1 para dimensões é pesquisado; se nenhum atributo for localizado, mova à próxima etapa.  
  
3.  O objeto de servidor é pesquisado usando o mesmo processo descrito na Etapa 1 para dimensões; se nenhum atributo for localizado, a coluna usará o identificador de idioma do Windows e inferirá o atributo de ordenação desse valor.  
  
 É importante observar que normalmente o identificador de idioma e a ordem de ordenação no banco de dados de origem têm pouco ou nenhum efeito sobre a forma como valores são armazenados na coluna de modelo de tabela. A exceção será se o banco de dados de origem transformar ou filtrar os valores solicitados.  
  
  
