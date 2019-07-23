---
title: Requisitos do sistema, instalação e arquivos de driver | Microsoft Docs
ms.custom: ''
ms.date: 02/14/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d90fa182-1dab-4d6f-bd85-a04dd1479986
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 76016e87767f4efbca9a6c845af6464ab3ca26ed
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989403"
---
# <a name="system-requirements-installation-and-driver-files"></a>Requisitos do sistema, instalação e arquivos de driver
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

O ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dá suporte a conexões para SQL Server 2014, SQL Server 2012, [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssKatmai](../../../includes/sskatmai_md.md)] e [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
O ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Windows pode ser instalado em um computador que também tenha uma ou mais versões do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
O ODBC Driver 13 e 13,1 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], além do, é compatível com SQL Server 2016. 

O ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dá suporte a todos os itens acima e também SQL Server 2017.

O ODBC Driver 17 for SQL Server dá suporte a SQL Server 2019 a partir da versão 17,3 do driver.

O nome do driver que você especifica em uma cadeia de `ODBC Driver 11 for SQL Server` conexão `ODBC Driver 13 for SQL Server` é ou (para 13 e 13,1) `ODBC Driver 17 for SQL Server`ou.
  
## <a name="supported-operating-systems"></a>Sistemas operacionais com suporte

Você pode executar aplicativos com o driver nos seguintes sistemas operacionais Windows:  

-   Windows Server 2008 R2 
-   Windows Server 2012
-   Windows Server 2012 R2    
-   Windows Vista SP2 *(somente driver ODBC 11)*  
-   Windows 7  
-   Windows 8
-   Windows 8.1
-   Windows 10
  
## <a name="installing-microsoft-odbc-driver-for-sql-server"></a>Instalando o Microsoft ODBC Driver for SQL Server

O driver é instalado quando você executa `msodbcsql.msi` um dos seguintes links:

- [Baixar o Microsoft ODBC Driver 17 for SQL Server no Windows](https://www.microsoft.com/download/details.aspx?id=56567)
- [Baixar o Microsoft ODBC Driver 13.1 for SQL Server no Windows](https://www.microsoft.com/download/details.aspx?id=53339)
- [Baixar o Microsoft ODBC Driver 13 for SQL Server no Windows](https://www.microsoft.com/download/details.aspx?id=50420)
- [Baixar o Microsoft ODBC Driver 11 for SQL Server no Windows](https://www.microsoft.com/download/details.aspx?id=36434). 

> [!NOTE]
> Para aqueles que têm o driver 17.1.0.1 ou inferior instalado, é recomendável que ele seja desinstalado manualmente antes de instalar a versão mais recente do driver

Ele pode ser instalado lado a lado com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  

Quando você invoca `msodbcsql.msi`, só os componentes cliente são instalados por padrão. Os componentes cliente são arquivos que dão suporte à execução de um aplicativo que foi desenvolvido usando o driver. Para instalar os componentes do SDK, especifique `ADDLOCAL=ALL` na linha de comando. Por exemplo:  
  
```  
msiexec /i msodbcsql.msi ADDLOCAL=ALL  
```  
  
 Especifique `IACCEPTMSODBCSQLLICENSETERMS=YES` para aceitar os termos da licença do usuário final se você usar a opção de instalação `/passive`, `/qn`, `/qb` ou `/qr`. Essa opção deve ser especificada com todas as letras maiúsculas. Por exemplo:  
  
```  
msiexec /quiet /passive /qn /i msodbcsql.msi IACCEPTMSODBCSQLLICENSETERMS=YES ADDLOCAL=ALL  
```  
  
 Para fazer uma desinstalação silenciosa:  
  
```  
msiexec /quiet /passive /qn /uninstall msodbcsql.msi  
```  
  
Quando um aplicativo usa o driver, ele deve indicar que depende do driver por meio da opção de instalação `APPGUID`. Isso permite que o instalador do driver relate os aplicativos dependentes antes da desinstalação. Para especificar uma dependência no driver, defina o parâmetro de linha de comando `APPGUID` com o código de produto na instalação silenciosa do driver. (É preciso criar um código de produto ao usar o Microsoft Installer para agrupar o programa de instalação do aplicativo.) Por exemplo:  
  
```  
msiexec /i msodbcsql.msi APPGUID={ <Your dependent application's APPGUID> }  
```  

## <a name="command-line-tools-sqlcmdexe-and-bcpexe"></a>Ferramentas de linha de comando: sqlcmd.exe e bcp.exe

As `bcp.exe` ferramentas `sqlcmd.exe` e para uso com o driver podem ser baixadas no [Microsoft utilitários de linha de comando 11 para SQL Server](https://www.microsoft.com/download/details.aspx?id=36433), [Microsoft utilitários de linha de comando 13 para SQL Server](https://www.microsoft.com/download/details.aspx?id=52680)ou [Microsoft utilitários de linha de comando 13,1 para SQL Server](https://www.microsoft.com/download/details.aspx?id=53591). O driver é um pré-requisito para instalar `sqlcmd.exe` o `bcp.exe`e o.
  
`bcp.exe`e `sqlcmd.exe` são instalados `110\Tools` na subpasta do `%PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC` para a versão 11, `130\Tools` e para 13 e 13,1.

Um aplicativo que usa funções do BCP precisa especificar o driver da mesma versão que a fornecida com o arquivo de cabeçalho e a biblioteca usados para compilar o aplicativo.  

Por exemplo, quando você compila um aplicativo ODBC com `msodbcsql11.lib` e `msodbcsql.h`, use "driver = {ODBC Driver 11 para SQL Server}" na cadeia de conexão.

## <a name="components-of-the-microsoft-odbc-driver-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Componentes do Microsoft ODBC Driver para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Windows 
 O driver ODBC no Windows contém os seguintes componentes:
 
|Componente|Descrição|  
|---------------|-----------------|  
|msodbcsql17.dll ou <br> msodbcsql13.dll ou <br> msodbcsql11.dll|O arquivo de biblioteca de vínculo dinâmico (DLL) que contém toda a funcionalidade do driver. Esse arquivo é instalado em%SYSTEMROOT%\System32.|  
|msodbcdiag17. dll ou <br> msodbcdiag13. dll ou <br> msodbcdiag11.dll|O arquivo da DLL (biblioteca de vínculo dinâmico) que contém a interface de diagnóstico do driver (rastreamento). Esse arquivo é instalado em%SYSTEMROOT%\System32.|
|msodbcsqlr17. rll ou <br> msodbcsqlr13.rll ou <br> msodbcsqlr11.rll|O arquivo de recursos que acompanha a biblioteca do driver. Esse arquivo é instalado em%SYSTEMROOT%\System32\1033.| 
|s13ch_msodbcsql.chm ou <br> s11ch_msodbcsql.chm |O arquivo de ajuda do Assistente para Fontes de Dados que documenta como criar uma fonte de dados do driver. Esse arquivo é instalado em%SYSTEMROOT%\System32\1033 <br /> <br /> **Observação:** Não há nenhum arquivo chm para o driver ODBC 17. |  
|msodbcsql.h|O arquivo de cabeçalho que contém todas as novas definições necessárias para usar o driver.<br /><br /> **Observação:**  você não pode referenciar msodbcsql.h e odbcss.h no mesmo programa.<br /><br /> O msodbcsql.h para o ODBC Driver 17 ou 13 é instalado em %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK. <br /> O msodbcsql.h para o ODBC Driver 11 é instalado em %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK.| 
|msodbcsql17.lib ou <br> msodbcsql13.lib ou <br> msodbcsql11.lib|O arquivo de biblioteca necessário para chamar as funções do utilitário **bcp** que fazem parte do driver.<br /><br /> **Observação:** se você referenciar esse arquivo de biblioteca no programa, verifique se ele está no caminho do sistema e no caminho do sistema dos usuários que usam o aplicativo.<br /><br /> O msodbcsql17.lib ou o msodbcsql13.lib é instalado em %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK.<br /> O msodbcsql11.lib é instalado em %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK.|

  
## <a name="see-also"></a>Consulte Também  
 [Microsoft ODBC Driver for SQL Server no Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
  
  
