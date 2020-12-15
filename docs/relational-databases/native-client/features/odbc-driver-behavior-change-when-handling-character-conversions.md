---
description: Alteração de comportamento do driver ODBC ao lidar com conversões de caracteres
title: Conversões de caracteres de manipulação de alterações ODBC
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 682a232a-bf89-4849-88a1-95b2fbac1467
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5d74887afafcc4ab0c00881081bf8abf941ac551
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97418534"
---
# <a name="odbc-driver-behavior-change-when-handling-character-conversions"></a>Alteração de comportamento do driver ODBC ao lidar com conversões de caracteres
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  O [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] driver ODBC do Native Client (SQLNCLI11.dll) alterou como ele faz de SQL_WCHAR * (nchar/nvarchar/nvarchar (max)) e SQL_CHAR \* (char/varchar/NARCHAR (max)) conversões. As funções ODBC, como SQLGetData, SQLBindCol, SQLBindParameter, retornam (-4) SQL_NO_TOTAL como o parâmetro de comprimento/indicador ao usar o driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2012 Native Client. As versões anteriores do driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client retornaram um valor de comprimento, que pode estar incorreto.  
  
## <a name="sqlgetdata-behavior"></a>Comportamento de SQLGetData  
 Muitas funções do Windows permitem especificar um tamanho do buffer de 0 e o comprimento retornado é o tamanho dos dados retornados. O seguinte padrão é comum para programadores do Windows:  
  
```  
int iSize = 0;  
BYTE * pBuffer = NULL;  
GetMyFavoriteAPI(pBuffer, &iSize);   // Returns needed size in iSize  
pBuffer = new BYTE[iSize];   // Allocate buffer   
GetMyFavoriteAPI(pBuffer, &iSize);   // Retrieve actual data  
```  
  
 No entanto, **SQLGetData** não deve ser usado neste cenário. Os padrões a seguir não devem ser usados:  
  
```  
// bad  
int iSize = 0;  
WCHAR * pBuffer = NULL;  
SQLGetData(hstmt, SQL_W_CHAR, ...., (SQLPOINTER*)0x1, 0, &iSize);   // Get storage size needed  
pBuffer = new WCHAR[(iSize/sizeof(WCHAR)) + 1];   // Allocate buffer  
SQLGetData(hstmt, SQL_W_CHAR, ...., (SQLPOINTER*)pBuffer, iSize, &iSize);   // Retrieve data  
```  
  
 **SQLGetData** só pode ser chamado para recuperar partes de dados reais. Não há suporte para o uso de **SQLGetData** para obter o tamanho dos dados.  
  
 O exemplo a seguir mostra o impacto da alteração do driver quando você usa o padrão incorreto. Este aplicativo consulta uma coluna **varchar** e associando como Unicode (SQL_UNICODE/SQL_WCHAR):  
  
 Consultá  `select convert(varchar(36), '123')`  
  
```  
SQLGetData(hstmt, SQL_WCHAR, ....., (SQLPOINTER*) 0x1, 0 , &iSize);   // Attempting to determine storage size needed  
```  
  
|Versão do driver ODBC [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client|Comprimento ou resultado do indicador|Descrição|  
|-----------------------------------------------------------------|---------------------------------|-----------------|  
|[!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] Native Client ou anterior|6|O driver presumiu incorretamente que a conversão de CHAR para WCHAR poderia ser realizada como o comprimento * 2.|  
|[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client (versão 11.0.2100.60) ou posterior|-4 (SQL_NO_TOTAL)|O driver não assume mais que a conversão de CHAR para WCHAR ou WCHAR em CHAR é uma ação (multiplicar) \* 2 ou (dividir)/2.<br /><br /> Chamar **SQLGetData** não retorna mais o comprimento da conversão esperada. O driver detecta a conversão para ou de CHAR e WCHAR e retorna (- 4) SQL_NO_TOTAL em vez do comportamento de *2 ou /2 que poderia estar incorreto.|  
  
 Use **SQLGetData** para recuperar as partes dos dados. (Pseudocódigo mostrado:)  
  
```  
while( (SQL_SUCCESS or SQL_SUCCESS_WITH_INFO) == SQLFetch(...) ) {  
   SQLNumCols(...iTotalCols...)  
   for(int iCol = 1; iCol < iTotalCols; iCol++) {  
      WCHAR* pBufOrig, pBuffer = new WCHAR[100];  
      SQLGetData(.... iCol ... pBuffer, 100, &iSize);   // Get original chunk  
      while(NOT ALL DATA RETREIVED (SQL_NO_TOTAL, ...) ) {  
         pBuffer += 50;   // Advance buffer for data retrieved  
         // May need to realloc the buffer when you reach current size  
         SQLGetData(.... iCol ... pBuffer, 100, &iSize);   // Get next chunk  
      }  
   }  
}  
```  
  
## <a name="sqlbindcol-behavior"></a>Comportamento de SQLBindCol  
 Consultá  `select convert(varchar(36), '1234567890')`  
  
```  
SQLBindCol(... SQL_W_CHAR, ...)   // Only bound a buffer of WCHAR[4] - Expecting String Data Right Truncation behavior  
```  
  
|Versão do driver ODBC [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client|Comprimento ou resultado do indicador|Descrição|  
|-----------------------------------------------------------------|---------------------------------|-----------------|  
|[!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] Native Client ou anterior|20|**SQLFetch** relata que há um truncamento no lado direito dos dados.<br /><br /> O comprimento é o comprimento dos dados retornados, não o que foi armazenado (presume a conversão *2 CHAR para WCHAR, que pode ter as marcas incorretas).<br /><br /> Os dados armazenados em buffer são 123\0. O buffer é garantido para ser terminado em NULL.|  
|[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client (versão 11.0.2100.60) ou posterior|-4 (SQL_NO_TOTAL)|**SQLFetch** relata que há um truncamento no lado direito dos dados.<br /><br /> O comprimento indica -4 (SQL_NO_TOTAL) porque o restante dos dados não foi convertido.<br /><br /> Os dados armazenados no buffer são 123\0. - O buffer é garantido para ser terminado em NULL.|  
  
## <a name="sqlbindparameter-output-parameter-behavior"></a>SQLBindParameter (comportamento de parâmetro OUTPUT)  
 Consultá  `create procedure spTest @p1 varchar(max) OUTPUT`  
  
 `select @p1 = replicate('B', 1234)`  
  
```  
SQLBindParameter(... SQL_W_CHAR, ...)   // Only bind up to first 64 characters  
```  
  
|Versão do driver ODBC [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client|Comprimento ou resultado do indicador|Descrição|  
|-----------------------------------------------------------------|---------------------------------|-----------------|  
|[!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] Native Client ou anterior|2468|**SQLFetch** não retorna mais dados disponíveis.<br /><br /> **SQLMoreResults** não retorna mais dados disponíveis.<br /><br /> O comprimento indica o tamanho dos dados retornados do servidor, não armazenados em buffer.<br /><br /> O buffer original contém 63 bytes e um terminador em NULL. O buffer é garantido para ser terminado em NULL.|  
|[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client (versão 11.0.2100.60) ou posterior|-4 (SQL_NO_TOTAL)|**SQLFetch** não retorna mais dados disponíveis.<br /><br /> **SQLMoreResults** não retorna mais dados disponíveis.<br /><br /> O comprimento indica (-4) SQL_NO_TOTAL porque o restante dos dados não foi convertido.<br /><br /> O buffer original contém 63 bytes e um terminador em NULL. O buffer é garantido para ser terminado em NULL.|  
  
## <a name="performing-char-and-wchar-conversions"></a>Execução de conversões CHAR e WCHAR  
 O driver ODBC do [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client oferece várias maneiras de executar conversões CHAR e WCHAR. A lógica é semelhante à manipulação de BLOBs (varchar (max), nvarchar (max),...):  
  
-   Os dados são salvos ou truncados no buffer especificado durante a associação com **SQLBindCol** ou **SQLBindParameter**.  
  
-   Se você não associar, poderá recuperar os dados em partes usando **SQLGetData** e **SQLParamData**.  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos do SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
