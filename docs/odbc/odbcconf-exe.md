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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d771f01d292312f8a0f0060c16e3c348bf2e009e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307527"
---
# <a name="odbcconfexe"></a>ODBCCONF. Exe
ODBCCONF.exe é uma ferramenta de linha de comando que permite configurar drivers ODBC e nomes de origem de dados.  
  
> [!NOTE]  
>  O DBCCONF.exe será removido em uma versão futura do Windows Data Access Components. Evite usar esse recurso e planeje modificar aplicativos que atualmente usam esse recurso. Você pode usar comandos PowerShell para gerenciar drivers e fontes de dados. Para obter mais informações sobre esses comandos PowerShell, consulte [cmdlets do Windows Data Access Components](/powershell/module/wdac).  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
ODBCCONF [switches] action  
```  
  
## <a name="arguments"></a>Argumentos  
 *Interruptores*  
 Zero ou mais opções de switch. Para obter a lista de switches disponíveis, consulte a seção Observações, mais tarde neste tópico.  
  
 *Ação*  
 Uma ação para realizar. Para obter a lista de opções disponíveis, consulte a seção Observações.  
  
## <a name="remarks"></a>Comentários  
 Os seguintes switches estão disponíveis:  
  
|Opção|Descrição|  
|------------|-----------------|  
|/A {*ação*}|Especifique uma ação.<br /><br /> /A é opcional se apenas uma ação for especificada.|  
|/?|Exibir o uso para ODBCCONF. Exe.|  
|/C|O processamento continua se uma ação falhar.|  
|/E|Apague o arquivo de resposta especificado com /F quando o processamento estiver concluído.|  
|/F|Use um arquivo de `odbcconf /F my.rsp`resposta, como .<br /><br /> my.rsp pode ficar assim:`REGSVR c:\my.dll`<br /><br /> /A não é usado em um arquivo de resposta.|  
|/H|Exibir o uso (Ajuda). Este interruptor é o mesmo que /?.|  
|/L[*modo*] *nome do arquivo*|Enviar saída do programa para um arquivo em um dos três modos: normal (n), verbose (v) e depuração (d). O modo Debug registra as DLLs carregadas por odbcconf.exe.<br /><br /> Se você especificar /L sem um modo, o arquivo de log estará vazio.<br /><br /> Por exemplo, **/Lv log.txt**.|  
|/R|A ação será realizada após um reboot.|  
|/S|Modo silencioso. Não exiba mensagens de erro.|  
  
 As seguintes ações estão disponíveis:  
  
|Ação|Descrição|  
|------------|-----------------|  
|*PARAMs de configuração específicas do driver_name**do driver*|Carrega a configuração apropriada do driver DLL e chama a função **ConfigDriver.**<br /><br /> Equivalente à [função SQLConfigDriver](../odbc/reference/syntax/sqlconfigdriver-function.md).<br /><br /> Por exemplo:<br /><br /> /A {CONFIGDRIVER " Driver Name" "CPTimeout=60"}<br /><br /> /A {CONFIGDRIVER " Driver Name" "DriverODBCVer=03.80"}|  
|CONFIGDSN *driver_name* *atributos* de &#124;*de nome*|Adiciona ou modifica uma fonte de dados do sistema.<br /><br /> Equivalente à [função SQLConfigDataSource](../odbc/reference/syntax/sqlconfigdatasource-function.md).<br /><br /> Por exemplo:<br /><br /> /A {CONFIGDSN "SQL Server" "DSN=name &#124; Server=srv"}|  
|CONFIGSYSDSN *driver_name* *Atributos* de &#124;*de nome*|Adiciona ou modifica uma fonte de dados do sistema.<br /><br /> Equivalente à [função SQLConfigDataSource](../odbc/reference/syntax/sqlconfigdatasource-function.md).<br /><br /> Por exemplo:<br /><br /> /A {CONFIGSYSDSN "SQL Server" "DSN=name &#124; Server=srv"}|  
|Installdriver|Equivalente à [função SQLInstallDriverEx](../odbc/reference/syntax/sqlinstalldriverex-function.md).<br /><br /> Para obter informações sobre a sintaxe de pares de valor de palavra-chave passada para INSTALLDRIVER, consulte [Subtecas de especificação do driver](../odbc/reference/install/driver-specification-subkeys.md).<br /><br /> Por exemplo:<br /><br /> /A {INSTALLDRIVER "Seu driver &#124; driver=c:\your.dll &#124; Setup=c:\your.dll &#124; APILevel=2 &#124; ConnectFunctions=YYY &#124; DriverODBCVer=03,50 &#124; FileUsage=0 &#124; SQLLevel=1"}|  
|*INSTALARconfiguração do tradutor tradutor**caminho do driver*|Adiciona informações sobre um tradutor ao **HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST. Chave de registro de tradutores INI\ODBC.**<br /><br /> Equivalente à [função SQLInstallTranslatorEx](../odbc/reference/syntax/sqlinstalltranslatorex-function.md).<br /><br /> Para obter informações sobre a sintaxe de pares de valor de palavra-chave passada para INSTALLDRIVER, consulte [Subtecas de especificação de tradutor](../odbc/reference/install/translator-specification-subkeys.md).<br /><br /> Por exemplo:<br /><br /> /A {INSTALLTRANSLATOR "Meu Tradutor &#124; Tradutor=c:\my.dll &#124; Setup=c:\my.dll"}|  
|*ROrC svr*|Registra um DLL.<br /><br /> Equivalente a regsvr32.exe.<br /><br /> Por exemplo:<br /><br /> /A {REGSVR c:\my.dll}|  
|SETFILEDSNDIR|Quando HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC. Ini\ODBC File DSN\DefaultDSNDir não existe, a ação SETFILEDSNDIR irá criá-la e atribuir-lhe o valor em HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft\Current\CurrentVersion\CommonFilesDir, anexado com \ODBC\Data Sources.<br /><br /> O valor em HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC. O Arquivo INI\ODBC DSN\DefaultDSNDir especifica o local padrão usado pelo Administrador de Origem de Dados do ODBC ao criar uma fonte de dados baseada em arquivos.<br /><br /> Por exemplo:<br /><br /> /A {SETFILEDSNDIR}|  
  
## <a name="see-also"></a>Consulte Também  
 [Microsoft ODBC (Open Database Connectivity)](../odbc/microsoft-open-database-connectivity-odbc.md)
