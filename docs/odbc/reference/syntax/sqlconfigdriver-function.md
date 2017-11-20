---
title: "Função no SQLConfigDriver | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9dd30a466fefda6f8b100fdd9595e9ab65e4d85f
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlconfigdriver-function"></a>Função no SQLConfigDriver
**Conformidade**  
 Versão introduzidas: ODBC 2.5  
  
 **Resumo**  
 **No SQLConfigDriver** carrega a DLL de instalação do driver apropriado e chama o **ConfigDriver** função.  
  
 A funcionalidade de **no SQLConfigDriver** também podem ser acessados com [ODBCCONF. EXE](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
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
 [Entrada] Identificador da janela pai. A função não exibirá caixas de diálogo se o identificador é nulo.  
  
 *Frequentes*  
 [Entrada] Tipo de solicitação. *Frequentes* deve conter um dos seguintes valores:  
  
 ODBC_CONFIG_DRIVER: Altera a conexão usada pelo driver de tempo limite de alternância.  
  
 ODBC_INSTALL_DRIVER: Instala um novo driver.  
  
 ODBC_REMOVE_DRIVER: Remove um driver existente.  
  
 Essa opção também pode ser específicos do driver, caso em que o *frequentes* para a primeira opção deve iniciar de ODBC_CONFIG_DRIVER_MAX + 1. O *frequentes* para qualquer opção adicional também deve iniciar de um valor maior do que ODBC_CONFIG_DRIVER_MAX + 1.  
  
 *lpszDriver*  
 [Entrada] O nome do driver como registrado nas informações do sistema.  
  
 *lpszArgs*  
 [Entrada] Uma cadeia de caracteres terminada em nulo que contém os argumentos para um determinado driver *frequentes*.  
  
 *lpszMsg*  
 [Saída] Uma cadeia terminada em nulo que contém uma mensagem de saída da configuração de driver.  
  
 *cbMsgMax*  
 [Entrada] Comprimento de *lpszMsg.*  
  
 *pcbMsgOut*  
 [Saída] Número total de bytes disponíveis para retornar em *lpszMsg*. Se o número de bytes disponíveis para retornar é maior que ou igual a *cbMsgMax*, a mensagem de saída na *lpszMsg* será truncado para *cbMsgMax* menos o encerramento nulo caractere. O *pcbMsgOut* argumento pode ser um ponteiro nulo.  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedida, FALSO se ele falhar.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **no SQLConfigDriver** retorna FALSE, um tipo de  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista o  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral de instalador|Ocorreu um erro para que nenhum erro específico do instalador.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Comprimento de buffer inválido|O *lpszMsg* argumento era inválido.|  
|ODBC_ERROR_INVALID_HWND|Identificador de janela inválido|O *hwndParent* argumento era inválido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitação inválido|O *frequentes* argumento não era um dos seguintes:<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> O *frequentes* argumento era uma opção específica do driver que era menor ou igual a ODBC_CONFIG_DRIVER_MAX.|  
|ODBC_ERROR_INVALID_NAME|Nome de driver ou conversor inválido|O *lpszDriver* argumento era inválido. Ele não pôde ser encontrado no registro.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Pares de valor de palavra-chave inválida|O *lpszArgs* argumento continha um erro de sintaxe.|  
|ODBC_ERROR_REQUEST_FAILED|*Solicitar* falha|O instalador não foi possível executar a operação solicitada pelo *frequentes* argumento. A chamada para **ConfigDriver** falhou.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Não foi possível carregar a biblioteca de instalação de driver ou conversor|Não foi possível carregar a biblioteca de instalação do driver.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não pôde executar a função devido a uma falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **No SQLConfigDriver** permite que um aplicativo chamar um driver **ConfigDriver** rotina sem precisar saber o nome e carregar a DLL de configuração específica do driver. Um programa de instalação chama esta função após a instalação do driver que dll foi instalado. O programa de chamada deve estar ciente de que essa função pode não estar disponível para todos os drivers. Nesse caso, o programa de chamada deve continuar sem erro.  
  
## <a name="driver-specific-options"></a>Opções específicas do driver  
 Um aplicativo pode solicitar recursos específicos do driver expostos pelo driver usando o *frequentes* argumento. O *frequentes* para a primeira opção serão ODBC_CONFIG_DRIVER_MAX + 1, e opções adicionais serão incrementadas em 1 desse valor. Argumentos necessários pelo driver para essa função deve ser fornecida em uma cadeia de caracteres terminada em nulo passado a *lpszArgs* argumento. Drivers fornecendo essa funcionalidade devem manter uma tabela de opções específicas do driver. As opções devem ser documentadas na documentação do driver. Autores de aplicativos que usam opções específicas do driver devem estar cientes de que esse uso fará o aplicativo menos interoperável.  
  
## <a name="setting-connection-pooling-timeout"></a>Tempo limite do pool de Conexão de configuração  
 Propriedades de tempo limite do pool de Conexão pode ser definida quando você definir a configuração do driver. **No SQLConfigDriver** é chamado com um *frequentes* de ODBC_CONFIG_DRIVER e *lpszArgs* definida como **CPTimeout**. **CPTimeout** determina o período de tempo que uma conexão pode permanecer no pool de conexão sem que está sendo usado. Quando o tempo limite expirar, a conexão é fechada e removido do pool. O tempo limite padrão é 60 segundos.  
  
 Quando **no SQLConfigDriver** é chamado com *frequentes* definida como ODBC_INSTALL_DRIVER ou ODBC_REMOVE_DRIVER, o Gerenciador de Driver carrega a DLL de instalação do driver apropriado e chama o  **ConfigDriver** função. Quando **no SQLConfigDriver** é chamado com um *frequentes* de ODBC_CONFIG_DRIVER, todo o processamento é executado no instalador do ODBC, para que a DLL de instalação do driver não precisa ser carregado.  
  
## <a name="messages"></a>Mensagens  
 Uma rotina de instalação do driver pode enviar uma mensagem de texto para um aplicativo como cadeias de caracteres terminada em nulo no *lpszMsg* buffer. A mensagem será truncada para *cbMsgMax* menos o caractere null de terminação pelo **ConfigDriver** função se ele for maior que ou igual a *cbMsgMax* caracteres.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Adicionar, modificar ou remover um driver|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)(na configuração de DLL)|  
|Removendo a fonte de dados padrão|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|

