---
description: Função SQLConfigDriver
title: Função SQLConfigDriver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLConfigDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLConfigDriver
helpviewer_keywords:
- SQLConfigDriver function [ODBC]
ms.assetid: 4f681961-ac9f-4d88-b065-5258ba112642
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 04ee54bba13730504ed08cfc1307858edea56282
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476152"
---
# <a name="sqlconfigdriver-function"></a>Função SQLConfigDriver
**Conformidade**  
 Versão introduzida: ODBC 2,5  
  
 **Resumo**  
 **SQLConfigDriver** carrega a DLL de configuração de driver apropriada e chama a função **ConfigDriver** .  
  
 A funcionalidade do **SQLConfigDriver** também pode ser acessada com [ODBCCONF.EXE](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL SQLConfigDriver(  
     HWND     hwndParent,  
     WORD     fRequest,  
     LPCSTR   lpszDriver,  
     LPCSTR   lpszArgs,  
     LPSTR    lpszMsg,  
     WORD     cbMsgMax,  
     WORD *   pcbMsgOut);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hwndParent*  
 Entrada Identificador de janela pai. A função não exibirá nenhuma caixa de diálogo se o identificador for nulo.  
  
 *fRequest*  
 Entrada Tipo de solicitação. *fRequest* deve conter um dos seguintes valores:  
  
 ODBC_CONFIG_DRIVER: altera o tempo limite do pool de conexões usado pelo driver.  
  
 ODBC_INSTALL_DRIVER: instala um novo driver.  
  
 ODBC_REMOVE_DRIVER: Remove um driver existente.  
  
 Essa opção também pode ser específica do driver; nesse caso, o *fRequest* da primeira opção deve começar de ODBC_CONFIG_DRIVER_MAX + 1. O *fRequest* para qualquer opção adicional também deve começar com um valor maior que ODBC_CONFIG_DRIVER_MAX + 1.  
  
 *lpszDriver*  
 Entrada O nome do driver conforme registrado nas informações do sistema.  
  
 *lpszArgs*  
 Entrada Uma cadeia de caracteres terminada em nulo que contém argumentos para um *fRequest*específico do driver.  
  
 *lpszMsg*  
 Der Uma cadeia de caracteres terminada em nulo que contém uma mensagem de saída da configuração do driver.  
  
 *cbMsgMax*  
 Entrada Comprimento de *lpszMsg.*  
  
 *pcbMsgOut*  
 Der Número total de bytes disponíveis para retornar em *lpszMsg*. Se o número de bytes disponíveis para retornar for maior ou igual a *cbMsgMax*, a mensagem de saída em *lpszMsg* será truncada para *cbMsgMax* menos o caractere de terminação nula. O argumento *pcbMsgOut* pode ser um ponteiro nulo.  
  
## <a name="returns"></a>Retornos  
 A função retornará TRUE se for bem-sucedida, FALSE se falhar.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLConfigDriver** retorna false, um valor * \* pfErrorCode* associado pode ser obtido chamando **SQLInstallerError**. A tabela a seguir lista os valores de * \* pfErrorCode* que podem ser retornados por **SQLInstallerError** e explica cada um no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral do instalador|Ocorreu um erro para o qual não havia nenhum erro do instalador específico.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Comprimento de buffer inválido|O argumento *lpszMsg* era inválido.|  
|ODBC_ERROR_INVALID_HWND|Identificador de janela inválido|O argumento *hwndParent* era inválido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitação inválido|O argumento *fRequest* não era um dos seguintes:<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> O argumento *fRequest* era uma opção específica de driver que era menor ou igual a ODBC_CONFIG_DRIVER_MAX.|  
|ODBC_ERROR_INVALID_NAME|Nome de driver ou tradutor inválido|O argumento *lpszDriver* era inválido. Ele não foi encontrado no registro.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Pares de palavra-chave-valor inválidos|O argumento *lpszArgs* continha um erro de sintaxe.|  
|ODBC_ERROR_REQUEST_FAILED|Falha na *solicitação*|O instalador não pôde executar a operação solicitada pelo argumento *fRequest* . Falha na chamada para **ConfigDriver** .|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Não foi possível carregar a biblioteca de instalação do driver ou do Tradutor|Não foi possível carregar a biblioteca de instalação do driver.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não pôde executar a função devido à falta de memória.|  
  
## <a name="comments"></a>Comentários  
 O **SQLConfigDriver** permite que um aplicativo chame a rotina **ConfigDriver** de um driver sem precisar saber o nome e carregar a DLL de instalação específica do driver. Um programa de instalação chama essa função depois que a DLL de instalação do driver é instalada. O programa de chamada deve estar ciente de que essa função pode não estar disponível para todos os drivers. Nesse caso, o programa de chamada deve continuar sem erros.  
  
## <a name="driver-specific-options"></a>Opções específicas do driver  
 Um aplicativo pode solicitar recursos específicos do driver expostos pelo driver usando o argumento *fRequest* . O *fRequest* da primeira opção será ODBC_CONFIG_DRIVER_MAX + 1, e as opções adicionais serão incrementadas em 1 a partir desse valor. Todos os argumentos exigidos pelo driver para essa função devem ser fornecidos em uma cadeia de caracteres terminada em nulo passada no argumento *lpszArgs* . Os drivers que fornecem essa funcionalidade devem manter uma tabela de opções específicas de driver. As opções devem ser totalmente documentadas na documentação do driver. Os gravadores de aplicativos que usam opções específicas de driver devem estar cientes de que esse uso tornará o aplicativo menos interoperável.  
  
## <a name="setting-connection-pooling-timeout"></a>Definindo o tempo limite do pooling de conexão  
 As propriedades de tempo limite do pooling de conexão podem ser definidas quando você define a configuração do driver. **SQLConfigDriver** é chamado com um *fRequest* de ODBC_CONFIG_DRIVER e *lpszArgs* definido como **CPTimeout**. **CPTimeout** determina o período de tempo que uma conexão pode permanecer no pool de conexões sem ser usada. Quando o tempo limite expira, a conexão é fechada e removida do pool. O tempo limite padrão é de 60 segundos.  
  
 Quando **SQLConfigDriver** é chamado com *fRequest* definido como ODBC_INSTALL_DRIVER ou ODBC_REMOVE_DRIVER, o Gerenciador de driver carrega a DLL de configuração de driver apropriada e chama a função **ConfigDriver** . Quando **SQLConfigDriver** é chamado com um *fRequest* de ODBC_CONFIG_DRIVER, todo o processamento é executado no ODBC Installer, para que a DLL de instalação do driver não precise ser carregada.  
  
## <a name="messages"></a>Mensagens  
 Uma rotina de instalação de driver pode enviar uma mensagem de texto a um aplicativo como cadeias de caracteres de terminação nula no buffer *lpszMsg* . A mensagem será truncada para *cbMsgMax* menos o caractere de terminação nula pela função **ConfigDriver** se for maior ou igual a caracteres *cbMsgMax* .  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Adicionando, modificando ou removendo um driver|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)(na DLL de instalação)|  
|Removendo a fonte de dados padrão|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|
