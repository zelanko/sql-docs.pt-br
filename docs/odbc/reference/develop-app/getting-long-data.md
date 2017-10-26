---
title: Obtendo dados Long | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- long data [ODBC]
- fetches [ODBC], long data
- result sets [ODBC], fetching
- SQLGetData function [ODBC], getting long data
- retrieving long data [ODBC]
ms.assetid: 6ccb44bc-8695-4bad-91af-363ef22bdb85
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0ea30c211e3cfd66acf1588ef9ca2a45fd1037d1
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="getting-long-data"></a>Obtendo dados Long
Definem DBMSs *dados long* como qualquer caractere ou dados binários em um determinado tamanho, como 255 caracteres. Esses dados podem ser pequenos o suficiente para ser armazenado em um único buffer, como uma descrição da parte de vários milhares de caracteres. No entanto, talvez seja muito longo para armazenar na memória, como documentos de texto longo ou bitmaps. Como esses dados não podem ser armazenadas em um único buffer, ele será recuperado do driver em partes com **SQLGetData** depois que os outros dados na linha foi buscados.  
  
> [!NOTE]  
>  Um aplicativo, na verdade, pode recuperar qualquer tipo de dados com **SQLGetData**, longo não apenas dados, embora apenas caracteres e dados binários podem ser recuperados em partes. No entanto, se os dados são pequenos o suficiente para caber em um único buffer, há geralmente não há motivo para usar **SQLGetData**. É muito mais fácil associar um buffer para a coluna e permitir que o driver de retornar os dados no buffer.  
  
 Para recuperar dados longos de uma coluna, um aplicativo primeiro chama **SQLFetchScroll** ou **SQLFetch** para mover para uma linha e buscar os dados para colunas associadas. O aplicativo chama **SQLGetData**. **SQLGetData** tem os mesmos argumentos que **SQLBindCol**: um identificador de instrução; um número de coluna; o comprimento C de bytes, o endereço e o tipo de dados de uma variável de aplicativo; e o endereço de um buffer de comprimento/indicador. Ambas as funções têm os mesmos argumentos porque eles executam essencialmente a mesma tarefa: elas tanto descrevem uma variável de aplicativo para o driver e especificar que os dados para uma determinada coluna devem ser retornados na variável. As principais diferenças são que **SQLGetData** é chamado depois que uma linha é buscada (e às vezes é conhecido como *associação tardia* por esse motivo) e que a associação especificada por **SQLGetData ** dura apenas para a duração da chamada.  
  
 Em relação a uma única coluna, **SQLGetData** se comporta como **SQLFetch**: recupera os dados para a coluna, converte-o para o tipo de variável de aplicativo e retorna-o na variável. Ele também retorna o comprimento de bytes dos dados no buffer de comprimento/indicador. Para obter mais informações sobre como **SQLFetch** retorna dados, consulte [buscar uma linha de dados](../../../odbc/reference/develop-app/fetching-a-row-of-data.md).  
  
 **SQLGetData** difere **SQLFetch** em um aspecto importante. Se for chamado mais de uma vez em sucessão para a mesma coluna, cada chamada retorne sucessiva parte dos dados. Cada chamada exceto a última chamada retorna SQL_SUCCESS_WITH_INFO e SQLSTATE 01004 (cadeia de caracteres dados à direita truncados); a última chamada retorna SQL_SUCCESS. Isso é como **SQLGetData** é usado para recuperar dados longos em partes. Quando não há mais dados para retornar, **SQLGetData** retorna SQL_NO_DATA. O aplicativo é responsável por reunir os dados longos, que pode significar concatenando as partes dos dados. Cada parte é terminada em nulo; o aplicativo deve remover o caractere null de terminação se concatenando as partes. Recuperando dados em partes pode ser feito para indicadores de comprimento variável, bem como para outros dados long. O valor retornado a redução de buffer de comprimento/indicador em cada chamada pelo número de bytes retornados da chamada anterior, embora seja comum para o driver não conseguir descobrir a quantidade de dados disponíveis e retornar um comprimento de bytes de SQL_NO_TOTAL. Por exemplo:  
  
```  
// Declare a binary buffer to retrieve 5000 bytes of data at a time.  
SQLCHAR       BinaryPtr[5000];  
SQLUINTEGER   PartID;  
SQLINTEGER    PartIDInd, BinaryLenOrInd, NumBytes;  
SQLRETURN     rc;   
SQLHSTMT      hstmt;  
  
// Create a result set containing the ID and picture of each part.  
SQLExecDirect(hstmt, "SELECT PartID, Picture FROM Pictures", SQL_NTS);  
  
// Bind PartID to the PartID column.  
SQLBindCol(hstmt, 1, SQL_C_ULONG, &PartID, 0, &PartIDInd);  
  
// Retrieve and display each row of data.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {  
   // Display the part ID and initialize the picture.  
   DisplayID(PartID, PartIDInd);  
   InitPicture();  
  
   // Retrieve the picture data in parts. Send each part and the number   
   // of bytes in each part to a function that displays it. The number   
   // of bytes is always 5000 if there were more than 5000 bytes   
   // available to return (cbBinaryBuffer > 5000). Code to check if   
   // rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
   while ((rc = SQLGetData(hstmt, 2, SQL_C_BINARY, BinaryPtr, sizeof(BinaryPtr),  
                           &BinaryLenOrInd)) != SQL_NO_DATA) {  
      NumBytes = (BinaryLenOrInd > 5000) || (BinaryLenOrInd == SQL_NO_TOTAL) ?  
                  5000 : BinaryLenOrInd;  
      DisplayNextPictPart(BinaryPtr, NumBytes);  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmt);  
```  
  
 Há várias restrições ao uso de **SQLGetData**. Em geral, as colunas são acessadas com **SQLGetData**:  
  
-   Deve ser acessado em ordem crescente número de coluna (devido à maneira como as colunas de um conjunto de resultados são lidos a partir da fonte de dados). Por exemplo, é um erro ao chamar **SQLGetData** coluna 5 e chamá-la para a coluna 4.  
  
-   Não pode ser associado.  
  
-   Deve ter um número de coluna maior que a última coluna associada. Por exemplo, se a última coluna associada for coluna 3, é um erro ao chamar **SQLGetData** para a coluna 2. Por esse motivo, a aplicativos assegure-se de colocar as colunas de dados longos no final da lista de seleção.  
  
-   Não pode ser usado se **SQLFetch** ou **SQLFetchScroll** foi chamado para recuperar mais de uma linha. Para obter mais informações, consulte [cursores em bloco usando](../../../odbc/reference/develop-app/using-block-cursors.md).  
  
 Alguns drivers não impor essas restrições. Aplicativos interoperáveis ou devem pressupor que eles existem ou determinam quais restrições não são impostas chamando **SQLGetInfo** com a opção SQL_GETDATA_EXTENSIONS.  
  
 Se o aplicativo não precisar de todos os dados em um caractere ou uma coluna de dados binários, ele pode reduzir o tráfego de rede em drivers baseados em DBMS, definindo o atributo da instrução SQL_ATTR_MAX_LENGTH antes de executar a instrução. Isso restringe o número de bytes de dados que serão retornados para qualquer caractere ou uma coluna binária. Por exemplo, suponha que uma coluna contiver documentos de texto longo. Um aplicativo que navega a tabela que contém esta coluna pode ter que exibir apenas a primeira página de cada documento. Embora esse atributo de instrução pode ser simulado no driver, não há nenhum motivo para fazer isso. Em particular, se um aplicativo deseja truncar caracteres ou dados binários, ele deve associar um buffer pequeno para a coluna com **SQLBindCol** e deixar que o driver truncar os dados.

