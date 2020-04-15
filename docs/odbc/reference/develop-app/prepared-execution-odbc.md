---
title: Execução Preparada ODBC | Microsoft Docs
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
ms.openlocfilehash: 147ca85b21296575ff55afbe66ab286cc4824fae
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282306"
---
# <a name="prepared-execution-odbc"></a>Execução preparada ODBC
Execução preparada é uma maneira eficiente de executar uma declaração mais de uma vez. A declaração é primeiramente compilada, ou *preparada,* em um plano de acesso. O plano de acesso é então executado uma ou mais vezes posteriormente. Para obter mais informações sobre planos de acesso, consulte [Processando uma declaração SQL](../../../odbc/reference/processing-a-sql-statement.md).  
  
 A execução preparada é comumente usada por aplicativos verticais e personalizados para executar repetidamente a mesma declaração SQL parametrizada. Por exemplo, o código a seguir prepara uma declaração para atualizar os preços de diferentes partes. Em seguida, executa a declaração várias vezes com diferentes valores de parâmetro cada vez.  
  
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
  
 A execução preparada é mais rápida do que a execução direta para declarações executadas mais de uma vez, principalmente porque a instrução é compilada apenas uma vez; as declarações executadas diretamente são compiladas cada vez que são executadas. A execução preparada também pode fornecer uma redução no tráfego de rede porque o motorista pode enviar um identificador de plano de acesso para a fonte de dados cada vez que a declaração é executada, em vez de uma declaração SQL inteira, se a fonte de dados suportar identificadores de plano de acesso.  
  
 O aplicativo pode recuperar os metadados para o conjunto de resultados após a declaração ser preparada e antes de ser executada. No entanto, a devolução de metadados para declarações preparadas e não executadas é cara para alguns drivers e deve ser evitada por aplicativos interoperáveis, se possível. Para obter mais informações, consulte [Metadados de conjunto de resultados](../../../odbc/reference/develop-app/result-set-metadata.md).  
  
 A execução preparada não deve ser usada para instruções executadas uma única vez. Para tais instruções, é um pouco mais lento do que a execução direta porque requer uma chamada de função ODBC adicional.  
  
> [!IMPORTANT]  
>  Cometer ou reverter uma transação, seja ligando explicitamente para **o SQLEndTran** ou trabalhando no modo de confirmação automática, faz com que algumas fontes de dados excluam os planos de acesso de todas as declarações em uma conexão. Para obter mais informações, consulte as opções de SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR na descrição da função [SQLGetInfo.](../../../odbc/reference/syntax/sqlgetinfo-function.md)  
  
 Para preparar e executar uma declaração, o aplicativo:  
  
1.  Chama **SQLPrepare** e passa-a uma string contendo a declaração SQL.  
  
2.  Define os valores de quaisquer parâmetros. Os parâmetros podem ser definidos antes ou depois de preparar a declaração. Para obter mais informações, consulte [Parâmetros de declaração,](../../../odbc/reference/develop-app/statement-parameters.md)mais tarde nesta seção.  
  
3.  Chama **SQLExecute** e faz qualquer processamento adicional necessário, como buscar dados.  
  
4.  Repete as etapas 2 e 3 conforme necessário.  
  
5.  Quando **o SQLPrepare** é chamado, o driver:  
  
    -   Modifica a declaração SQL para usar a gramática SQL da fonte de dados sem analisar a declaração. Isso inclui a substituição das seqüências de fuga discutidas em [Seqüências de Fuga no ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md). O aplicativo pode recuperar a forma modificada de uma declaração SQL ligando para **SQLNativeSql**. As seqüências de escape não são substituídas se o atributo de declaração SQL_ATTR_NOSCAN estiver definido.  
  
    -   Envia a declaração à fonte de dados para preparação.  
  
    -   Armazena o identificador do plano de acesso retornado para execução posterior (se a preparação foi bem sucedida) ou retorna quaisquer erros (se a preparação falhou). Os erros incluem erros sintáticos, como SQLSTATE 42000 (erro de sintaxe ou violação de acesso) e erros semânticos, como SQLSTATE 42S02 (tabela base ou exibição não encontrada).  
  
        > [!NOTE]  
        >  Alguns drivers não retornam erros neste momento, mas os devolvem quando a declaração é executada ou quando as funções do catálogo são chamadas. Assim, **o SQLPrepare** pode parecer ter tido sucesso quando, na verdade, falhou.  
  
6.  Quando **o SQLExecute** é chamado, o driver:  
  
    -   Recupera os valores atuais do parâmetro e converte-os conforme necessário. Para obter mais informações, consulte [Parâmetros de declaração,](../../../odbc/reference/develop-app/statement-parameters.md)mais tarde nesta seção.  
  
    -   Envia o identificador do plano de acesso e os valores dos parâmetros convertidos para a fonte de dados.  
  
    -   Retorna qualquer erro. Estes são geralmente erros de tempo de execução, como SQLSTATE 24000 (estado cursor inválido). No entanto, alguns motoristas retornam erros sintáticos e semânticos neste momento.  
  
 Se a fonte de dados não suportar a preparação da declaração, o motorista deve emulá-la na medida do possível. Por exemplo, o driver pode não fazer nada quando **o SQLPrepare** é chamado e, em seguida, executar a execução direta da declaração quando **o SQLExecute** é chamado.  
  
 Se a fonte de dados suportar a verificação de sintaxe sem execução, o driver poderá enviar a declaração para verificação quando **o SQLPrepare** for chamado e enviar a declaração para execução quando **o SQLExecute** for chamado.  
  
 Se o driver não puder emular a preparação da declaração, ele armazena a declaração quando o **SQLPrepare** é chamado e o envia para execução quando **o SQLExecute** é chamado.  
  
 Como a preparação da declaração emulada não é perfeita, **o SQLExecute** pode retornar quaisquer erros normalmente retornados pelo **SQLPrepare**.
