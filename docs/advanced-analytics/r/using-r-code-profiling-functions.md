---
title: Usar o código de R, criação de perfil de funções – serviços do SQL Server Machine Learning
description: Melhorar o desempenho e obtenha resultados mais rápidos de cálculos de R no SQL Server usando R, funções de criação de perfil para retornar informações sobre chamadas de função interna.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/12/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 7bd54130ecb17241f0a5cddf4d80e186d7a8a427
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645016"
---
# <a name="use-r-code-profiling-functions-to-improve-performance"></a>Usar funções de criação de perfil de código de R para melhorar o desempenho
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Além de usar recursos do SQL Server e ferramentas para monitorar a execução do script R, você pode usar ferramentas de desempenho fornecidas por outros pacotes de R para obter mais informações sobre chamadas de função internas. 

> [!TIP]
> Este artigo fornece recursos básicos para você começar. Para obter diretrizes, recomendamos a *desempenho* seção ["Advanced R", de Hadley Wickham](http://adv-r.had.co.nz).

## <a name="using-rprof"></a>Usando RPROF

[*rprof* ](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/Rprof) é uma função incluída no pacote base [ **utils**](https://www.rdocumentation.org/packages/utils/versions/3.5.1), que é carregado por padrão. 

Em geral, a função *rprof* funciona escrevendo a pilha de chamadas em um arquivo aos intervalos especificados. Você pode usar o [ *summaryRprof* ](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/summaryRprof) função para processar o arquivo de saída. Uma vantagem de *rprof* é que ele executa a amostragem, reduzindo a carga de desempenho do monitoramento.

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

A documentação do Microsoft R Open, que é instalado por padrão, inclui um manual sobre o desenvolvimento de extensões para a linguagem R que aborda [criação de perfil e depuração](https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging) detalhadamente. Você pode encontrar a documentação do mesma em seu computador em C:\Program Files\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\doc\manual.

## <a name="see-also"></a>Confira também

+ [pacote de utilitários de R](https://www.rdocumentation.org/packages/utils/versions/3.5.1)
+ ["Advanced R" de Hadley Wickham](http://adv-r.had.co.nz)
