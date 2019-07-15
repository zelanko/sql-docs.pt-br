---
title: Pesquisar texto com expressões regulares | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- vs.regularexpressionbuilder
helpviewer_keywords:
- regular expressions [SQL Server Management Studio]
- Query Editor [SQL Server Management Studio], regular expression searches
- searches [SQL Server Management Studio], regular expressions
ms.assetid: a057690c-d118-4159-8e4d-2ed5ccfe79d3
author: markingmyname
ms.author: maghan
manager: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fbd0a8fdf994f58894be41d340051a9bd7f1a34c
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67686694"
---
# <a name="search-text-with-regular-expressions"></a>Pesquisar texto com expressões regulares
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

As expressões regulares são notação concisa e flexível para pesquisa e substituição de padrões de texto. Um conjunto específico de expressões regulares pode ser usado no campo **Localizar** da caixa de diálogo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **Find and Replace** dialog box.  
  
## <a name="find-using-regular-expressions"></a>Localizar usando expressões regulares  
  
1.  Para habilitar o uso de expressões regulares no campo **Localizar** durante as operações **QuickFind**, **FindinFiles**, **Substituição Rápida** ou **Substituir em Arquivos**, selecione a opção **Usar** em **Opções de Localização** e escolha **Expressões regulares**.  
  
2.  O botão triangular **Lista de Referências** próximo ao campo **Localizar** torna-se disponível. Clique no botão para exibir uma lista das expressões regulares usadas frequentemente. Quando você seleciona qualquer item do Construtor de Expressões, o item é inserido na cadeia de caracteres **Localizar** .  
  
> [!NOTE]  
> Há diferenças de sintaxe entre as expressões regulares que podem ser usadas em cadeias **Localizar** e aquelas que são válidas na programação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework. Por exemplo, em **Localizar e Substituir**a notação de chaves {} é usada para expressões marcadas. Então a expressão "zo {1}" corresponde a todas as ocorrências de "zo" seguidas pela marca 1, como em "Alonzo1" e "Gonzo1". Entretanto, dentro do .NET Framework, a notação {} é usada para quantificadores. Então a expressão "zo{1}" corresponde a todas as ocorrências de "z" seguidas exatamente por um “o”, como em "zone" e não "zoo".  
  
 A tabela a seguir descreve as expressões regulares disponíveis na **Lista de Referências**.  
  
|Expression|Sintaxe|Descrição|  
|----------------|------------|-----------------|  
|Qualquer caractere|.|Faz a correspondência de qualquer caractere único menos uma quebra de linha.|  
|Zero ou mais|*|Faz a correspondência de zero ou mais ocorrências da expressão precedente, com todas as correspondentes possíveis.|  
|Um ou mais|+|Faz a correspondência de pelo menos uma ocorrência da expressão precedente.|  
|Início de linha|^|Ancora a cadeia de caracteres correspondente ao início de uma linha.|  
|Término de linha|$|Ancora a cadeia de caracteres correspondente ao fim de uma linha.|  
|Início de uma palavra|\<|Faz a correspondência apenas quando uma palavra começar neste ponto do texto.|  
|Término de palavra|>|Faz a correspondência só quando uma palavra terminar neste ponto do texto.|  
|Quebra de linha|\n|Faz a correspondência a uma quebra de linha independente de plataforma. Em uma expressão de substituição, insere uma quebra de linha.|  
|Qualquer caractere no conjunto|[]|Faz a correspondência de qualquer um dos caracteres dentro de []. Para especificar um intervalo de caracteres, relacione o caractere de início e término separado por um traço (-), como em [a-z].|  
|Qualquer caractere que não faz parte do conjunto|[^...]|Faz a correspondência de qualquer caractere que não pertence ao conjunto de caracteres depois de ^.|  
|Ou|&#124;|Faz a correspondência da expressão antes ou depois do símbolo OR (&#124;). Usada principalmente dentro de grupos. Por exemplo, banho (esponja&#124;lama) corresponde a “banho de esponja” e “banho de lama”.|  
|Escape|\|Faz a correspondência do caractere que segue a barra invertida (\\) como um literal. Isso permite que você encontre os caracteres usados em notação de expressão regular, como { e ^. Por exemplo, \\^ pesquisa pelo caractere ^.|  
|Expressão marcada|{}|Corresponde o texto marcado com a expressão anexada.|  
|Identificador do C/C++|:i|Faz a correspondência da expressão ([a-zA-Z_$][a-zA-Z0-9_$]*).|  
|Cadeia de caracteres entre aspas|:q|Faz a correspondência da expressão (("[^"]*")&#124;('[^']\*')).|  
|Espaço ou tabulação|:b|Faz a correspondência de caracteres de espaço ou de tabulação.|  
|Integer|:z|Faz a correspondência da expressão ([0-9]+).|  
  
 A lista de todas as expressões regulares válidas em operações **Localizar e Substituir** é mais longa do que pode ser exibido na **Lista de Referências**. Você também pode inserir qualquer uma das seguintes expressões regulares em uma cadeia de caracteres **Localizar** :  
  
|Expression|Sintaxe|Descrição|  
|----------------|------------|-----------------|  
|Mínimo – zero ou mais|@|Faz a correspondência de zero ou mais ocorrências da expressão precedente, correspondendo o mínimo de caracteres possível.|  
|Mínimo – um ou mais|#|Faz a correspondência de uma ou mais ocorrências da expressão precedente, correspondendo o mínimo de caracteres possível.|  
|Repetir n vezes|^n|Faz a correspondência de n ocorrências da expressão precedente. Por exemplo, [0-9]^4 corresponde a qualquer sequência de quatro dígitos.|  
|Agrupamento|()|Agrupa uma subexpressão.|  
|Enésimo texto marcado|\n|Em uma expressão **Localizar e Substituir** , indica o texto correspondente da enésima expressão marcada, em que n é um número de 1 a 9.<br /><br /> Em uma expressão **Substituir** , \0 insere o texto inteiro correspondente.|  
|Campo justificado à direita|\\(w,n)|Em uma expressão **Substituir** , justifica a enésima expressão marcada à direita em um campo de, pelo menos, *w* caracteres de largura.|  
|Campo justificado à esquerda|\\(-w,n)|Em uma expressão **Substituir** , justifica a enésima expressão marcada à esquerda em um campo de, pelo menos, *w* caracteres de largura.|  
|Evitar correspondência|~(X)|Evita a correspondência quando X é exibido em um certo ponto da expressão. Por exemplo, real~(ity) faz a correspondência de "real" em "realty" e "really", mas não "real" em "reality".|  
|Caractere alfanumérico|:a|Faz a correspondência da expressão ([a-zA-Z0-9]).|  
|Caractere alfabético|:c|Faz a correspondência da expressão ([a-zA-Z]).|  
|Dígito decimal|:d|Faz a correspondência da expressão ([0-9]).|  
|Dígito hexadecimal|:h|Faz a correspondência da expressão ([0-9a-fA-F]+).|  
|Número racional|:n|Faz a correspondência da expressão (([0-9]+.[0-9]*)&#124;([0-9]\*.[0-9]+)&#124;([0-9]+)).|  
|Cadeia de caracteres alfabéticos|:w|Faz a correspondência da expressão ([a-zA-Z]+).|  
|Escape|\e|Unicode U+001B.|  
|Sino|\g|Unicode U+0007.|  
|Backspace|\h|Unicode U+0008.|  
|Tab|\t|Faz a correspondência de um caractere de tabulação, Unicode U+0009.|  
|Caractere unicode|\x#### ou \u####|Corresponde um caractere dado por valor Unicode onde #### são dígitos hexadecimais. Você pode especificar um caractere fora do Plano Multilíngue Básico (isto é, um substituto) com o ponto de código ISO 10646 ou com dois pontos de código Unicode que dão os valores do par de substitutos.|  
  
 A tabela a seguir relaciona a sintaxe para correspondência por propriedades de caracteres Unicode padrão. A abreviação de duas letras é igual à relacionada no banco de dados de propriedades de caractere Unicode. Elas podem ser especificadas como parte de um conjunto de caracteres. Por exemplo, a expressão [:Nd:Nl:No] faz a correspondência de qualquer tipo de dígito.  
  
|Expression|Sintaxe|Descrição|  
|----------------|------------|-----------------|  
|Letra maiúscula|:Lu|Faz a correspondência de qualquer letra maiúscula. Por exemplo, Luhe faz a correspondência de "The" mas não "the".|  
|Letra minúscula|:Ll|Faz a correspondência de qualquer letra minúscula. Por exemplo, Llhe faz a correspondência de "the" mas não "The".|  
|Tipo de letra de título|:Lt|Faz a correspondência de caracteres que combinam uma letra maiúscula com uma letra minúscula, como Nj e Dz.|  
|Letra de modificador|:Lm|Faz a correspondência de letras ou pontuação, como vírgulas, acento cruzado e aspas duplas, usados para indicar modificações na letra precedente.|  
|Outra letra|:Lo|Faz a correspondência de outras letras, como a letra gótica ahsa.|  
|Dígito decimal|:Nd|Faz a correspondência de dígitos decimais como 0-9 e seus equivalentes de largura total.|  
|Dígito de letra|:Nl|Faz a correspondência de dígitos de letra como numerais romanos e o número zero ideográfico.|  
|Outro dígito|:No|Faz a correspondência de outros dígitos, como o antigo número um itálico.|  
|Pontuação de abertura|:Ps|Faz a correspondência de pontuação aberta, como parênteses e colchetes de abertura.|  
|Pontuação de fechamento|:Pe|Faz a correspondência de pontuação fechada, como parênteses e colchetes de fechamento.|  
|Pontuação de aspas iniciais|:Pi|Faz a correspondência de aspas duplas iniciais.|  
|Pontuação de aspas finais|:Pf|Faz a correspondência de aspas simples e aspas duplas finais.|  
|Pontuação de traço|:Pd|Faz a correspondência de traço.|  
|Pontuação de conector|:Pc|Faz a correspondência de marca de sublinhado.|  
|Outra pontuação|:Po|Faz a correspondência de (,), ?, ", !, @, #, %, &, *, \\, (:), (;), ' e /.|  
|Separador de espaço|:Zs|Faz a correspondência de espaços em branco.|  
|Separador de linha|:Zl|Faz a correspondência do caractere Unicode U+2028.|  
|Separador de parágrafo|:Zp|Faz a correspondência do caractere Unicode U+2029.|  
|Marca sem-espaçamento|:Mn|Faz a correspondência de marcas sem-espaçamento.|  
|Marca de combinação|:Mc|Faz a correspondência de marcas de combinação.|  
|Marca de circunscrição|:Me|Faz a correspondência de marcas de circunscrição.|  
|Símbolo matemático|:Sm|Corresponde a +, =, ~, &#124;, \< e >.|  
|Símbolo de moeda|:Sc|Faz a correspondência de $ e outros símbolos de moeda.|  
|Símbolo de modificador|:Sk|Faz a correspondência de símbolos de modificador como acento circunflexo, acento grave e acento circunflexo invertido.|  
|Outro símbolo|:So|Faz a correspondência de outros símbolos, como o sinal de protegido por direitos autorais, o sinal de parágrafo e o sinal de grau.|  
|Outro controle|:Cc|Faz a correspondência de término de linha.|  
|Outro formato|:Cf|Caractere de controle de formatação como os caracteres de controle bidirecionais.|  
|Substituto|:Cs|Faz a correspondência de uma metade de um par de substituto.|  
|Outros de uso particular|:Co|Faz a correspondência de qualquer caractere da área de uso particular.|  
|Outro não atribuído|:Cn|Faz a correspondência de caracteres que não mapeiam um caractere Unicode.|  
  
 Além das propriedades de caracteres Unicode padrão, as propriedades adicionais a seguir podem ser especificadas como parte de um conjunto de caracteres.  
  
|Expression|Sintaxe|Descrição|  
|----------------|------------|-----------------|  
|Alfa|:Al|Faz a correspondência de qualquer caractere. Por exemplo: Alhe faz a correspondência de palavras como "The", "then", e "reached".|  
|Numérico|:Nu|Faz a correspondência de qualquer número ou dígito.|  
|Pontuação|:Pu|Faz a correspondência de qualquer marca de pontuação, como?, @, ' etc.|  
|Espaço em branco|:Wh|Faz a correspondência de todos os tipos de espaço em branco, inclusive espaços de publicação e ideográficos.|  
|Bidi|:Bi|Faz a correspondência de caracteres de scripts da direita para esquerda, como árabe e hebreu.|  
|Hangul|:Ha|Faz a correspondência de Hangul coreano e Jamos combinável.|  
|Hiragana|:Hi|Faz a correspondência de caracteres de hiragana.|  
|Katakana|:Ka|Faz a correspondência de caracteres de katakana.|  
|Han/Kanji/Ideográfico|:Id|Faz a correspondência de caracteres ideográficos, como Han e Kanji.|  
  
## <a name="see-also"></a>Consulte Também  
 [Pesquisar e substituir](../../relational-databases/scripting/search-and-replace.md)   
 [Pesquisar texto com curingas](../../relational-databases/scripting/search-text-with-wildcards.md)  
