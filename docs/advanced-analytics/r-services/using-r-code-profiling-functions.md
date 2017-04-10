---
title: "Usando fun&#231;&#245;es de cria&#231;&#227;o de perfil de c&#243;digo de R | Microsoft Docs"
ms.custom: ""
ms.date: "11/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 132db249-b9f1-48f5-a63e-c9806cacc4af
caps.latest.revision: 6
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 5
---
# Usando fun&#231;&#245;es de cria&#231;&#227;o de perfil de c&#243;digo de R
Além de usar recursos do SQL Server e ferramentas para monitorar a execução do script R, você pode usar ferramentas de desempenho fornecidas por outros pacotes de R para obter mais informações sobre chamadas de função interna. Este tópico fornece uma lista de alguns recursos básicos para você começar. Para obter orientações, recomendamos o capítulo em [desempenho](http://adv-r.had.co.nz/Performance.html) no livro "" Advanced R"", de Hadley Wickham.

## <a name="using-rprof"></a>Usando RPROF

*rprof* é uma função incluída no pacote base **utils**, que é carregado por padrão. Uma vantagem de *rprof* é que ele executa a amostragem, reduzindo assim a carga de desempenho do monitoramento.

Para usar o R de criação de perfil em seu código, você chama essa função e especifique seus parâmetros, incluindo o nome do local do arquivo de log será gravado. Consulte a Ajuda do *rprof* para obter detalhes.

Em geral, o *rprof* função funciona escrevendo a pilha de chamadas em um arquivo, em intervalos especificados. Você pode usar o *summaryRprof* função para processar o arquivo de saída. 

Criação de perfil pode ser ativada e desativado em seu código. Para ativar a criação de perfil, suspender a criação de perfil e reiniciá-lo, você usaria uma sequência de chamadas para *rprof*:

1. Especifique o arquivo de saída de criação de perfil.

    ```R
    varOutputFile <- "C:/TEMP/run001.log")
    Rprof(varOutputFile)
    ```
2. Desativar a criação de perfil
    ```R
    Rprof(NULL)
    ```
    
3. Reinicie a criação de perfil
    ```R
    Rprof(append=TRUE)
    ```


> [!NOTE] Usando essa função requer que o Windows Perl esteja instalado no computador onde o código é executado. Portanto, é recomendável que você criar o perfil de código durante o desenvolvimento em um ambiente de R e, em seguida, implante o código depurado no SQL Server.  


## <a name="r-system-functions"></a>Funções do sistema R

A linguagem R inclui muitas funções de pacote básico para retornar o conteúdo de variáveis do sistema. 

Por exemplo, como parte do seu código R, você pode usar `Sys.timezone` para obter o fuso horário atual, ou `Sys.Time` para obter a hora do sistema de R. 

Para obter informações sobre funções individuais do sistema R, digite o nome da função como argumento para R `help()` função em um prompt de comando de R.

```R
help("Sys.time")
```

## <a name="debugging-and-profiling-in-r"></a>Depuração e criação de perfil em R

A documentação do Microsoft R Open, que é instalado por padrão, inclui um manual sobre o desenvolvimento de extensões para a linguagem de R que aborda a criação de perfis e depuração em detalhes.

O capítulo também está disponível online: [https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging](https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging)

### <a name="location-of-r-help-files"></a>Local dos arquivos de ajuda de R

C:\Program Files\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\doc\manual


