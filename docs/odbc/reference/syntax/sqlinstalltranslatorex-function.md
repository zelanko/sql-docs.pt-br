---
description: Função SQLInstallTranslatorEx
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
ms.openlocfilehash: 7957a04e0dafaeb2177401f775c5cdbb75135569
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421140"
---
# <a name="sqlinstalltranslatorex-function"></a>Função SQLInstallTranslatorEx
**Conformidade**  
 Versão introduzida: ODBC 3,0  
  
 **Resumo**  
 **SQLInstallTranslatorEx** adiciona informações sobre um tradutor à seção Odbcinst.ini da chave do registro de informações do sistema (HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST.INI de conversores do \odbc).  
  
 A funcionalidade do **SQLInstallTranslatorEx** também pode ser acessada com [ODBCCONF.EXE](../../../odbc/odbcconf-exe.md).  
  
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
 *lpszTranslator*  
 Entrada Isso deve conter uma lista dupla de pares de palavras-chave com terminação nula que descreve o tradutor. Para obter mais informações sobre a sintaxe do par de valor de palavra-chave, consulte [subchaves de especificação do tradutor](../../../odbc/reference/install/translator-specification-subkeys.md).  
  
 O **Tradutor** e as palavras-chave de **instalação** devem ser incluídos na cadeia de caracteres *lpszTranslator* . A DLL de tradução é listada com a palavra-chave **Translator** e a DLL de instalação do tradutor é listada com a palavra-chave **Setup** . Cada par é encerrado com um byte nulo e a lista inteira é encerrada com um byte nulo. (Ou seja, dois bytes nulos marcam o final da lista.) O formato de *lpszTranslator* é o seguinte:  
  
 \0Translator =*Translator-dll-filename*\ 0 [instalação =*instalação-dll-nome-* do-arquivo \ 0] \ 0  
  
 *lpszPathIn*  
 Entrada Caminho completo de onde o tradutor deve ser instalado ou um ponteiro nulo. Se *lpszPath* for um ponteiro nulo, os tradutores serão instalados no diretório do sistema.  
  
 *lpszPathOut*  
 Der O caminho do diretório de destino onde o tradutor deve ser instalado. Se o tradutor nunca tiver sido instalado, *lpszPathOut* será o mesmo que *lpszPathIn*. Se existir uma instalação anterior do tradutor, *lpszPathOut* será o caminho da instalação anterior.  
  
 *cbPathOutMax*  
 Entrada Comprimento de *lpszPathOut.*  
  
 *pcbPathOut*  
 Der Número total de bytes disponíveis para retornar em *lpszPathOut*. Se o número de bytes disponíveis para retornar for maior ou igual a *cbPathOutMax*, o caminho de saída em *lpszPathOut* será truncado para *pcbPathOutMax* menos o caractere de terminação nula. O argumento *pcbPathOut* pode ser um ponteiro nulo.  
  
 *fRequest*  
 Entrada Tipo de solicitação. *fRequest* deve conter um dos seguintes valores:  
  
 ODBC_INSTALL_INQUIRY: consulte sobre onde um tradutor pode ser instalado.  
  
 ODBC_INSTALL_COMPLETE: conclua a solicitação de instalação.  
  
 *lpdwUsageCount*  
 Der A contagem de uso do tradutor depois que essa função foi chamada.  
  
 Os aplicativos não devem definir a contagem de uso. O ODBC manterá essa contagem.  
  
## <a name="returns"></a>Retornos  
 A função retornará TRUE se for bem-sucedida, FALSE se falhar.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLInstallTranslatorEx** retorna false, um valor * \* pfErrorCode* associado pode ser obtido chamando **SQLInstallerError**. A tabela a seguir lista os valores de * \* pfErrorCode* que podem ser retornados por **SQLInstallerError** e explica cada um no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral do instalador|Ocorreu um erro para o qual não havia nenhum erro do instalador específico.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Comprimento de buffer inválido|O argumento *lpszPathOut* não era grande o suficiente para conter o caminho de saída. O buffer contém o caminho truncado.<br /><br /> O argumento *cbPathOutMax* era 0 e o argumento *fRequest* foi ODBC_INSTALL_COMPLETE.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitação inválido|O argumento *fRequest* não era um dos seguintes:<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Pares de palavra-chave-valor inválidos|O argumento *lpszTranslator* continha um erro de sintaxe.|  
|ODBC_ERROR_INVALID_PATH|Caminho de instalação inválido|O argumento *lpszPathIn* continha um caminho inválido.|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|Sequência de parâmetros inválida|O argumento *lpszTranslator* não continha uma lista de pares de palavra-chave-valor.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Não foi possível incrementar ou decrementar a contagem de uso de componentes do registro|O instalador não pôde incrementar a contagem de uso do tradutor.|  
  
## <a name="comments"></a>Comentários  
 O **SQLInstallTranslatorEx** fornece um mecanismo para instalar apenas o tradutor. Na verdade, essa função não copia nenhum arquivo. O programa de chamada é responsável por copiar os arquivos do tradutor.  
  
 **SQLInstallTranslatorEx** incrementa a contagem de uso do componente para o tradutor instalado em 1. Se já existir uma versão do tradutor, mas a contagem de uso do componente para o tradutor não existir, o novo valor de contagem de uso do componente será definido como 2.  
  
 O programa de instalação do aplicativo é responsável por copiar fisicamente o arquivo do tradutor e manter a contagem de uso do arquivo. Se o arquivo do tradutor não tiver sido instalado anteriormente, o programa de instalação do aplicativo deverá copiar o arquivo ou os arquivos e criar a contagem de uso de arquivo ou arquivos. Se o arquivo tiver sido instalado anteriormente, o programa de instalação simplesmente incrementará a contagem de uso do arquivo.  
  
 Se uma versão mais antiga do tradutor tiver sido instalada anteriormente pelo aplicativo, o tradutor deverá ser desinstalado e reinstalado, para que a contagem de uso do componente do tradutor seja válida. **SQLRemoveTranslator** deve ser chamado para diminuir a contagem de uso do componente e, em seguida, **SQLInstallTranslatorEx** deve ser chamado para incrementar a contagem de uso do componente. O programa de instalação do aplicativo deve substituir o arquivo ou arquivos antigos pelo novo arquivo. A contagem de uso do arquivo permanecerá a mesma, e outros aplicativos que usaram o arquivo de versão mais antiga agora usarão a versão mais recente.  
  
 O comprimento do caminho em *lpszPathOut* no **SQLInstallTranslatorEx** permite um processo de instalação de duas fases, portanto, um aplicativo pode determinar qual *cbPathOutMax* deve ser chamando **SQLInstallTranslatorEx** com um *fRequest* no modo de ODBC_INSTALL_INQUIRY. Isso retornará o número total de bytes disponíveis no buffer *pcbPathOut* . **SQLInstallTranslatorEx** pode ser chamado com um *fRequest* de ODBC_INSTALL_COMPLETE e o argumento *cbPathOutMax* definido como o valor no buffer *pcbPathOut* , mais o caractere de terminação nula.  
  
 Se você optar por não usar o modelo de duas fases para **SQLInstallTranslatorEx**, deverá definir *cbPathOutMax*, que define o tamanho do armazenamento para o caminho do diretório de destino, para o valor _MAX_PATH, conforme definido em STDLIB. h, para evitar truncamento.  
  
 Quando *fRequest* é ODBC_INSTALL_COMPLETE, **SQLInstallTranslatorEx** não permite que *LpszPathOut* seja nulo (ou *cbPathOutMax* como 0). Se *fRequest* for ODBC_INSTALL_COMPLETE, false será retornado quando o número de bytes disponíveis para retornar for maior ou igual a *cbPathOutMax*, com o resultado de que o truncamento ocorre.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Retornando uma opção de conversão padrão|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|Selecionando tradutores|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|Removendo tradutores|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
