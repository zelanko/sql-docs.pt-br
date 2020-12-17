---
title: Funções auxiliares de sqlrutils
description: O sqlrutils é um pacote de R da Microsoft que fornece um mecanismo para que os usuários de R coloquem seus scripts de R em um procedimento armazenado T-SQL, registrem esse procedimento armazenado em um banco de dados e executem o procedimento armazenado em um ambiente de desenvolvimento de R. O pacote está incluído nos Serviços de Machine Learning do SQL Server e no SQL Server 2016 R Services.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/14/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15'
ms.openlocfilehash: ac81810036e4159843142cb419deb3d06c57848c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470787"
---
# <a name="sqlrutils-r-package-in-sql-server-machine-learning-services"></a>sqlrutils (pacote de R nos Serviços de Machine Learning do SQL Server)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

O **sqlrutils** é um pacote de R da Microsoft que fornece um mecanismo para que os usuários de R coloquem seus scripts de R em um procedimento armazenado T-SQL, registrem esse procedimento armazenado em um banco de dados e executem o procedimento armazenado em um ambiente de desenvolvimento de R. O pacote está incluído nos [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md) e no [SQL Server 2016 R Services](sql-server-r-services.md).

Ao converter o código R para executar dentro de um único procedimento armazenado, você pode fazer um uso mais eficaz dos serviços de R do SQL Server, o que exige que o script de R seja inserido como um parâmetro de [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). O pacote **sqlrutils** ajuda a criar esse script de R incorporado e definir os parâmetros relacionados de maneira apropriada.

O pacote **sqlrutils** executa essas tarefas:

- Salva o script T-SQL gerado como uma cadeia de caracteres dentro de uma estrutura de dados de R
- Opcionalmente, gere um arquivo .sql para o script T-SQL, que você pode editar ou executar para criar um procedimento armazenado
- Registra o procedimento armazenado criado recentemente na instância do SQL Server do seu ambiente de desenvolvimento de R

Você também pode executar o procedimento armazenado em um ambiente de R, transmitindo parâmetros bem formados e processando os resultados. Ou, você pode usar o procedimento armazenado do SQL Server para oferecer suporte a cenários comuns de integração de banco de dados, como ETL, treinamento de modelo e pontuação de alto volume.

> [!NOTE]
> Se você pretende executar o procedimento armazenado em um ambiente de R chamando a função *executeStoredProcedure* , você deve usar um provedor ODBC 3.8, como o ODBC Driver 13 para SQL Server.  
  
## <a name="full-reference-documentation"></a>Documentação de referência completa

O pacote **sqlrutils** é distribuído em vários produtos da Microsoft, mas o uso é o mesmo com o pacote no SQL Server ou em outro produto. Como as funções são as mesmas, a [documentação para funções individuais do sqlrutils](/machine-learning-server/r-reference/revoscaler/revoscaler) é publicada em apenas uma localização sob a [referência de R](/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para o Microsoft Machine Learning Server. Se existirem comportamentos específicos do produto, as discrepâncias serão indicadas na página de ajuda da função.

## <a name="functions-list"></a>Lista de funções

A seção a seguir fornece uma visão geral das funções que você pode chamar do pacote **sqlrutils** para desenvolver um procedimento armazenado contendo o código R inserido. Para obter detalhes sobre os parâmetros para cada função ou método, confira a Ajuda do R para o pacote: `help(package="sqlrutils")`

|Função | Descrição |
|------|-------------|
|[executeStoredProcedure](/machine-learning-server/r-reference/sqlrutils/executestoredprocedure)| Executar um procedimento armazenado do SQL.|
|[getInputParameters](/machine-learning-server/r-reference/sqlrutils/getinputparameters)| Obter uma lista de parâmetros de entrada para o procedimento armazenado.| 
|[InputData](/machine-learning-server/r-reference/sqlrutils/inputdata)| Define a fonte de dados no SQL Server que será usada no quadro de dados de R. Você especifica o nome do data.frame no qual armazena os dados de entrada e uma consulta para obter os dados, ou um valor padrão. Só há suporte para consultas SELECT simples. | 
|[InputParameter](/machine-learning-server/r-reference/sqlrutils/inputparameter)| Define um único parâmetro de entrada que será inserido no script T-SQL. Você deve fornecer o nome do parâmetro e seu tipo de dados de R.| 
|[OutputData](/machine-learning-server/r-reference/sqlrutils/outputdata)| Gera um objeto de dados intermediário que será necessário se a função R retornar uma lista que contém um data.frame. O objeto *OutputData* é usado para armazenar o nome de um único data.frame obtido da lista.| 
|[OutputParameter](/machine-learning-server/r-reference/sqlrutils/outputparameter) | Gera um objeto de dados intermediário que será necessário se a função R retornar uma lista. O objeto *OutputParameter* armazena o nome e o tipo de dados de um único membro da lista, supondo que o membro **não** é um quadro de dados. |
|[registerStoredProcedure](/machine-learning-server/r-reference/sqlrutils/registerstoredprocedure) | Registrar o procedimento armazenado com um banco de dados.|
|[setInputDataQuery](/machine-learning-server/r-reference/sqlrutils/setinputdataquery)| Atribuir uma consulta a um parâmetro de dados de entrada do procedimento armazenado.| 
|[setInputParameterValue](/machine-learning-server/r-reference/sqlrutils/setinputparametervalue)| Atribuir um valor a um parâmetro de entrada do procedimento armazenado.| 
|[StoredProcedure](/machine-learning-server/r-reference/sqlrutils/storedprocedure)| Um objeto de procedimento armazenado.|


## <a name="how-to-use-sqlrutils"></a>Como usar o sqlrutils

As funções do pacote **sqlrutils** devem ser executadas em um computador que tenha o SQL Server Machine Learning com R. Se você estiver trabalhando em uma estação de trabalho cliente, defina um contexto de computação remota para alternar a execução para o SQL Server. O fluxo de trabalho para usar esse pacote inclui as seguintes etapas:

+ Definir parâmetros de procedimento armazenado (entradas, saídas ou ambos) 
+ Gerar e registrar o procedimento armazenado    
+ Executar o procedimento armazenado  

Em uma sessão de R, carregue **sqlrutils** da linha de comando digitando `library(sqlrutils)`.

> [!Note]
> Você poderá carregar esse pacote em um computador que não tem o SQL Server (por exemplo, em uma instância do Cliente R) se alterar o contexto de computação para o SQL Server e executar o código nesse contexto de computação.


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