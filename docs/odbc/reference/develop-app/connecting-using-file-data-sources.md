---
title: Conectando usando fontes de dados de arquivos | Microsoft Docs
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
ms.openlocfilehash: 8c752fc3b09c06c68dcc216cacac63744dc3101b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287406"
---
# <a name="connecting-using-file-data-sources"></a>Conectar-se usando fontes de dados de arquivo
As informações de conexão de uma fonte de dados de arquivo são armazenadas em um arquivo .dsn. Como resultado, a seqüência de conexão pode ser usada repetidamente por um único usuário ou compartilhada entre vários usuários se eles tiverem o driver apropriado instalado. O arquivo contém um nome de driver (ou outro nome de origem de dados no caso de uma fonte de dados de arquivo não compartilhável) e, opcionalmente, uma seqüência de conexão que pode ser usada pelo **SQLDriverConnect**. O Gerenciador de drivers cria a seqüência de conexão para a chamada para **SQLDriverConnect** a partir das palavras-chave no arquivo .dsn.  
  
 Uma fonte de dados de arquivo permite que um aplicativo especifique opções de conexão sem ter que criar uma string de conexão para uso com **o SQLDriverConnect**. A fonte de dados do arquivo geralmente é criada especificando a palavra-chave **SAVEFILE,** o que faz com que o Gerenciador de driver salve a seqüência de conexão de saída criada por uma chamada para **SQLDriverConnect** para o arquivo .dsn. Essa seqüência de conexões pode ser usada repetidamente chamando **SQLDriverConnect** com a palavra-chave **FILEDSN.** Isso simplifica o processo de conexão e fornece uma fonte persistente da seqüência de conexões.  
  
 As fontes de dados de arquivo também podem ser criadas chamando **SQLCreateDataSource** no instalador DLL. As informações podem ser escritas no arquivo .dsn ligando para **SQLWriteFileDSN**e lidas no arquivo .dsn ligando para **SQLReadFileDSN;** ambas as funções também estão no instalador DLL. Para obter informações sobre o instalador DLL, consulte [Configurando fontes de dados](../../../odbc/reference/install/configuring-data-sources.md).  
  
 As palavras-chave usadas para informações de conexão estão na seção [ODBC] de um arquivo .dsn. A informação mínima que um arquivo .dsn compartilhável teria na seção [ODBC] é a palavra-chave DRIVER:  
  
```  
DRIVER = SQL Server  
```  
  
 O arquivo .dsn compartilhável geralmente contém uma seqüência de conexões, da seguinte forma:  
  
```  
DRIVER = SQL Server  
UID = Larry  
DATABASE = MyDB  
```  
  
 Quando a fonte de dados do arquivo não pode ser compartilhada, o arquivo .dsn contém apenas uma palavra-chave **DSN.** Quando o Gerenciador de driver é enviado as informações em uma fonte de dados de arquivo não compartilhável, ele se conecta conforme necessário à fonte de dados indicada pela palavra-chave **DSN.** Um arquivo .dsn não compartilhável conteria a seguinte palavra-chave:  
  
```  
DSN = MyDataSource  
```  
  
 A seqüência de conexão usada para uma fonte de dados de arquivo é a união das palavras-chave especificadas no arquivo .dsn e as palavras-chave especificadas na seqüência de conexões na chamada para **SQLDriverConnect**. Se alguma das palavras-chave no arquivo .dsn entrar em conflito com palavras-chave na seqüência de conexões, o Gerenciador de driver decidir qual valor de palavra-chave deve ser usado. Para obter mais informações, consulte [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
## <a name="see-also"></a>Consulte Também  
 [https://support.microsoft.com/kb/165866](https://support.microsoft.com/kb/165866)
