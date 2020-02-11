---
title: Subchaves de especificação do driver | Microsoft Docs
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
ms.openlocfilehash: 8f5523c54286ed2e7cc554745dc269599115793e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68094175"
---
# <a name="driver-specification-subkeys"></a>Subchaves de especificação de driver
Cada driver listado na subchave de drivers ODBC tem uma subchave própria. Essa subchave tem o mesmo nome que o valor correspondente na subchave de drivers ODBC. Os valores nessa subchave listam os caminhos completos das DLLs de instalação do driver e Driver, os valores das palavras-chave do driver retornadas por **SQLDrivers**e a contagem de uso. Os formatos dos valores são mostrados na tabela a seguir.  
  
|Nome|Tipo de dados|data|  
|----------|---------------|----------|  
|APILevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|ConnectFunctions|REG_SZ|{**Y**&#124;**n**} {**y**&#124;**n**} {**y**&#124;**n**}|  
|CreateDSN|REG_SZ|*Descrição do driver*|  
|Driver|REG_SZ|*Driver-DLL-caminho*|  
|DriverODBCVer|REG_SZ|*nn. nn*|  
|FileExtns|REG_SZ|**\*.** *arquivo-extension1*[**,\*.** *arquivo-extension2*] ...|  
|Uso de|REG_SZ|**0** &#124; **1** &#124; **2**|  
|Instalação|REG_SZ|*Instalação-DLL-caminho*|  
|Sqllevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|UsageCount|REG_DWORD|*contagem*|  
  
 O uso de cada palavra-chave é mostrado na tabela a seguir.  
  
|Palavra-chave|Uso|  
|-------------|-----------|  
|**APILevel**|Um número que indica o nível de conformidade da interface ODBC com suporte do driver:<br /><br /> 0 = Nenhum<br /><br /> 1 = nível 1 com suporte<br /><br /> 2 = nível 2 com suporte<br /><br /> Isso deve ser o mesmo que o valor retornado para a opção SQL_ODBC_INTERFACE_CONFORMANCE em **SQLGetInfo**.|  
|**CreateDSN**|O nome de uma ou mais fontes de dados a serem criadas quando o driver for instalado. As informações do sistema devem incluir uma seção de especificação de fonte de dados para cada fonte de dados listada com a palavra-chave **CreateDSN** . Essas seções não devem incluir a palavra-chave do **Driver** , pois isso é especificado na seção especificação do driver, mas deve incluir informações suficientes para a função **ConfigDSN** na DLL de instalação do driver para criar uma especificação de fonte de dados sem exibir nenhuma caixa de diálogo. Para o formato de uma seção especificação de fonte de dados, consulte [subchaves de especificação da fonte de dados](../../../odbc/reference/install/data-source-specification-subkeys.md).|  
|**ConnectFunctions**|Uma cadeia de caracteres de três caracteres que indica se o driver dá suporte a **SQLConnect**, **SQLDriverConnect**e **SQLBrowseConnect**. Se o driver oferecer suporte a **SQLConnect**, o primeiro caractere será "Y"; caso contrário, será "N". Se o driver oferecer suporte a **SQLDriverConnect**, o segundo caractere será "Y"; caso contrário, será "N". Se o driver oferecer suporte a **SQLBrowseConnect**, o terceiro caractere será "Y"; caso contrário, será "N". Por exemplo, se um driver oferecer suporte a **SQLConnect** e **SQLDriverConnect** , mas não **SQLBrowseConnect**, a cadeia de caracteres de três caracteres será "YYN".|  
|**DriverODBCVer**|Uma cadeia de caracteres com a versão do ODBC à qual o driver dá suporte. A versão é do formato *nn. nn*, em que os dois primeiros dígitos são a versão principal e os próximos dois dígitos são a versão secundária. Para a versão do ODBC descrita neste manual, o driver deve retornar "3, 0".<br /><br /> Isso deve ser o mesmo que o valor retornado para a opção SQL_DRIVER_ODBC_VER em **SQLGetInfo**.|  
|**FileExtns**|Para drivers baseados em arquivo, uma lista separada por vírgulas de extensões dos arquivos que o driver pode usar. Por exemplo, um driver do dBASE pode \*especificar. dbf e um driver de arquivo de texto \*formatado pode especificar\*. txt,. csv. Para obter um exemplo de como um aplicativo pode usar essas informações, consulte a palavra-chave **fileusage** .|  
|**Uso de**|Um número que indica como um driver baseado em arquivo trata diretamente os arquivos em uma fonte de dados.<br /><br /> 0 = o driver não é um driver baseado em arquivo. Por exemplo, um driver ORACLE é um driver baseado em DBMS.<br /><br /> 1 = um driver baseado em arquivo trata os arquivos em uma fonte de dados como tabelas. Por exemplo, um driver Xbase trata cada arquivo Xbase como uma tabela.<br /><br /> 2 = um driver baseado em arquivo trata os arquivos em uma fonte de dados como um catálogo. Por exemplo, um driver de acesso ao Microsoft® trata cada arquivo do Microsoft Access como um banco de dados completo.<br /><br /> Um aplicativo pode usar isso para determinar como os usuários selecionarão os dados. Por exemplo, os usuários Xbase e Paradox geralmente consideram os dados armazenados em arquivos, enquanto os usuários do ORACLE e do Microsoft Access geralmente consideram os dados armazenados em tabelas.<br /><br /> Quando um usuário seleciona **Abrir arquivo de dados** no menu **arquivo** , um aplicativo pode exibir a caixa de diálogo comum **Abrir arquivo do Windows** . A lista de tipos de arquivo usaria as extensões de arquivo especificadas com a palavra-chave **FileExtns** para drivers que especificam um valor de **fileusage** de 1 e "Y" como o segundo caractere do valor da palavra-chave **ConnectFunctions** . Depois que o usuário selecionar um arquivo, o aplicativo chamaria **SQLDriverConnect** com a palavra-chave do **Driver** e executaria uma instrução **Select \* from *table-name* ** .<br /><br /> Quando o usuário seleciona **importar dados** no menu **arquivo** , um aplicativo pode exibir uma lista de descrições de drivers que especificam um valor de **fileusage** de 0 ou 2 e "Y" como o segundo caractere do valor da palavra-chave **ConnectFunctions** . Depois que o usuário selecionar um driver, o aplicativo chamaria **SQLDriverConnect** com a palavra-chave **Driver** e, em seguida, exibiria uma caixa de diálogo personalizada **selecionar tabela** .|  
|**Sqllevel**|Um número que indica a gramática do SQL-92 suportada pelo driver:<br /><br /> 0 = entrada do SQL-92<br /><br /> 1 = transição de FIPS127-2<br /><br /> 2 = SQL-92 intermediário<br /><br /> 3 = SQL-92 completo<br /><br /> Isso deve ser o mesmo que o valor retornado para a opção SQL_SQL_CONFORMANCE em **SQLGetInfo**.|  
  
 Para obter informações sobre contagens de uso, consulte [contagem de uso](../../../odbc/reference/install/usage-counting.md) anteriormente nesta seção.  
  
 Os aplicativos não devem definir a contagem de uso. O ODBC manterá essa contagem.  
  
 Por exemplo, suponha que um driver para arquivos de texto formatados tenha uma DLL de driver denominada Text. dll, uma DLL de instalação de driver separada denominada txtsetup. dll e tenha sido instalada três vezes. Se o driver der suporte ao nível de conformidade da API de nível 1, o oferecerá suporte ao nível mínimo de conformidade da gramática do SQL, tratará arquivos como tabelas e poderá usar arquivos com as extensões. txt e. csv, os valores na subchave de texto poderão ser os seguintes:  
  
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
