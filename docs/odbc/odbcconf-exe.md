---
title: ODBCCONF. EXE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- odbcconf.exe
ms.assetid: 3bf2be83-61f9-4183-836b-85204ac7116a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b70622ea038b61883ce7a5307a558a5667139fb1
ms.sourcegitcommit: a26cb217adfbbfb3636dff43fb19a46462e2e994
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74491967"
---
# <a name="odbcconfexe"></a>ODBCCONF. EXE
ODBCCONF. exe é uma ferramenta de linha de comando que permite configurar drivers ODBC e nomes de fonte de dados.  
  
> [!NOTE]  
>  O ODBCCONF. exe será removido em uma versão futura do Windows Data Access Components. Evite usar esse recurso e planeje modificar os aplicativos que atualmente usam esse recurso. Você pode usar comandos do PowerShell para gerenciar drivers e fontes de dados. Para obter mais informações sobre esses comandos do PowerShell, consulte [cmdlets de componentes de acesso a dados do Windows](/powershell/module/wdac).  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
ODBCCONF [switches] action  
```  
  
## <a name="arguments"></a>Argumentos  
 *comutadores*  
 Zero ou mais opções de comutação. Para obter a lista de opções disponíveis, consulte a seção comentários, mais adiante neste tópico.  
  
 *Action*  
 Uma ação a ser executada. Para obter a lista de opções disponíveis, consulte a seção comentários.  
  
## <a name="remarks"></a>Comentários  
 As seguintes opções estão disponíveis:  
  
|Opção|Descrição|  
|------------|-----------------|  
|/A {*ação*}|Especifique uma ação.<br /><br /> /A será opcional se apenas uma ação for especificada.|  
|/?|Exibir o uso de ODBCCONF. EXE.|  
|/C|O processamento continuará se uma ação falhar.|  
|/E|Apague o arquivo de resposta especificado com/F quando o processamento for concluído.|  
|/F|Use um arquivo de resposta, como `odbcconf /F my.rsp`.<br /><br /> o My. rsp pode ter esta aparência:`REGSVR c:\my.dll`<br /><br /> /A não é usado em um arquivo de resposta.|  
|/H|Exibir uso (ajuda). Essa opção é a mesma que/?.|  
|/L [*modo*] *nome do arquivo*|Envie a saída do programa para um arquivo em um dos três modos: normal (n), Verbose (v) e Debug (d). O modo de depuração registra as DLLs que são carregadas pelo odbcconf. exe.<br /><br /> Se você especificar/L sem um modo, o arquivo de log estará vazio.<br /><br /> Por exemplo, **/LV log. txt**.|  
|/R|A ação será executada após uma reinicialização.|  
|/S|Modo silencioso. Não exibir mensagens de erro.|  
  
 As seguintes ações estão disponíveis:  
  
|Ação|Descrição|  
|------------|-----------------|  
|*Parâmetros de configuração específicos do driver CONFIGDRIVER driver_name * **|Carrega a DLL de configuração de driver apropriada e chama a função **ConfigDriver** .<br /><br /> Equivalente à [função SQLConfigDriver](../odbc/reference/syntax/sqlconfigdriver-function.md).<br /><br /> Por exemplo:<br /><br /> /A {CONFIGDRIVER "nome do driver" "CPTimeout = 60"}<br /><br /> /A {CONFIGDRIVER "nome do driver" "DriverODBCVer = 03.80"}|  
|CONFIGDSN *driver_name* DSN =*nome* &#124; *atributos*|Adiciona ou modifica uma fonte de dados do sistema.<br /><br /> Equivalente à [função SQLConfigDataSource](../odbc/reference/syntax/sqlconfigdatasource-function.md).<br /><br /> Por exemplo:<br /><br /> /A {CONFIGDSN "SQL Server" "DSN = Name &#124; Server = SRV"}|  
|CONFIGSYSDSN *driver_name* DSN =*nome* &#124; *atributos*|Adiciona ou modifica uma fonte de dados do sistema.<br /><br /> Equivalente à [função SQLConfigDataSource](../odbc/reference/syntax/sqlconfigdatasource-function.md).<br /><br /> Por exemplo:<br /><br /> /A {CONFIGSYSDSN "SQL Server" "DSN = Name &#124; Server = SRV"}|  
|INSTALLDRIVER|Equivalente à [função SQLInstallDriverEx](../odbc/reference/syntax/sqlinstalldriverex-function.md).<br /><br /> Para obter informações sobre a sintaxe de pares de palavras-chave e valor passado para INSTALLDRIVER, consulte [subchaves de especificação de driver](../odbc/reference/install/driver-specification-subkeys.md).<br /><br /> Por exemplo:<br /><br /> /A {INSTALLDRIVER "seu driver &#124; driver = c:\Your.dll &#124; instalação = c:\Your.dll &#124; APILevel = 2 &#124; ConnectFunctions = YYY &#124; DriverODBCVer = 03.50 &#124; fileusage = 0 &#124; sqllevel = 1"}|  
|*Configuração do tradutor INSTALLTRANSLATOR * * caminho do driver*|Adiciona informações sobre um tradutor ao **HKEY_LOCAL_MACHINE \software\odbc\odbcinst. **Chave do registro de tradutores INI\ODBC.<br /><br /> Equivalente à [função SQLInstallTranslatorEx](../odbc/reference/syntax/sqlinstalltranslatorex-function.md).<br /><br /> Para obter informações sobre a sintaxe de pares de palavras-chave e valor passados para INSTALLDRIVER, consulte [subchaves de especificação do tradutor](../odbc/reference/install/translator-specification-subkeys.md).<br /><br /> Por exemplo:<br /><br /> /A {INSTALLTRANSLATOR "meu tradutor &#124; Tradutor = c:\My.dll &#124; setup = c:\My.dll"}|  
|*Dll* regsvr|Registra uma DLL.<br /><br /> Equivalente a regsvr32. exe.<br /><br /> Por exemplo:<br /><br /> /A {REGSVR c:\My.dll}|  
|SETFILEDSNDIR|Quando HKEY_LOCAL_MACHINE \SOFTWARE\ODBC\ODBC. O arquivo INI\ODBC DSN\DefaultDSNDir não existe, a ação SETFILEDSNDIR o criará e atribuirá a ele o valor em HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Windows\CurrentVersion\CommonFilesDir, acrescentado com as fontes \ODBC\Data.<br /><br /> O valor em HKEY_LOCAL_MACHINE \SOFTWARE\ODBC\ODBC. O arquivo INI\ODBC DSN\DefaultDSNDir especifica o local padrão usado pelo administrador de fonte de dados ODBC ao criar uma fonte de dados baseada em arquivo.<br /><br /> Por exemplo:<br /><br /> /A {SETFILEDSNDIR}|  
  
## <a name="see-also"></a>Consulte Também  
 [ODBC (Microsoft Open Database Connectivity)](../odbc/microsoft-open-database-connectivity-odbc.md)
