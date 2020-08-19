---
description: Obter dados Long
title: Obtendo dados longos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- long data [ODBC]
- fetches [ODBC], long data
- result sets [ODBC], fetching
- SQLGetData function [ODBC], getting long data
- retrieving long data [ODBC]
ms.assetid: 6ccb44bc-8695-4bad-91af-363ef22bdb85
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c3a40bc3f4f65f747776d747d79868340de06f53
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429278"
---
# <a name="getting-long-data"></a>Obter dados Long
DBMSs definem *dados longos* como qualquer caractere ou dados binários em um determinado tamanho, como 255 caracteres. Esses dados podem ser pequenos o suficiente para serem armazenados em um único buffer, como uma descrição de parte de vários milhares de caracteres. No entanto, pode ser muito longo para armazenar na memória, como documentos de texto longo ou bitmaps. Como esses dados não podem ser armazenados em um único buffer, eles são recuperados do driver em partes com **SQLGetData** depois que os outros dados na linha são buscados.  
  
> [!NOTE]  
>  Um aplicativo pode realmente recuperar qualquer tipo de dados com **SQLGetData**, não apenas dados longos, embora apenas dados de caracteres e binários possam ser recuperados em partes. No entanto, se os dados forem pequenos o suficiente para caber em um único buffer, geralmente não há motivo para usar **SQLGetData**. É muito mais fácil associar um buffer à coluna e permitir que o driver retorne os dados no buffer.  
  
 Para recuperar dados longos de uma coluna, um aplicativo primeiro chama **SQLFetchScroll** ou **SQLFetch** para mover para uma linha e buscar os dados para as colunas associadas. O aplicativo então chama **SQLGetData**. **SQLGetData** tem os mesmos argumentos que **SQLBindCol**: um identificador de instrução; um número de coluna; o tipo de dados C, o endereço e o comprimento de bytes de uma variável de aplicativo; e o endereço de um buffer de comprimento/indicador. Ambas as funções têm os mesmos argumentos porque executam essencialmente a mesma tarefa: elas descrevem uma variável de aplicativo para o driver e especificam que os dados de uma determinada coluna devem ser retornados nessa variável. As principais diferenças são que **SQLGetData** é chamado depois que uma linha é buscada (e, às vezes, é referida como *associação tardia* por esse motivo) e que a associação especificada por **SQLGetData** dura apenas a duração da chamada.  
  
 Em relação a uma única coluna, **SQLGetData** se comporta como **SQLFetch**: recupera os dados da coluna, converte-os no tipo da variável do aplicativo e retorna-os nessa variável. Ele também retorna o comprimento de bytes dos dados no buffer de comprimento/indicador. Para obter mais informações sobre como **SQLFetch** retorna dados, consulte [buscando uma linha de dados](../../../odbc/reference/develop-app/fetching-a-row-of-data.md).  
  
 **SQLGetData** difere de **SQLFetch** em um aspecto importante. Se ele for chamado mais de uma vez em sucessivamente para a mesma coluna, cada chamada retornará uma parte sucessiva dos dados. Cada chamada, exceto a última chamada, retorna SQL_SUCCESS_WITH_INFO e SQLSTATE 01004 (dados de cadeia de caracteres, truncados à direita); a última chamada retorna SQL_SUCCESS. É assim que o **SQLGetData** é usado para recuperar dados longos em partes. Quando não há mais dados a serem retornados, **SQLGetData** retorna SQL_NO_DATA. O aplicativo é responsável por colocar os dados longos juntos, o que pode significar concatenar as partes dos dados. Cada parte é terminada em nulo; o aplicativo deve remover o caractere de terminação nula se estiver concatenando as partes. A recuperação de dados em partes pode ser feita para indicadores de comprimento variável, bem como para outros dados longos. O valor retornado no buffer de comprimento/indicador diminui em cada chamada pelo número de bytes retornados na chamada anterior, embora seja comum que o driver não possa descobrir a quantidade de dados disponíveis e retornar um comprimento de bytes de SQL_NO_TOTAL. Por exemplo:   
  
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
  
 Há várias restrições no uso de **SQLGetData**. Geralmente, as colunas acessadas com **SQLGetData**:  
  
-   Deve ser acessado na ordem de aumento do número da coluna (devido à maneira como as colunas de um conjunto de resultados são lidas da fonte de dados). Por exemplo, é um erro chamar **SQLGetData** para a coluna 5 e, em seguida, chamá-la para a coluna 4.  
  
-   Não pode ser associado.  
  
-   Deve ter um número de coluna superior à última coluna associada. Por exemplo, se a última coluna associada for a coluna 3, será um erro para chamar **SQLGetData** para a coluna 2. Por esse motivo, os aplicativos devem fazer com que você coloque colunas de dados longas no final da lista de seleção.  
  
-   Não poderá ser usado se **SQLFetch** ou **SQLFetchScroll** tiver sido chamado para recuperar mais de uma linha. Para obter mais informações, consulte [usando cursores de bloco](../../../odbc/reference/develop-app/using-block-cursors.md).  
  
 Alguns drivers não impõem essas restrições. Os aplicativos interoperáveis devem presumir que existam ou determinar quais restrições não são impostas chamando **SQLGetInfo** com a opção SQL_GETDATA_EXTENSIONS.  
  
 Se o aplicativo não precisar de todos os dados em uma coluna de dados binários ou de caracteres, ele poderá reduzir o tráfego de rede em drivers baseados em DBMS definindo o atributo de instrução SQL_ATTR_MAX_LENGTH antes de executar a instrução. Isso restringe o número de bytes de dados que serão retornados para qualquer caractere ou coluna binária. Por exemplo, suponha que uma coluna contenha documentos de texto longo. Um aplicativo que procura a tabela que contém essa coluna pode ter que exibir apenas a primeira página de cada documento. Embora esse atributo de instrução possa ser simulado no driver, não há motivo para fazer isso. Em particular, se um aplicativo quiser truncar dados de caractere ou binário, ele deverá associar um pequeno buffer à coluna com **SQLBindCol** e deixar que o driver TRUNCATE os dados.
