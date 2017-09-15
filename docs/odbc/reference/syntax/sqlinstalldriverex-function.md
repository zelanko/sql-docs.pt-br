---
title: "Função SQLInstallDriverEx | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLInstallDriverEx
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallDriverEx
helpviewer_keywords:
- SQLInstallDriverEx function [ODBC]
ms.assetid: 1dd74544-f4e9-46e1-9b5f-c11d84fdab4c
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2eda9fe4e6a5f300f83512f669ad5206f89effe6
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlinstalldriverex-function"></a>Função SQLInstallDriverEx
**Conformidade**  
 Versão introduzidas: ODBC 3.0  
  
 **Resumo**  
 **SQLInstallDriverEx** adiciona informações sobre o driver para a entrada Odbcinst.ini nas informações do sistema e incrementa o driver *UsageCount* em 1. No entanto, se uma versão de driver já existe, mas o *UsageCount* valor para o driver não existir, o novo *UsageCount* valor é definido como 2.  
  
 Essa função realmente não copia todos os arquivos. É responsabilidade do programa de chamada para copiar os arquivos do driver para o diretório de destino corretamente.  
  
 A funcionalidade de **SQLInstallDriverEx** também podem ser acessados com [ODBCCONF. EXE](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BOOL SQLInstallDriverEx(  
     LPCSTR    lpszDriver,  
     LPCSTR    lpszPathIn,  
     LPSTR     lpszPathOut,  
     WORD      cbPathOutMax,  
     WORD *    pcbPathOut,  
     WORD      fRequest,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszDriver*  
 [Entrada] A descrição do driver (geralmente o nome do DBMS associado) apresentada aos usuários em vez do nome físico do driver. O *lpszDriver* argumento deve conter uma lista duplamente terminada em nulo de pares de palavra-chave-valor que descreve o driver. Para obter mais informações sobre os pares de valor de palavra-chave, consulte [subchaves de especificação de Driver](../../../odbc/reference/install/driver-specification-subkeys.md). Para obter mais informações sobre a cadeia de caracteres terminada em nulo duplamente, consulte [ConfigDSN função](../../../odbc/reference/syntax/configdsn-function.md).  
  
 *lpszPathIn*  
 [Entrada] Caminho completo do diretório de destino da instalação ou um ponteiro nulo. Se *lpszPathIn* é um ponteiro nulo, os drivers serão instalados no diretório do sistema.  
  
 *lpszPathOut*  
 [Saída] Caminho do diretório de destino onde o driver deve ser instalado. Se o driver anteriormente não foi instalado, *lpszPathOut* deve ser o mesmo que *lpszPathIn*. Se o driver foi instalado anteriormente, *lpszPathOut* é o caminho da instalação anterior.  
  
 *cbPathOutMax*  
 [Entrada] Comprimento de *lpszPathOut*.  
  
 *pcbPathOut*  
 [Saída] Número total de bytes (excluindo o caractere null de terminação) disponíveis para retornar em *lpszPathOut*. Se o número de bytes disponíveis para retornar é maior que ou igual a *cbPathOutMax*, o caminho de saída em *lpszPathOut* será truncado para *cbPathOutMax* menos de caractere de terminação nula. O *pcbPathOut* argumento pode ser um ponteiro nulo.  
  
 *Frequentes*  
 [Entrada] Tipo de solicitação. O *frequentes* argumento deve conter um dos seguintes valores:  
  
 ODBC_INSTALL_INQUIRY: Saber em que um driver pode ser instalado.  
  
 ODBC_INSTALL_COMPLETE: Conclua a solicitação de instalação.  
  
 *lpdwUsageCount*  
 [Saída] A contagem de uso do driver depois que essa função foi chamada.  
  
 Aplicativos não devem definir a contagem de uso. ODBC manterá essa contagem.  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedida, FALSO se ele falhar.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLInstallDriverEx** retorna FALSE, um tipo de * \*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista o * \*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral de instalador|Ocorreu um erro para que nenhum erro específico do instalador.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Comprimento de buffer inválido|O *lpszPathOut* argumento não era grande o suficiente para conter o caminho de saída. O buffer contém o caminho truncado.<br /><br /> O *cbPathOutMax* argumento era 0, e *frequentes* foi ODBC_INSTALL_COMPLETE.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitação inválido|O *frequentes* argumento não era um dos seguintes:<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Pares de valor de palavra-chave inválida|O *lpszDriver* argumento continha um erro de sintaxe.|  
|ODBC_ERROR_INVALID_PATH|Caminho de instalação inválido|O *lpszPathIn* argumento continha um caminho inválido.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Não foi possível carregar a biblioteca de instalação de driver ou conversor|Não foi possível carregar a biblioteca de instalação do driver.|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|Sequência de parâmetro inválido|O *lpszDriver* argumento não continha uma lista de pares de valor de palavra-chave.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Não foi possível incrementar ou decrementar a contagem de uso do componente|Falha do instalador usado incrementar a contagem de utilização do driver.|  
  
## <a name="comments"></a>Comentários  
 O *lpszDriver* argumento é uma lista de atributos na forma de pares de valor de palavra-chave. Cada par é encerrada com um byte nulo e a lista inteira é encerrada com um byte nulo. (Ou seja, dois bytes nulos marcar o fim da lista.) O formato desta lista é da seguinte maneira:  
  
 *driver desc* ** \\ **0Driver**=***nome da DLL de driver* ** \\ **0 [instalação**=***nome da DLL de instalação***\\**0]  
  
 [*driver-attr-keyword1***=***value1***\\**0] [*keyword2 de attr de driver * ** = ** *value2***\\**0]... ** \\ **0  
  
 onde \0 é um byte nulo e *driver-attr-keywordn* é qualquer palavra-chave do atributo de driver. As palavras-chave devem aparecer na ordem especificada. Por exemplo, suponha que um driver para arquivos de texto formatado tem driver separado e DLLs de instalação e pode usar arquivos com as extensões. txt e. csv. O *lpszDriver* argumento para esse driver poderia ser como segue:  
  
```  
Text\0Driver=TEXT.DLL\0Setup=TXTSETUP.DLL\0FileUsage=1\0  
FileExtns=*.txt,*.csv\0\0  
```  
  
 Suponha que um driver para SQL Server não tem uma DLL de instalação separado e não tem quaisquer palavras-chave do atributo de driver. O *lpszDriver* argumento para esse driver poderia ser como segue:  
  
```  
SQL Server\0Driver=SQLSRVR.DLL\0\0  
```  
  
 Depois de **SQLInstallDriverEx** recupera informações sobre o driver a partir de *lpszDriver* argumento, ele adiciona a descrição do driver para a seção [Drivers ODBC] da entrada Odbcinst.ini no sistema informações. Em seguida, cria uma seção com a descrição do driver e adiciona caminhos completos do driver DLL e a DLL de configuração. Finalmente, ele retorna o caminho do diretório de destino da instalação, mas não copiar os arquivos de driver para ela. O programa de chamada, na verdade, deve copiar os arquivos de driver para o diretório de destino.  
  
 **SQLInstallDriverEx** incrementa a contagem de uso do componente para o driver instalado em 1. Se já existe uma versão do driver, mas a contagem de uso do componente para o driver não existir, o novo valor de contagem de uso do componente é definido como 2.  
  
 O programa de instalação do aplicativo é responsável por copiar fisicamente o arquivo de driver e manter a contagem de uso de arquivos. Se o arquivo do driver anteriormente não foi instalado, o programa de instalação do aplicativo deve copiar o arquivo no *lpszPathIn* caminho e crie a contagem de uso de arquivos. Se o arquivo tiver sido instalado anteriormente, o programa de instalação simplesmente incrementa a contagem de uso de arquivo e retorna o caminho da instalação anterior no *lpszPathOut* argumento.  
  
> [!NOTE]  
>  Para obter mais informações sobre contagens de uso do componente e contagens de uso de arquivo, consulte [contagem de uso](../../../odbc/reference/install/usage-counting.md).  
  
 Se uma versão mais antiga do arquivo do driver foi instalada anteriormente pelo aplicativo, o driver deve ser desinstalado e reinstalado, para que a contagem de uso do componente de driver é válida. **No SQLConfigDriver** (com um *frequentes* de ODBC_REMOVE_DRIVER) deve ser chamada primeiro e, em seguida, **no SQLRemoveDriver** deve ser chamado para decrementar a contagem de uso do componente. **SQLInstallDriverEx** , em seguida, deve ser chamado para reinstalar o driver, incrementar a contagem de uso do componente. O programa de instalação do aplicativo deve substituir o arquivo antigo com o novo arquivo. A contagem de uso de arquivo permanece o mesmo, e qualquer outro aplicativo que usavam o arquivo de versão mais antigo agora usará a versão mais recente.  
  
> [!NOTE]  
>  Se o driver foi instalado anteriormente e **SQLInstallDriverEx** é chamado para instalar o driver em um diretório diferente, a função retornará TRUE, mas *lpszPathOut* incluirá o diretório onde o driver já foi instalado. Não incluirá o diretório digitado no *lpszDriver* argumento.  
  
 O comprimento do caminho em *lpszPathOut* na **SQLInstallDriverEx** permite que um processo de instalação de duas fases, para que um aplicativo possa determinar o que *cbPathOutMax* deve ser chamando **SQLInstallDriverEx** com um *frequentes* de modo ODBC_INSTALL_INQUIRY. Isso retornará o número total de bytes disponíveis no *pcbPathOut* buffer. **SQLInstallDriverEx** , em seguida, pode ser chamado com um *frequentes* de ODBC_INSTALL_COMPLETE e o *cbPathOutMax* argumento definido como o valor de *pcbPathOut*buffer mais o caractere de terminação nula.  
  
 Se você optar por não usar o modelo de duas fases para **SQLInstallDriverEx**, você deve definir *cbPathOutMax*, que define o tamanho do armazenamento para o caminho do diretório de destino, para o valor MAX_PATH, como definido em Stdlib.h, para evitar truncamento.  
  
 Quando *frequentes* é ODBC_INSTALL_COMPLETE, **SQLInstallDriverEx** não permite *lpszPathOut* NULL (ou *cbPathOutMax* para ser 0). Se *frequentes* é ODBC_INSTALL_COMPLETE, FALSE será retornado quando o número de bytes disponíveis para retornar é maior que ou igual a *cbPathOutMax*, sabendo que o truncamento ocorre.  
  
 Depois de **SQLInstallDriverEx** foi chamado e o programa de instalação do aplicativo copiou o arquivo de driver (se necessário), a instalação do driver DLL deve chamar **no SQLConfigDriver** para definir a configuração para o driver.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Instalando o Gerenciador de Driver|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
