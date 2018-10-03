---
title: Usando os arquivos de biblioteca e cabeçalho do SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- header files [SQL Server Native Client]
- SQLNCLI, header files
- OLE DB, header files
- library files [SQL Server Native Client]
- SQL Server Native Client, header files
- data access [SQL Server Native Client], header files
- SQL Server Native Client ODBC driver,header files
- data access [SQL Server Native Client], library files
- SQL Server Native Client, library files
- ODBC applications, header files
- SQLNCLI, library files
ms.assetid: 69889a98-7740-4667-aecd-adfc0b37f6f0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 800b3e43129bba36db0836f9a58a3ad1e47b40c1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48141176"
---
# <a name="using-the-sql-server-native-client-header-and-library-files"></a>Usando os arquivos de biblioteca e de cabeçalho do SQL Server Native Client
  Os arquivos de biblioteca e de cabeçalho do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client são instalados com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Quando você for desenvolver um aplicativo, é importante copiar e instalar todos os arquivos necessários para o desenvolvimento no seu ambiente de desenvolvimento. Para obter mais informações sobre como instalar e redistribuir [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, consulte [instalar o SQL Server Native Client](installing-sql-server-native-client.md).  
  
 Os arquivos de biblioteca e de cabeçalho do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client são instalados no seguinte local:  
  
 *%PROGRAM FILES%* \Microsoft SQL Server\110\SDK  
  
 O arquivo de cabeçalho do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (sqlncli.h) pode ser usado para adicionar a funcionalidade de acesso a dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client a seus aplicativos personalizados. O arquivo de cabeçalho do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client contém todas as definições, atributos, propriedades e interfaces necessários para tirar proveito dos novos recursos introduzidos no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Além do arquivo de cabeçalho do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, também há um arquivo de biblioteca sqlncli11.lib que é a biblioteca de exportação para a funcionalidade BCP (programa de cópia em massa) do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para ODBC.  
  
 O arquivo de cabeçalho do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client tem compatibilidade com versões anteriores dos arquivos de cabeçalho sqloledb.h e odbcss.h usados com o MDAC (Microsoft Data Access Components), mas não contém o CLSIDs para SQLOLEDB (o provedor OLE DB para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fornecido com o MDAC), nem símbolos para a funcionalidade XML (para a qual não há suporte no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client).  
  
 Os aplicativos ODBC não podem referenciar o cabeçalho do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (sqlncli.h) e o odbcss.h no mesmo programa. Mesmo que você não esteja usando nenhum dos recursos introduzidos no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], o arquivo de cabeçalho do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client funcionará no lugar do antigo odbcss.h.  
  
 Os aplicativos OLE DB que usam o provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client precisam apenas referenciar sqlncli.h. Se um aplicativo usar o MDAC (SQLOLEDB) e o provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, ele poderá referenciar sqloledb.h e sqlncli.h, mas a referência a sqloledb.h deve vir primeiro.  
  
## <a name="using-the-sql-server-native-client-header-file"></a>Usando o arquivo de cabeçalho do SQL Server Native Client  
 Para usar o arquivo de cabeçalho do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, você deve usar uma instrução `include` no seu código de programação C/C++. As seções a seguir descrevem como fazer isto para aplicativos OLE DB e ODBC.  
  
> [!NOTE]  
>  Os arquivos de cabeçalho e de biblioteca do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client podem ser compilados apenas usando o Visual Studio C++ 2002 ou posterior.  
  
### <a name="ole-db"></a>OLE DB  
 Para usar o arquivo de cabeçalho do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client em um aplicativo OLE DB usando as seguintes linhas do código de programação:  
  
```  
#define _SQLNCLI_OLEDB_  
include "sqlncli.h";  
```  
  
> [!NOTE]  
>  A primeira linha de código mostrada acima deverá ser omitida se as duas APIs OLE DB e ODBC forem usadas pelo aplicativo. Além disso, se o aplicativo tiver uma instrução `include` para sqloledb.h, a instrução `include` para sqlncli.h deverá vir depois dela.  
  
 Ao criar uma conexão com uma fonte de dados por meio do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, use "SQLNCLI11" como a cadeia de caracteres de nome do provedor.  
  
### <a name="odbc"></a>ODBC  
 Para usar o arquivo de cabeçalho do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client em um aplicativo ODBC usando as seguintes linhas do código de programação:  
  
```  
#define _SQLNCLI_ODBC_  
include "sqlncli.h";  
```  
  
> [!NOTE]  
>  A primeira linha do código mostrado acima deve ser omitida se o OLE DB e ODBC APIs são usadas pelo aplicativo. Além disso, se o aplicativo tiver uma instrução `#include` para odbcss.h, ela deve ser removida.  
  
 Ao criar uma conexão com uma fonte de dados por meio do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, use "SQL Server Native Client 11.0" como a cadeia de caracteres de nome do driver.  
  
## <a name="component-names-and-properties-by-version"></a>Propriedades e nomes de componentes por versão  
  
|Propriedade|SQL Server Native Client<br /><br /> SQL Server 2005|SQL Server Native Client 10.0<br /><br /> SQL Server 2008|SQL Server Native Client 11.0<br /><br /> [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]|MDAC|  
|--------------|--------------------------------------------------|-------------------------------------------------------|---------------------------------------------------------------|----------|  
|Nome do driver ODBC|SQL Native Client|SQL Server Native Client 10.0|SQL Server Native Client 11.0|SQL Server|  
|Nome do arquivo de cabeçalho ODBC|Sqlncli.h|Sqlncli.h|Sqlncli.h|Odbcss.h|  
|DLL do driver ODBC|Sqlncli.dll|Sqlncl10.dll|Sqlncl11.dll|sqlsrv32.dll|  
|Arquivo de biblioteca ODBC para APIs BCP|Sqlncli.lib|Sqlncli10.lib|Sqlncli11.lib|Odbcbcp.lib|  
|DLL ODBC para APIs BCP|Sqlncli.dll|Sqlncli10.dll|Sqlncli11.dll|Odbcbcp.dll|  
|OLE DB PROGID|SQLNCLI|SQLNCLI10|SQLNCLI11|SQLOLEDB|  
|Nome do arquivo de cabeçalho OLE DB|Sqlncli.h|Sqlncli.h|Sqlncli.h|Sqloledb.h|  
|DLL do provedor OLE DB|Sqlncli.dll|Sqlncli10.dll|Sqlncli11.dll|Sqloledb.dll|  
  
 O sqlncli.h dá suporte a várias versões do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client por meio da macro SQLNCLI_VER. Por padrão, SQLNCLI_VER usa como padrão a versão mais recente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Para criar um aplicativo que usa sqlncli10.dll em vez de sqlncli11.dll, defina SQLNCLI_VER como 10.  
  
## <a name="static-linking-and-bcp-functions"></a>Vinculação estática e funções BCP  
 Quando um aplicativo usa funções BCP, é importante que ele especifique na cadeia de conexão o driver da mesma versão que a fornecida com o arquivo de cabeçalho e a biblioteca usada para compilar o aplicativo.  
  
 Por exemplo, se você compilar um aplicativo usando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, e o arquivo de biblioteca associado (sqlncli11.lib) e o arquivo de cabeçalho (sqlncli.h) de \Arquivos de Programas \Microsoft SQL Server\110\SDK, não se esqueça de especificar (usando o ODBC como um exemplo) "DRIVER={SQL Server Native Client 11.0}" na cadeia de conexão.  
  
 Para obter mais informações, consulte executando [executando operações de cópia em massa](../features/performing-bulk-copy-operations.md).  
  
## <a name="see-also"></a>Consulte também  
 [Criando aplicativos com o SQL Server Native Client](building-applications-with-sql-server-native-client.md)  
  
  
