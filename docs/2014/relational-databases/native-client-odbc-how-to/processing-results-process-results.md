---
title: Processar resultados (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- processing results [ODBC]
ms.assetid: 4810fe3f-78ee-4f0d-8bcc-a4659fbcf46f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 57fff62c09a23a416c3e65d7aa14604b4c513915
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48062566"
---
# <a name="process-results-odbc"></a>Processar resultados (ODBC)
    
### <a name="to-process-results"></a>Para processar resultados  
  
1.  Recupere informações do conjunto de resultados.  
  
2.  Se forem usadas colunas associadas, para cada coluna à qual deseja associar, chame [SQLBindCol](../native-client-odbc-api/sqlbindcol.md) para associar um buffer de programa à coluna.  
  
3.  Para cada linha no conjunto de resultados:  
  
    -   Chame [SQLFetch](http://go.microsoft.com/fwlink/?LinkId=58401) para acessar a próxima linha.  
  
    -   Se forem usadas colunas associadas, use os dados disponíveis agora nos buffers de coluna associados.  
  
    -   Se forem usadas colunas desassociadas, chame [SQLGetData](../native-client-odbc-api/sqlgetdata.md) uma ou mais vezes para obter os dados dessas colunas depois da última coluna associada. As chamadas a `SQLGetData` deveriam estar em ordem crescente de número de coluna.  
  
    -   Chame `SQLGetData` várias vezes para obter dados de uma coluna de textos ou imagens.  
  
4.  Quando [SQLFetch](http://go.microsoft.com/fwlink/?LinkId=58401) sinalizar o término do conjunto de resultados retornando SQL_NO_DATA, chame [SQLMoreResults](../native-client-odbc-api/sqlmoreresults.md) para determinar se há outro conjunto de resultados disponível.  
  
    -   Se SQL_SUCCESS for retornado, outro conjunto de resultados estará disponível.  
  
    -   Se SQL_NO_DATA for retornado, nenhum outro conjunto de resultados estará disponível.  
  
    -   Se SQL_SUCCESS_WITH_INFO ou SQL_ERROR for retornado, chame [SQLGetDiagRec](http://go.microsoft.com/fwlink/?LinkId=58402) para determinar se a saída de uma instrução PRINT ou RAISERROR estará disponível.  
  
         Se parâmetros de instrução associados forem usados para parâmetros de saída ou o valor retornado de um procedimento armazenado, use os dados disponíveis agora nos buffers de parâmetro associados. Além disso, quando são usados parâmetros associados, cada chamada para [SQLExecute](http://go.microsoft.com/fwlink/?LinkId=58400) ou [SQLExecDirect](http://go.microsoft.com/fwlink/?LinkId=58399) terá executado a instrução SQL por *S* vezes, em que *S* é o número de elementos na matriz de parâmetros associados. Isso significa que haverá *S* conjuntos de resultados a serem processados, em que cada conjunto consiste em todos os conjuntos de resultados, parâmetros de saída e códigos de retorno normalmente retornados por uma única execução da instrução SQL.  
  
    > [!NOTE]  
    >  Quando um conjunto de resultados contém linhas computadas, cada linha computada é disponibilizada como um conjunto de resultados separado. Esses conjuntos de resultados computados são intercalados nas linhas normais e dividem as linhas normais em vários conjuntos de resultados.  
  
5.  Outra opção é chamar [SQLFreeStmt](../native-client-odbc-api/sqlfreestmt.md) com SQL_UNBIND para liberar qualquer buffer de coluna associado.  
  
6.  Se outro conjunto de resultados estiver disponível, vá para a Etapa 1.  
  
> [!NOTE]  
>  Para cancelar o processamento de um conjunto de resultados antes que [SQLFetch](http://go.microsoft.com/fwlink/?LinkId=58401) retorne SQL_NO_DATA, chame [SQLCloseCursor](../native-client-odbc-api/sqlclosecursor.md).  
  
## <a name="see-also"></a>Consulte também  
 [Tópicos explicativos de resultados de processamento &#40;ODBC&#41;](../../database-engine/dev-guide/processing-results-how-to-topics-odbc.md)  
  
  
