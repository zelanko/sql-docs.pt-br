---
title: Função ConfigDriver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- ConfigDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- ConfigDriver
helpviewer_keywords:
- ConfigDriver [ODBC]
ms.assetid: 9473f48f-bcae-4784-89c1-7839bad4ed13
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6a2da5fd5ce01bd97f13d7c8d805c615c1ac436a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303957"
---
# <a name="configdriver-function"></a>Função ConfigDriver
**Conformidade**  
 Versão introduzida: ODBC 2.5  
  
 **Resumo**  
 **ConfigDriver** permite que um programa de configuração execute e desinstale funções sem exigir que o programa chame **ConfigDSN**. Essa função executará funções específicas do driver, como criar informações específicas do sistema e executar conversões de DSN durante a instalação, bem como limpar as modificações das informações do sistema durante a desinstalação. Esta função é exposta pela configuração do driver DLL ou por uma DLL de configuração separada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL ConfigDriver(  
      HWND    hwndParent,  
      WORD    fRequest,  
      LPCSTR  lpszDriver,  
      LPCSTR  lpszArgs,  
      LPSTR   lpszMsg,  
      WORD    cbMsgMax,  
      WORD *  pcbMsgOut);  
```  
  
## <a name="arguments"></a>Argumentos  
 *Hwndparent*  
 [Entrada] Alça da janela dos pais. A função não exibirá nenhuma caixa de diálogo se a alça estiver nula.  
  
 *fSolicitar*  
 [Entrada] Tipo de pedido. O *argumento fRequest* deve conter um dos seguintes valores:  
  
 ODBC_INSTALL_DRIVER: Instale um novo driver.  
  
 ODBC_REMOVE_DRIVER: Remova um motorista.  
  
 Essa opção também pode ser específica do driver, nesse caso o argumento *fRequest* para a primeira opção deve começar a partir de ODBC_CONFIG_DRIVER_MAX+1. O *argumento fRequest* para qualquer opção adicional também deve partir de um valor maior que ODBC_CONFIG_DRIVER_MAX+1.  
  
 *Lpszdriver*  
 [Entrada] O nome do motorista registrado na chave Odbcinst.ini das informações do sistema.  
  
 *lpszArgs*  
 [Entrada] Uma seqüência de terminadas nula contendo argumentos para um *fRequest*específico do driver .  
  
 *lpszMsg*  
 [Saída] Uma seqüência de terminadas nula contendo uma mensagem de saída da configuração do driver.  
  
 *cbMsgMax*  
 [Entrada] Comprimento de *lpszMsg*.  
  
 *pcbMsgOut*  
 [Saída] Número total de bytes disponíveis para retornar em *lpszMsg*.  
  
 Se o número de bytes disponíveis para retornar for maior ou igual ao *cbMsgMax,* a mensagem de saída em *lpszMsg* é truncada para *cbMsgMax* menos o caractere de rescisão nula. O *argumento pcbMsgOut* pode ser um ponteiro nulo.  
  
## <a name="returns"></a>Retornos  
 A função retorna TRUE se for bem sucedida, FALSA se falhar.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o ConfigDriver** retorna FALSE, um valor * \*pfErrorCode* associado é postado no buffer de erro do instalador por uma chamada para **SQLPostInstallerError** e pode ser obtido ligando para **SQLInstallerError**. A tabela a * \** seguir lista os valores pfErrorCode que podem ser retornados pelo **SQLInstallerError** e explica cada um no contexto desta função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|Alça de janela inválida|O argumento *hwndParent* era inválido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitação inválida|O argumento *fRequest* não foi um dos seguintes:<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> A opção específica do motorista era menor ou igual a ODBC_CONFIG_DRIVER_MAX.|  
|ODBC_ERROR_INVALID_NAME|Nome de motorista ou tradutor inválido|O argumento *lpszDriver* era inválido. Não foi possível encontrar no registro.|  
|ODBC_ERROR_REQUEST_FAILED|*Falha na solicitação*|Não foi possível realizar a operação solicitada pelo argumento *fRequest.*|  
|ODBC_ERROR_DRIVER_SPECIFIC|Erro específico do driver ou tradutor|Um erro específico do driver para o qual não há um erro de instalador ODBC definido. O argumento *SzError* em uma chamada para a função **SQLPostInstallerError** deve conter a mensagem de erro específica do driver.|  
  
## <a name="comments"></a>Comentários  
  
### <a name="driver-specific-options"></a>Opções específicas do driver  
 Um aplicativo pode solicitar recursos específicos do driver expostos pelo motorista usando o argumento *fRequest.* O *fRequest* para a primeira opção será ODBC_CONFIG_DRIVER_MAX mais 1, e opções adicionais serão incrementadas por 1 a partir desse valor. Quaisquer argumentos exigidos pelo driver para essa função devem ser fornecidos em uma seqüência de terminação nula aprovada no argumento *lpszArgs.* Os drivers que fornecem essa funcionalidade devem manter uma tabela de opções específicas para o motorista. As opções devem estar totalmente documentadas na documentação do motorista. Os escritores de aplicativos que usam opções específicas para o motorista devem estar cientes de que isso tornará o aplicativo menos interoperável.  
  
### <a name="messages"></a>Mensagens  
 Uma rotina de configuração do driver pode enviar uma mensagem de texto para um aplicativo como uma seqüência de caracteres com término nulo no buffer *lpszMsg.* A mensagem será truncada para *cbMsgMax* menos o caractere de rescisão nula pela função **ConfigDriver** se for maior ou igual aos *caracteres cbMsgMax.*
