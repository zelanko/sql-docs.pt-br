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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 57a2fb53226af9aeb6e546f6109a3e182ffc754f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65536555"
---
# <a name="sqlinstalltranslatorex-function"></a>Função SQLInstallTranslatorEx
**Conformidade com**  
 Versão introduzida: ODBC 3.0  
  
 **Resumo**  
 **SQLInstallTranslatorEx** adiciona informações sobre um conversor para a seção Odbcinst. ini, as informações do sistema (HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST. INI\ODBC tradutores chave do registro).  
  
 A funcionalidade do **SQLInstallTranslatorEx** também podem ser acessados com [ODBCCONF. EXE](../../../odbc/odbcconf-exe.md).  
  
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
 [Entrada] Isso deve conter uma lista duplamente terminada em nulo de pares de palavra-chave-valor que descreve o tradutor. Para obter mais informações sobre a sintaxe de par de valor de palavra-chave, consulte [subchaves de especificação do conversor](../../../odbc/reference/install/translator-specification-subkeys.md).  
  
 O **tradutor** e **instalação** palavras-chave devem ser incluídas na *lpszTranslator* cadeia de caracteres. A tradução DLL está listado com o **tradutor** palavra-chave e a configuração de conversor DLL está listado com o **instalação** palavra-chave. Cada par é encerrada com um byte nulo e a lista inteira é encerrada com um byte nulo. (Ou seja, dois bytes NULL marcam o final da lista.) O formato do *lpszTranslator* é da seguinte maneira:  
  
 \0Translator=*translator-DLL-filename*\0[Setup=*setup-DLL-filename*\0]\0  
  
 *lpszPathIn*  
 [Entrada] Caminho completo do qual o conversor deve ser instalado ou um ponteiro nulo. Se *lpszPath* for um ponteiro nulo, os tradutores serão instalados no diretório do sistema.  
  
 *lpszPathOut*  
 [Saída] O caminho do diretório de destino no qual o conversor deve ser instalado. Se o conversor nunca tiver sido instalado, *lpszPathOut* é o mesmo que *lpszPathIn*. Se houver uma instalação anterior, o conversor *lpszPathOut* é o caminho da instalação anterior.  
  
 *cbPathOutMax*  
 [Entrada] Comprimento de *lpszPathOut.*  
  
 *pcbPathOut*  
 [Saída] Número total de bytes disponíveis para retornar na *lpszPathOut*. Se o número de bytes disponíveis para retornar for maior que ou igual a *cbPathOutMax*, o caminho de saída na *lpszPathOut* será truncado com *pcbPathOutMax* menos o caractere de finalização null. O *pcbPathOut* argumento pode ser um ponteiro nulo.  
  
 *fRequest*  
 [Entrada] Tipo de solicitação. *Frequentes* deve conter um dos seguintes valores:  
  
 ODBC_INSTALL_INQUIRY: Pesquisa sobre onde um tradutor pode ser instalado.  
  
 ODBC_INSTALL_COMPLETE: Conclua a solicitação de instalação.  
  
 *lpdwUsageCount*  
 [Saída] A contagem de utilização do tradutor depois que essa função foi chamada.  
  
 Aplicativos não devem definir a contagem de uso. ODBC manterá essa contagem.  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedida, FALSO se ele falhar.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLInstallTranslatorEx** retornar FALSE, um associado  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista os  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral de instalador|Ocorreu um erro para que nenhum erro específico do instalador.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Comprimento de buffer inválido|O *lpszPathOut* argumento não era grande o suficiente para conter o caminho de saída. O buffer contém o caminho truncado.<br /><br /> O *cbPathOutMax* argumento era 0 e o *frequentes* argumento era ODBC_INSTALL_COMPLETE.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitação inválido|O *frequentes* argumento não era um dos seguintes:<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Pares de valor de palavra-chave inválido|O *lpszTranslator* argumento continha um erro de sintaxe.|  
|ODBC_ERROR_INVALID_PATH|Caminho de instalação inválido|O *lpszPathIn* argumento continha um caminho inválido.|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|Sequência de parâmetro inválido|O *lpszTranslator* argumento não contém uma lista de pares de palavra-chave-valor.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Não foi possível incrementar ou decrementar a contagem de utilização de componente do registro|O instalador não conseguiu incrementar a contagem de utilização do tradutor.|  
  
## <a name="comments"></a>Comentários  
 **SQLInstallTranslatorEx** fornece um mecanismo para instalar apenas o tradutor. Essa função não copia, na verdade, todos os arquivos. O programa de chamada é responsável por copiar os arquivos de tradução.  
  
 **SQLInstallTranslatorEx** incrementa a contagem de utilização de componente para o conversor instalado em 1. Se já existe uma versão do tradutor, mas a contagem de utilização de componente para o conversor não existir, o novo valor de contagem de uso do componente é definido como 2.  
  
 O programa de instalação do aplicativo é responsável por fisicamente copiando o arquivo de tradução e manter a contagem de utilização do arquivo. Se o arquivo de tradução não tiver sido instalado anteriormente, o programa de instalação do aplicativo deve copiar o arquivo ou arquivos e criar o arquivo ou arquivos de contagem de uso. Se o arquivo tiver sido instalado anteriormente, o programa de instalação simplesmente incrementa a contagem de uso de arquivos.  
  
 Se uma versão mais antiga do tradutor foi instalada anteriormente pelo aplicativo, o conversor deve ser desinstalado e reinstalado, para que a contagem de uso do componente conversor é válida. **SQLRemoveTranslator** deve ser chamado para diminuir a contagem de uso do componente e então **SQLInstallTranslatorEx** deve ser chamado para incrementar a contagem de uso do componente. O programa de instalação do aplicativo deve substituir o arquivo antigo ou arquivos com o novo arquivo. A contagem de uso de arquivos permanecerão os mesmos e outros aplicativos que usaram o arquivo de versão mais antigo agora usará a versão mais recente.  
  
 O comprimento do caminho em *lpszPathOut* na **SQLInstallTranslatorEx** permite que um processo de duas fases de instalação, para que um aplicativo possa determinar quais *cbPathOutMax* deve ser chamando **SQLInstallTranslatorEx** com um *frequentes* do modo ODBC_INSTALL_INQUIRY. Isso retornará o número total de bytes disponíveis na *pcbPathOut* buffer. **SQLInstallTranslatorEx** , em seguida, pode ser chamado com um *frequentes* de ODBC_INSTALL_COMPLETE e o *cbPathOutMax* argumento definido como o valor no *pcbPathOut* buffer, mais o caractere nulo de terminação.  
  
 Se você optar por não usar o modelo de duas fases para **SQLInstallTranslatorEx**, você deve definir *cbPathOutMax*, que define o tamanho do armazenamento para o caminho do diretório de destino, para o valor MAX_PATH, como definida em stdlib. h, para evitar truncamento.  
  
 Quando *frequentes* é ODBC_INSTALL_COMPLETE, **SQLInstallTranslatorEx** não permite *lpszPathOut* NULL (ou *cbPathOutMax* deve ser 0). Se *frequentes* é ODBC_INSTALL_COMPLETE, FALSO é retornado quando o número de bytes disponíveis para retornar é maior que ou igual a *cbPathOutMax*, com o resultado que o truncamento ocorre.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Retornando uma opção de conversão padrão|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|Selecionando os tradutores|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|Removendo os tradutores|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
