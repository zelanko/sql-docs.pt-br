---
title: funções auxiliares sqlrutils
description: Use a biblioteca de funções sqlrutils em SQL Server 2016 R Services e SQL Server Serviços de Machine Learning com R para gerar procedimentos armazenados que contenham o script R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3de8d438691afb7ebf1aabe15265227b7876b837
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715035"
---
# <a name="sqlrutils-r-library-in-sql-server"></a>sqlrutils (R library in SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

O pacote **sqlrutils** fornece um mecanismo para que os usuários de R coloquem seus scripts de R em um procedimento armazenado T-SQL, registrem esse procedimento armazenado em um banco de dados, e executem o procedimento armazenado em um ambiente de desenvolvimento de R. 

Ao converter o código R para executar dentro de um único procedimento armazenado, você pode fazer um uso mais eficaz dos serviços de R do SQL Server, o que exige que o script de R seja inserido como um parâmetro de [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). O pacote **sqlrutils** ajuda a criar esse script de R incorporado e definir os parâmetros relacionados de maneira apropriada.

O pacote **sqlrutils** executa essas tarefas:

- Salva o script T-SQL gerado como uma cadeia de caracteres dentro de uma estrutura de dados de R
- Opcionalmente, gera um arquivo .sql para o script T-SQL, que você pode editar ou executar para criar um procedimento armazenado
- Registra o procedimento armazenado criado recentemente na instância do SQL Server do seu ambiente de desenvolvimento de R

Você também pode executar o procedimento armazenado em um ambiente de R, transmitindo parâmetros bem formados e processando os resultados. Ou, você pode usar o procedimento armazenado do SQL Server para oferecer suporte a cenários comuns de integração de banco de dados, como ETL, treinamento de modelo e pontuação de alto volume.

  > [!NOTE]
  > Se você pretende executar o procedimento armazenado em um ambiente de R chamando a função *executeStoredProcedure* , você deve usar um provedor ODBC 3.8, como o ODBC Driver 13 para SQL Server.  
  
## <a name="full-reference-documentation"></a>Documentação de referência completa

A biblioteca **sqlrutils** é distribuída em vários produtos da Microsoft, mas o uso é o mesmo se você obter a biblioteca em SQL Server ou em outro produto. Como as funções são as mesmas, a [documentação para funções individuais sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) é publicada em apenas um local sob a [referência de R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para Microsoft Machine Learning Server. Se existirem comportamentos específicos do produto, as discrepâncias serão indicadas na página de ajuda da função.

## <a name="functions-list"></a>Lista de funções

A seção a seguir fornece uma visão geral das funções que você pode chamar do pacote **sqlrutils** para desenvolver um procedimento armazenado que contém o código R incorporado. Para obter detalhes sobre os parâmetros para cada método ou função, consulte a ajuda do R para o pacote:`help(package="sqlrutils")`

|Função | Descrição |
|------|-------------|
|[executeStoredProcedure](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/executestoredprocedure)| Execute um procedimento armazenado SQL.|
|[getInputParameters](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/getinputparameters)| Obtenha uma lista de parâmetros de entrada para o procedimento armazenado.| 
|[InputData](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/inputdata)| Define a fonte de dados no SQL Server que será usada no quadro de dados de R. Você especifica o nome do data.frame no qual armazena os dados de entrada e uma consulta para obter os dados, ou um valor padrão. Só há suporte para consultas SELECT simples. | 
|[InputParameter](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/inputparameter)| Define um único parâmetro de entrada que será inserido no script T-SQL. Você deve fornecer o nome do parâmetro e seu tipo de dados de R.| 
|[OutputData](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/outputdata)| Gera um objeto de dados intermediário que será necessário se a função R retornar uma lista que contém um data.frame. O objeto *OutputData* é usado para armazenar o nome de um único data.frame obtido da lista.| 
|[OutputParameter](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/outputparameter) | Gera um objeto de dados intermediário que será necessário se a função R retornar uma lista. O objeto *OutputParameter* armazena o nome e o tipo de dados de um único membro da lista, supondo que o membro **não** é um quadro de dados. |
|[registerStoredProcedure](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/registerstoredprocedure) | Registre o procedimento armazenado com um banco de dados.|
|[setInputDataQuery](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/setinputdataquery)| Atribua uma consulta a um parâmetro de dados de entrada do procedimento armazenado.| 
|[setInputParameterValue](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/setinputparametervalue)| Atribua um valor a um parâmetro de entrada do procedimento armazenado.| 
|[StoredProcedure](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/storedprocedure)| Um objeto de procedimento armazenado.|


## <a name="how-to-use-sqlrutils"></a>Como usar o sqlrutils

As funções de biblioteca **sqlrutils** devem ser executadas em um computador que tenha SQL Server Machine Learning com o R. Se você estiver trabalhando em uma estação de trabalho cliente, defina um contexto de computação remota para alternar a execução para SQL Server. O fluxo de trabalho para usar esse pacote inclui as seguintes etapas:

+ Definir parâmetros de procedimento armazenado (entradas, saídas ou ambos) 
+ Gerar e registrar o procedimento armazenado    
+ Executar o procedimento armazenado  

Em uma sessão de R, carregue **sqlrutils** da linha de comando digitando `library(sqlrutils)`.

> [!Note]
> Você pode carregar essa biblioteca no computador que não tem SQL Server (por exemplo, em uma instância de cliente do R) se você alterar o contexto de computação para SQL Server e executar o código nesse contexto de computação.


### <a name="define-stored-procedure-parameters-and-inputs"></a>Definir parâmetros e entradas de procedimento armazenado

`StoredProcedure` é o construtor principal usado para criar o procedimento armazenado. Este construtor gera um *Objeto de procedimento armazenado do SQL Server* e, opcionalmente, cria um arquivo de texto que contém uma consulta que pode ser usada para gerar o procedimento armazenado usando um comando T-SQL. 

Opcionalmente, a função *StoredProcedure* também pode registrar o procedimento armazenado com a instância e o banco de dados especificado.

+ Use o argumento `func` para especificar uma função de R válida. Todas as variáveis que a função usa devem ser definidas dentro da função ou ser fornecidas como parâmetros de entrada. Esses parâmetros podem incluir no máximo um quadros de dados.

+ A função R deve retornar um quadro de dados, uma lista nomeada ou um valor NULO. Se a função retorna uma lista, a lista pode conter no máximo um data.frame.

+ Use o argumento `spName` para especificar o nome do procedimento armazenado que você deseja criar.

+ Você pode transmitir parâmetros opcionais de entrada e de saída, usando os objetos criados por essas funções auxiliares: `setInputData`, `setInputParameter`e `setOutputParameter`.

+  Opcionalmente, use `filePath` para fornecer o caminho e o nome de um arquivo .sql a ser criado. Você pode executar esse arquivo na instância do SQL Server para gerar o procedimento armazenado usando a T-SQL.

+ Para definir o servidor e o banco de dados em que o procedimento armazenado será salvo, use os argumentos `dbName` e  `connectionString`.

+ Para obter uma lista dos objetos *InputData* e *InputParameter* que foram usados para criar um objeto específico *StoredProcedure* , chame `getInputParameters`. 

+ Para registrar o procedimento armazenado com o banco de dados especificado, use `registerStoredProcedure`.

O objeto de procedimento armazenado normalmente não tem quaisquer dados ou valores associados a ele, a menos que um valor padrão foi especificado. Os dados não serão recuperados até que o procedimento armazenado seja executado. 

### <a name="specify-inputs-and-execute"></a>Especificar entradas e executar

+ Use `setInputDataQuery` para atribuir uma consulta a um objeto *InputParameter* . Por exemplo, se você tiver criado um objeto de procedimento armazenado em R, você pode usar `setInputDataQuery` para transmitir argumentos para a função *StoredProcedure* a fim de executar o procedimento armazenado com as entradas desejadas.

+ Use `setInputValue` para atribuir valores específicos para um parâmetro armazenado como um objeto *InputParameter* . Em seguida, transmita o objeto de parâmetro e sua atribuição de valor para a função *StoredProcedure* a fim de executar o procedimento armazenado com os valores definidos.

+ Use `executeStoredProcedure` para executar um procedimento armazenado definido como um objeto *StoredProcedure* . Chame essa função apenas ao executar um procedimento armazenado de código R. Não use esta opção quando executar o procedimento armazenado do SQL Server usando a T-SQL.

> [!NOTE]
> A função *executeStoredProcedure* requer um provedor ODBC 3.8, como o ODBC Driver 13 para SQL Server.  

## <a name="see-also"></a>Confira também

[Como criar um procedimento armazenado usando sqlrutils](how-to-create-a-stored-procedure-using-sqlrutils.md)

