---
title: Função SQLInstallDriverEx | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 673e3e53468780ef261a22b00a2ec1bb9df0e184
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68030598"
---
# <a name="sqlinstalldriverex-function"></a>Função SQLInstallDriverEx
**Conformidade com**  
 Versão introduzida: ODBC 3.0  
  
 **Resumo**  
 **SQLInstallDriverEx** adiciona informações sobre o driver para a entrada Odbcinst. ini nas informações do sistema e incrementa o driver *UsageCount* em 1. No entanto, se uma versão do driver já existe, mas o *UsageCount* valor para o driver não existir, a nova *UsageCount* valor é definido como 2.  
  
 Essa função não copia, na verdade, todos os arquivos. É responsabilidade do programa de chamada para copiar os arquivos do driver para o diretório de destino corretamente.  
  
 A funcionalidade do **SQLInstallDriverEx** também podem ser acessados com [ODBCCONF. EXE](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
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
 [Entrada] A descrição do driver (geralmente o nome do DBMS associado) apresentada aos usuários em vez do nome físico de driver. O *lpszDriver* argumento deve conter uma lista duplamente terminada em nulo de pares de palavra-chave-valor que descreve o driver. Para obter mais informações sobre pares de valor de palavra-chave, consulte [subchaves de especificação de Driver](../../../odbc/reference/install/driver-specification-subkeys.md). Para obter mais informações sobre a cadeia de caracteres duplamente terminada em nulo, consulte [função ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md).  
  
 *lpszPathIn*  
 [Entrada] Caminho completo do diretório de destino da instalação ou um ponteiro nulo. Se *lpszPathIn* for um ponteiro nulo, os drivers serão instalados no diretório do sistema.  
  
 *lpszPathOut*  
 [Saída] Caminho do diretório de destino onde o driver deve ser instalado. Se o driver não tenha sido instalado anteriormente, *lpszPathOut* deve ser o mesmo que *lpszPathIn*. Se o driver foi instalado anteriormente, *lpszPathOut* é o caminho da instalação anterior.  
  
 *cbPathOutMax*  
 [Entrada] Comprimento da *lpszPathOut*.  
  
 *pcbPathOut*  
 [Saída] Número total de bytes (exceto o caractere nulo de terminação) disponíveis para retornar na *lpszPathOut*. Se o número de bytes disponíveis para retornar for maior que ou igual a *cbPathOutMax*, o caminho de saída na *lpszPathOut* será truncado com *cbPathOutMax* menos o caractere de finalização null. O *pcbPathOut* argumento pode ser um ponteiro nulo.  
  
 *fRequest*  
 [Entrada] Tipo de solicitação. O *frequentes* argumento deve conter um dos seguintes valores:  
  
 ODBC_INSTALL_INQUIRY: Pesquisa sobre onde um driver pode ser instalado.  
  
 ODBC_INSTALL_COMPLETE: Conclua a solicitação de instalação.  
  
 *lpdwUsageCount*  
 [Saída] A contagem de utilização do driver depois que essa função foi chamada.  
  
 Aplicativos não devem definir a contagem de uso. ODBC manterá essa contagem.  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedida, FALSO se ele falhar.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLInstallDriverEx** retornar FALSE, um associado  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista os  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral de instalador|Ocorreu um erro para que nenhum erro específico do instalador.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Comprimento de buffer inválido|O *lpszPathOut* argumento não era grande o suficiente para conter o caminho de saída. O buffer contém o caminho truncado.<br /><br /> O *cbPathOutMax* argumento era 0, e *frequentes* foi ODBC_INSTALL_COMPLETE.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitação inválido|O *frequentes* argumento não era um dos seguintes:<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Pares de valor de palavra-chave inválido|O *lpszDriver* argumento continha um erro de sintaxe.|  
|ODBC_ERROR_INVALID_PATH|Caminho de instalação inválido|O *lpszPathIn* argumento continha um caminho inválido.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Não foi possível carregar a biblioteca de instalação do driver ou conversor|Não foi possível carregar a biblioteca de instalação do driver.|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|Sequência de parâmetro inválido|O *lpszDriver* argumento não contém uma lista de pares de palavra-chave-valor.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Não foi possível incrementar ou decrementar a contagem de utilização de componente|O instalador não conseguiu incrementar a contagem de utilização do driver.|  
  
## <a name="comments"></a>Comentários  
 O *lpszDriver* argumento é uma lista de atributos na forma de pares de palavra-chave-valor. Cada par é encerrada com um byte nulo e a lista inteira é encerrada com um byte nulo. (Ou seja, dois bytes nulos marcam o final da lista.) O formato dessa lista é da seguinte maneira:  
  
 _driver-desc_ **\\** 0Driver **=** _driver-DLL-filename_ **\\** 0[Setup **=** _setup-DLL-filename_<b>\\</b>0]  
  
 [_attr-driver-keyword1_ **=** _value1_<b>\\</b>0] [_driver-attr-keyword2_  **=** _value2_<b>\\</b>0]... <b> \\ </b>0  
  
 onde \0 é um byte nulo e *attr-driver-keywordn* é qualquer palavra-chave do atributo de driver. As palavras-chave deverá aparecer na ordem especificada. Por exemplo, suponha que um driver para arquivos de texto formatado tem DLLs de instalação e de driver separado e pode usar os arquivos com as extensões. txt e. csv. O *lpszDriver* argumento para esse driver pode ser da seguinte maneira:  
  
```  
Text\0Driver=TEXT.DLL\0Setup=TXTSETUP.DLL\0FileUsage=1\0  
FileExtns=*.txt,*.csv\0\0  
```  
  
 Suponha que um driver para SQL Server não tem uma DLL de instalação separado e não tem quaisquer palavras-chave do atributo de driver. O *lpszDriver* argumento para esse driver pode ser da seguinte maneira:  
  
```  
SQL Server\0Driver=SQLSRVR.DLL\0\0  
```  
  
 Após **SQLInstallDriverEx** recupera informações sobre o driver a partir de *lpszDriver* argumento, ele adiciona a descrição do driver para a seção [ODBC Drivers] da entrada Odbcinst. ini no sistema informações. Em seguida, cria uma seção chamada com a descrição do driver e adiciona os caminhos completos de DLL do driver e o DLL de instalação. Por fim, ele retorna o caminho do diretório de destino da instalação, mas não copia os arquivos de driver para ele. O programa de chamada, na verdade, deve copiar os arquivos de driver para o diretório de destino.  
  
 **SQLInstallDriverEx** incrementa a contagem de utilização de componente para o driver instalado em 1. Se já houver uma versão do driver, mas a contagem de utilização de componente para o driver não existir, o novo valor de contagem de uso do componente é definido como 2.  
  
 O programa de instalação do aplicativo é responsável por fisicamente copiando o arquivo de driver e manter a contagem de uso de arquivos. Se o arquivo de driver não tiver sido instalado anteriormente, o programa de instalação do aplicativo deve copiar o arquivo na *lpszPathIn* caminho e criar a contagem de uso de arquivos. Se o arquivo tiver sido instalado anteriormente, o programa de instalação simplesmente incrementa a contagem de uso de arquivo e retorna o caminho da instalação anterior na *lpszPathOut* argumento.  
  
> [!NOTE]  
>  Para obter mais informações sobre contagens de uso do componente e contagens de uso de arquivo, consulte [contagem de uso](../../../odbc/reference/install/usage-counting.md).  
  
 Se uma versão mais antiga do arquivo do driver foi instalada anteriormente pelo aplicativo, o driver deve ser desinstalado e reinstalado, para que a contagem de uso do componente de driver é válida. **SQLConfigDriver** (com um *frequentes* de ODBC_REMOVE_DRIVER) deve ser chamado primeiro e então **SQLRemoveDriver** deve ser chamado para diminuir a contagem de uso do componente. **SQLInstallDriverEx** , em seguida, deve ser chamado para reinstalar o driver, incrementar a contagem de uso do componente. O programa de instalação do aplicativo deve substituir o arquivo antigo com o novo arquivo. A contagem de uso de arquivos permanecerão os mesmos, e qualquer outro aplicativo que usou o arquivo de versão mais antigo agora usará a versão mais recente.  
  
> [!NOTE]  
>  Se o driver foi instalado anteriormente e **SQLInstallDriverEx** é chamado para instalar o driver em um diretório diferente, a função retornará TRUE, mas *lpszPathOut* incluirá o diretório em que o driver já foi instalado. Ele não incluirá o diretório digitado na *lpszDriver* argumento.  
  
 O comprimento do caminho em *lpszPathOut* na **SQLInstallDriverEx** permite que um processo de duas fases de instalação, para que um aplicativo possa determinar quais *cbPathOutMax* deve ser por chamando **SQLInstallDriverEx** com um *frequentes* do modo ODBC_INSTALL_INQUIRY. Isso retornará o número total de bytes disponíveis na *pcbPathOut* buffer. **SQLInstallDriverEx** , em seguida, pode ser chamado com um *frequentes* de ODBC_INSTALL_COMPLETE e o *cbPathOutMax* argumento definido como o valor no *pcbPathOut*buffer, mais o caractere nulo de terminação.  
  
 Se você optar por não usar o modelo de duas fases para **SQLInstallDriverEx**, você deve definir *cbPathOutMax*, que define o tamanho do armazenamento para o caminho do diretório de destino, para o valor MAX_PATH, como definida em stdlib. h, para evitar truncamento.  
  
 Quando *frequentes* é ODBC_INSTALL_COMPLETE, **SQLInstallDriverEx** não permite *lpszPathOut* NULL (ou *cbPathOutMax* ser 0). Se *frequentes* é ODBC_INSTALL_COMPLETE, FALSO é retornado quando o número de bytes disponíveis para retornar é maior que ou igual a *cbPathOutMax*, com o resultado que o truncamento ocorre.  
  
 Após **SQLInstallDriverEx** foi chamado e o programa de instalação do aplicativo tiver copiado o arquivo de driver (se necessário), a instalação do driver DLL deve chamar **SQLConfigDriver** para definir a configuração para o driver.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Instalando o Gerenciador de Driver|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
