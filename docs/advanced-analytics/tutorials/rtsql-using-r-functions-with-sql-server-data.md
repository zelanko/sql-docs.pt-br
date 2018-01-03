---
title: "Usando funções de R com dados do SQL Server (R no início rápido do SQL) | Microsoft Docs"
ms.custom: 
ms.date: 07/26/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
dev_langs:
- R
- SQL
ms.assetid: e2fe5d90-eee9-4daf-9eae-21d17b3ef320
caps.latest.revision: "8"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 0a536b0d569fba36c84b550bec0b60896b448e45
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2017
---
# <a name="using-r-functions-with-sql-server-data-r-in-sql-quickstart"></a>Usando funções de R com dados do SQL Server (R no início rápido do SQL)

Agora que você está familiarizado com operações básicas, chegou a hora de divertir-se um pouco com o R. Por exemplo, muitas funções estatísticas avançadas podem ser complicadas de implementar usando T-SQL, mas exigem apenas uma única linha de código R.  Com R Services, é fácil inserir scripts R de utilitário em um procedimento armazenado.

Nestes exemplos, você inserirá R matemático e funções de utilitário em um procedimento armazenado do SQL Server.

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>Criar um procedimento armazenado para gerar números aleatórios

Para simplificar, vamos usar o R `stats` pacote, que é instalado e carregado por padrão com os serviços de R. O pacote contém centenas de funções para tarefas estatísticas comuns, entre elas, a função `rnorm`, que gera um número específico de números aleatórios usando a distribuição normal, dado um desvio padrão e uma média.

Por exemplo, esse código R retorna 100 números em uma média de 50, dado um desvio padrão de 3.

```R
as.data.frame(rnorm(100, mean = 50, sd = 3));
```

Para chamar esta linha de R de T-SQL, execute sp_execute_external_script e adicione a função R no parâmetro de script de R, como este:

```sql
EXEC sp_execute_external_script
      @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(100, mean = 50, sd =3));'
    , @input_data_1 = N'   ;'
      WITH RESULT SETS (([Density] float NOT NULL));
```

E se você quiser facilitar a geração de um conjunto de números aleatórios diferente?

Isso é fácil quando combinado com o SQL Server: defina um procedimento armazenado que obtém os argumentos do usuário. Em seguida, passe esses argumentos para o script de R como variáveis.

```sql
CREATE PROCEDURE MyRNorm (@param1 int, @param2 int, @param3 int)
AS
    EXEC sp_execute_external_script
      @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(mynumbers, mymean, mysd));'
    , @input_data_1 = N'   ;'
    , @params = N' @mynumbers int, @mymean int, @mysd int'
    , @mynumbers = @param1
    , @mymean = @param2
    , @mysd = @param3
    WITH RESULT SETS (([Density] float NOT NULL));
```

+ A primeira linha define cada um dos parâmetros de entrada SQL necessários quando o procedimento armazenado é executado.

+ A linha que começa com `@params` define todas as variáveis usadas pelo código R e os tipos de dados SQL correspondentes.

+ As linhas imediatamente após mapeiam os nomes de parâmetro SQL para os nomes de variável R correspondentes.

Agora que você encapsulou a função R em um procedimento armazenado, pode facilmente chamar a função e passar valores diferentes, como este:

```sql
EXEC MyRNorm @param1 = 100,@param2 = 50, @param3 = 3
```

## <a name="related-resources"></a>Recursos relacionados

+ Você deseja instalar mais pacotes de R obter mais avançado de funções estatísticas? Consulte [instalando e Gerenciando pacotes R](../r/installing-and-managing-r-packages.md).

+ Para ajudá-lo a converter seu código R autônomo em um formato que pode ser parametrizado facilmente usando procedimentos armazenados do SQL Server, a equipe do Microsoft R tiver fornecido um novo pacote de R, **sqlrutils**. Para obter mais informações, consulte [como criar um procedimento armazenado usando sqlrutils](../r/how-to-create-a-stored-procedure-using-sqlrutils.md).

## <a name="use-r-utility-functions-for-troubleshooting"></a>Usar funções de utilitário de R para solução de problemas

Por padrão, uma instalação do R inclui o `utils` pacote, que fornece uma variedade de funções de utilitário para investigar o atual ambiente de R. Isso poderá ser útil se você estiver encontrando discrepâncias na maneira como o código R é executado no SQL Server e em ambientes externos.

Por exemplo, você pode usar a função R `memory.limit()` para obter memória para o ambiente atual de R. Uma vez que o pacote `utils` é instalado, mas não carregado por padrão, primeiro é necessário usar a função `library()` para carregá-lo.

```sql
EXECUTE sp_execute_external_script
      @language = N'R'
    , @script = N'
        library(utils);
        mymemory <- memory.limit();
        OutputDataSet <- as.data.frame(mymemory);'
    , @input_data_1 = N' ;'
WITH RESULT SETS (([Col1] int not null));
```

Muitos usuários, como usar as funções de tempo do sistema em R, como `system.time` e `proc.time`, para capturar o tempo usado por processos de R e analisar problemas de desempenho.

Para obter um exemplo, consulte este tutorial: [Criar recursos de dados](../tutorials/walkthrough-create-data-features.md). Neste passo a passo, funções de tempo R são inseridas na solução para comparar o desempenho de dois métodos para criar recursos de dados: funções R vs. funções T-SQL.

## <a name="next-lesson"></a>Próxima lição

Em seguida, você criará um modelo de previsão usando R no SQL Server.

[Criar um modelo preditivo](../tutorials/rtsql-create-a-predictive-model-r.md)
