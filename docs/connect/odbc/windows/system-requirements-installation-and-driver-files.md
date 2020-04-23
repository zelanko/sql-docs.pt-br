---
title: Requisitos do sistema, instalação e arquivos de driver | Microsoft Docs
description: Este artigo descreve os requisitos de sistema para o Microsoft ODBC Driver for SQL Server.
ms.custom: ''
ms.date: 03/18/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d90fa182-1dab-4d6f-bd85-a04dd1479986
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e2b56528a369d58238a545afc20b35787003b6b1
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81484445"
---
# <a name="system-requirements-installation-and-driver-files"></a>Requisitos do sistema, instalação e arquivos de driver

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Este artigo aborda os drivers ODBC que se conectam ao SQL Server.

## <a name="sql-version-compatibility"></a>Compatibilidade com versões do SQL

A compatibilidade indica que um driver foi testado quanto à compatibilidade em relação às versões existentes do SQL no momento da versão do driver. As versões do SQL Server geralmente tentam manter a compatibilidade com versões anteriores dos drivers de cliente existentes. Porém, novos recursos em versões do SQL Server podem não estar disponíveis com drivers cliente mais antigos.

|Versão do driver|Banco de Dados SQL do Azure|Data Warehouse SQL do Azure|Instância Gerenciada do Azure SQL|SQL Server 2019|Microsoft SQL Server 2017|SQL Server 2016|SQL Server 2014|SQL Server 2012|SQL Server 2008 R2|SQL Server 2008|SQL Server 2005|
|-|-|-|-|-|-|-|-|-|-|-|-|
|17.5|S|S|S|S|S|S|S|S| | | |
|17.4|S|S|S|S|S|S|S|S| | | |
|17.3|S|S|S|S|S|S|S|S|S|S| |
|17.2|S|S|S| |S|S|S|S|S|S| |
|17.1|S|S|S| |S|S|S|S|S|S| |
|17.0|S|S|S| |S|S|S|S|S|S| |
|13.1| | | | |S|S|S|S|S|S| |
|13  | | | | | |S|S|S|S|S| |
|11  | | | | | | |S|S|S|S|S|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

### <a name="connection-string-details"></a>Detalhes da cadeia de conexão

O nome do driver que você especifica em uma cadeia de conexão é `ODBC Driver 11 for SQL Server` ou `ODBC Driver 13 for SQL Server` (para 13 e 13,1) ou `ODBC Driver 17 for SQL Server`.

## <a name="supported-operating-systems"></a>Sistemas operacionais compatíveis

A seguinte matriz indica suporte à versão do driver para versões do sistema operacional Windows:

|Versão do driver|Windows Server 2019|Windows Server 2016|Windows Server 2012 R2|Windows Server 2012|Windows Server 2008 R2|Windows 10|Windows 8.1|Windows 7|Windows Vista SP2|
|-|-|-|-|-|-|-|-|-|-|
|17.5|S|S|S|S| |S|S| | |
|17.4|S|S|S|S|S|S|S|S| |
|17.3|S|S|S|S|S|S|S|S| |
|17.2| |S|S|S|S|S|S|S| |
|17.1| |S|S|S|S|S|S|S| |
|17.0| |S|S|S|S|S|S|S| |
|13.1| |S|S|S|S|S|S|S| |
|13  | | | |S|S| |S|S| |
|11  | | | |S|S| | |S|S|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

## <a name="installing-microsoft-odbc-driver-for-sql-server"></a>Instalando o Microsoft ODBC Driver for SQL Server

O driver é instalado quando você executa `msodbcsql.msi` de um dos [Downloads do Windows](../download-odbc-driver-for-sql-server.md#download-for-windows).

> [!NOTE]
> Para aqueles que têm o driver 17.1.0.1 ou anterior instalado, é recomendável que ele seja desinstalado manualmente antes de instalar a versão mais recente do driver.

### <a name="side-by-side-with-native-client"></a>Lado a lado com o Native Client

O driver pode ser instalado lado a lado com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. As versões principais do driver (11, 13, 17) podem ser instaladas lado a lado entre si também.

Quando você invoca `msodbcsql.msi`, só os componentes cliente são instalados por padrão. Os componentes cliente são arquivos que dão suporte à execução de um aplicativo que foi desenvolvido usando o driver. Para instalar os componentes do SDK, especifique `ADDLOCAL=ALL` na linha de comando. Veja um exemplo.
  
```console
msiexec /i msodbcsql.msi ADDLOCAL=ALL  
```  

### <a name="end-user-license"></a>Licença de usuário final

Especifique `IACCEPTMSODBCSQLLICENSETERMS=YES` para aceitar os termos da licença do usuário final se você usar a opção de instalação `/passive`, `/qn`, `/qb` ou `/qr`. Essa opção deve ser especificada com todas as letras maiúsculas. Veja um exemplo.
  
```console
msiexec /quiet /passive /qn /i msodbcsql.msi IACCEPTMSODBCSQLLICENSETERMS=YES ADDLOCAL=ALL  
```  

### <a name="silent-uninstall"></a>Desinstalação silenciosa

O exemplo a seguir mostra como realizar uma desinstalação silenciosa.
  
```console
msiexec /quiet /passive /qn /uninstall msodbcsql.msi  
```  

### <a name="indicate-dependency"></a>Indicar dependência

Quando um aplicativo usa o driver, ele deve indicar que depende do driver por meio da opção de instalação `APPGUID`. esta indicação permite que o instalador do driver relate aplicativos dependentes antes da desinstalação. Para especificar uma dependência no driver, defina o parâmetro de linha de comando `APPGUID` com o código de produto na instalação silenciosa do driver. É preciso criar um código de produto ao usar o Microsoft Installer para agrupar o programa de instalação do aplicativo. Veja um exemplo.
  
```console
msiexec /i msodbcsql.msi APPGUID={ <Your dependent application's APPGUID> }  
```  

## <a name="command-line-tools-sqlcmdexe-and-bcpexe"></a>Ferramentas de linha de comando: sqlcmd.exe e bcp.exe

As ferramentas `bcp.exe` e `sqlcmd.exe` para uso com o driver podem ser baixadas em [Utilitários de Linha de Comando 11 da Microsoft para SQL Server](https://www.microsoft.com/download/details.aspx?id=36433), [Utilitários de Linha de Comando 13 da Microsoft para SQL Server](https://www.microsoft.com/download/details.aspx?id=52680) ou [Utilitários de Linha de Comando 13.1 da Microsoft para SQL Server](https://www.microsoft.com/download/details.aspx?id=53591). O driver é um pré-requisito para instalar `sqlcmd.exe` e `bcp.exe`.
  
`bcp.exe` e `sqlcmd.exe` são instalados na subpasta `110\Tools` do `%PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC` para a versão 11 e `130\Tools` para a 13 e a 13,1.

Um aplicativo que usa funções do BCP precisa especificar o driver da mesma versão que a fornecida com o arquivo de cabeçalho e a biblioteca usados para compilar o aplicativo.  

Por exemplo, quando você compilar um aplicativo ODBC com `msodbcsql11.lib` e `msodbcsql.h`, use "DRIVER={ODBC Driver 11 for SQL Server}" na cadeia de conexão.

## <a name="components-of-the-microsoft-odbc-driver-for-ssnoversion-on-windows"></a>Componentes do Microsoft ODBC Driver para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Windows

O driver ODBC no Windows contém os seguintes componentes:

| Componente | Descrição |
| :-------- | :---------- |
|msodbcsql17.dll ou <br/> msodbcsql13.dll ou <br/> msodbcsql11.dll|O arquivo de biblioteca de vínculo dinâmico (DLL) que contém toda a funcionalidade do driver. Este arquivo é instalado em %SYSTEMROOT%\System32.|  
|msodbcdiag17.dll ou <br/> msodbcdiag13.dll ou <br/> msodbcdiag11.dll|O arquivo DLL (biblioteca de vínculo dinâmico) que contém a interface de diagnóstico (rastreamento) do driver. Este arquivo é instalado em %SYSTEMROOT%\System32.|
|msodbcsqlr17.rll ou <br/> msodbcsqlr13.rll ou <br/> msodbcsqlr11.rll|O arquivo de recursos que acompanha a biblioteca do driver. Este arquivo é instalado em %SYSTEMROOT%\System32\1033.| 
|s13ch_msodbcsql.chm ou <br/> s11ch_msodbcsql.chm |O arquivo de ajuda do Assistente para Fontes de Dados que documenta como criar uma fonte de dados do driver. Este arquivo é instalado em %SYSTEMROOT%\System32\1033 <br /> <br /> **OBSERVAÇÃO:** Não há nenhum arquivo chm para o Driver ODBC 17. |  
|msodbcsql.h|O arquivo de cabeçalho que contém todas as novas definições necessárias para usar o driver.<br /><br /> **Observação:**  Você não pode referenciar msodbcsql.h e odbcss.h no mesmo programa.<br /><br /> O msodbcsql.h para o ODBC Driver 17 ou 13 é instalado em %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK. <br /> O msodbcsql.h para o ODBC Driver 11 é instalado em %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK.| 
|msodbcsql17.lib ou <br/> msodbcsql13.lib ou <br/> msodbcsql11.lib|O arquivo de biblioteca necessário para chamar as funções do utilitário **bcp** que fazem parte do driver.<br /><br /> **Observação:**  se você referenciar esse arquivo de biblioteca no programa, verifique se ele está no caminho do sistema e no caminho do sistema dos usuários que usam o aplicativo.<br /><br /> O msodbcsql17.lib ou o msodbcsql13.lib é instalado em %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK.<br /> O msodbcsql11.lib é instalado em %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK.|
| &nbsp; | &nbsp; |

## <a name="see-also"></a>Confira também

[Microsoft ODBC Driver for SQL Server no Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
