---
title: Driver especificação subchaves | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], driver specification subkeys
- driver specification subkeys [ODBC]
- registry entries for components [ODBC], driver specification subkeys
- drivers subkey [ODBC]
ms.assetid: b4d802ef-b199-4e64-b7a5-6f2b3e5e2c80
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 017e2ff63f93fed46df72e35f1a4f678a147aa04
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32920391"
---
# <a name="driver-specification-subkeys"></a>Subchaves de especificação de driver
Cada driver listado na subchave Drivers ODBC tem uma subchave de seu próprio. Essa subchave tem o mesmo nome que o valor correspondente na subchave Drivers ODBC. Os valores sob essa subchave listam os caminhos completos do driver e o programa de instalação do driver DLLs, os valores das palavras-chave driver retornados por **SQLDrivers**e a contagem de uso. Os formatos dos valores são conforme mostrado na tabela a seguir.  
  
|Nome|Tipo de dados|data|  
|----------|---------------|----------|  
|APILevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|ConnectFunctions|REG_SZ|{**Y**&#124; **N**} {**Y**&#124; **N**} {**Y**&#124; **N**}|  
|CreateDSN|REG_SZ|*Descrição do driver*|  
|Driver|REG_SZ|*caminho de DLL do driver*|  
|DriverODBCVer|REG_SZ|*nn.nn*|  
|FileExtns|REG_SZ|**\*.** *arquivo extension1*[**,\*.** *arquivo extension2*]...|  
|FileUsage|REG_SZ|**0** &#124; **1** &#124; **2**|  
|Instalação|REG_SZ|*caminho da DLL de instalação*|  
|SQLLevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|UsageCount|REG_DWORD|*contagem*|  
  
 O uso de cada palavra-chave é mostrado na tabela a seguir.  
  
|Palavra-chave|Uso|  
|-------------|-----------|  
|**APILevel**|Um número que indica o ODBC interface compatível com o driver de nível de conformidade:<br /><br /> 0 = Nenhum<br /><br /> 1 = 1 de nível de suporte<br /><br /> 2 = nível 2 com suporte<br /><br /> Isso deve ser o mesmo que o valor retornado para a opção SQL_ODBC_INTERFACE_CONFORMANCE **SQLGetInfo**.|  
|**CreateDSN**|O nome de uma ou mais fontes de dados a ser criado quando o driver está instalado. As informações do sistema devem incluir uma seção de especificação de fonte de dados para cada fonte de dados listado com o **CreateDSN** palavra-chave. Essas seções não devem incluir o **Driver** palavra-chave, porque isso é especificado na seção de especificação de driver, mas deve incluir informações suficientes para o **ConfigDSN** função no driver DLL para criar uma especificação de fonte de dados sem exibir uma caixa de diálogo de configuração. Para o formato de uma seção de especificação de fonte de dados, consulte [subchaves de especificação de fonte de dados](../../../odbc/reference/install/data-source-specification-subkeys.md).|  
|**ConnectFunctions**|Uma cadeia de caracteres de três caracteres que indica se o driver dá suporte a **SQLConnect**, **SQLDriverConnect**, e **SQLBrowseConnect**. Se o driver dá suporte a **SQLConnect**, o primeiro caractere é "Y"; caso contrário, ele é "N". Se o driver dá suporte a **SQLDriverConnect**, o segundo caractere é "Y"; caso contrário, ele é "N". Se o driver dá suporte a **SQLBrowseConnect**, o terceiro caractere é "Y"; caso contrário, ele é "N". Por exemplo, se um driver compatível com **SQLConnect** e **SQLDriverConnect** mas não **SQLBrowseConnect**, a cadeia de caracteres de três é "YYN".|  
|**DriverODBCVer**|Uma cadeia de caracteres com a versão do ODBC que o driver dá suporte. É a versão do formulário *nn.nn*, em que os dois primeiros dígitos são a versão principal, e os dois dígitos são a versão secundária. Para obter a versão do ODBC descrito neste manual, o driver deve retornar "03.00".<br /><br /> Isso deve ser o mesmo que o valor retornado para a opção SQL_DRIVER_ODBC_VER **SQLGetInfo**.|  
|**FileExtns**|Para drivers baseados em arquivo, uma lista separada por vírgulas das extensões dos arquivos de driver pode usar. Por exemplo, um driver dBASE pode especificar \*. dbf e um driver de arquivo de texto formatado podem especificar \*. txt,\*. csv. Para obter um exemplo de como um aplicativo pode usar essas informações, consulte o **FileUsage** palavra-chave.|  
|**FileUsage**|Um número que indica como um driver baseada em arquivo trata diretamente os arquivos em uma fonte de dados.<br /><br /> 0 = o driver não é um driver baseada em arquivo. Por exemplo, um driver ORACLE é um driver de DBMS.<br /><br /> 1 = arquivos de trata um driver baseada em arquivo em uma fonte de dados como tabelas. Por exemplo, um driver Xbase trata cada arquivo Xbase como uma tabela.<br /><br /> 2 = arquivos de trata um driver baseada em arquivo em uma fonte de dados como um catálogo. Por exemplo, um driver do Microsoft® Access trata cada arquivo do Microsoft Access como um banco de dados completo.<br /><br /> Um aplicativo pode usar isso para determinar como os usuários irão selecionar dados. Por exemplo, usuários Xbase e Paradox geralmente pensar de dados armazenados em arquivos, enquanto usuários ORACLE e o Microsoft Access geralmente considere dos dados armazenados em tabelas.<br /><br /> Quando um usuário seleciona **abrir arquivo de dados** do **arquivo** menu, um aplicativo pode exibir o **abrir do arquivo Windows** caixa de diálogo comum. A lista de tipos de arquivo usaria as extensões de arquivo especificadas com o **FileExtns** palavra-chave para drivers que especificam um **FileUsage** valor 1 e "Y" como o segundo caractere do valor da  **ConnectFunctions** palavra-chave. Depois que o usuário seleciona um arquivo, o aplicativo deve chamar **SQLDriverConnect** com o **DRIVER** palavra-chave e, em seguida, execute uma **selecione \* FROM *nome de tabela***   instrução.<br /><br /> Quando o usuário seleciona **importar dados** do **arquivo** menu, um aplicativo pode exibir uma lista de descrições de drivers que especificam um **FileUsage** valor 0 ou 2 e "Y" como o segundo caractere do valor da **ConnectFunctions** palavra-chave. Depois que o usuário seleciona um driver, o aplicativo deve chamar **SQLDriverConnect** com o **DRIVER** palavra-chave e, em seguida, exibir um personalizado **Selecionar tabela** caixa de diálogo.|  
|**SQLLevel**|Um número que indica a gramática de SQL-92 suportada do driver:<br /><br /> 0 = a entrada do SQL-92<br /><br /> 1 = transição FIPS127-2<br /><br /> 2 = intermediário de SQL-92<br /><br /> 3 = completo do SQL-92<br /><br /> Isso deve ser o mesmo que o valor retornado para a opção SQL_SQL_CONFORMANCE **SQLGetInfo**.|  
  
 Para obter informações sobre contagens de uso, consulte [contagem de uso](../../../odbc/reference/install/usage-counting.md) anteriormente nesta seção.  
  
 Aplicativos não devem definir a contagem de uso. ODBC manterá essa contagem.  
  
 Por exemplo, suponha que um driver para arquivos de texto formatado tem um DLL denominada Text.dll do driver, uma instalação de driver separado DLL denominada Txtsetup.dll e instalou três vezes. Se o driver dá suporte ao nível de conformidade com a API do nível 1, oferece o nível de conformidade de gramática SQL mínima, trata arquivos como tabelas e pode usar arquivos com as extensões. txt e. csv, os valores na subchave texto podem ser como segue:  
  
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
