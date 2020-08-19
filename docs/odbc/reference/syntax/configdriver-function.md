---
description: Função ConfigDriver
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
ms.openlocfilehash: 3d59765d1b6a6a662c02b459e07bac10895838a2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428948"
---
# <a name="configdriver-function"></a>Função ConfigDriver
**Conformidade**  
 Versão introduzida: ODBC 2,5  
  
 **Resumo**  
 O **ConfigDriver** permite que um programa de instalação execute funções de instalação e desinstalação sem exigir que o programa chame **ConfigDSN**. Essa função executará funções específicas do driver, como a criação de informações do sistema específicas do driver e a execução de conversões de DSN durante a instalação, bem como a limpeza das modificações de informações do sistema durante a desinstalação. Essa função é exposta pela DLL de instalação do driver ou por uma DLL de instalação separada.  
  
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
 *hwndParent*  
 Entrada Identificador de janela pai. A função não exibirá nenhuma caixa de diálogo se o identificador for nulo.  
  
 *fRequest*  
 Entrada Tipo de solicitação. O argumento *fRequest* deve conter um dos seguintes valores:  
  
 ODBC_INSTALL_DRIVER: instalar um novo driver.  
  
 ODBC_REMOVE_DRIVER: remover um driver.  
  
 Essa opção também pode ser específica de driver; nesse caso, o argumento *fRequest* para a primeira opção deve começar de ODBC_CONFIG_DRIVER_MAX + 1. O argumento *fRequest* para qualquer opção adicional também deve começar com um valor maior que ODBC_CONFIG_DRIVER_MAX + 1.  
  
 *lpszDriver*  
 Entrada O nome do driver, conforme registrado na chave de Odbcinst.ini das informações do sistema.  
  
 *lpszArgs*  
 Entrada Uma cadeia de caracteres terminada em nulo que contém argumentos para um *fRequest*específico do driver.  
  
 *lpszMsg*  
 Der Uma cadeia de caracteres terminada em nulo que contém uma mensagem de saída da configuração do driver.  
  
 *cbMsgMax*  
 Entrada Comprimento de *lpszMsg*.  
  
 *pcbMsgOut*  
 Der Número total de bytes disponíveis para retornar em *lpszMsg*.  
  
 Se o número de bytes disponíveis para retornar for maior ou igual a *cbMsgMax*, a mensagem de saída em *lpszMsg* será truncada para *cbMsgMax* menos o caractere de terminação nula. O argumento *pcbMsgOut* pode ser um ponteiro nulo.  
  
## <a name="returns"></a>Retornos  
 A função retornará TRUE se for bem-sucedida, FALSE se falhar.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **ConfigDriver** retorna false, um valor de * \* pfErrorCode* associado é Postado no buffer de erros do instalador por uma chamada para **SQLPostInstallerError** e pode ser obtido chamando **SQLInstallerError**. A tabela a seguir lista os valores de * \* pfErrorCode* que podem ser retornados por **SQLInstallerError** e explica cada um no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|Identificador de janela inválido|O argumento *hwndParent* era inválido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitação inválido|O argumento *fRequest* não era um dos seguintes:<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> A opção específica do driver era menor ou igual a ODBC_CONFIG_DRIVER_MAX.|  
|ODBC_ERROR_INVALID_NAME|Nome de driver ou tradutor inválido|O argumento *lpszDriver* era inválido. Ele não foi encontrado no registro.|  
|ODBC_ERROR_REQUEST_FAILED|Falha na *solicitação*|Não foi possível executar a operação solicitada pelo argumento *fRequest* .|  
|ODBC_ERROR_DRIVER_SPECIFIC|Erro específico do driver ou do Tradutor|Um erro específico de driver para o qual não há erro de instalador ODBC definido. O argumento *SzError* em uma chamada para a função **SQLPostInstallerError** deve conter a mensagem de erro específica do driver.|  
  
## <a name="comments"></a>Comentários  
  
### <a name="driver-specific-options"></a>Opções específicas do driver  
 Um aplicativo pode solicitar recursos específicos do driver expostos pelo driver usando o argumento *fRequest* . O *fRequest* da primeira opção será ODBC_CONFIG_DRIVER_MAX mais 1, e as opções adicionais serão incrementadas em 1 a partir desse valor. Todos os argumentos exigidos pelo driver para essa função devem ser fornecidos em uma cadeia de caracteres terminada em nulo passada no argumento *lpszArgs* . Os drivers que fornecem essa funcionalidade devem manter uma tabela de opções específicas de driver. As opções devem ser totalmente documentadas na documentação do driver. Os criadores de aplicativos que usam opções específicas de driver devem estar cientes de que isso tornará o aplicativo menos interoperável.  
  
### <a name="messages"></a>Mensagens  
 Uma rotina de instalação de driver pode enviar uma mensagem de texto para um aplicativo como uma cadeia de caracteres terminada em nulo no buffer *lpszMsg* . A mensagem será truncada para *cbMsgMax* menos o caractere de terminação nula pela função **ConfigDriver** se for maior ou igual a caracteres *cbMsgMax* .
