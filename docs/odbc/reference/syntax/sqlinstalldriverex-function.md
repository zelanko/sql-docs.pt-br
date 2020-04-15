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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302118"
---
# <a name="sqlinstalldriverex-function"></a>Função SQLInstallDriverEx
**Conformidade**  
 Versão introduzida: ODBC 3.0  
  
 **Resumo**  
 **O SQLInstallDriverEx** adiciona informações sobre o driver à entrada Odbcinst.ini nas informações do sistema e incrementa o *UseCount* do driver em 1. No entanto, se uma versão do driver já existe, mas o valor *UsageCount* para o driver não existe, o novo valor *UseCount* será definido como 2.  
  
 Esta função não copia nenhum arquivo. É responsabilidade do programa de chamada copiar os arquivos do driver para o diretório de destino corretamente.  
  
 A funcionalidade do **SQLInstallDriverEx** também pode ser acessada com [o ODBCCONF. EXE](../../../odbc/odbcconf-exe.md).  
  
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
 *Lpszdriver*  
 [Entrada] A descrição do driver (geralmente o nome do DBMS associado) apresentado aos usuários em vez do nome do motorista físico. O argumento *lpszDriver* deve conter uma lista duplamente nula de pares de valores de palavras-chave descrevendo o driver. Para obter mais informações sobre pares de valor de palavras-chave, consulte [Subtecas de especificação do driver](../../../odbc/reference/install/driver-specification-subkeys.md). Para obter mais informações sobre a seqüência de seqüência duplamente nula, consulte [Função ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md).  
  
 *lpszPathIn*  
 [Entrada] Caminho completo do diretório de destino da instalação, ou um ponteiro nulo. Se *lpszPathIn* for um ponteiro nulo, os drivers serão instalados no diretório do sistema.  
  
 *lpszPathOut*  
 [Saída] Caminho do diretório de destino onde o driver deve ser instalado. Se o driver não tiver sido instalado anteriormente, *lpszPathOut* deve ser o mesmo que *lpszPathIn*. Se o driver foi instalado anteriormente, *lpszPathOut* é o caminho da instalação anterior.  
  
 *cbPathOutMax*  
 [Entrada] Comprimento de *lpszPathOut*.  
  
 *pcbpathOut*  
 [Saída] Número total de bytes (excluindo o caractere de rescisão nula) disponível para retornar em *lpszPathOut*. Se o número de bytes disponíveis para retornar for maior ou igual ao *cbPathOutMax,* o caminho de saída no *lpszPathOut* será truncado para *cbPathOutMax* menos o caractere de rescisão nula. O *argumento pcbPathOut* pode ser um ponteiro nulo.  
  
 *fSolicitar*  
 [Entrada] Tipo de pedido. O *argumento fRequest* deve conter um dos seguintes valores:  
  
 ODBC_INSTALL_INQUIRY: Pergunte onde um driver pode ser instalado.  
  
 ODBC_INSTALL_COMPLETE: Complete a solicitação de instalação.  
  
 *lpdwUsagecount*  
 [Saída] A contagem de uso do driver após esta função foi chamada.  
  
 Os aplicativos não devem definir a contagem de uso. A ODBC manterá essa contagem.  
  
## <a name="returns"></a>Retornos  
 A função retorna TRUE se for bem sucedida, FALSA se falhar.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLInstallDriverEx** retorna FALSE, um valor * \*pfErrorCode* associado pode ser obtido ligando para **SQLInstallerError**. A tabela a * \** seguir lista os valores pfErrorCode que podem ser retornados pelo **SQLInstallerError** e explica cada um no contexto desta função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro do instalador geral|Ocorreu um erro para o qual não houve erro específico do instalador.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Comprimento de buffer inválido|O argumento *lpszPathOut* não era grande o suficiente para conter o caminho de saída. O buffer contém o caminho truncado.<br /><br /> O argumento *cbPathOutMax* foi 0, e *fRequest* foi ODBC_INSTALL_COMPLETE.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitação inválida|O argumento *fRequest* não foi um dos seguintes:<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Pares de valores de palavras-chave inválidos|O argumento *lpszDriver* continha um erro de sintaxe.|  
|ODBC_ERROR_INVALID_PATH|Caminho de instalação inválido|O argumento *lpszPathIn* continha um caminho inválido.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Não foi possível carregar a biblioteca de configuração do driver ou tradutor|A biblioteca de configuração do driver não pôde ser carregada.|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|Seqüência de parâmetros inválidos|O argumento *lpszDriver* não continha uma lista de pares de valor de palavras-chave.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Não foi possível incrementar ou diminuir a contagem de uso de componentes|O instalador não conseguiu aumentar a contagem de uso do driver.|  
  
## <a name="comments"></a>Comentários  
 O argumento *lpszDriver* é uma lista de atributos na forma de pares de valor de palavras-chave. Cada par é encerrado com um byte nulo, e toda a lista é encerrada com um byte nulo. (Ou seja, dois bytes nulos marcam o fim da lista.) O formato desta lista é o seguinte:  
  
 _driver-desc_ **\\****=** 0Driver_driver-DLL-filename_**\\**0[Configuração de**=**_configuração-DLL-filename_<b>\\</b>0]  
  
 [_driver-attr-keyword1_**=**_value1_<b>\\</b>0] [_driver-attr-keyword2_**=**_value2_<b>\\</b>0]... <b>\\</b>0  
  
 onde \0 é um byte nulo e *driver-attr-keywordn* é qualquer palavra-chave de atributo do driver. As palavras-chave devem aparecer na ordem especificada. Por exemplo, suponha que um driver para arquivos de texto formatados tenha DLLs de driver e configuração separados e possa usar arquivos com as extensões .txt e .csv. O argumento *lpszDriver* para este driver pode ser o seguinte:  
  
```  
Text\0Driver=TEXT.DLL\0Setup=TXTSETUP.DLL\0FileUsage=1\0  
FileExtns=*.txt,*.csv\0\0  
```  
  
 Suponha que um driver para SQL Server não tenha uma Configuração Separada DLL e não tenha nenhuma palavra-chave de atributo de driver. O argumento *lpszDriver* para este driver pode ser o seguinte:  
  
```  
SQL Server\0Driver=SQLSRVR.DLL\0\0  
```  
  
 Depois **que o SQLInstallDriverEx** recupera informações sobre o driver a partir do argumento *lpszDriver,* ele adiciona a descrição do driver à seção [Drivers ODBC] da entrada Odbcinst.ini nas informações do sistema. Em seguida, cria uma seção intitulada com a descrição do driver e adiciona os caminhos completos do Driver DLL e da configuração DLL. Finalmente, ele retorna o caminho do diretório de destino da instalação, mas não copia os arquivos do driver para ele. O programa de chamada deve realmente copiar os arquivos do driver para o diretório de destino.  
  
 **SQLInstallDriverEx** aumenta a contagem de uso do componente para o driver instalado em 1. Se uma versão do driver já existir, mas a contagem de uso do componente para o driver não existir, o novo valor de contagem de uso do componente será definido como 2.  
  
 O programa de configuração do aplicativo é responsável por copiar fisicamente o arquivo do driver e manter a contagem de uso do arquivo. Se o arquivo do driver não tiver sido instalado anteriormente, o programa de configuração do aplicativo deve copiar o arquivo no caminho *lpszPathIn* e criar a contagem de uso do arquivo. Se o arquivo tiver sido instalado anteriormente, o programa de configuração apenas incrementa a contagem de uso do arquivo e retorna o caminho da instalação anterior no argumento *lpszPathOut.*  
  
> [!NOTE]  
>  Para obter mais informações sobre contagem de uso de componentes e contagem de uso de arquivos, consulte [Contagem de uso](../../../odbc/reference/install/usage-counting.md).  
  
 Se uma versão mais antiga do arquivo do driver foi previamente instalada pelo aplicativo, o driver deve ser desinstalado e depois reinstalado, de modo que a contagem de uso do componente do driver seja válida. **SQLConfigDriver** (com um *fRequest* of ODBC_REMOVE_DRIVER) deve ser primeiro chamado e, em seguida, **SQLRemoveDriver** deve ser chamado para diminuir a contagem de uso do componente. **O SQLInstallDriverEx** deve então ser chamado para reinstalar o driver, incrementando a contagem de uso do componente. O programa de configuração do aplicativo deve substituir o arquivo antigo pelo novo arquivo. A contagem de uso do arquivo permanecerá a mesma, e qualquer outro aplicativo que usou o arquivo de versão mais antiga agora usará a versão mais recente.  
  
> [!NOTE]  
>  Se o driver foi instalado anteriormente e **o SQLInstallDriverEx** for chamado para instalar o driver em um diretório diferente, a função retornará TRUE, mas *lpszPathOut* incluirá o diretório onde o driver já estava instalado. Ele não incluirá o diretório inserido no argumento *lpszDriver.*  
  
 O comprimento do caminho em *lpszPathOut* no **SQLInstallDriverEx** permite um processo de instalação em duas fases, para que um aplicativo possa determinar o que *cbPathOutMax* deve ser ligando para **SQLInstallDriverEx** com um *fRequest* de ODBC_INSTALL_INQUIRY mode. Isso retornará o número total de bytes disponíveis no buffer *pcbPathOut.* **O SQLInstallDriverEx** pode então ser chamado com um *fRequest* of ODBC_INSTALL_COMPLETE e o argumento *cbPathOutMax* definido para o valor no buffer *pcbPathOut,* mais o caractere de rescisão nula.  
  
 Se você optar por não usar o modelo bifásico para **SQLInstallDriverEx,** você deve definir *cbPathOutMax*, que define o tamanho do armazenamento para o caminho do diretório de destino, para o valor _MAX_PATH, como definido em Stdlib.h, para evitar truncamento.  
  
 Quando *fRequest* é ODBC_INSTALL_COMPLETE, **o SQLInstallDriverEx** não permite que *o lpszPathOut* seja NULL (ou *cbPathOutMax* seja 0). Se *fRequest* for ODBC_INSTALL_COMPLETE, FALSE é devolvido quando o número de bytes disponíveis para retornar for maior ou igual a *cbPathOutMax*, com o resultado que ocorre a truncação.  
  
 Depois **que o SQLInstallDriverEx** foi chamado e o programa de configuração do aplicativo copiou o arquivo do driver (se necessário), a configuração do driver DLL deve ligar para **o SQLConfigDriver** para definir a configuração para o driver.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Instalando o Gerenciador de Driver|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
