---
title: Subchaves de especificação de driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], driver specification subkeys
- driver specification subkeys [ODBC]
- registry entries for components [ODBC], driver specification subkeys
- drivers subkey [ODBC]
ms.assetid: b4d802ef-b199-4e64-b7a5-6f2b3e5e2c80
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b15aa278e2fe38afe93f5628433a6c8f4b41cd8e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47656814"
---
# <a name="driver-specification-subkeys"></a>Subchaves de especificação de driver
Cada driver listado na subchave de Drivers ODBC tem uma subchave de seu próprio. Essa subchave tem o mesmo nome que o valor correspondente sob a subchave de Drivers ODBC. Os valores sob essa subchave listam os caminhos completos do driver e DLLs, os valores das palavras-chave driver retornados pela instalação de driver **SQLDrivers**e a contagem de uso. Os formatos de valores são conforme mostrado na tabela a seguir.  
  
|Nome|Tipo de dados|data|  
|----------|---------------|----------|  
|APILevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|ConnectFunctions|REG_SZ|{**Y**&#124; **N**} {**Y**&#124; **N**} {**Y**&#124; **N**}|  
|CreateDSN|REG_SZ|*Descrição do driver*|  
|Driver|REG_SZ|*caminho de DLL do driver*|  
|DriverODBCVer|REG_SZ|*nn.nn*|  
|FileExtns|REG_SZ|**\*.** *arquivo extension1*[**,\*.** *arquivo extension2*]...|  
|FileUsage|REG_SZ|**0** &#124; **1** &#124; **2**|  
|Instalação|REG_SZ|*caminho de DLL de instalação*|  
|SQLLevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|UsageCount|REG_DWORD|*contagem*|  
  
 O uso de cada palavra-chave é mostrado na tabela a seguir.  
  
|Palavra-chave|Uso|  
|-------------|-----------|  
|**APILevel**|Um número que indica o ODBC com suporte pelo driver de nível de conformidade de interface:<br /><br /> 0 = Nenhum<br /><br /> 1 = o nível 1 com suporte<br /><br /> 2 = 2 de nível de suporte<br /><br /> Isso deve ser o mesmo que o valor retornado para a opção SQL_ODBC_INTERFACE_CONFORMANCE na **SQLGetInfo**.|  
|**CreateDSN**|O nome de uma ou mais fontes de dados a ser criado quando o driver está instalado. As informações do sistema devem incluir uma seção de especificação de fonte de dados para cada fonte de dados listado com o **CreateDSN** palavra-chave. Essas seções não devem incluir o **Driver** palavra-chave, porque isso é especificado na seção de especificação de driver, mas deve incluir informações suficientes para que o **ConfigDSN** função no driver DLL para criar uma especificação de fonte de dados sem exibir todas as caixas de diálogo de instalação. Para o formato de uma seção de especificação de fonte de dados, consulte [subchaves de especificação de fonte de dados](../../../odbc/reference/install/data-source-specification-subkeys.md).|  
|**ConnectFunctions**|Uma cadeia de caracteres de três caracteres que indica se o driver dá suporte à **SQLConnect**, **SQLDriverConnect**, e **SQLBrowseConnect**. Se o driver dá suporte ao **SQLConnect**, o primeiro caractere é "Y"; caso contrário, ele é "N". Se o driver dá suporte ao **SQLDriverConnect**, o segundo caractere for "Y"; caso contrário, ele é "N". Se o driver dá suporte ao **SQLBrowseConnect**, o terceiro caractere é "Y"; caso contrário, ele é "N". Por exemplo, se um driver compatível com **SQLConnect** e **SQLDriverConnect** , mas não **SQLBrowseConnect**, a cadeia de caracteres de três caracteres é "YYN".|  
|**DriverODBCVer**|Uma cadeia de caracteres com a versão do ODBC compatíveis com o driver. A versão está no formato *nn.nn*, em que os dois primeiros dígitos são a versão principal e os próximos dois dígitos são a versão secundária. Para obter a versão do ODBC descrita neste manual, o driver deve retornar "03.00".<br /><br /> Isso deve ser o mesmo que o valor retornado para a opção SQL_DRIVER_ODBC_VER na **SQLGetInfo**.|  
|**FileExtns**|Para drivers baseados em arquivo, uma lista separada por vírgulas das extensões dos arquivos de driver pode usar. Por exemplo, um driver do dBASE pode especificar \*. dbf e um driver de arquivo de texto formatado podem especificar \*. txt,\*. csv. Para obter um exemplo de como um aplicativo pode usar essas informações, consulte o **FileUsage** palavra-chave.|  
|**FileUsage**|Um número que indica como um driver de arquivo trata diretamente os arquivos em uma fonte de dados.<br /><br /> 0 = o driver não é um driver de arquivo. Por exemplo, um driver do ORACLE é um driver baseados em DBMS.<br /><br /> 1 = arquivos de trata um driver com base em arquivo em uma fonte de dados como tabelas. Por exemplo, um driver do Xbase trata cada arquivo Xbase como uma tabela.<br /><br /> 2 = arquivos de trata um driver com base em arquivo em uma fonte de dados como um catálogo. Por exemplo, um driver do Microsoft® Access trata cada arquivo do Microsoft Access como um banco de dados completo.<br /><br /> Um aplicativo pode usar isso para determinar como os usuários selecionarão dados. Por exemplo, usuários Xbase e Paradox geralmente imaginar como armazenado em arquivos, enquanto os usuários do ORACLE e Microsoft Access geralmente considera dados como armazenado em tabelas de dados.<br /><br /> Quando um usuário escolhe **abrir arquivo de dados** da **arquivo** menu, um aplicativo pode exibir o **Windows File Open** caixa de diálogo comum. A lista de tipos de arquivo usaria as extensões de arquivo especificadas com o **FileExtns** palavra-chave para os drivers que especificam um **FileUsage** valor 1 e "Y" como o segundo caractere do valor da  **ConnectFunctions** palavra-chave. Depois que o usuário seleciona um arquivo, o aplicativo chamaria **SQLDriverConnect** com o **DRIVER** palavra-chave e, em seguida, execute uma **selecione \* FROM *nome de tabela***   instrução.<br /><br /> Quando o usuário seleciona **importação de dados** da **arquivo** menu, um aplicativo pode exibir uma lista de descrições para os drivers que especificam um **FileUsage** valor 0 ou 2 e "Y" como o segundo caractere do valor de **ConnectFunctions** palavra-chave. Depois que o usuário seleciona um driver, o aplicativo chamaria **SQLDriverConnect** com o **DRIVER** palavra-chave e exiba um personalizado **Selecionar tabela** caixa de diálogo.|  
|**SQLLevel**|Um número que indica a gramática de SQL-92 com suporte pelo driver:<br /><br /> 0 = a entrada do SQL-92<br /><br /> 1 = Transitional FIPS127-2<br /><br /> 2 = SQL-92 intermediário<br /><br /> 3 = SQL-92 Full<br /><br /> Isso deve ser o mesmo que o valor retornado para a opção SQL_SQL_CONFORMANCE na **SQLGetInfo**.|  
  
 Para obter informações sobre contagens de uso, consulte [contagem de uso](../../../odbc/reference/install/usage-counting.md) anteriormente nesta seção.  
  
 Aplicativos não devem definir a contagem de uso. ODBC manterá essa contagem.  
  
 Por exemplo, suponha que um driver para arquivos de texto formatado tem um driver de DLL denominado Text.dll, uma instalação de driver separado DLL chamado Txtsetup.dll e tiver sido instalado três vezes. Se o driver dá suporte ao nível de conformidade com a API do nível 1, oferece o nível de conformidade com a gramática SQL mínima, trata-os como tabelas e pode usar os arquivos com as extensões. txt e. csv, os valores sob a subchave de texto podem ser da seguinte maneira:  
  
```  
APILevel : REG_SZ : 1  
ConnectFunctions : REG_SZ : YYN  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\TEXT.DLL  
DriverODBCVer : REG_SZ : 03.00.00  
FileExtns : REG_SZ : *.txt,*.csv  
FileUsage : REG_SZ : 1  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\TXTSETUP.DLL  
SQLLevel : REG_SZ : 0  
UsageCount : REG_DWORD : 0x3  
```
