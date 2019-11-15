---
title: Usar funções de criação de perfil de código de R
description: Melhore o desempenho e obtenha resultados mais rápidos sobre computações de R em SQL Server usando funções de criação de perfil de R para retornar informações sobre chamadas de função internas.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/12/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e03ae1a8c4cdab87f46f63da6271886b4518b5e3
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715011"
---
# <a name="use-r-code-profiling-functions-to-improve-performance"></a>Use as funções de criação de perfil de código R para melhorar o desempenho
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Além de usar recursos do SQL Server e ferramentas para monitorar a execução do script R, você pode usar ferramentas de desempenho fornecidas por outros pacotes de R para obter mais informações sobre chamadas de função internas. 

> [!TIP]
> Este artigo fornece recursos básicos para você começar. Para obter diretrizes de especialistas, recomendamos a seção *Performance (Desempenho)* no livro ["Advanced R" (R avançado), de Hadley Wickham](http://adv-r.had.co.nz).

## <a name="using-rprof"></a>Usando RPROF

[*rprof*](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/Rprof) é uma função incluída no pacote base [**utils**](https://www.rdocumentation.org/packages/utils/versions/3.5.1), que é carregado por padrão. 

Em geral, a função *rprof* funciona escrevendo a pilha de chamadas em um arquivo aos intervalos especificados. Você pode usar a função [*summaryRprof*](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/summaryRprof) para processar o arquivo de saída. Uma vantagem de *rprof* é que ele executa a amostragem, reduzindo a carga de desempenho do monitoramento.

Para usar o R de criação de perfil em seu código, você chama essa função e especifica seus parâmetros, incluindo o nome do local do arquivo de log que será gravado. A criação de perfil pode ser ativada e desativada em seu código. A sintaxe a seguir ilustra o uso básico: 

```R
# Specify profiling output file.
varOutputFile <- "C:/TEMP/run001.log")
Rprof(varOutputFile)

# Turn off profiling
Rprof(NULL)
    
# Restart profiling
Rprof(append=TRUE)
```

> [!NOTE]
> Usar essa função requer que o Windows Perl esteja instalado no computador em que o código é executado. Portanto, é recomendável criar o perfil de código durante o desenvolvimento em um ambiente de R e, em seguida, implantar o código depurado no SQL Server.  


## <a name="r-system-functions"></a>Funções do Sistema R

A linguagem R inclui muitas funções de pacote básico para retornar o conteúdo de variáveis do sistema. Por exemplo, como parte do seu código R, você pode usar `Sys.timezone` para obter o fuso horário atual ou `Sys.Time` para obter a hora do sistema de R. 

Para obter informações sobre funções individuais do sistema R, digite o nome da função como argumento para a função R `help()` em um prompt de comando de R.

```R
help("Sys.time")
```

## <a name="debugging-and-profiling-in-r"></a>Depuração e criação de perfil em R

A documentação do Microsoft R Open, que é instalado por padrão, inclui um manual sobre o desenvolvimento de extensões para a linguagem R que aborda a [criação de perfis e depuração](https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging) em detalhes. Você pode encontrar a mesma documentação em seu computador em C:\Arquivos de Programas\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\doc\manual.

## <a name="see-also"></a>Confira também

+ [Pacote utils de R](https://www.rdocumentation.org/packages/utils/versions/3.5.1)
+ ["Advanced R" (R avançado) por Hadley Wickham](http://adv-r.had.co.nz)
