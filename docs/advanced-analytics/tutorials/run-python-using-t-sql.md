---
title: Executar Python usando o T-SQL | Microsoft Docs
ms.custom: 
ms.date: 09/19/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2016
dev_langs: Python
caps.latest.revision: "2"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 2812e9529a9cdb4dc5fd8019a28ccc060ba68d1a
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="run-python-using-t-sql"></a>Executar Python usando o T-SQL

Este exemplo mostra como você pode executar um script simples do Python no SQL Server, usando o procedimento armazenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)

## <a name="step-1-create-the-test-data-table"></a>Etapa 1. Criar a tabela de dados de teste

Primeiro, você criará alguns dados adicionais, para usar ao mapear os nomes dos dias da semana para os dados de origem. Execute a seguinte instrução T-SQL para criar a tabela.

```SQL
CREATE TABLE PythonTest (
    [DayOfWeek] varchar(10) NOT NULL,
    [Amount] float NOT NULL
    )
GO

INSERT INTO PythonTest VALUES
('Sunday', 10.0),
('Monday', 11.1),
('Tuesday', 12.2),
('Wednesday', 13.3),
('Thursday', 14.4),
('Friday', 15.5),
('Saturday', 16.6),
('Friday', 17.7),
('Monday', 18.8),
('Sunday', 19.9)
GO
```

## <a name="step-2-run-the-hello-world-script"></a>Etapa 2. Execute o script "Hello World"

O código a seguir carrega o executável do Python, passa os dados de entrada e para cada linha de dados de entrada, atualiza o nome do dia na tabela com um número que representa o índice de dia da semana.

Anote o parâmetro  *@RowsPerRead* . Esse parâmetro especifica o número de linhas que são passados para o tempo de execução do Python do SQL Server.

A biblioteca de análise de dados de Python, conhecido como **pandas**, é necessário para passar dados para o SQL Server e está incluído por padrão, com serviços de aprendizado de máquina.

```sql
DECLARE @ParamINT INT = 1234567
DECLARE @ParamCharN VARCHAR(6) = 'INPUT '

print '------------------------------------------------------------------------'
print 'Output parameters (before):'
print FORMATMESSAGE('ParamINT=%d', @ParamINT)
print FORMATMESSAGE('ParamCharN=%s', @ParamCharN)

print 'Dataset (before):'
SELECT * FROM PythonTest

print '------------------------------------------------------------------------'
print 'Dataset (after):'
DECLARE @RowsPerRead INT = 5

execute sp_execute_external_script 
@language = N'Python',
@script = N'
import sys
import os
print("*******************************")
print(sys.version)
print("Hello World")
print(os.getcwd())
print("*******************************")
if ParamINT == 1234567:
       ParamINT = 1
else:
       ParamINT += 1

ParamCharN="OUTPUT"
OutputDataSet = InputDataSet

global daysMap

daysMap = {
       "Monday" : 1,
       "Tuesday" : 2,
       "Wednesday" : 3,
       "Thursday" : 4,
       "Friday" : 5,
       "Saturday" : 6,
       "Sunday" : 7
       }

OutputDataSet["DayOfWeek"] = pandas.Series([daysMap[i] for i in OutputDataSet["DayOfWeek"]], index = OutputDataSet.index, dtype = "int32")
', 
@input_data_1 = N'SELECT * FROM PythonTest', 
@params = N'@r_rowsPerRead INT, @ParamINT INT OUTPUT, @ParamCharN CHAR(6) OUTPUT',
@r_rowsPerRead = @RowsPerRead,
@paramINT = @ParamINT OUTPUT,
@paramCharN = @ParamCharN OUTPUT
with result sets (("DayOfWeek" int null, "Amount" float null))

print 'Output parameters (after):'
print FORMATMESSAGE('ParamINT=%d', @ParamINT)
print FORMATMESSAGE('ParamCharN=%s', @ParamCharN)
GO
```

> [!TIP]
> Os parâmetros para esse procedimento armazenado são descritos mais detalhadamente neste guia de início rápido: [código R usando o T-SQL](rtsql-using-r-code-in-transact-sql-quickstart.md).

## <a name="step-3-view-the-results"></a>Etapa 3. Exibir os resultados

O procedimento armazenado obtém os dados originais, aplica-se o script de Python e, em seguida, retorna os dados modificados no **resultados** painel do Management Studio ou outra ferramenta de consulta SQL.


|DayOfWeek (antes)| Valor|DayOfWeek (após) |
|-----|-----|-----|
|Domingo|10|7|
|Segunda-feira|11.1|1|
|Terça-feira|12.2|2|
|Quarta-feira|13.3|3|
|Quinta-feira|14.4|4|
|Sexta-feira|15.5|5|
|Sábado|16.6|6|
|Sexta-feira|17.7|5|
|Segunda-feira|18.8|1|
|Domingo|19.9|7|

Mensagens de status ou erros retornados para o console de Python são retornados como mensagens de **consulta** janela. Aqui está um trecho da saída que você verá:

*Resultados de exemplo*

```
Output parameters (before):
ParamINT=1234567
ParamCharN=INPUT 
Dataset (before):

(10 rows affected)

Dataset (after):
STDOUT message(s) from external script: 
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy

3.5.2 |Anaconda 4.2.0 (64-bit)| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
Hello World
C:\PROGRA~1\MICROS~2\MSSQL1~1.MSS\MSSQL\EXTENS~1\MSSQLSERVER01\7A70B3FB-FBA2-4C52-96D6-8634DB843229

3.5.2 |Anaconda 4.2.0 (64-bit)| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
Hello World
C:\PROGRA~1\MICROS~2\MSSQL1~1.MSS\MSSQL\EXTENS~1\MSSQLSERVER01\7A70B3FB-FBA2-4C52-96D6-8634DB843229

(10 rows affected)
Output parameters (after):
ParamINT=2
ParamCharN=OUTPUT
```

+ O **mensagem** saída inclui o diretório de trabalho usado para a execução do script. Neste exemplo, MSSQLSERVER01 refere-se à conta de trabalho alocada pelo SQL Server para gerenciar o trabalho. 

    O GUID é o nome de uma pasta temporária é criada durante a execução do script para armazenar os artefatos de dados e de script. Essas pastas temporárias são protegidas pelo SQL Server e são limpos pelo objeto de trabalho do Windows depois que o script foi encerrado.

+ A seção que contém a mensagem "Hello World" imprime duas vezes. Isso acontece porque o valor de  *@RowsPerRead*  foi definido como 5 e há 10 linhas na tabela; portanto, duas chamadas para Python são necessários para processar todas as linhas na tabela.

    A execução de produção, é recomendável fazer experiências com valores diferentes para determinar o número máximo de linhas que devem ser passados em cada lote. O número ideal de linhas é dependente de dados e é afetado pelo número de colunas no conjunto de dados e o tipo de dados que estão sendo transmitidos.

## <a name="resources"></a>Recursos

Consulte esses exemplos adicionais do Python e tutoriais para dicas avançadas e demonstrações de ponta a ponta.

+ [Usar o Python revoscalepy para criar um modelo](use-python-revoscalepy-to-create-model.md)
+ [Python no banco de dados para desenvolvedores em SQL](sqldev-in-database-python-for-sql-developers.md)
+ [Criar um modelo de previsão usando Python e o SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

## <a name="troubleshooting"></a>Solução de problemas

Se você não encontrar o procedimento armazenado, `sp_execute_external_script`, isso significa que você provavelmente ainda não terminou de configurar a instância para dar suporte à execução do script externo. Depois de executar a instalação do SQL Server 2017 e selecionar Python como a idioma de aprendizado de máquina, você deve habilitar explicitamente o recurso usando `sp_configure`e, em seguida, reinicie a instância. Para obter detalhes, consulte [instalação serviços de aprendizado de máquina com Python](../python/setup-python-machine-learning-services.md).