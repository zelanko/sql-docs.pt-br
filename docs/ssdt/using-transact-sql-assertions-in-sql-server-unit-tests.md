---
title: Usar asserções Transact-SQL nos testes de unidade do SQL Server | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 55d8be9c-9282-47d3-be7f-e2c26f00c95e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 34cea0d4a251266d21218cefaee2d5f122e574ff
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52543899"
---
# <a name="using-transact-sql-assertions-in-sql-server-unit-tests"></a>Usando asserções Transact-SQL nos testes de unidade do SQL Server
Em um teste de unidade do SQL Server, um script de teste Transact\-SQL executa e retorna um resultado. Muitas vezes, os resultados são retornados como um conjunto de resultados. Você pode validar resultados usando condições de teste. Por exemplo, você pode usar uma condição de teste para verificar quantas linhas foram retornadas em um conjunto de resultados específico ou para verificar quanto tempo um teste específico levou para ser executado. Para saber mais sobre as condições de teste, confira [Usar as condições de teste em Testes de unidade do SQL Server](../ssdt/using-test-conditions-in-sql-server-unit-tests.md).  
  
Em vez de usar as condições de teste, você também pode usar as asserções Transact\-SQL, que são instruções THROW ou RAISERROR em um script Transact\-SQL. Em determinadas circunstâncias, talvez você prefira usar uma asserção Transact\-SQL, em vez de uma condição de teste.  
  
## <a name="using-transact-sql-assertions"></a>Usando asserções Transact-SQL  
Considere os seguintes pontos antes de decidir validar dados usando asserções Transact\-SQL ou condições de teste.  
  
-   **Desempenho**. É mais rápido executar uma asserção Transact\-SQL no servidor do que mover primeiro dados para um computador cliente e manipulá-los localmente.  
  
-   **Familiaridade com a linguagem**. Talvez você prefira uma linguagem específica com base na sua experiência atual e, portanto, escolha asserções Transact\-SQL ou Visual C\# ou condições de teste do Visual Basic.  
  
-   **Validação complicada**. Em alguns casos, você pode criar testes mais complexos no Visual C\# ou Visual Basic e validar os testes no cliente.  
  
-   **Simplicidade**. É geralmente mais simples usar uma condição de teste pré-definida do que escrever o script equivalente no Transact\-SQL.  
  
-   **Bibliotecas de validação herdadas**. Se você já tiver um código que executa a validação, poderá usá-lo em um teste de unidade do SQL Server, em vez de usar condições de teste.  
  
## <a name="mark-unit-test-methods-with-the-expected-exception"></a>Marcar métodos de teste de unidade com a exceção esperada  
Para marcar um método de teste de unidade do SQL Server com as exceções esperadas, adicione o seguinte atributo:  
  
```vb  
<ExpectedSqlException(MessageNumber=nnnnn, Severity=x, MatchFirstError=false, State=y)> _  
```  
  
```csharp  
[ExpectedSqlException(MessageNumber=nnnnn, Severity=x, MatchFirstError=false, State=y)]  
```  
  
Onde:  
  
-   *nnnnn* é o número da mensagem esperada; por exemplo, 14025  
  
-   *x* é o nível de severidade da exceção esperada  
  
-   *y* é o estado da exceção esperada  
  
Todos os parâmetros não especificados são ignorados. Você passa esses parâmetros para a instrução RAISERROR no código do banco de dados. Se você especificar MatchFirstError = true, o atributo corresponderá a qualquer SqlError na exceção. O comportamento padrão (MatchFirstError = true) é retornar somente o primeiro erro.  
  
Para obter um exemplo de como usar as exceções esperadas e um teste de unidade negativo do SQL Server, consulte [Passo a passo: criar e executar um teste de unidade do SQL Server](../ssdt/walkthrough-creating-and-running-a-sql-server-unit-test.md).  
  
## <a name="the-raiserror-statement"></a>A instrução RAISERROR  
  
> [!NOTE]  
> Use THROW em vez de RAISERROR. RAISERROR agora foi substituído.  
  
Você pode usar diretamente asserções de Transact\-SQL no servidor usando a instrução RAISERROR no script Transact\-SQL. Sua sintaxe é:  
  
**RAISERROR (@ErrorMessage, @ErrorSeverity, @ErrorState)**  
  
onde:  
  
@ErrorMessage é qualquer mensagem de erro definida pelo usuário. Você pode formatar essa cadeia de caracteres de mensagem semelhante à função printf_s.  
  
@ErrorSeverity é um nível de gravidade definido pelo usuário de 0 a 18.  
  
> [!NOTE]  
> Os valores '0' e '10' para o nível de severidade não ocasionam a falha do teste de unidade do SQL Server. Você pode usar qualquer outro valor no intervalo de 0 a 18 para provocar a falha do teste.  
  
@ErrorState é um número inteiro arbitrário de 1 a 127. Você pode usar esse número inteiro para fazer a distinção entre as ocorrências de um único erro gerado em locais diferentes no código.  
  
Para saber mais, confira [RAISERROR (Transact-SQL)](https://msdn.microsoft.com/library/ms178592.aspx). Confira um exemplo de como usar RAISERROR em um teste de unidade do SQL Server no tópico [Como gravar um teste de unidade do SQL Server executado no escopo de uma única transação](../ssdt/how-to-write-sql-server-unit-test-that-runs-in-single-transaction-scope.md).  
  
## <a name="see-also"></a>Consulte Também  
[Criando e definindo testes de unidade do SQL Server](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[Usar condições de teste nos testes de unidade do SQL Server](../ssdt/using-test-conditions-in-sql-server-unit-tests.md)  
[Verificar o código do banco de dados usando os testes de unidade do SQL Server](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
[Como abrir um teste de unidade do SQL Server para edição](../ssdt/how-to-open-a-sql-server-unit-test-to-edit.md)  
  
