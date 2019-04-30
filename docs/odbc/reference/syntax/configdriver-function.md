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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d69db144a460bb2f662c8ba906bf0302cdf98388
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63232077"
---
# <a name="configdriver-function"></a>Função ConfigDriver
**Conformidade com**  
 Versão introduzida: ODBC 2.5  
  
 **Resumo**  
 **ConfigDriver** permite que um programa de instalação realizar a instalar e desinstalar funções, sem a necessidade do programa chamar **ConfigDSN**. Essa função executará funções específicas de driver como criação de informações do sistema específicos do driver e executar conversões de DSN durante a instalação, bem como limpeza de modificações no sistema de informações durante a desinstalação. Essa função é exposta pela DLL de instalação do driver ou uma DLL de instalação separado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
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
 *hwndParent*  
 [Entrada] Identificador de janela pai. A função não exibirá nenhuma caixa de diálogo se o identificador for nulo.  
  
 *fRequest*  
 [Entrada] Tipo de solicitação. O *frequentes* argumento deve conter um dos seguintes valores:  
  
 ODBC_INSTALL_DRIVER: Instale um novo driver.  
  
 ODBC_REMOVE_DRIVER: Remova um driver.  
  
 Essa opção também pode ser específicos do driver, caso em que o *frequentes* argumento para a primeira opção deve iniciar de ODBC_CONFIG_DRIVER_MAX + 1. O *frequentes* argumento para qualquer opção adicional também deve iniciar de um valor maior que ODBC_CONFIG_DRIVER_MAX + 1.  
  
 *lpszDriver*  
 [Entrada] O nome do driver como registrado na chave do Odbcinst. ini, as informações do sistema.  
  
 *lpszArgs*  
 [Entrada] Uma cadeia de caracteres terminada em nulo que contém argumentos para um específicos de driver *frequentes*.  
  
 *lpszMsg*  
 [Saída] Uma cadeia terminada em nulo que contém uma mensagem de saída da configuração do driver.  
  
 *cbMsgMax*  
 [Entrada] Comprimento da *lpszMsg*.  
  
 *pcbMsgOut*  
 [Saída] Número total de bytes disponíveis para retornar na *lpszMsg*.  
  
 Se o número de bytes disponíveis para retornar for maior que ou igual a *cbMsgMax*, a mensagem de saída na *lpszMsg* será truncado com *cbMsgMax* menos a terminação null caractere. O *pcbMsgOut* argumento pode ser um ponteiro nulo.  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedida, FALSO se ele falhar.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **ConfigDriver** retornar FALSE, um associado  *\*pfErrorCode* valor é postado no buffer de erro do instalador por uma chamada para **SQLPostInstallerError** e pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista os  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|Identificador de janela inválido|O *hwndParent* argumento era inválido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitação inválido|O *frequentes* argumento não era um dos seguintes:<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> A opção específica do driver era menor que ou igual a ODBC_CONFIG_DRIVER_MAX.|  
|ODBC_ERROR_INVALID_NAME|Nome inválido de driver ou conversor|O *lpszDriver* argumento era inválido. Ele não pôde ser encontrado no registro.|  
|ODBC_ERROR_REQUEST_FAILED|*Solicitar* falhou|Não foi possível executar a operação solicitada pelo *frequentes* argumento.|  
|ODBC_ERROR_DRIVER_SPECIFIC|Erro específico do driver ou do tradutor|Um erro específico do driver para o qual não há nenhum erro de instalador ODBC definido. O *SzError* argumento em uma chamada para o **SQLPostInstallerError** função deve conter a mensagem de erro específico do driver.|  
  
## <a name="comments"></a>Comentários  
  
### <a name="driver-specific-options"></a>Opções específicas do driver  
 Um aplicativo pode solicitar recursos específicos do driver expostos pelo driver usando o *frequentes* argumento. O *frequentes* para a primeira opção serão ODBC_CONFIG_DRIVER_MAX mais 1, e as opções adicionais serão incrementadas em 1 desse valor. Quaisquer argumentos exigidos pelo driver para essa função deve ser fornecida em uma cadeia de caracteres terminada em nulo passado a *lpszArgs* argumento. Drivers de fornecer tal funcionalidade devem manter uma tabela de opções específicas do driver. As opções devem ser totalmente documentadas na documentação do driver. Os autores de aplicativos que usam as opções específicas do driver devem estar cientes de que isso fará o aplicativo menos interoperável.  
  
### <a name="messages"></a>Mensagens  
 Uma rotina de instalação do driver pode enviar uma mensagem de texto para um aplicativo como uma cadeia de caracteres terminada em nulo a *lpszMsg* buffer. A mensagem será truncada para *cbMsgMax* menos o caractere nulo de terminação, o **ConfigDriver** funcionará se ele é maior que ou igual a *cbMsgMax* caracteres.
