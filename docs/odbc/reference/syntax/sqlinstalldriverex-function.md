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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 054e8b6b9eae26bd5f973f3d46d7ef37363a8e79
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302118"
---
# <a name="sqlinstalldriverex-function"></a>Função SQLInstallDriverEx
**Conformidade**  
 Versão introduzida: ODBC 3,0  
  
 **Resumo**  
 O **SQLInstallDriverEx** adiciona informações sobre o driver à entrada Odbcinst. ini nas informações do sistema e incrementa o *UsageCount* do driver em 1. No entanto, se já existir uma versão do driver, mas o valor de *UsageCount* para o driver não existir, o novo valor *UsageCount* será definido como 2.  
  
 Na verdade, essa função não copia nenhum arquivo. É responsabilidade do programa de chamada copiar os arquivos do driver para o diretório de destino corretamente.  
  
 A funcionalidade do **SQLInstallDriverEx** também pode ser acessada com [ODBCCONF. EXE](../../../odbc/odbcconf-exe.md).  
  
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
 Entrada A descrição do driver (geralmente o nome do DBMS associado) apresentado aos usuários em vez do nome do driver físico. O argumento *lpszDriver* deve conter uma lista dupla de pares de palavras-chave com terminação nula que descreve o driver. Para obter mais informações sobre pares de palavra-chave-valor, consulte [subchaves de especificação do driver](../../../odbc/reference/install/driver-specification-subkeys.md). Para obter mais informações sobre a cadeia de caracteres de terminação nula dupla, consulte [função ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md).  
  
 *lpszPathIn*  
 Entrada Caminho completo do diretório de destino da instalação ou um ponteiro nulo. Se *lpszPathIn* for um ponteiro nulo, os drivers serão instalados no diretório do sistema.  
  
 *lpszPathOut*  
 Der Caminho do diretório de destino onde o driver deve ser instalado. Se o driver não tiver sido instalado anteriormente, *lpszPathOut* deverá ser o mesmo que *lpszPathIn*. Se o driver tiver sido instalado anteriormente, *lpszPathOut* será o caminho da instalação anterior.  
  
 *cbPathOutMax*  
 Entrada Comprimento de *lpszPathOut*.  
  
 *pcbPathOut*  
 Der Número total de bytes (exceto o caractere de terminação nula) disponíveis para retornar em *lpszPathOut*. Se o número de bytes disponíveis para retornar for maior ou igual a *cbPathOutMax*, o caminho de saída em *lpszPathOut* será truncado para *cbPathOutMax* menos o caractere de terminação nula. O argumento *pcbPathOut* pode ser um ponteiro nulo.  
  
 *fRequest*  
 Entrada Tipo de solicitação. O argumento *fRequest* deve conter um dos seguintes valores:  
  
 ODBC_INSTALL_INQUIRY: consulte sobre onde um driver pode ser instalado.  
  
 ODBC_INSTALL_COMPLETE: conclua a solicitação de instalação.  
  
 *lpdwUsageCount*  
 Der A contagem de uso do driver depois que essa função foi chamada.  
  
 Os aplicativos não devem definir a contagem de uso. O ODBC manterá essa contagem.  
  
## <a name="returns"></a>Retornos  
 A função retornará TRUE se for bem-sucedida, FALSE se falhar.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLInstallDriverEx** retorna false, um valor * \*pfErrorCode* associado pode ser obtido chamando **SQLInstallerError**. A tabela a seguir lista os valores de * \*pfErrorCode* que podem ser retornados por **SQLInstallerError** e explica cada um no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral do instalador|Ocorreu um erro para o qual não havia nenhum erro do instalador específico.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Comprimento de buffer inválido|O argumento *lpszPathOut* não era grande o suficiente para conter o caminho de saída. O buffer contém o caminho truncado.<br /><br /> O argumento *cbPathOutMax* era 0 e *fRequest* foi ODBC_INSTALL_COMPLETE.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitação inválido|O argumento *fRequest* não era um dos seguintes:<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Pares de palavra-chave-valor inválidos|O argumento *lpszDriver* continha um erro de sintaxe.|  
|ODBC_ERROR_INVALID_PATH|Caminho de instalação inválido|O argumento *lpszPathIn* continha um caminho inválido.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Não foi possível carregar a biblioteca de instalação do driver ou do Tradutor|Não foi possível carregar a biblioteca de instalação do driver.|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|Sequência de parâmetros inválida|O argumento *lpszDriver* não continha uma lista de pares de palavra-chave-valor.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Não foi possível incrementar ou decrementar a contagem de uso do componente|O instalador não pôde incrementar a contagem de uso do driver.|  
  
## <a name="comments"></a>Comentários  
 O argumento *lpszDriver* é uma lista de atributos na forma de pares de palavra-chave-valor. Cada par é encerrado com um byte nulo e a lista inteira é encerrada com um byte nulo. (Ou seja, dois bytes nulos marcam o final da lista.) O formato dessa lista é o seguinte:  
  
 _Driver-desc_ **\\**0Driver**=**_Driver-dll-filename_**\\**0 [**=** Setup_Setup-dll-filename_<b>\\</b>0]  
  
 [_Driver-attr-keyword1_**=**_value1_<b>\\</b>0] [_Driver-attr-keyword2_**=**_value2_<b>\\</b>0]... <b>\\</b>0  
  
 onde \ 0 é um byte nulo e *Driver-attr-keywordn* é qualquer palavra-chave de atributo de driver. As palavras-chave devem aparecer na ordem especificada. Por exemplo, suponha que um driver para arquivos de texto formatados tenha DLLs de driver e instalação separadas e possa usar arquivos com as extensões. txt e. csv. O argumento *lpszDriver* para esse driver pode ser o seguinte:  
  
```  
Text\0Driver=TEXT.DLL\0Setup=TXTSETUP.DLL\0FileUsage=1\0  
FileExtns=*.txt,*.csv\0\0  
```  
  
 Suponha que um driver para SQL Server não tenha uma DLL de instalação separada e não tenha nenhuma palavra-chave de atributo de driver. O argumento *lpszDriver* para esse driver pode ser o seguinte:  
  
```  
SQL Server\0Driver=SQLSRVR.DLL\0\0  
```  
  
 Depois que o **SQLInstallDriverEx** recupera informações sobre o driver do argumento *lpszDriver* , ele adiciona a descrição do driver à seção [drivers ODBC] da entrada Odbcinst. ini nas informações do sistema. Em seguida, ele cria uma seção intitulada com a descrição do driver e adiciona os caminhos completos da DLL do driver e a DLL de instalação. Por fim, ele retorna o caminho do diretório de destino da instalação, mas não copia os arquivos de driver para ele. O programa de chamada deve realmente copiar os arquivos de driver para o diretório de destino.  
  
 **SQLInstallDriverEx** incrementa a contagem de uso do componente para o driver instalado em 1. Se já existir uma versão do driver, mas a contagem de uso do componente para o driver não existir, o novo valor de contagem de uso do componente será definido como 2.  
  
 O programa de instalação do aplicativo é responsável por copiar fisicamente o arquivo de driver e manter a contagem de uso do arquivo. Se o arquivo de driver não tiver sido instalado anteriormente, o programa de instalação do aplicativo deverá copiar o arquivo no caminho *lpszPathIn* e criar a contagem de uso do arquivo. Se o arquivo tiver sido instalado anteriormente, o programa de instalação simplesmente incrementará a contagem de uso do arquivo e retornará o caminho da instalação anterior no argumento *lpszPathOut* .  
  
> [!NOTE]  
>  Para obter mais informações sobre contagens de uso de componente e contagens de uso de arquivo, consulte [contagem de uso](../../../odbc/reference/install/usage-counting.md).  
  
 Se uma versão mais antiga do arquivo de driver tiver sido instalada anteriormente pelo aplicativo, o driver deverá ser desinstalado e reinstalado, para que a contagem de uso do componente do driver seja válida. **SQLConfigDriver** (com um *fRequest* de ODBC_REMOVE_DRIVER) deve ser chamado primeiro e, em seguida, **SQLRemoveDriver** deve ser chamado para diminuir a contagem de uso do componente. **SQLInstallDriverEx** deve ser chamado para reinstalar o driver, incrementando a contagem de uso do componente. O programa de instalação do aplicativo deve substituir o arquivo antigo pelo novo arquivo. A contagem de uso do arquivo permanecerá a mesma, e qualquer outro aplicativo que usava o arquivo de versão mais antiga agora usará a versão mais recente.  
  
> [!NOTE]  
>  Se o driver tiver sido instalado anteriormente e **SQLInstallDriverEx** for chamado para instalar o driver em um diretório diferente, a função retornará true, mas o *lpszPathOut* incluirá o diretório em que o driver já foi instalado. Ele não incluirá o diretório inserido no argumento *lpszDriver* .  
  
 O comprimento do caminho em *lpszPathOut* no **SQLInstallDriverEx** permite um processo de instalação de duas fases, portanto, um aplicativo pode determinar qual *cbPathOutMax* deve ser chamando **SQLInstallDriverEx** com um *fRequest* no modo de ODBC_INSTALL_INQUIRY. Isso retornará o número total de bytes disponíveis no buffer *pcbPathOut* . **SQLInstallDriverEx** pode ser chamado com um *fRequest* de ODBC_INSTALL_COMPLETE e o argumento *cbPathOutMax* definido como o valor no buffer *pcbPathOut* , mais o caractere de terminação nula.  
  
 Se você optar por não usar o modelo de duas fases para **SQLInstallDriverEx**, deverá definir *cbPathOutMax*, que define o tamanho do armazenamento para o caminho do diretório de destino, para o valor _MAX_PATH, conforme definido em STDLIB. h, para evitar truncamento.  
  
 Quando *fRequest* é ODBC_INSTALL_COMPLETE, **SQLInstallDriverEx** não permite que *LpszPathOut* seja nulo (ou *cbPathOutMax* como 0). Se *fRequest* for ODBC_INSTALL_COMPLETE, false será retornado quando o número de bytes disponíveis para retornar for maior ou igual a *cbPathOutMax*, com o resultado de que o truncamento ocorre.  
  
 Depois que **SQLInstallDriverEx** tiver sido chamado e o programa de instalação do aplicativo tiver copiado o arquivo de driver (se necessário), a DLL de instalação do driver deverá chamar **SQLConfigDriver** para definir a configuração do driver.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Instalando o Gerenciador de Driver|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
