---
title: ODBCCONF. EXE | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- odbcconf.exe
ms.assetid: 3bf2be83-61f9-4183-836b-85204ac7116a
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: db8ff09a2b77f51c97ab73d6d994e1e1b4dce2a1
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="odbcconfexe"></a>ODBCCONF. EXE
ODBCCONF.exe é uma ferramenta de linha de comando que permite que você configure os nomes de fonte de dados e drivers ODBC.  
  
> [!NOTE]  
>  ODBCCONF.exe será removido em uma versão futura do Windows Data Access Components. Evite usar esse recurso e planeje modificar os aplicativos que atualmente o utilizam. Você pode usar comandos do PowerShell para gerenciar drivers e fontes de dados. Para obter mais informações sobre esses comandos do PowerShell, consulte [cmdlets do Windows Data Access Components](https://technet.microsoft.com/library/hh771019.aspx).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
ODBCCONF [switches] action  
```  
  
## <a name="arguments"></a>Argumentos  
 *Opções*  
 Zero ou mais opções de comutador. Para obter a lista de opções disponíveis, consulte a seção comentários posteriormente neste tópico.  
  
 *ação*  
 Uma ação a ser executada. Para obter a lista das opções disponíveis, consulte a seção comentários.  
  
## <a name="remarks"></a>Comentários  
 As seguintes opções estão disponíveis:  
  
|Opção|Description|  
|------------|-----------------|  
|/A {*ação*}|Especifique uma ação.<br /><br /> /A é opcional se apenas uma ação é especificada.|  
|/?|Exibir uso de ODBCCONF. EXE.|  
|/C|O processamento continuará se a uma ação falha.|  
|/E|Apaga o arquivo de resposta especificado com /F quando o processamento é concluído.|  
|/F|Usar um arquivo de resposta, como `odbcconf /F my.rsp`.<br /><br /> My.rsp pode ter esta aparência:`REGSVR c:\my.dll`<br /><br /> /A não é usado em um arquivo de resposta.|  
|/H|Exibir uso (Ajuda). Essa opção é o mesmo que /?.|  
|/L [*modo*] *nome de arquivo*|Enviar a saída de programa para um arquivo em um dos três modos: normal (n), detalhado (v) e depuração (d). As DLLs que são carregados por odbcconf.exe de registros de modo de depuração.<br /><br /> Se você especificar /L sem um modo, o arquivo de log será vazio.<br /><br /> Por exemplo, **/Lv txt**.|  
|/R|A ação será executada após uma reinicialização.|  
|/S|Modo silencioso. Não exiba mensagens de erro.|  
  
 As seguintes ações estão disponíveis:  
  
|Ação|Description|  
|------------|-----------------|  
|CONFIGDRIVER *nome_do_driver**parâmetros de configuração específicos de driver*|Carrega a DLL de instalação do driver apropriado e chama o **ConfigDriver** função.<br /><br /> Equivalente a [no SQLConfigDriver função](../odbc/reference/syntax/sqlconfigdriver-function.md).<br /><br /> Por exemplo:<br /><br /> /A {CONFIGDRIVER "Nome do Driver" "CPTimeout = 60"}<br /><br /> /A {CONFIGDRIVER "Nome do Driver" "DriverODBCVer = 03.80"}|  
|CONFIGDSN *nome_do_driver* DSN =*nome* &#124; *atributos*|Adiciona ou modifica uma fonte de dados do sistema.<br /><br /> Equivalente a [função SQLConfigDataSource](../odbc/reference/syntax/sqlconfigdatasource-function.md).<br /><br /> Por exemplo:<br /><br /> /A {CONFIGDSN "SQL Server" "DSN = nome &#124; Server = srv "}|  
|CONFIGSYSDSN *nome_do_driver* DSN =*nome* &#124; *atributos*|Adiciona ou modifica uma fonte de dados do sistema.<br /><br /> Equivalente a [função SQLConfigDataSource](../odbc/reference/syntax/sqlconfigdatasource-function.md).<br /><br /> Por exemplo:<br /><br /> /A {CONFIGSYSDSN "SQL Server" "DSN = nome &#124; Server = srv "}|  
|INSTALLDRIVER|Equivalente a [SQLInstallDriverEx função](../odbc/reference/syntax/sqlinstalldriverex-function.md).<br /><br /> Para obter informações sobre a sintaxe de pares de palavra-chave-valor passada para INSTALLDRIVER, consulte [subchaves de especificação de Driver](../odbc/reference/install/driver-specification-subkeys.md).<br /><br /> Por exemplo:<br /><br /> /A {INSTALLDRIVER "seu Driver &#124; Driver=c:\your.dll &#124; Setup=c:\your.dll &#124; APILevel = 2 &#124; ConnectFunctions = YYY &#124; DriverODBCVer = 03.50 &#124; FileUsage = 0 &#124; SQLLevel = 1"}|  
|INSTALLTRANSLATOR *configuração conversor**caminho de driver*|Adiciona informações sobre um conversor para o **HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST.INI\ODBC tradutores** chave do registro.<br /><br /> Equivalente a [SQLInstallTranslatorEx função](../odbc/reference/syntax/sqlinstalltranslatorex-function.md).<br /><br /> Para obter informações sobre a sintaxe de pares de palavra-chave-valor passada para INSTALLDRIVER, consulte [subchaves de especificação de conversor](../odbc/reference/install/translator-specification-subkeys.md).<br /><br /> Por exemplo:<br /><br /> /A {INSTALLTRANSLATOR "Meu conversor &#124; Translator=c:\My.dll &#124; Setup=c:\My.dll"}|  
|Executar REGSVR *dll*|Registra uma DLL.<br /><br /> Equivalente a regsvr32.exe.<br /><br /> Por exemplo:<br /><br /> /A {executar REGSVR c:\my.dll}|  
|SETFILEDSNDIR|Quando HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC.INI\ODBC DSN\DefaultDSNDir de arquivo não existir, a ação de SETFILEDSNDIR irá criá-lo e atribua o valor em HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\CommonFilesDir, concatenado com \ODBC\Data fontes.<br /><br /> O valor no HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC.INI\ODBC arquivo DSN\DefaultDSNDir Especifica o local padrão usado pelo administrador de fonte de dados ODBC ao criar uma fonte de dados com base em arquivo.<br /><br /> Por exemplo:<br /><br /> /A {SETFILEDSNDIR}|  
  
## <a name="see-also"></a>Consulte também  
 [Microsoft ODBC (Open Database Connectivity)](../odbc/microsoft-open-database-connectivity-odbc.md)

