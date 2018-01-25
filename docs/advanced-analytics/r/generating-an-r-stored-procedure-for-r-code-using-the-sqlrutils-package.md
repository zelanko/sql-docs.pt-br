---
title: "Gerando um procedimento armazenado de R para o código de R usando o pacote sqlrutils | Microsoft Docs"
ms.custom: 
ms.date: 02/28/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: d8739f16-ac26-4f69-870c-51c77cf286d3
caps.latest.revision: "8"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 4948cdd841c2b97e50623dac7b9d6ba9ef923220
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package"></a>Gerando um procedimento armazenado de R para o código R usando o pacote sqlrutils
O pacote **sqlrutils** fornece um mecanismo para que os usuários de R coloquem seus scripts de R em um procedimento armazenado T-SQL, registrem esse procedimento armazenado em um banco de dados, e executem o procedimento armazenado em um ambiente de desenvolvimento de R. 

Ao converter o código R para executar dentro de um único procedimento armazenado, você pode fazer um uso mais eficaz dos serviços de R do SQL Server, o que exige que o script de R seja inserido como um parâmetro de [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). O pacote **sqlrutils** ajuda a criar esse script de R incorporado e definir os parâmetros relacionados de maneira apropriada.

O pacote **sqlrutils** executa essas tarefas:

- Salva o script T-SQL gerado como uma cadeia de caracteres dentro de uma estrutura de dados de R
- Opcionalmente, gera um arquivo .sql para o script T-SQL, que você pode editar ou executar para criar um procedimento armazenado
- Registra o procedimento armazenado criado recentemente na instância do SQL Server do seu ambiente de desenvolvimento de R

Você também pode executar o procedimento armazenado em um ambiente de R, transmitindo parâmetros bem formados e processando os resultados. Ou, você pode usar o procedimento armazenado do SQL Server para oferecer suporte a cenários comuns de integração de banco de dados, como ETL, treinamento de modelo e pontuação de alto volume.

  > [!NOTE]
  > Se você pretende executar o procedimento armazenado em um ambiente de R chamando a função *executeStoredProcedure* , você deve usar um provedor ODBC 3.8, como o ODBC Driver 13 para SQL Server.  
  
## <a name="functions-provided-in-sqlrutils"></a>Funções fornecidas no sqlrutils

A lista a seguir fornece uma visão geral das funções que você pode chamar do pacote **sqlrutils** para desenvolver um procedimento armazenado para usar nos serviços de R do SQL Server. Para obter detalhes sobre os parâmetros para cada função ou método, consulte a ajuda de R para o pacote:

```R
help(package="sqlrutils") 
```

**Definir parâmetros e entradas de procedimento armazenado**

- `InputData`. Define a fonte de dados no SQL Server que será usada no quadro de dados de R. Você especifica o nome do data.frame no qual armazena os dados de entrada e uma consulta para obter os dados, ou um valor padrão. Só há suporte para consultas SELECT simples.

- `InputParameter`. Define um único parâmetro de entrada que será inserido no script T-SQL. Você deve fornecer o nome do parâmetro e seu tipo de dados de R.

- `OutputData`. Gera um objeto de dados intermediário que será necessário se a função R retornar uma lista que contém um data.frame. 
   O objeto *OutputData* é usado para armazenar o nome de um único data.frame obtido da lista. 

- `OutputParameter`. Gera um objeto de dados intermediário que será necessário se a função R retornar uma lista. O objeto *OutputParameter* armazena o nome e o tipo de dados de um único membro da lista, supondo que o membro **não** é um quadro de dados. 


**Gerar e registrar o procedimento armazenado**


- `StoredProcedure` é o construtor principal usado para criar o procedimento armazenado.  Este construtor gera um *Objeto de procedimento armazenado do SQL Server* e, opcionalmente, cria um arquivo de texto que contém uma consulta que pode ser usada para gerar o procedimento armazenado usando um comando T-SQL. Opcionalmente, a função *StoredProcedure* também pode registrar o procedimento armazenado com a instância e o banco de dados especificado.

   + Use o argumento `func` para especificar uma função de R válida. Todas as variáveis que a função usa devem ser definidas dentro da função ou ser fornecidas como parâmetros de entrada. Esses parâmetros podem incluir no máximo um quadros de dados.
   + A função R deve retornar um quadro de dados, uma lista nomeada ou um valor NULO. Se a função retorna uma lista, a lista pode conter no máximo um data.frame.
   + Use o argumento `spName` para especificar o nome do procedimento armazenado que você deseja criar.
   + Você pode transmitir parâmetros opcionais de entrada e de saída, usando os objetos criados por essas funções auxiliares: `setInputData`, `setInputParameter`e `setOutputParameter`.
   +  Opcionalmente, use `filePath` para fornecer o caminho e o nome de um arquivo .sql a ser criado. Você pode executar esse arquivo na instância do SQL Server para gerar o procedimento armazenado usando a T-SQL.
   + Para definir o servidor e o banco de dados em que o procedimento armazenado será salvo, use os argumentos `dbName` e  `connectionString`.
   + Para obter uma lista dos objetos *InputData* e *InputParameter* que foram usados para criar um objeto específico *StoredProcedure* , chame `getInputParameters`. 
   + Para registrar o procedimento armazenado com o banco de dados especificado, use `registerStoredProcedure`.

   O objeto de procedimento armazenado normalmente não tem quaisquer dados ou valores associados a ele, a menos que um valor padrão foi especificado. Os dados não serão recuperados até que o procedimento armazenado seja executado. 


**Especificar entradas e executar**

- Use `setInputDataQuery` para atribuir uma consulta a um objeto *InputParameter* . Por exemplo, se você tiver criado um objeto de procedimento armazenado em R, você pode usar `setInputDataQuery` para transmitir argumentos para a função *StoredProcedure* a fim de executar o procedimento armazenado com as entradas desejadas.

- Use `setInputValue` para atribuir valores específicos para um parâmetro armazenado como um objeto *InputParameter* . Em seguida, transmita o objeto de parâmetro e sua atribuição de valor para a função *StoredProcedure* a fim de executar o procedimento armazenado com os valores definidos.

- Use `executeStoredProcedure` para executar um procedimento armazenado definido como um objeto *StoredProcedure* . Chame essa função apenas ao executar um procedimento armazenado de código R. Não use esta opção quando executar o procedimento armazenado do SQL Server usando a T-SQL.

  > [!NOTE]
  > A função *executeStoredProcedure* requer um provedor ODBC 3.8, como o ODBC Driver 13 para SQL Server.  
  
  



## <a name="see-also"></a>Consulte também
[Como criar um procedimento armazenado usando sqlrutils](../../advanced-analytics/r-services/how-to-create-a-stored-procedure-using-sqlrutils.md)

