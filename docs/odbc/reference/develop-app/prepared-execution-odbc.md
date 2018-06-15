---
title: A execução ODBC preparada | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- prepared execution [ODBC]
- SQL statements [ODBC], prepared execution
- SQL statements [ODBC], executing
ms.assetid: f08c8a98-31ee-48b2-9dbf-6f31c2166dbb
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1e03123e34834033b4c53fb1eb5818f6c78def82
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32913171"
---
# <a name="prepared-execution-odbc"></a>Execução preparada ODBC
Execução preparada é uma maneira eficiente de executar uma instrução mais de uma vez. A instrução é compilada pela primeira vez, ou *preparado,* em um plano de acesso. O plano de acesso é executada uma ou mais vezes em um momento posterior. Para obter mais informações sobre planos de acesso, consulte [processar uma instrução SQL](../../../odbc/reference/processing-a-sql-statement.md).  
  
 Execução preparada geralmente é usada por aplicativos de verticais e personalizados para executar repetidamente a mesma instrução SQL com parâmetros. Por exemplo, o código a seguir prepara uma instrução para atualizar os preços de partes diferentes. Em seguida, executar a instrução várias vezes com valores de parâmetros diferentes cada vez.  
  
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
  
 Execução preparada é mais rápida do que a execução direta para instruções executadas mais de uma vez, principalmente porque a instrução é compilada somente uma vez; instruções executadas diretamente são compiladas sempre que eles são executados. Execução preparada também pode fornecer que uma redução no tráfego de rede porque o driver pode enviar um identificador de plano de acesso à fonte de dados cada vez que a instrução é executada, em vez de toda uma instrução SQL, se o acesso a dados fonte dá suporte a identificadores de plano.  
  
 O aplicativo pode recuperar os metadados do conjunto de resultados após a instrução é preparada e antes de ser executado. No entanto, retornando metadados para preparado, instruções desfazê é caras para alguns drivers e deve ser evitado por aplicativos interoperáveis se possível. Para obter mais informações, consulte [metadados de conjunto de resultados](../../../odbc/reference/develop-app/result-set-metadata.md).  
  
 A execução preparada não deve ser usada para instruções executadas uma única vez. Para tais instruções, é um pouco mais lenta que a execução direta porque requer uma chamada de função ODBC adicional.  
  
> [!IMPORTANT]  
>  Confirmar ou reverter uma transação, ou explicitamente chamando **SQLEndTran** ou trabalhando no modo de confirmação automática, faz com que algumas fontes de dados excluir os planos de acesso para todas as instruções em uma conexão. Para obter mais informações, consulte as opções SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR no [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descrição da função.  
  
 Para preparar e executar uma instrução, o aplicativo:  
  
1.  Chamadas **SQLPrepare** e passa uma cadeia de caracteres que contém a instrução SQL.  
  
2.  Define os valores de quaisquer parâmetros. Parâmetros podem ser definidos, na verdade, antes ou depois de preparar a instrução. Para obter mais informações, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md), mais adiante nesta seção.  
  
3.  Chamadas **SQLExecute** e executa qualquer processamento adicional é necessário, como buscar dados.  
  
4.  Repete as etapas 2 e 3 conforme necessário.  
  
5.  Quando **SQLPrepare** é chamado, o driver:  
  
    -   Modifica a instrução SQL para usar a gramática SQL da fonte de dados sem analisar a instrução. Isso inclui substituindo as sequências de escape discutidas [sequências de Escape no ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md). O aplicativo pode recuperar o formulário de modificação de uma instrução SQL chamando **SQLNativeSql**. Sequências de escape não são substituídas, se o atributo de instrução SQL_ATTR_NOSCAN está definido.  
  
    -   Envia a instrução para a fonte de dados para preparação.  
  
    -   Armazena o identificador do plano de acesso retornado para execução posterior (se a preparação bem-sucedida) ou retorna erros (se a preparação da falha). Os erros incluem erros sintáticos como SQLSTATE 42000 (sintaxe ou violação de acesso) e erros semânticos como SQLSTATE 42S02 (Base a tabela ou exibição não encontrado).  
  
        > [!NOTE]  
        >  Alguns drivers não retornar erros neste ponto, mas retorná-los em vez disso, quando a instrução é executada ou quando são chamadas de funções de catálogo. Portanto, **SQLPrepare** podem parecer tiveram êxito quando na verdade ele falhou.  
  
6.  Quando **SQLExecute** é chamado, o driver:  
  
    -   Recupera os valores de parâmetro atuais e converte-os conforme necessário. Para obter mais informações, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md), mais adiante nesta seção.  
  
    -   Envia o identificador do plano de acesso e os valores de parâmetro convertido para a fonte de dados.  
  
    -   Retorna erros. Esses são erros de tempo de execução geralmente como SQLSTATE 24000 (estado de cursor inválido). No entanto, alguns drivers de retornam erros de sintaxe e semânticos neste momento.  
  
 Se a fonte de dados não der suporte a preparação da instrução, o driver deve emulá-lo até o limite permitido. Por exemplo, o driver pode fazer nada quando **SQLPrepare** é chamado e, em seguida, executar a execução direta da instrução quando **SQLExecute** é chamado.  
  
 Se a fonte de dados oferece suporte à verificação sem execução de sintaxe, o driver pode enviar a instrução para verificar quando **SQLPrepare** é chamado e enviar a instrução para execução quando **SQLExecute** é chamado.  
  
 Se o driver não pode emular a preparação da instrução, ele armazena a instrução quando **SQLPrepare** é chamado e o envia para execução quando **SQLExecute** é chamado.  
  
 Como preparação emulado não é perfeita, **SQLExecute** pode retornar os erros normalmente retornados por **SQLPrepare**.
