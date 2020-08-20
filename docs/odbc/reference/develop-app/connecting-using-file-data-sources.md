---
description: Conectar-se usando fontes de dados de arquivo
title: Conectando usando fontes de dados de arquivo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], file data sources
- SQLDriverConnect function [ODBC], connecting using file data sources
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], file data sources
- file data sources [ODBC]
ms.assetid: 3003f8c2-8be6-41cc-8d9c-612e9bd0f3ae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0ab210a77d1d6516b6b54ba25767d859ff9102fb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476758"
---
# <a name="connecting-using-file-data-sources"></a>Conectar-se usando fontes de dados de arquivo
As informações de conexão para uma fonte de dados de arquivo são armazenadas em um arquivo. DSN. Como resultado, a cadeia de conexão pode ser usada repetidamente por um único usuário ou compartilhada entre vários usuários se eles tiverem o driver apropriado instalado. O arquivo contém um nome de driver (ou outro nome de fonte de dados no caso de uma fonte de dados de arquivo não compartilhável) e, opcionalmente, uma cadeia de conexão que pode ser usada pelo **SQLDriverConnect**. O Gerenciador de driver cria a cadeia de conexão para a chamada para **SQLDriverConnect** a partir das palavras-chave no arquivo. DSN.  
  
 Uma fonte de dados de arquivo permite que um aplicativo especifique opções de conexão sem precisar criar uma cadeia de conexão para uso com **SQLDriverConnect**. A fonte de dados de arquivo geralmente é criada especificando-se a palavra-chave **SaveFile** , que faz com que o Gerenciador de driver salve a cadeia de conexão de saída criada por uma chamada para **SQLDriverConnect** no arquivo. DSN. Essa cadeia de conexão pode ser usada repetidamente chamando **SQLDriverConnect** com a palavra-chave **FILEDSN** . Isso simplifica o processo de conexão e fornece uma fonte persistente da cadeia de conexão.  
  
 As fontes de dados de arquivo também podem ser criadas chamando **SQLCreateDataSource** na DLL do instalador. As informações podem ser gravadas no arquivo. DSN chamando **SQLWriteFileDSN**e lidas a partir do arquivo. DSN chamando **SQLReadFileDSN**; ambas as funções também estão na DLL do instalador. Para obter informações sobre a DLL do instalador, consulte [Configurando fontes de dados](../../../odbc/reference/install/configuring-data-sources.md).  
  
 As palavras-chave usadas para informações de conexão estão na seção [ODBC] de um arquivo. DSN. As informações mínimas que um arquivo. DSN compartilhável teria na seção [ODBC] são a palavra-chave do DRIVER:  
  
```  
DRIVER = SQL Server  
```  
  
 O arquivo. DSN compartilhável geralmente contém uma cadeia de conexão, da seguinte maneira:  
  
```  
DRIVER = SQL Server  
UID = Larry  
DATABASE = MyDB  
```  
  
 Quando a fonte de dados de arquivo não é compartilhável, o arquivo. DSN contém apenas uma palavra-chave **DSN** . Quando o Gerenciador de driver recebe as informações em uma fonte de dados de arquivo não compartilhável, ele se conecta conforme necessário para a fonte de dados indicada pela palavra-chave **DSN** . Um arquivo. DSN não compartilhável conterá a seguinte palavra-chave:  
  
```  
DSN = MyDataSource  
```  
  
 A cadeia de conexão usada para uma fonte de dados de arquivo é a União das palavras-chave especificadas no arquivo. DSN e as palavras-chave especificadas na cadeia de conexão na chamada de **SQLDriverConnect**. Se qualquer uma das palavras-chave no arquivo. DSN entrar em conflito com palavras-chave na cadeia de conexão, o Gerenciador de driver decide qual valor de palavra-chave deve ser usado. Para obter mais informações, consulte [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
## <a name="see-also"></a>Consulte Também  
 [https://support.microsoft.com/kb/165866](https://support.microsoft.com/kb/165866)
