---
description: Execução preparada ODBC
title: Execução preparada ODBC | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6141af2cde7106419ab1eb68f86d5817f055aab2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465738"
---
# <a name="prepared-execution-odbc"></a>Execução preparada ODBC
A execução preparada é uma maneira eficiente de executar uma instrução mais de uma vez. A instrução é primeiro compilada ou *preparada* em um plano de acesso. O plano de acesso é então executado uma ou mais vezes em um momento posterior. Para obter mais informações sobre planos de acesso, consulte [processando uma instrução SQL](../../../odbc/reference/processing-a-sql-statement.md).  
  
 A execução preparada é comumente usada por aplicativos verticais e personalizados para executar repetidamente a mesma instrução SQL parametrizada. Por exemplo, o código a seguir prepara uma instrução para atualizar os preços de diferentes partes. Em seguida, ele executa a instrução várias vezes com valores de parâmetro diferentes a cada vez.  
  
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
  
 A execução preparada é mais rápida do que a execução direta de instruções executadas mais de uma vez, principalmente porque a instrução é compilada apenas uma vez; as instruções executadas diretamente são compiladas cada vez que são executadas. A execução preparada também pode fornecer uma redução no tráfego de rede, pois o driver pode enviar um identificador de plano de acesso para a fonte de dados cada vez que a instrução for executada, em vez de uma instrução SQL inteira, se a fonte de dados der suporte a identificadores de plano de acesso.  
  
 O aplicativo pode recuperar os metadados para o conjunto de resultados depois que a instrução é preparada e antes de ser executada. No entanto, retornar metadados para instruções preparadas e não executadas é caro para alguns drivers e deve ser evitado por aplicativos interoperáveis, se possível. Para obter mais informações, consulte [metadados do conjunto de resultados](../../../odbc/reference/develop-app/result-set-metadata.md).  
  
 A execução preparada não deve ser usada para instruções executadas uma única vez. Para essas instruções, é um pouco mais lento do que a execução direta porque requer uma chamada de função ODBC adicional.  
  
> [!IMPORTANT]  
>  A confirmação ou reversão de uma transação, seja chamando explicitamente **SQLEndTran** ou trabalhando no modo de confirmação automática, faz com que algumas fontes de dados excluam os planos de acesso para todas as instruções em uma conexão. Para obter mais informações, consulte as opções SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR na descrição da função [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) .  
  
 Para preparar e executar uma instrução, o aplicativo:  
  
1.  Chama **SQLPrepare** e passa a ele uma cadeia de caracteres que contém a instrução SQL.  
  
2.  Define os valores de qualquer parâmetro. Os parâmetros podem realmente ser definidos antes ou depois da preparação da instrução. Para obter mais informações, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md), mais adiante nesta seção.  
  
3.  Chama **SQLExecute** e faz qualquer processamento adicional necessário, como buscar dados.  
  
4.  Repete as etapas 2 e 3, conforme necessário.  
  
5.  Quando **SQLPrepare** for chamado, o driver:  
  
    -   Modifica a instrução SQL para usar a gramática SQL da fonte de dados sem analisar a instrução. Isso inclui substituir as sequências de escape abordadas em [sequências de escape no ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md). O aplicativo pode recuperar a forma modificada de uma instrução SQL chamando **SQLNativeSql**. As sequências de escape não serão substituídas se o atributo da instrução SQL_ATTR_NOSCAN for definido.  
  
    -   Envia a instrução à fonte de dados para preparação.  
  
    -   Armazena o identificador do plano de acesso retornado para execução posterior (se a preparação for bem-sucedida) ou retorna quaisquer erros (se a preparação falhar). Os erros incluem erros sintáticos como SQLSTATE 42000 (erro de sintaxe ou violação de acesso) e erros semânticos como SQLSTATE 42S02 (tabela base ou exibição não encontrada).  
  
        > [!NOTE]  
        >  Alguns drivers não retornam erros neste ponto, mas, em vez disso, retornam-os quando a instrução é executada ou quando as funções de catálogo são chamadas. Portanto, o **SQLPrepare** pode parecer ter êxito quando, na verdade, falhou.  
  
6.  Quando **SQLExecute** é chamado, o driver:  
  
    -   Recupera os valores de parâmetro atuais e os converte conforme necessário. Para obter mais informações, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md), mais adiante nesta seção.  
  
    -   Envia o identificador do plano de acesso e os valores de parâmetro convertidos para a fonte de dados.  
  
    -   Retorna quaisquer erros. Esses são geralmente erros de tempo de execução como o SQLSTATE 24000 (estado de cursor inválido). No entanto, alguns drivers retornam erros sintáticos e semânticos neste momento.  
  
 Se a fonte de dados não oferecer suporte à preparação de instrução, o driver deverá emular isso na extensão possível. Por exemplo, o driver pode não fazer nada quando **SQLPrepare** é chamado e, em seguida, executa a execução direta da instrução quando **SQLExecute** é chamado.  
  
 Se a fonte de dados der suporte à verificação de sintaxe sem execução, o driver poderá enviar a instrução para verificar quando **SQLPrepare** é chamado e enviar a instrução para execução quando **SQLExecute** é chamado.  
  
 Se o driver não puder emular a preparação da instrução, ele armazenará a instrução quando **SQLPrepare** for chamado e o enviará para execução quando **SQLExecute** for chamado.  
  
 Como a preparação da instrução emulada não é perfeita, **SQLExecute** pode retornar erros normalmente retornados por **SQLPrepare**.
