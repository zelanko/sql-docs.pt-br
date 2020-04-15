---
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
ms.openlocfilehash: da901c22eb26af063397b4af184179ebe5c75924
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298986"
---
# <a name="getting-long-data"></a>Obter dados Long
DBMSs *definem dados longos* como qualquer caractere ou dados binários em um determinado tamanho, como 255 caracteres. Esses dados podem ser pequenos o suficiente para serem armazenados em um único buffer, como uma descrição de parte de vários milhares de caracteres. No entanto, pode ser muito tempo para armazenar na memória, como documentos de texto longos ou bitmaps. Como esses dados não podem ser armazenados em um único buffer, ele é recuperado do driver em partes com **SQLGetData** depois que os outros dados da linha foram buscados.  
  
> [!NOTE]  
>  Um aplicativo pode realmente recuperar qualquer tipo de dados com **SQLGetData**, não apenas dados longos, embora apenas dados de caracteres e binários possam ser recuperados em partes. No entanto, se os dados são pequenos o suficiente para caber em um único buffer, geralmente não há razão para usar **SQLGetData**. É muito mais fácil vincular um buffer à coluna e deixar o driver retornar os dados no buffer.  
  
 Para recuperar dados longos de uma coluna, um aplicativo primeiro chama **SQLFetchScroll** ou **SQLFetch** para mover-se para uma linha e buscar os dados para colunas vinculadas. O aplicativo então chama **SQLGetData**. **SQLGetData** tem os mesmos argumentos **do SQLBindCol**: uma alça de declaração; um número de coluna; o tipo de dados C, endereço e comprimento de byte de uma variável de aplicação; e o endereço de um buffer de comprimento/indicador. Ambas as funções têm os mesmos argumentos porque executam essencialmente a mesma tarefa: Ambas descrevem uma variável de aplicativo para o driver e especificam que os dados de uma determinada coluna devem ser devolvidos nessa variável. As principais diferenças são que **o SQLGetData** é chamado depois que uma linha é buscada (e às vezes é referida como *vinculação tardia* por essa razão) e que a vinculação especificada pelo **SQLGetData** dura apenas durante a duração da chamada.  
  
 Em relação a uma única coluna, **sqlGetData** se comporta como **SQLFetch**: Ele recupera os dados para a coluna, converte-os para o tipo da variável de aplicativo e retorna-os nessa variável. Ele também retorna o comprimento do byte dos dados no buffer de comprimento/indicador. Para obter mais informações sobre como **o SQLFetch** retorna dados, consulte [Buscar uma linha de dados](../../../odbc/reference/develop-app/fetching-a-row-of-data.md).  
  
 **SQLGetData** difere do **SQLFetch** em um aspecto importante. Se for chamado mais de uma vez em sucessão para a mesma coluna, cada chamada retorna uma parte sucessiva dos dados. Cada chamada, exceto a última chamada, retorna SQL_SUCCESS_WITH_INFO e SQLSTATE 01004 (dados de string, truncados à direita); a última chamada retorna SQL_SUCCESS. É assim que **o SQLGetData** é usado para recuperar dados longos em partes. Quando não há mais dados para retornar, **o SQLGetData** retorna SQL_NO_DATA. O aplicativo é responsável por juntar os dados longos, o que pode significar concatenar as partes dos dados. Cada parte é nula; o aplicativo deve remover o caractere de rescisão nula se concatenar as peças. A recuperação de dados em partes pode ser feita para marcadores de comprimento variável, bem como para outros dados longos. O valor retornado no buffer de comprimento/indicador diminui em cada chamada pelo número de bytes retornados na chamada anterior, embora seja comum que o motorista não consiga descobrir a quantidade de dados disponíveis e retornar um byte de SQL_NO_TOTAL. Por exemplo:  
  
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
  
 Existem várias restrições ao uso **do SQLGetData**. Geralmente, as colunas acessadas com **SQLGetData**:  
  
-   Deve ser acessado por ordem de aumento do número da coluna (devido à forma como as colunas de um conjunto de resultados são lidas a partir da fonte de dados). Por exemplo, é um erro chamar **SQLGetData** para a coluna 5 e, em seguida, chamá-lo para a coluna 4.  
  
-   Não pode ser amarrado.  
  
-   Deve ter um número de coluna mais alto do que a última coluna vinculada. Por exemplo, se a última coluna vinculada for a coluna 3, é um erro chamar **SQLGetData** para a coluna 2. Por essa razão, os aplicativos devem ter certeza de colocar longas colunas de dados no final da lista selecionada.  
  
-   Não será possível ser usado se **SQLFetch** ou **SQLFetchScroll foram** chamados para recuperar mais de uma linha. Para obter mais informações, consulte [Usando cursors de bloco .](../../../odbc/reference/develop-app/using-block-cursors.md)  
  
 Alguns motoristas não aplicam essas restrições. Os aplicativos interoperáveis devem assumir que existem ou determinar quais restrições não são aplicadas ligando para **o SQLGetInfo** com a opção SQL_GETDATA_EXTENSIONS.  
  
 Se o aplicativo não precisar de todos os dados em uma coluna de dados de caracteres ou binários, ele pode reduzir o tráfego de rede em drivers baseados em DBMS, definindo o atributo de declaração SQL_ATTR_MAX_LENGTH antes de executar a declaração. Isso restringe o número de bytes de dados que serão devolvidos para qualquer caractere ou coluna binária. Por exemplo, suponha que uma coluna contenha documentos de texto longos. Um aplicativo que navega pela tabela que contém esta coluna pode ter que exibir apenas a primeira página de cada documento. Embora este atributo de declaração possa ser simulado no motorista, não há razão para fazer isso. Em particular, se um aplicativo quiser truncar caracteres ou dados binários, ele deve vincular um pequeno buffer à coluna com **SQLBindCol** e deixar o driver truncar os dados.
