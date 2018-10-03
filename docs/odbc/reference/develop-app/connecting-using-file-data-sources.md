---
title: Conectando-se usando fontes de dados de arquivo | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: af24a0656f46f0256775f4ea1649ab806e207fdb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47856307"
---
# <a name="connecting-using-file-data-sources"></a>Conectar-se usando fontes de dados de arquivo
As informações de conexão para uma fonte de dados de arquivo são armazenadas em um arquivo. DSN. Como resultado, a cadeia de caracteres de conexão pode ser usada repetidamente por um único usuário ou compartilhada entre vários usuários se eles tiverem o driver apropriado instalado. O arquivo contém um nome de driver (ou outro nome de fonte de dados no caso de uma fonte de dados de arquivos não compartilháveis) e, opcionalmente, uma cadeia de conexão que pode ser usada por **SQLDriverConnect**. O Gerenciador de Driver cria a cadeia de caracteres de conexão para a chamada para **SQLDriverConnect** de palavras-chave no arquivo. DSN.  
  
 Uma fonte de dados de arquivo permite que um aplicativo especificar opções de conexão sem precisar criar uma cadeia de caracteres de conexão para uso com **SQLDriverConnect**. Normalmente, a fonte de dados de arquivo é criada especificando o **SAVEFILE** palavra-chave, que faz com que o Gerenciador de Driver para salvar a cadeia de conexão de saída criada por uma chamada para **SQLDriverConnect** para o arquivo. DSN. Cadeia de caracteres de conexão pode ser usada repetidamente chamando **SQLDriverConnect** com o **FILEDSN** palavra-chave. Isso simplifica o processo de conexão e fornece uma fonte persistente da cadeia de caracteres de conexão.  
  
 Fontes de dados de arquivo também podem ser criados chamando **SQLCreateDataSource** no instalador do DLL. Informações podem ser gravadas no arquivo. DSN chamando **SQLWriteFileDSN**e ler o arquivo. DSN chamando **SQLReadFileDSN**; ambas as funções também são a DLL do instalador. Para obter informações sobre o DLL do instalador, consulte [Configurando fontes de dados](../../../odbc/reference/install/configuring-data-sources.md).  
  
 As palavras-chave usadas para obter informações de conexão estão na seção [ODBC] de um arquivo. DSN. As informações mínimas que teria um arquivo. DSN compartilhável na seção [ODBC] são a palavra-chave DRIVER:  
  
```  
DRIVER = SQL Server  
```  
  
 O arquivo. DSN compartilhável geralmente contém uma cadeia de caracteres de conexão, da seguinte maneira:  
  
```  
DRIVER = SQL Server  
UID = Larry  
DATABASE = MyDB  
```  
  
 Quando a fonte de dados do arquivo é não compartilhável, o arquivo. DSN contém apenas um **DSN** palavra-chave. Quando o Gerenciador de Driver é enviado as informações em uma fonte de dados de arquivos não compartilháveis, ele se conecta conforme o necessário para a fonte de dados indicada pelo **DSN** palavra-chave. Um arquivo. DSN não compartilhável conteria a palavra-chave seguinte:  
  
```  
DSN = MyDataSource  
```  
  
 A cadeia de caracteres de conexão usada para uma fonte de dados do arquivo é a união entre as palavras-chave especificadas no arquivo. DSN e as palavras-chave especificadas na cadeia de conexão na chamada para **SQLDriverConnect**. Se qualquer uma das palavras-chave no arquivo. DSN entrarem em conflito com palavras-chave na cadeia de conexão, o Gerenciador de Driver decide qual valor de palavra-chave deve ser usado. Para obter mais informações, consulte [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
## <a name="see-also"></a>Consulte também  
 [http://support.microsoft.com/kb/165866](http://support.microsoft.com/kb/165866)
