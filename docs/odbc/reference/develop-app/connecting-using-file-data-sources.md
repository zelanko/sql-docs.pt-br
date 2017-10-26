---
title: Conectando-se com as fontes de dados de arquivo | Microsoft Docs
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
- connecting to driver [ODBC], file data sources
- SQLDriverConnect function [ODBC], connecting using file data sources
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], file data sources
- file data sources [ODBC]
ms.assetid: 3003f8c2-8be6-41cc-8d9c-612e9bd0f3ae
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5f8a5d949127e7ad87866a0272fbd285fe12ceed
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="connecting-using-file-data-sources"></a>Conectando-se com as fontes de dados de arquivo
As informações de conexão para uma fonte de dados de arquivo são armazenadas em um arquivo. DSN. Como resultado, a cadeia de caracteres de conexão pode ser usada repetidamente por um único usuário ou compartilhada entre vários usuários se eles tiverem a unidade apropriada instalada. O arquivo contém um nome de driver (ou outro nome de fonte de dados no caso de uma fonte de dados de arquivos não compartilháveis) e, opcionalmente, uma cadeia de conexão que pode ser usada por **SQLDriverConnect**. O Gerenciador de Driver cria a cadeia de caracteres de conexão para a chamada **SQLDriverConnect** das palavras-chave no arquivo. DSN.  
  
 Uma fonte de dados do arquivo permite que um aplicativo especificar as opções de conexão sem a necessidade de criar uma cadeia de caracteres de conexão para uso com **SQLDriverConnect**. A fonte de dados de arquivo normalmente é criada especificando o **SAVEFILE** palavra-chave, que faz com que o Gerenciador de Driver para salvar a cadeia de caracteres de conexão de saída criada por uma chamada para **SQLDriverConnect** para o arquivo. DSN. Cadeia de caracteres de conexão pode ser usada repetidamente chamando **SQLDriverConnect** com o **FILEDSN** palavra-chave. Isso simplifica o processo de conexão e fornece uma fonte persistente da cadeia de caracteres de conexão.  
  
 Fontes de dados de arquivo também podem ser criadas chamando **SQLCreateDataSource** no instalador do DLL. Informações podem ser gravadas no arquivo. DSN chamando **SQLWriteFileDSN**e ler o arquivo. DSN chamando **SQLReadFileDSN**; ambas as funções também estão no instalador do DLL. Para obter informações sobre o instalador de DLL, consulte [configurar fontes de dados](../../../odbc/reference/install/configuring-data-sources.md).  
  
 As palavras-chave usadas para obter informações de conexão estão na seção [ODBC] de um arquivo. DSN. O mínimo de informações que um arquivo. DSN compartilhável teria na seção [ODBC] é a palavra-chave DRIVER:  
  
```  
DRIVER = SQL Server  
```  
  
 O arquivo. DSN compartilhável geralmente contém uma cadeia de caracteres de conexão, da seguinte maneira:  
  
```  
DRIVER = SQL Server  
UID = Larry  
DATABASE = MyDB  
```  
  
 Quando a fonte de dados de arquivos for, o arquivo. DSN contém apenas um **DSN** palavra-chave. Quando o Gerenciador de Driver é enviado as informações em uma fonte de dados de arquivos não compartilháveis, ele se conecta conforme o necessário para a fonte de dados indicada pelo **DSN** palavra-chave. Um arquivo. DSN conterá a seguinte palavra-chave:  
  
```  
DSN = MyDataSource  
```  
  
 A cadeia de caracteres de conexão usada para uma fonte de dados de arquivo é a união das palavras-chave especificadas no arquivo. DSN e as palavras-chave especificadas na cadeia de conexão na chamada para **SQLDriverConnect**. Se qualquer uma das palavras-chave no arquivo. DSN em conflito com palavras-chave na cadeia de conexão, o Gerenciador de Driver decide qual valor de palavra-chave deve ser usado. Para obter mais informações, consulte [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
## <a name="see-also"></a>Consulte também  
 [http://support.microsoft.com/kb/165866](http://support.microsoft.com/kb/165866)

