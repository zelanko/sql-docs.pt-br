---
title: "Função ConfigDriver | Microsoft Docs"
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
- ConfigDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- ConfigDriver
helpviewer_keywords:
- ConfigDriver [ODBC]
ms.assetid: 9473f48f-bcae-4784-89c1-7839bad4ed13
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 037d4ffcbe7d81c6e4a9c1a524f5f4977621f277
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="configdriver-function"></a>Função ConfigDriver
**Conformidade**  
 Versão introduzidas: ODBC 2.5  
  
 **Resumo**  
 **ConfigDriver** permite que um programa de instalação executar a instalação e desinstalar funções sem a necessidade do programa chamar **ConfigDSN**. Essa função executará a funções específicas de driver como Criando informações específicas do driver de sistema e executar conversões de DSN durante a instalação, bem como limpar modificações no sistema de informações durante a desinstalação. Essa função é exposta pelo DLL de instalação do driver ou uma DLL de instalação separados.  
  
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
 [Entrada] Identificador da janela pai. A função não exibirá caixas de diálogo se o identificador é nulo.  
  
 *Frequentes*  
 [Entrada] Tipo de solicitação. O *frequentes* argumento deve conter um dos seguintes valores:  
  
 ODBC_INSTALL_DRIVER: Instale um novo driver.  
  
 ODBC_REMOVE_DRIVER: Remova um driver.  
  
 Essa opção também pode ser específicos do driver, caso em que o *frequentes* argumento para a primeira opção deve iniciar de ODBC_CONFIG_DRIVER_MAX + 1. O *frequentes* também deve iniciar o argumento para qualquer opção adicional de um valor maior do que ODBC_CONFIG_DRIVER_MAX + 1.  
  
 *lpszDriver*  
 [Entrada] O nome do driver como registrado na chave Odbcinst.ini as informações do sistema.  
  
 *lpszArgs*  
 [Entrada] Uma cadeia de caracteres terminada em nulo que contém argumentos para um determinado driver *frequentes*.  
  
 *lpszMsg*  
 [Saída] Uma cadeia terminada em nulo que contém uma mensagem de saída da configuração de driver.  
  
 *cbMsgMax*  
 [Entrada] Comprimento de *lpszMsg*.  
  
 *pcbMsgOut*  
 [Saída] Número total de bytes disponíveis para retornar em *lpszMsg*.  
  
 Se o número de bytes disponíveis para retornar é maior que ou igual a *cbMsgMax*, a mensagem de saída na *lpszMsg* será truncado para *cbMsgMax* menos o encerramento nulo caractere. O *pcbMsgOut* argumento pode ser um ponteiro nulo.  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedida, FALSO se ele falhar.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **ConfigDriver** retorna FALSE, um tipo de  *\*pfErrorCode* valor é postado para o buffer de erro de instalador por uma chamada para **SQLPostInstallerError** e pode ser obtida chamando **SQLInstallerError**. A seguinte tabela lista o  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|Identificador de janela inválido|O *hwndParent* argumento era inválido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitação inválido|O *frequentes* argumento não era um dos seguintes:<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> A opção específica do driver era menor ou igual a ODBC_CONFIG_DRIVER_MAX.|  
|ODBC_ERROR_INVALID_NAME|Nome de driver ou conversor inválido|O *lpszDriver* argumento era inválido. Ele não pôde ser encontrado no registro.|  
|ODBC_ERROR_REQUEST_FAILED|*Solicitar* falha|Não foi possível executar a operação solicitada pelo *frequentes* argumento.|  
|ODBC_ERROR_DRIVER_SPECIFIC|Erro específico do driver ou do conversor|Um erro específico do driver para o qual não há nenhum erro de instalador ODBC definido. O *SzError* argumento em uma chamada para o **SQLPostInstallerError** a função deve conter a mensagem de erro específica do driver.|  
  
## <a name="comments"></a>Comentários  
  
### <a name="driver-specific-options"></a>Opções específicas do driver  
 Um aplicativo pode solicitar recursos específicos do driver expostos pelo driver usando o *frequentes* argumento. O *frequentes* para a primeira opção serão ODBC_CONFIG_DRIVER_MAX mais 1, e opções adicionais serão incrementadas em 1 desse valor. Argumentos necessários pelo driver para essa função deve ser fornecida em uma cadeia de caracteres terminada em nulo passado a *lpszArgs* argumento. Drivers fornecendo essa funcionalidade devem manter uma tabela de opções específicas do driver. As opções devem ser documentadas na documentação do driver. Autores de aplicativos que usam opções específicas do driver devem estar cientes de que isso fará o aplicativo menos interoperável.  
  
### <a name="messages"></a>Mensagens  
 Uma rotina de instalação do driver pode enviar uma mensagem de texto para um aplicativo como uma cadeia de caracteres terminada em nulo no *lpszMsg* buffer. A mensagem será truncada para *cbMsgMax* menos o caractere null de terminação pelo **ConfigDriver** função se ele for maior que ou igual a *cbMsgMax* caracteres.

