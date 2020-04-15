---
title: Função SQLInstallTranslatorEx | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallTranslatorEx
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallTranslatorEx
helpviewer_keywords:
- SQLInstallTranslatorEx function [ODBC]
ms.assetid: a0630602-53c1-4db0-98ce-70d160aedf8d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5cf52c26bf9e4a26f13a27a0e763fbaa30bd18ec
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302087"
---
# <a name="sqlinstalltranslatorex-function"></a>Função SQLInstallTranslatorEx
**Conformidade**  
 Versão introduzida: ODBC 3.0  
  
 **Resumo**  
 **O SQLInstallTranslatorEx** adiciona informações sobre um tradutor à seção Odbcinst.ini das informações do sistema (HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST. Chave de registro de tradutores INI\ODBC).  
  
 A funcionalidade do **SQLInstallTranslatorEx** também pode ser acessada com [o ODBCCONF. EXE](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL SQLInstallTranslatorEx(  
     LPCSTR    lpszTranslator,  
     LPCSTR    lpszPathIn,  
     LPSTR     lpszPathOut,  
     WORD      cbPathOutMax,  
     WORD *    pcbPathOut,  
     WORD      fRequest,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszTradutor*  
 [Entrada] Isso deve conter uma lista duplamente nula de pares de valor escancarado descrevendo o tradutor. Para obter mais informações sobre a sintaxe do par de valor de palavra-chave, consulte [Subchaves de especificação de tradutor](../../../odbc/reference/install/translator-specification-subkeys.md).  
  
 As palavras-chave **Tradutor** e **Configuração** devem ser incluídas na seqüência *lpszTranslator.* A dLL de tradução está listada com a palavra-chave **Tradutor,** e a configuração do tradutor DLL está listada com a palavra-chave **Configuração.** Cada par é encerrado com um byte NULL, e toda a lista é encerrada com um byte NULL. (Ou seja, dois bytes NULOS marcam o fim da lista.) O formato do *lpszTranslator* é o seguinte:  
  
 \0Tradutor=*tradutor-DLL-filename*\0[Configuração=*configuração-DLL-filename*\0]\0  
  
 *lpszPathIn*  
 [Entrada] Caminho completo de onde o tradutor deve ser instalado ou um ponteiro nulo. Se *lpszPath* for um ponteiro nulo, os tradutores serão instalados no diretório do sistema.  
  
 *lpszPathOut*  
 [Saída] O caminho do diretório de destino onde o tradutor deve ser instalado. Se o tradutor nunca foi instalado, *lpszPathOut* é o mesmo que *lpszPathIn*. Se houver uma instalação prévia do tradutor, *lpszPathOut* é o caminho da instalação anterior.  
  
 *cbPathOutMax*  
 [Entrada] Comprimento de *lpszPathOut.*  
  
 *pcbpathOut*  
 [Saída] Número total de bytes disponíveis para retornar em *lpszPathOut*. Se o número de bytes disponíveis para retornar for maior ou igual ao *cbPathOutMax,* o caminho de saída no *lpszPathOut* será truncado para *pcbPathOutMax* menos o caractere de rescisão nula. O *argumento pcbPathOut* pode ser um ponteiro nulo.  
  
 *fSolicitar*  
 [Entrada] Tipo de pedido. *fSolicite* conter um dos seguintes valores:  
  
 ODBC_INSTALL_INQUIRY: Pergunte onde um tradutor pode ser instalado.  
  
 ODBC_INSTALL_COMPLETE: Complete a solicitação de instalação.  
  
 *lpdwUsagecount*  
 [Saída] A contagem de uso do tradutor após esta função foi chamada.  
  
 Os aplicativos não devem definir a contagem de uso. A ODBC manterá essa contagem.  
  
## <a name="returns"></a>Retornos  
 A função retorna TRUE se for bem sucedida, FALSA se falhar.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLInstallTranslatorEx** retorna FALSE, um valor * \*pfErrorCode* associado pode ser obtido ligando para **SQLInstallerError**. A tabela a * \** seguir lista os valores pfErrorCode que podem ser retornados pelo **SQLInstallerError** e explica cada um no contexto desta função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro do instalador geral|Ocorreu um erro para o qual não houve erro específico do instalador.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Comprimento de buffer inválido|O argumento *lpszPathOut* não era grande o suficiente para conter o caminho de saída. O buffer contém o caminho truncado.<br /><br /> O argumento *cbPathOutMax* foi 0, e o argumento *fRequest* foi ODBC_INSTALL_COMPLETE.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitação inválida|O argumento *fRequest* não foi um dos seguintes:<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Pares de valores de palavras-chave inválidos|O argumento *lpszTranslator* continha um erro de sintaxe.|  
|ODBC_ERROR_INVALID_PATH|Caminho de instalação inválido|O argumento *lpszPathIn* continha um caminho inválido.|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|Seqüência de parâmetros inválidos|O argumento *lpszTranslator* não continha uma lista de pares de valor de palavras-chave.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Não foi possível incrementar ou diminuir a contagem de componentes do registro|O instalador não conseguiu aumentar a contagem de uso do tradutor.|  
  
## <a name="comments"></a>Comentários  
 **O SQLInstallTranslatorEx** fornece um mecanismo para instalar apenas o tradutor. Esta função não copia nenhum arquivo. O programa de chamada é responsável por copiar os arquivos do tradutor.  
  
 **SQLInstallTranslatorEx** incrementa a contagem de uso do componente para o tradutor instalado por 1. Se uma versão do tradutor já existir, mas a contagem de uso do componente para o tradutor não existir, o novo valor de contagem de uso do componente será definido como 2.  
  
 O programa de configuração do aplicativo é responsável por copiar fisicamente o arquivo do tradutor e manter a contagem de uso do arquivo. Se o arquivo tradutor não tiver sido instalado anteriormente, o programa de configuração do aplicativo deve copiar o arquivo ou os arquivos e criar a contagem de uso de arquivos ou arquivos. Se o arquivo tiver sido instalado anteriormente, o programa de configuração simplesmente incrementa a contagem de uso do arquivo.  
  
 Se uma versão mais antiga do tradutor foi previamente instalada pelo aplicativo, o tradutor deve ser desinstalado e depois reinstalado, de modo que a contagem de uso do componente tradutor seja válida. **SQLRemoveTranslator** deve ser chamado para diminuir a contagem de uso do componente e, em seguida, **sQLInstallTranslatorEx** deve ser chamado para incrementar a contagem de uso do componente. O programa de configuração do aplicativo deve substituir o arquivo antigo ou arquivos pelo novo arquivo. A contagem de uso do arquivo permanecerá a mesma, e outros aplicativos que usaram o arquivo de versão mais antiga agora usarão a versão mais recente.  
  
 O comprimento do caminho em *lpszPathOut* no **SQLInstallTranslatorEx** permite um processo de instalação em duas fases, para que um aplicativo possa determinar o que *cbPathOutMax* deve ser ligando para **SQLInstallTranslatorEx** com um *fRequest* de ODBC_INSTALL_INQUIRY mode. Isso retornará o número total de bytes disponíveis no buffer *pcbPathOut.* **O SQLInstallTranslatorEx** pode então ser chamado com um *fRequest* of ODBC_INSTALL_COMPLETE e o argumento *cbPathOutMax* definido para o valor no buffer *pcbPathOut,* mais o caractere de rescisão nula.  
  
 Se você optar por não usar o modelo bifásico para **SQLInstallTranslatorEx,** você deve definir *cbPathOutMax*, que define o tamanho do armazenamento para o caminho do diretório de destino, para o valor _MAX_PATH, como definido em Stdlib.h, para evitar truncamento.  
  
 Quando *fRequest* é ODBC_INSTALL_COMPLETE, **o SQLInstallTranslatorEx** não permite que *o lpszPathOut* seja NULO (ou *cbPathOutMax* seja 0). Se *fRequest* for ODBC_INSTALL_COMPLETE, FALSE é devolvido quando o número de bytes disponíveis para retornar for maior ou igual a *cbPathOutMax*, com o resultado que ocorre a truncação.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Retornando uma opção de tradução padrão|[Tradutor de config](../../../odbc/reference/syntax/configtranslator-function.md)|  
|Selecionando tradutores|[SqlGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|Removendo tradutores|[SQLRemoveTradutor](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
