---
title: Aprimorar o desempenho usando a função de criação de perfil de código R
description: Colete informações úteis para aprimorar o desempenho e obtenha resultados mais rápidos sobre computações de R no SQL Server usando as funções de criação de perfil de R. A função *rprof* coleta e retorna informações sobre chamadas de função internas.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 10/30/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d15f31dc2c289df910b06de8cb1f48647dbde33c
ms.sourcegitcommit: 49ee3d388ddb52ed9cf78d42cff7797ad6d668f2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2020
ms.locfileid: "94384745"
---
# <a name="use-r-code-profiling-functions-to-improve-performance"></a>Use as funções de criação de perfil de código R para melhorar o desempenho
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Este artigo descreve as ferramentas de desempenho fornecidas pelos pacotes do R para obter informações sobre chamadas de função internas. É possível usar essas informações para aprimorar o desempenho de seu código.

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

A documentação do Microsoft R Open, que é instalado por padrão, inclui um manual sobre o desenvolvimento de extensões para a linguagem R que aborda a [criação de perfis e depuração](https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging) em detalhes.

## <a name="next-steps"></a>Próximas etapas

+ Para obter mais informações sobre como otimizar scripts R no SQL Server, confira [Ajuste de desempenho e otimização de dados para R](r-and-data-optimization-r-services.md).
+ Para obter informações mais completas sobre o ajuste de desempenho no SQL Server, confira a [Central de Desempenho para o Mecanismo de Banco de Dados do SQL Server e Banco de Dados SQL do Azure](/sql/relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database).
+ Para obter mais informações sobre o pacote utils, confira [O pacote utils do R](https://www.rdocumentation.org/packages/utils/versions/3.5.1).
+ Para discussões aprofundadas sobre a programação em R, confira ["R avançado", de Hadley Wickham](http://adv-r.had.co.nz).
