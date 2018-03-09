---
title: "Função SQLInstallTranslatorEx | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLInstallTranslatorEx
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLInstallTranslatorEx
helpviewer_keywords: SQLInstallTranslatorEx function [ODBC]
ms.assetid: a0630602-53c1-4db0-98ce-70d160aedf8d
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 220d3e6b0cc62c2d3d238332975c32e9c38bc030
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlinstalltranslatorex-function"></a>Função SQLInstallTranslatorEx
**Conformidade**  
 Versão introduzidas: ODBC 3.0  
  
 **Resumo**  
 **SQLInstallTranslatorEx** adiciona informações sobre um conversor para a seção Odbcinst.ini as informações do sistema (HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST. INI\ODBC tradutores chave do registro).  
  
 A funcionalidade de **SQLInstallTranslatorEx** também podem ser acessados com [ODBCCONF. EXE](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
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
 [Entrada] Isso deve conter uma lista duplamente terminada em nulo de pares de palavra-chave-valor que descreve o conversor. Para obter mais informações sobre a sintaxe de par de valor de palavra-chave, consulte [subchaves de especificação de conversor](../../../odbc/reference/install/translator-specification-subkeys.md).  
  
 O **conversor** e **instalação** palavras-chave devem ser incluídas no *lpszTranslator* cadeia de caracteres. A conversão DLL está listado com o **conversor** palavra-chave e a instalação do tradutor DLL está listado com o **instalação** palavra-chave. Cada par é encerrada com um byte nulo e a lista inteira é encerrada com um byte nulo. (Ou seja, dois bytes NULL marcar o fim da lista.) O formato de *lpszTranslator* é o seguinte:  
  
 \0Translator=*nome da DLL de conversor*\0[Setup=*nome da DLL de instalação*\0]\0  
  
 *lpszPathIn*  
 [Entrada] Caminho completo de onde o conversor está instalado ou um ponteiro nulo. Se *lpszPath* é um ponteiro nulo, os tradutores serão instalados no diretório do sistema.  
  
 *lpszPathOut*  
 [Saída] O caminho do diretório de destino onde o conversor deve ser instalado. Se o conversor nunca tiver sido instalado, *lpszPathOut* é o mesmo que *lpszPathIn*. Se houver uma instalação anterior do tradutor, *lpszPathOut* é o caminho da instalação anterior.  
  
 *cbPathOutMax*  
 [Entrada] Comprimento de *lpszPathOut.*  
  
 *pcbPathOut*  
 [Saída] Número total de bytes disponíveis para retornar em *lpszPathOut*. Se o número de bytes disponíveis para retornar é maior que ou igual a *cbPathOutMax*, o caminho de saída em *lpszPathOut* será truncado para *pcbPathOutMax* menos de caractere de terminação nula. O *pcbPathOut* argumento pode ser um ponteiro nulo.  
  
 *Frequentes*  
 [Entrada] Tipo de solicitação. *Frequentes* deve conter um dos seguintes valores:  
  
 ODBC_INSTALL_INQUIRY: Saber onde um conversor pode ser instalado.  
  
 ODBC_INSTALL_COMPLETE: Conclua a solicitação de instalação.  
  
 *lpdwUsageCount*  
 [Saída] A contagem de uso do tradutor depois que essa função foi chamada.  
  
 Aplicativos não devem definir a contagem de uso. ODBC manterá essa contagem.  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedida, FALSO se ele falhar.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLInstallTranslatorEx** retorna FALSE, um tipo de  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista o  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral de instalador|Ocorreu um erro para que nenhum erro específico do instalador.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Comprimento de buffer inválido|O *lpszPathOut* argumento não era grande o suficiente para conter o caminho de saída. O buffer contém o caminho truncado.<br /><br /> O *cbPathOutMax* argumento era 0 e o *frequentes* argumento foi ODBC_INSTALL_COMPLETE.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitação inválido|O *frequentes* argumento não era um dos seguintes:<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Pares de valor de palavra-chave inválida|O *lpszTranslator* argumento continha um erro de sintaxe.|  
|ODBC_ERROR_INVALID_PATH|Caminho de instalação inválido|O *lpszPathIn* argumento continha um caminho inválido.|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|Sequência de parâmetro inválido|O *lpszTranslator* argumento não continha uma lista de pares de valor de palavra-chave.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Não foi possível incrementar ou decrementar a contagem de uso de componentes do registro|Falha do instalador usado incrementar a contagem de utilização do tradutor.|  
  
## <a name="comments"></a>Comentários  
 **SQLInstallTranslatorEx** fornece um mecanismo para instalar apenas o conversor. Essa função realmente não copia todos os arquivos. O programa de chamada é responsável por copiar os arquivos do conversor.  
  
 **SQLInstallTranslatorEx** incrementa a contagem de uso do componente para o conversor instalado em 1. Se já existe uma versão do tradutor, mas a contagem de uso do componente para o conversor não existir, o novo valor de contagem de uso do componente é definido como 2.  
  
 O programa de instalação do aplicativo é responsável por copiar fisicamente o arquivo de conversor e manter a contagem de uso de arquivos. Se o arquivo de conversor anteriormente não foi instalado, o programa de instalação do aplicativo deve copiar o arquivo ou arquivos e criar o arquivo ou arquivos a contagem de uso. Se o arquivo tiver sido instalado anteriormente, o programa de instalação simplesmente incrementa a contagem de uso de arquivos.  
  
 Se uma versão mais antiga do tradutor foi instalada anteriormente pelo aplicativo, o conversor deve ser desinstalado e reinstalado, para que a contagem de uso do componente de conversor válida. **No SQLRemoveTranslator** deve ser chamado para diminuir a contagem de uso do componente e, em seguida, **SQLInstallTranslatorEx** deve ser chamado para incrementar a contagem de uso do componente. O programa de instalação do aplicativo deve substituir o arquivo antigo ou arquivos com o novo arquivo. A contagem de uso de arquivo permanece o mesmo, e outros aplicativos que usavam o arquivo de versão mais antigo agora usará a versão mais recente.  
  
 O comprimento do caminho em *lpszPathOut* na **SQLInstallTranslatorEx** permite que um processo de instalação de duas fases, para que um aplicativo possa determinar o que *cbPathOutMax* devem ser chamando **SQLInstallTranslatorEx** com um *frequentes* de modo ODBC_INSTALL_INQUIRY. Isso retornará o número total de bytes disponíveis no *pcbPathOut* buffer. **SQLInstallTranslatorEx** , em seguida, pode ser chamado com um *frequentes* de ODBC_INSTALL_COMPLETE e o *cbPathOutMax* argumento definido como o valor de *pcbPathOut* buffer mais o caractere de terminação nula.  
  
 Se você optar por não usar o modelo de duas fases para **SQLInstallTranslatorEx**, você deve definir *cbPathOutMax*, que define o tamanho do armazenamento para o caminho do diretório de destino, para o valor MAX_PATH, como definido em Stdlib.h, para evitar truncamento.  
  
 Quando *frequentes* é ODBC_INSTALL_COMPLETE, **SQLInstallTranslatorEx** não permite *lpszPathOut* NULL (ou *cbPathOutMax* deve ser 0). Se *frequentes* é ODBC_INSTALL_COMPLETE, FALSE será retornado quando o número de bytes disponíveis para retornar é maior que ou igual a *cbPathOutMax*, sabendo que o truncamento ocorre.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Retornando uma opção de conversão padrão|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|Selecionando os tradutores|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|Removendo os tradutores|[No SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
