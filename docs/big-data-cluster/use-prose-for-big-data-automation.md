---
title: Wrangling de dados usando o Acelerador de código PROSA | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/01/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 3a247cd33a4fdf2df35359db953e8d14444ace88
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48795796"
---
# <a name="data-wrangling-using-prose-code-accelerator"></a>Wrangling de dados usando o Acelerador de código PROSA

Acelerador de código PROSA gera código legível do Python para suas tarefas de wrangling de dados. Você pode combinar o código gerado com o código escrito manualmente de uma maneira perfeita enquanto estiver trabalhando em um bloco de anotações no Studio de dados do Azure. Este artigo fornece uma visão geral de como você pode usar o Acelerador de código.

 > [!NOTE]
 > Programar Synthesis using Examples, também conhecido como PROSA, é uma tecnologia da Microsoft que gera o código legível por humanos usando inteligência Artificial. Isso é feito analisando um usuário intenção, bem como dados, gerando vários programas de release candidate e escolher o melhor programa usando algoritmos de classificação. Para saber mais sobre a tecnologia de PROSA, visite o [home page da PROSA](https://microsoft.github.io/prose/).

O Acelerador de código vem pré-instalado com o Studio de dados do Azure. Você pode importá-lo como qualquer outro pacote do Python no bloco de anotações. Por convenção, vamos importá-lo como cx de forma abreviada.

```python
import prose.codeaccelerator as cx
```

Na versão atual, o Acelerador de código de forma inteligente pode gerar código Python para as seguintes tarefas:

- Lendo arquivos de dados para um Pandas ou dataframe Pyspark.
- Corrigindo os tipos de dados em um dataframe.
- Localizando as expressões regulares que representam padrões em uma lista de cadeias de caracteres.

Para obter uma visão geral dos métodos de acelerador de código, consulte o [documentação](https://aka.ms/prose-codeaccelerator-overview).

## <a name="reading-data-from-a-file-to-a-dataframe"></a>Ler dados de um arquivo em um dataframe

Geralmente, lendo os arquivos a um dataframe envolve examinando o conteúdo do arquivo e determinar os parâmetros corretos a serem passados para uma biblioteca de carregamento de dados. Dependendo da complexidade do arquivo, identificar os parâmetros corretos pode exigir várias iterações.

Acelerador de código PROSA resolve esse problema, a estrutura do arquivo de dados de análise e geração automática de código para carregar o arquivo. Na maioria dos casos, o código gerado analisa os dados corretamente. Em alguns casos, talvez você precise ajustar o código para atender às suas necessidades.

Considere o seguinte exemplo:

 ```python
import prose.codeaccelerator as cx

# Call the ReadCsvBuilder builder to analyze the file content and generate code to load it
builder = cx.ReadCsvBuilder(r'C:/911.txt')

#Set target to pyspark if generating code to use pyspark library
#builder.Target = "pyspark"

#Get the code generated to fix the data types
builder.learn().code()
 ```

O bloco de código anterior imprime o seguinte código python para ler um arquivo delimitado. Observe como PROSA detecta automaticamente o número de linhas a ignorar, cabeçalhos, quotechars, delimitadores, etc.

 ```python
import pandas as pd

def read_file(file):
    names = ["lat",
             "lng",
             "desc",
             "zip",
             "title"]

    df = pd.read_csv(file,
        skiprows = 11,
        header = None,
        names = names,
        quotechar = "\"",
        delimiter = "|",
        index_col = False,
        dtype = str,
        na_values = [],
        keep_default_na = False,
        skipinitialspace = True)
    return df
 ```

Acelerador de código pode gerar código para carga delimitados, JSON e arquivos de largura fixa para um dataframe. Para ler arquivos de largura fixa, o `ReadFwfBuilder` , opcionalmente, usa um arquivo de esquema legível por humanos que ele pode analisar para obter as posições de coluna. Para obter mais informações, consulte o [documentação](https://aka.ms/prose-codeaccelerator-docs).

## <a name="fixing-data-types-in-a-dataframe"></a>Corrigindo os tipos de dados em um dataframe

É comum ter um pandas ou dataframe pyspark com tipos de dados errado. Muitas vezes, isso acontece por causa de alguns não em conformidade com os valores em uma coluna. Como resultado, inteiros são lidos como Float ou cadeias de caracteres e datas são lidas como cadeias de caracteres. O esforço necessário para corrigir manualmente os tipos de dados é proporcional ao número de colunas.

Você pode usar o `DetectTypesBuilder` nessas situações. Ele analisa os dados e, ao invés de corrigir os tipos de dados de uma maneira de caixa preta, ele gera código para corrigir os tipos de dados. O código funciona como um ponto de partida. Você pode examinar, usar ou modificá-lo conforme necessário.

```python
import prose.codeaccelerator as cx

builder = cx.DetectTypesBuilder(df)

#Set target to pyspark if working with pyspark
#builder.Target = "pyspark"

#Get the code generated to fix the data types
builder.learn().code()
```

Para obter mais informações, consulte o [documentação](https://aka.ms/prose-codeaccelerator-fixtypes).

## <a name="identifying-patterns-in-strings"></a>Identificação de padrões em cadeias de caracteres

Outro cenário comum é detectar padrões em uma coluna de cadeia de caracteres com a finalidade de limpeza ou de agrupamento. Por exemplo, você pode ter uma coluna de data com datas em vários formatos diferentes. Para padronizar os valores, você talvez queira escrever instruções condicionais usando expressões regulares.


|   |Nome                      |BirthDate      |
|---|:-------------------------|:--------------|
| 0 |Bertram du Plessis        |1995           |
| 1 |Naiara Moravcikova        |Unknown (desconhecido)        |
| 2 |Jihoo Spel                |2014           |
| 3 |Viachaslau Gordan Hilario |22 de abril de 67      |
| 4 |Maya de Villiers          |19 de março de 60      |

Dependendo do volume e diversidade nos dados, a escrita de expressões regulares para padrões diferentes na coluna pode ser uma tarefa muito demorada. O `FindPatternsBuilder` é uma ferramenta de aceleração de código poderoso que resolve o problema acima por meio da geração de expressões regulares para obter uma lista de cadeias de caracteres.

```python
import prose.codeaccelerator as cx

builder = cx.FindPatternsBuilder(df['BirthDate'])

#Set target to pyspark if working with pyspark
#builder.Target = "pyspark"

builder.learn().regexes
```

Aqui estão as expressões regulares geradas pelo `FindPatternsBuilder` para os dados acima.

```
^[0-9]{2}-[A-Z][a-z]+-[0-9]{2}$
^[0-9]{2}[\s][A-Z][a-z]+[\s][0-9]{4}$
^[0-9]{4}$
^Unknown$
```

Além da geração de expressões regulares, `FindPatternsBuilder` também pode gerar código para os valores com base em regexes gerado de clustering. Ele também pode afirmar que todos os valores em uma coluna em conformidade com as expressões regulares geradas. Para saber mais e ver outros cenários úteis, consulte o [documentação](https://aka.ms/prose-codeaccelerator-findpatterns).
