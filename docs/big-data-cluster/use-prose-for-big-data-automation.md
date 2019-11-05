---
title: Gerar código para tarefas de estruturação de dados
titleSuffix: Azure Data Studio
description: Este artigo descreve como usar o Acelerador de Código PROSE no Azure Data Studio para gerar automaticamente o código para tarefas comuns de estruturação de dados.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e21c172bf886695a3d424d25907a0c36e4b22f20
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67957680"
---
# <a name="data-wrangling-using-prose-code-accelerator"></a>Estruturação de dados usando o Acelerador de Código PROSE

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O Acelerador de Código PROSE gera código Python legível para suas tarefas de estruturação de dados. Você pode misturar o código gerado com seu código escrito à mão de forma direta ao trabalhar em um notebook dentro do Azure Data Studio. Este artigo fornece uma visão geral de como você pode usar o Acelerador de Código.

 > [!NOTE]
 > Program Synthesis using Examples, também conhecido como PROSE, é uma tecnologia da Microsoft que gera código legível usando o IA. Ele faz isso analisando a intenção de um usuário, bem como dados, gerando vários programas candidatos e escolhendo o melhor programa usando algoritmos de classificação. Para saber mais sobre a tecnologia PROSE, visite [home page do PROSE](https://microsoft.github.io/prose/).

O Acelerador de Código vem pré-instalado com o Azure Data Studio. Você pode importá-lo como qualquer outro pacote do Python no notebook. Por convenção, podemos importá-lo como cx, na forma reduzida.

```python
import prose.codeaccelerator as cx
```

Na versão atual, o Acelerador de Código pode gerar de forma inteligente o código Python para as seguintes tarefas:

- Ler arquivos de dados para um dataframe do Pandas ou do Pyspark.
- Corrigir tipos de dados em um dataframe.
- Localizar expressões regulares representando padrões em uma lista de cadeias de caracteres.

Para obter uma visão geral dos métodos do Acelerador de Código, confira a [documentação](https://aka.ms/prose-codeaccelerator-overview).

## <a name="reading-data-from-a-file-to-a-dataframe"></a>Ler dados de um arquivo para um dataframe

Geralmente, a leitura de arquivos para um dataframe envolve analisar o conteúdo do arquivo e determinar os parâmetros corretos a serem passados para uma biblioteca de carregamento de dados. Dependendo da complexidade do arquivo, identificar os parâmetros corretos pode exigir várias iterações.

O Acelerador de Código PROSE resolve esse problema analisando a estrutura do arquivo de dados e gerando automaticamente o código para carregar o arquivo. Na maioria dos casos, o código gerado analisa os dados corretamente. Em alguns casos, talvez seja necessário ajustar o código para atender às suas necessidades.

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

O bloco de código anterior imprime o código Python a seguir para ler um arquivo delimitado. Observe como o PROSE descobre automaticamente o número de linhas a serem ignoradas, os cabeçalhos, quotechars, delimitadores etc.

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

O Acelerador de Código pode gerar código para carregar arquivos delimitados, JSON e de largura fixa em um dataframe. Para a leitura de arquivos de largura fixa, o `ReadFwfBuilder` também usa um arquivo de esquema legível por humanos que pode ser analisado para obter as posições de coluna. Para saber mais, confira a [documentação](https://aka.ms/prose-codeaccelerator-docs).

## <a name="fixing-data-types-in-a-dataframe"></a>Corrigir tipos de dados em um dataframe

É comum ter um dataframe do Pandas ou do Pyspark com tipos de dados errados. Geralmente, isso ocorre devido a alguns valores não conformes em uma coluna. Como resultado, os inteiros são lidos como Float ou Cadeias de caracteres e as datas são lidas como cadeias de caracteres. O esforço necessário para corrigir manualmente os tipos de dados é proporcional ao número de colunas.

Você pode usar o `DetectTypesBuilder` nessas situações. Ele analisa os dados e, em vez de corrigir os tipos de dados de maneira desconhecida, ele gera código para corrigir os tipos de dados. O código serve como ponto de partida. Você pode revisá-lo, usá-lo ou modificá-lo conforme necessário.

```python
import prose.codeaccelerator as cx

builder = cx.DetectTypesBuilder(df)

#Set target to pyspark if working with pyspark
#builder.Target = "pyspark"

#Get the code generated to fix the data types
builder.learn().code()
```

Para saber mais, confira a [documentação](https://aka.ms/prose-codeaccelerator-fixtypes).

## <a name="identifying-patterns-in-strings"></a>Identificar padrões em cadeias de caracteres

Outro cenário comum é detectar padrões em uma coluna de cadeia de caracteres com a finalidade de limpar ou agrupar. Por exemplo, você pode ter uma coluna de data com datas em vários formatos diferentes. Para padronizar os valores, talvez você queira escrever instruções condicionais usando expressões regulares.


|   |Nome                      |BirthDate      |
|---|:-------------------------|:--------------|
| 0 |Bertram du Plessis        |1995           |
| 1 |Naiara Moravcikova        |Unknown (desconhecido)        |
| 2 |Jihoo Spel                |2014           |
| 3 |Viachaslau Gordan Hilario |22 de abril de 1967      |
| 4 |Maya de Villiers          |19 de março de 1960      |

Dependendo do volume e da diversidade de dados, escrever expressões regulares para padrões diferentes na coluna pode ser uma tarefa muito demorada. O `FindPatternsBuilder` é uma ferramenta de aceleração de código poderosa que resolve o problema acima, gerando expressões regulares para uma lista de cadeias de caracteres.

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

Além da geração de expressões regulares, o `FindPatternsBuilder` também pode gerar código para clusterizar os valores com base em regexes gerados. Ele também pode afirmar que todos os valores em uma coluna estão em conformidade com as expressões regulares geradas. Para saber mais e ver outros cenários úteis, confira a [documentação](https://aka.ms/prose-codeaccelerator-findpatterns).
