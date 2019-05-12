---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 20316f2a7932768951633ae24e1b1e180c1dfb49
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537573"
---
# <a name="sqlconfigdriver-function"></a>Função SQLConfigDriver
**Conformidade com**  
 Versão introduzida: ODBC 2.5  
  
 **Resumo**  
 **SQLConfigDriver** carrega a DLL de instalação do driver apropriado e chama o **ConfigDriver** função.  
  
 A funcionalidade do **SQLConfigDriver** também podem ser acessados com [ODBCCONF. EXE](../../../odbc/odbcconf-exe.md).  
  
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
 [Entrada] Identificador de janela pai. A função não exibirá nenhuma caixa de diálogo se o identificador for nulo.  
  
 *fRequest*  
 [Entrada] Tipo de solicitação. *Frequentes* deve conter um dos seguintes valores:  
  
 ODBC_CONFIG_DRIVER: Altera o tempo limite usado pelo driver de pooling de conexão.  
  
 ODBC_INSTALL_DRIVER: Instala um novo driver.  
  
 ODBC_REMOVE_DRIVER: Remove um driver existente.  
  
 Essa opção também pode ser específicos do driver, caso em que o *frequentes* para a primeira opção deve iniciar de ODBC_CONFIG_DRIVER_MAX + 1. O *frequentes* para qualquer opção adicional também deve iniciar de um valor maior que ODBC_CONFIG_DRIVER_MAX + 1.  
  
 *lpszDriver*  
 [Entrada] O nome do driver como registrado nas informações do sistema.  
  
 *lpszArgs*  
 [Entrada] Uma cadeia de caracteres terminada em nulo que contém os argumentos para um determinado de driver *frequentes*.  
  
 *lpszMsg*  
 [Saída] Uma cadeia terminada em nulo que contém uma mensagem de saída da configuração do driver.  
  
 *cbMsgMax*  
 [Entrada] Comprimento de *lpszMsg.*  
  
 *pcbMsgOut*  
 [Saída] Número total de bytes disponíveis para retornar na *lpszMsg*. Se o número de bytes disponíveis para retornar for maior que ou igual a *cbMsgMax*, a mensagem de saída na *lpszMsg* será truncado com *cbMsgMax* menos a terminação null caractere. O *pcbMsgOut* argumento pode ser um ponteiro nulo.  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedida, FALSO se ele falhar.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLConfigDriver** retornar FALSE, um associado  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista os  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral de instalador|Ocorreu um erro para que nenhum erro específico do instalador.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Comprimento de buffer inválido|O *lpszMsg* argumento era inválido.|  
|ODBC_ERROR_INVALID_HWND|Identificador de janela inválido|O *hwndParent* argumento era inválido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitação inválido|O *frequentes* argumento não era um dos seguintes:<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> O *frequentes* argumento era uma opção específica do driver que era menor ou igual a ODBC_CONFIG_DRIVER_MAX.|  
|ODBC_ERROR_INVALID_NAME|Nome inválido de driver ou conversor|O *lpszDriver* argumento era inválido. Ele não pôde ser encontrado no registro.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Pares de valor de palavra-chave inválido|O *lpszArgs* argumento continha um erro de sintaxe.|  
|ODBC_ERROR_REQUEST_FAILED|*Solicitar* falhou|O instalador não foi possível executar a operação solicitada pelo *frequentes* argumento. A chamada para **ConfigDriver** falhou.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Não foi possível carregar a biblioteca de instalação do driver ou conversor|Não foi possível carregar a biblioteca de instalação do driver.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não foi possível executar a função devido à falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **SQLConfigDriver** permite que um aplicativo chamar um driver **ConfigDriver** rotina sem precisar saber o nome e carregar a DLL de instalação específicas do driver. Um programa de instalação chama essa função após a instalação do driver que dll foi instalado. O programa de chamada deve estar ciente de que essa função pode não estar disponível para todos os drivers. Nesse caso, o programa de chamada deve continuar sem erro.  
  
## <a name="driver-specific-options"></a>Opções específicas do driver  
 Um aplicativo pode solicitar recursos específicos do driver expostos pelo driver usando o *frequentes* argumento. O *frequentes* para a primeira opção serão ODBC_CONFIG_DRIVER_MAX + 1, e as opções adicionais serão incrementadas em 1 desse valor. Quaisquer argumentos exigidos pelo driver para essa função deve ser fornecida em uma cadeia de caracteres terminada em nulo passado a *lpszArgs* argumento. Drivers de fornecer tal funcionalidade devem manter uma tabela de opções específicas do driver. As opções devem ser totalmente documentadas na documentação do driver. Os autores de aplicativos que usam as opções específicas do driver devem estar cientes de que esse uso tornará o aplicativo menos interoperável.  
  
## <a name="setting-connection-pooling-timeout"></a>Tempo limite do pool de Conexão de configuração  
 Propriedades de tempo limite de pool de Conexão pode ser definida quando você definir a configuração do driver. **SQLConfigDriver** é chamado com um *frequentes* de ODBC_CONFIG_DRIVER e *lpszArgs* definido como **CPTimeout**. **CPTimeout** determina o período de tempo que uma conexão pode permanecer no pool de conexão sem que está sendo usado. Quando o tempo limite expira, a conexão é fechada e removido do pool. O tempo limite padrão é 60 segundos.  
  
 Quando **SQLConfigDriver** for chamado com *frequentes* definido como ODBC_INSTALL_DRIVER ou ODBC_REMOVE_DRIVER, o Gerenciador de Driver carrega a DLL de instalação do driver apropriado e chama o  **ConfigDriver** função. Quando **SQLConfigDriver** for chamado com um *frequentes* de ODBC_CONFIG_DRIVER, todo o processamento é executado no instalador do ODBC, para que a DLL de instalação do driver não precisa ser carregado.  
  
## <a name="messages"></a>Mensagens  
 Uma rotina de instalação do driver pode enviar uma mensagem de texto para um aplicativo como cadeias de caracteres terminada em nulo na *lpszMsg* buffer. A mensagem será truncada para *cbMsgMax* menos o caractere nulo de terminação, o **ConfigDriver** funcionará se ele é maior que ou igual a *cbMsgMax* caracteres.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Adicionar, modificar ou remover um driver|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)(na configuração de DLL)|  
|Removendo a fonte de dados padrão|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|
