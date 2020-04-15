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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0da15cef06e5d8392408108ce88b53f7885eb65e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301241"
---
# <a name="sqlconfigdriver-function"></a>Função SQLConfigDriver
**Conformidade**  
 Versão introduzida: ODBC 2.5  
  
 **Resumo**  
 **O SQLConfigDriver** carrega a DLL de configuração de driver apropriada e chama a função **ConfigDriver.**  
  
 A funcionalidade do **SQLConfigDriver** também pode ser acessada com [ODBCCONF. EXE](../../../odbc/odbcconf-exe.md).  
  
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
 *Hwndparent*  
 [Entrada] Alça da janela dos pais. A função não exibirá nenhuma caixa de diálogo se a alça estiver nula.  
  
 *fSolicitar*  
 [Entrada] Tipo de pedido. *fSolicite* conter um dos seguintes valores:  
  
 ODBC_CONFIG_DRIVER: Altera o tempo de intervalo de conexão usado pelo motorista.  
  
 ODBC_INSTALL_DRIVER: Instala um novo driver.  
  
 ODBC_REMOVE_DRIVER: Remove um driver existente.  
  
 Esta opção também pode ser específica do driver, nesse caso o *fRequest* para a primeira opção deve começar a partir de ODBC_CONFIG_DRIVER_MAX+1. O *fRequest* para qualquer opção adicional também deve partir de um valor maior que ODBC_CONFIG_DRIVER_MAX+1.  
  
 *Lpszdriver*  
 [Entrada] O nome do motorista registrado nas informações do sistema.  
  
 *lpszArgs*  
 [Entrada] Uma seqüência de terminadas nula que contém argumentos para um *fRequest*específico do driver .  
  
 *lpszMsg*  
 [Saída] Uma seqüência de caracteres com término nulo que contém uma mensagem de saída da configuração do driver.  
  
 *cbMsgMax*  
 [Entrada] Comprimento de *lpszMsg.*  
  
 *pcbMsgOut*  
 [Saída] Número total de bytes disponíveis para retornar em *lpszMsg*. Se o número de bytes disponíveis para retornar for maior ou igual ao *cbMsgMax,* a mensagem de saída em *lpszMsg* é truncada para *cbMsgMax* menos o caractere de rescisão nula. O *argumento pcbMsgOut* pode ser um ponteiro nulo.  
  
## <a name="returns"></a>Retornos  
 A função retorna TRUE se for bem sucedida, FALSA se falhar.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLConfigDriver** retorna FALSE, um valor * \*pfErrorCode* associado pode ser obtido ligando para **SQLInstallerError**. A tabela a * \** seguir lista os valores pfErrorCode que podem ser retornados pelo **SQLInstallerError** e explica cada um no contexto desta função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro do instalador geral|Ocorreu um erro para o qual não houve erro específico do instalador.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Comprimento de buffer inválido|O argumento *lpszMsg* era inválido.|  
|ODBC_ERROR_INVALID_HWND|Alça de janela inválida|O argumento *hwndParent* era inválido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitação inválida|O argumento *fRequest* não foi um dos seguintes:<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> O *argumento fRequest* era uma opção específica do driver que era menor ou igual a ODBC_CONFIG_DRIVER_MAX.|  
|ODBC_ERROR_INVALID_NAME|Nome de motorista ou tradutor inválido|O argumento *lpszDriver* era inválido. Não foi possível encontrar no registro.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Pares de valores de palavras-chave inválidos|O argumento *lpszArgs* continha um erro de sintaxe.|  
|ODBC_ERROR_REQUEST_FAILED|*Falha na solicitação*|O instalador não pôde realizar a operação solicitada pelo argumento *fRequest.* A chamada para **ConfigDriver** falhou.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Não foi possível carregar a biblioteca de configuração do driver ou tradutor|A biblioteca de configuração do driver não pôde ser carregada.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não conseguiu executar a função por falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **O SQLConfigDriver** permite que um aplicativo chame a rotina de **ConfigDriver** de um driver sem ter que saber o nome e carregar a configuração específica do driver DLL. Um programa de configuração chama essa função depois que a DLL de configuração do driver foi instalada. O programa de chamada deve estar ciente de que esta função pode não estar disponível para todos os drivers. Nesse caso, o programa de chamada deve continuar sem erro.  
  
## <a name="driver-specific-options"></a>Opções específicas do driver  
 Um aplicativo pode solicitar recursos específicos do driver expostos pelo motorista usando o argumento *fRequest.* O *fRequest* para a primeira opção será ODBC_CONFIG_DRIVER_MAX+1, e as opções adicionais serão incrementadas por 1 a partir desse valor. Quaisquer argumentos exigidos pelo driver para essa função devem ser fornecidos em uma seqüência de terminação nula aprovada no argumento *lpszArgs.* Os drivers que fornecem essa funcionalidade devem manter uma tabela de opções específicas para o motorista. As opções devem estar totalmente documentadas na documentação do motorista. Os escritores de aplicativos que usam opções específicas para o motorista devem estar cientes de que esse uso tornará o aplicativo menos interoperável.  
  
## <a name="setting-connection-pooling-timeout"></a>Definindo o tempo de agrupamento de conexões  
 As propriedades de tempo de tempo de pool de conexão podem ser definidas quando você define a configuração do driver. **SQLConfigDriver** é chamado com um *fRequest* of ODBC_CONFIG_DRIVER e *lpszArgs* definido como **CPTimeout**. **O CPTimeout** determina o período de tempo que uma conexão pode permanecer no pool de conexões sem ser usada. Quando o intervalo expirar, a conexão é fechada e removida da piscina. O tempo de intervalo padrão é de 60 segundos.  
  
 Quando **o SQLConfigDriver** é chamado com *fRequest* definido para ODBC_INSTALL_DRIVER ou ODBC_REMOVE_DRIVER, o Driver Manager carrega a configuração apropriada do driver DLL e chama a função **ConfigDriver.** Quando **o SQLConfigDriver** é chamado com um *fRequest* of ODBC_CONFIG_DRIVER, todo o processamento é realizado no instalador ODBC, de modo que a configuração do driver DLL não precise ser carregada.  
  
## <a name="messages"></a>Mensagens  
 Uma rotina de configuração do driver pode enviar uma mensagem de texto para um aplicativo como strings com término nulo no buffer *lpszMsg.* A mensagem será truncada para *cbMsgMax* menos o caractere de rescisão nula pela função **ConfigDriver** se for maior ou igual aos *caracteres cbMsgMax.*  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Adicionando, modificando ou removendo um driver|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)(na configuração DLL)|  
|Removendo a fonte de dados padrão|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|
