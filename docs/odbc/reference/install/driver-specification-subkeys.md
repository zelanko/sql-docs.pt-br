---
title: Subtectas de especificação do driver | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 47aa75f647e5fd8a88168611a3b21284962c70a4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280576"
---
# <a name="driver-specification-subkeys"></a>Subchaves de especificação de driver
Cada driver listado na subchave Drivers ODBC tem uma subchave própria. Esta subchave tem o mesmo nome do valor correspondente sob a sub-chave Drivers ODBC. Os valores sob esta lista de sub-chaves os caminhos completos dos DLLs de configuração do driver e do driver, os valores das palavras-chave do driver retornados pelos **SQLDrivers**e a contagem de uso. Os formatos dos valores são mostrados na tabela a seguir.  
  
|Nome|Tipo de dados|Dados|  
|----------|---------------|----------|  
|APILevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|Funções de conexão|REG_SZ|{**Y**&#124;**N**}{**Y**&#124;**N**}{**Y**&#124;**N**}|  
|CriadoSN|REG_SZ|*driver-descrição*|  
|Driver|REG_SZ|*driver-DLL-path*|  
|DriverODBCVer|REG_SZ|*nn.nn*|  
|FileExtns|REG_SZ|**\*.** *extensão de arquivo1*[**. .\*** *extensão de arquivo2*] ...|  
|FileUse|REG_SZ|**0** &#124; **1** &#124; **2**|  
|Instalação|REG_SZ|*setup-DLL-path*|  
|SQLLevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|Contagem de usos|REG_DWORD|*contagem*|  
  
 O uso de cada palavra-chave é mostrado na tabela a seguir.  
  
|Palavra-chave|Uso|  
|-------------|-----------|  
|**APILevel**|Um número que indica o nível de conformidade da interface ODBC suportado pelo driver:<br /><br /> 0 = Nenhum<br /><br /> 1 = Nível 1 suportado<br /><br /> 2 = Nível 2 suportado<br /><br /> Isso deve ser o mesmo que o valor retornado para a opção SQL_ODBC_INTERFACE_CONFORMANCE no **SQLGetInfo**.|  
|**CriadoSN**|O nome de uma ou mais fontes de dados a serem criadas quando o driver estiver instalado. As informações do sistema devem incluir uma seção de especificação de origem de dados para cada fonte de dados listada com a palavra-chave **CreateDSN.** Essas seções não devem incluir a palavra-chave **Driver,** porque esta é especificada na seção de especificação do driver, mas deve incluir informações suficientes para a função **ConfigDSN** na configuração do driver DLL para criar uma especificação de origem de dados sem exibir nenhuma caixa de diálogo. Para o formato de uma seção de especificação de origem de dados, consulte [Subchaves de especificação de origem de dados](../../../odbc/reference/install/data-source-specification-subkeys.md).|  
|**Funções de conexão**|Uma seqüência de três caracteres indicando se o driver suporta **SQLConnect,** **SQLDriverConnect**e **SQLBrowseConnect**. Se o driver suportar **o SQLConnect,** o primeiro caractere será "Y"; caso contrário, é "N". Se o driver suportar **o SQLDriverConnect,** o segundo caractere é "Y"; caso contrário, é "N". Se o driver suportar **SQLBrowseConnect,** o terceiro caractere é "Y"; caso contrário, é "N". Por exemplo, se um driver suportar **SQLConnect** e **SQLDriverConnect,** mas não **SQLBrowseConnect,** a seqüência de caracteres de três caracteres será "YYN".|  
|**DriverODBCVer**|Uma seqüência de caracteres com a versão de ODBC que o driver suporta. A versão é do formulário *nn.nn,* onde os dois primeiros dígitos são a versão principal e os próximos dois dígitos são a versão menor. Para a versão do ODBC descrita neste manual, o motorista deve retornar "03.00".<br /><br /> Isso deve ser o mesmo que o valor retornado para a opção SQL_DRIVER_ODBC_VER no **SQLGetInfo**.|  
|**FileExtns**|Para drivers baseados em arquivos, uma lista separada por comuma de extensões dos arquivos que o motorista pode usar. Por exemplo, um driver \*dBASE pode especificar .dbf \*e um driver\*de arquivo de texto formatado pode especificar .txt, .csv. Para um exemplo de como um aplicativo pode usar essas informações, consulte a **palavra-chave FileUsage.**|  
|**FileUse**|Um número indicando como um driver baseado em arquivos trata diretamente arquivos em uma fonte de dados.<br /><br /> 0 = O driver não é um driver baseado em arquivos. Por exemplo, um driver ORACLE é um driver baseado em DBMS.<br /><br /> 1 = Um driver baseado em arquivos trata arquivos em uma fonte de dados como tabelas. Por exemplo, um driver Xbase trata cada arquivo Xbase como uma tabela.<br /><br /> 2 = Um driver baseado em arquivos trata arquivos em uma fonte de dados como um catálogo. Por exemplo, um driver de acesso ® Microsoft trata cada arquivo do Microsoft Access como um banco de dados completo.<br /><br /> Um aplicativo pode usar isso para determinar como os usuários selecionarão dados. Por exemplo, os usuários do Xbase e do Paradox muitas vezes pensam em dados como armazenados em arquivos, enquanto os usuários do ORACLE e do Microsoft Access geralmente pensam em dados como armazenados em tabelas.<br /><br /> Quando um usuário seleciona **Abrir arquivo** de dados do menu **Arquivo,** um aplicativo pode exibir a caixa de diálogo comum **Windows File Open.** A lista de tipos de arquivo usaria as extensões de arquivo especificadas com a palavra-chave **FileExtns** para drivers que especificam um valor **fileUsage** de 1 e "Y" como o segundo caractere do valor da palavra-chave **ConnectFunctions.** Depois que o usuário seleciona um arquivo, o aplicativo ligaria **sqldriverConnect** com a palavra-chave **DRIVER** e, em seguida, executaria uma declaração **SELECT \* FROM *nome de tabela.* **<br /><br /> Quando o usuário seleciona **Importar Dados** do menu **Arquivo,** um aplicativo pode exibir uma lista de descrições para drivers que especificam um valor de **FileUse** de 0 ou 2 e "Y" como o segundo caractere do valor da palavra-chave **ConnectFunctions.** Depois que o usuário seleciona um driver, o aplicativo ligaria para **SQLDriverConnect** com a palavra-chave **DRIVER** e, em seguida, exibiria uma caixa de diálogo **Selecionar tabela** personalizada.|  
|**SQLLevel**|Um número que indica a gramática SQL-92 suportada pelo driver:<br /><br /> 0 = Entrada SQL-92<br /><br /> 1 = FIPS127-2 Transicional<br /><br /> 2 = Intermediário SQL-92<br /><br /> 3 = SQL-92 Completo<br /><br /> Isso deve ser o mesmo que o valor retornado para a opção SQL_SQL_CONFORMANCE no **SQLGetInfo**.|  
  
 Para obter informações sobre contagem de uso, consulte [Contagem de uso](../../../odbc/reference/install/usage-counting.md) anteriormente nesta seção.  
  
 Os aplicativos não devem definir a contagem de uso. A ODBC manterá essa contagem.  
  
 Por exemplo, suponha que um driver para arquivos de texto formatados tenha um Driver DLL chamado Text.dll, uma configuração de driver separada DLL chamada Txtsetup.dll, e foi instalado três vezes. Se o driver suportar o nível de conformidade da API nível 1, suportar o nível mínimo de conformidade gramatical SQL, tratar arquivos como tabelas e pode usar arquivos com as extensões .txt e .csv, os valores sob a subchave Text podem ser os seguintes:  
  
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
