---
title: A execução ODBC preparada | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- prepared execution [ODBC]
- SQL statements [ODBC], prepared execution
- SQL statements [ODBC], executing
ms.assetid: f08c8a98-31ee-48b2-9dbf-6f31c2166dbb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2107ca1eeecc6fad24311c5bce629784ae4ceff0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68023285"
---
# <a name="prepared-execution-odbc"></a>Execução preparada ODBC
Execução preparada é uma maneira eficiente para executar uma instrução mais de uma vez. A instrução é compilada pela primeira vez, ou *preparado,* em um plano de acesso. O plano de acesso é, então, executado uma ou mais vezes em um momento posterior. Para obter mais informações sobre os planos de acesso, consulte [processar uma instrução SQL](../../../odbc/reference/processing-a-sql-statement.md).  
  
 Execução preparada normalmente é usada por aplicativos verticais e personalizados para executar repetidamente a mesma instrução SQL com parâmetros. Por exemplo, o código a seguir prepara uma instrução para atualizar os preços das diferentes partes. Em seguida, executar a instrução várias vezes com valores de parâmetros diferentes cada vez.  
  
```  
SQLREAL       Price;  
SQLUINTEGER   PartID;  
SQLINTEGER    PartIDInd = 0, PriceInd = 0;  
  
// Prepare a statement to update salaries in the Employees table.  
SQLPrepare(hstmt, "UPDATE Parts SET Price = ? WHERE PartID = ?", SQL_NTS);  
  
// Bind Price to the parameter for the Price column and PartID to  
// the parameter for the PartID column.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  &Price, 0, &PriceInd);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 10, 0,  
                  &PartID, 0, &PartIDInd);  
  
// Repeatedly execute the statement.  
while (GetPrice(&PartID, &Price)) {  
   SQLExecute(hstmt);  
}  
```  
  
 Execução preparada é mais rápida que a execução direta para instruções executadas mais de uma vez, principalmente porque a instrução é compilada somente uma vez. instruções executadas diretamente são compiladas sempre que forem executados. Execução preparada também pode fornecer que uma redução no tráfego de rede porque o driver pode enviar um identificador de plano de acesso à fonte de dados cada vez que a instrução é executada, em vez de uma instrução SQL inteira, se o acesso a dados fonte dá suporte a identificadores de plano.  
  
 O aplicativo pode recuperar os metadados do conjunto de resultados após a instrução é preparada e antes de ser executado. No entanto, retornando metadados para preparado, instruções não executadas é caras para alguns drivers e deve ser evitada pelos aplicativos interoperáveis se possível. Para obter mais informações, consulte [metadados de conjunto de resultados](../../../odbc/reference/develop-app/result-set-metadata.md).  
  
 A execução preparada não deve ser usada para instruções executadas uma única vez. Para tais instruções, é um pouco mais lento do que a execução direta porque ele requer uma chamada de função ODBC adicional.  
  
> [!IMPORTANT]  
>  Confirmar ou reverter uma transação, ou explicitamente chamando **SQLEndTran** ou trabalhando no modo de confirmação automática, faz com que algumas fontes de dados excluir os planos de acesso para todas as instruções em uma conexão. Para obter mais informações, consulte as opções SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR na [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descrição da função.  
  
 Para preparar e executar uma instrução, o aplicativo:  
  
1.  Chamadas **SQLPrepare** e passa uma cadeia de caracteres que contém a instrução SQL.  
  
2.  Define os valores de quaisquer parâmetros. Parâmetros podem ser definidos, na verdade, antes ou depois de preparar a instrução. Para obter mais informações, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md), mais adiante nesta seção.  
  
3.  Chamadas **SQLExecute** e executa qualquer processamento adicional que é necessário, como buscar dados.  
  
4.  Repete as etapas 2 e 3 conforme necessário.  
  
5.  Quando **SQLPrepare** é chamado, o driver:  
  
    -   Modifica a instrução SQL para usar a gramática SQL da fonte de dados sem analisar a instrução. Isso inclui substituindo as sequências de escape discutidas [sequências de Escape no ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md). O aplicativo pode recuperar o formulário modificado de uma instrução SQL, chamando **SQLNativeSql**. Sequências de escape não são substituídas, se o atributo de instrução SQL_ATTR_NOSCAN está definido.  
  
    -   Envia a instrução para a fonte de dados para preparação.  
  
    -   Armazena o identificador de plano de acesso retornado para execução posterior (se a preparação bem-sucedida) ou retorna erros (se a preparação da falha). Os erros incluem erros sintáticos, como o SQLSTATE 42000 (sintaxe ou violação de acesso) e erros semânticos, como o SQLSTATE 42S02 (Base a tabela ou exibição não encontrado).  
  
        > [!NOTE]  
        >  Alguns drivers não retornar erros neste momento, mas retornar em vez disso, quando a instrução é executada ou quando são chamadas de funções de catálogo. Portanto, **SQLPrepare** podem parecer ter êxito quando na verdade ele falhou.  
  
6.  Quando **SQLExecute** é chamado, o driver:  
  
    -   Recupera os valores de parâmetro atuais e converte-os conforme necessário. Para obter mais informações, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md), mais adiante nesta seção.  
  
    -   Envia o identificador do plano de acesso e os valores de parâmetro convertido para a fonte de dados.  
  
    -   Retorna todos os erros. Esses são erros de tempo de execução geralmente como o SQLSTATE 24000 (estado de cursor inválido). No entanto, alguns drivers retornam erros sintáticos e semânticos neste momento.  
  
 Se a fonte de dados não der suporte a preparação da instrução, o driver deve emulá-lo a medida do possível. Por exemplo, o driver pode fazer nada quando **SQLPrepare** é chamado e, em seguida, realizar a execução direta da instrução quando **SQLExecute** é chamado.  
  
 Se a fonte de dados oferece suporte à verificação sem execução de sintaxe, o driver pode enviar a instrução de verificação quando **SQLPrepare** é chamado e enviar a instrução para execução quando **SQLExecute** é chamado.  
  
 Se o driver não pode emular a preparação da instrução, ele armazena a instrução quando **SQLPrepare** é chamado e a envia para execução quando **SQLExecute** é chamado.  
  
 Como preparação da instrução emulado não é perfeita, **SQLExecute** pode retornar os erros normalmente retornados por **SQLPrepare**.
