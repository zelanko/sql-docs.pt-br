---
title: Atualizando um Driver 3.5 para um Driver 3.8 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ffba36ac-d22e-40b9-911a-973fa9e10bd3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 97b100b1ade97e1e88cf1421f09a7723412c8b76
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915494"
---
# <a name="upgrading-a-35-driver-to-a-38-driver"></a>Atualizar um driver 3.5 para um driver 3.8
Este tópico fornece diretrizes e considerações para atualizar um driver de ODBC 3.5 a um driver ODBC 3.8.  
  
##### <a name="version-numbers"></a>Números de versão  
 As diretrizes a seguir se relacionam com números de versão:  
  
-   Um driver deve dar suporte a SQL_OV_ODBC3_80 para SQL_ATTR_ODBC_VERSION, retornando valores diferentes de SQL_OV_ODBC2, SQL_OV_ODBC3 e SQL_OV_ODBC3_80 SQL_ERROR. Versões futuras do Gerenciador de Driver suporá que um driver dá suporte a um nível de compatibilidade do ODBC, se o driver retornará SQL_SUCCESS do [função SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md).  
  
-   Um driver de versão 3.8 deve retornar 03.80 da **SQLGetInfo** quando SQL_DRIVER_ODBC_VER é passado para *tipo de informação*. No entanto, gerentes de Driver mais antigos, que foram incluídos em versões anteriores do Microsoft Windows, tratará o driver como um driver de versão 3.5 e emitirá um aviso.  
  
     No Windows 7, a versão do Gerenciador de Driver é 03.80. No Windows 8, a versão do Gerenciador de Driver é 03.81 via o SQL_DM_VER SQLGetInfo (*tipo de informação* parâmetro). SQL_ODBC_VER informa a versão como 03.80 no Windows 7 e Windows 8.  
  
##### <a name="driver-specific-c-data-types"></a>Tipos de dados C específicos do driver  
 Um driver pode personalizou os tipos de dados C quando trabalha com um aplicativo de ODBC versão 3.8. (Para obter mais informações, consulte [tipos de dados C em ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).) No entanto, não há nenhum requisito para um driver 3.8 implementar quaisquer tipos de C específicos do driver. Mas o driver ainda deve realizar a verificação de intervalo de tipos C; o Gerenciador de Driver não fará isso para 3.8 drivers. Para facilitar o desenvolvimento de driver, o valor do tipo de dados do C específico, driver pode ser definido no seguinte formato:  
  
```  
SQL_DRIVER_C_TYPE_BASE+0, SQL_DRIVER_C_TYPE_BASE+1  
```  
  
##### <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>Tipos de dados específicos do driver, tipos de descritor, tipos de informação, tipos de diagnóstico e atributos  
 Ao desenvolver um novo driver, você deve usar o intervalo de específicos de driver para tipos de dados, tipos de descritor, tipos de informação, tipos de diagnóstico e atributos. Intervalos específicos de driver e seus valores de tipo de base são discutidos [tipos de dados específicos do Driver, tipos de descritor, tipos de informação, tipos de diagnóstico e atributos](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
##### <a name="connection-pooling"></a>Pool de conexões  
 Para um melhor gerenciamento de pool de conexão, o ODBC 3.8 apresenta o atributo de conexão SQL_ATTR_RESET_CONNECTION na **SQLSetConnectAttr**. SQL_RESET_CONNECTION_YES é o único valor válido para este atributo. SQL_ATTR_RESET_CONNECTION será definido apenas antes que o Gerenciador de Driver coloca uma conexão no pool de conexão, permitindo que o driver redefinir os outros atributos de conexão para seus valores padrão.  
  
 Para evitar a comunicação desnecessária com o servidor, um driver pode adiar o atributo de conexão de redefinição até a próxima comunicação com o servidor remoto, depois que a conexão for reutilizada do pool.  
  
 Observe que SQL_ATTR_RESET_CONNECTION só é usado na comunicação entre o Gerenciador de Driver e um driver. Um aplicativo não é possível definir esse atributo diretamente. Todos os drivers de versão 3.8 devem implementar esse atributo de conexão.  
  
##### <a name="streamed-output-parameters"></a>Parâmetros de saída em fluxo  
 ODBC versão 3.8 apresenta os parâmetros de saída em fluxo, uma maneira mais escalonável para recuperar parâmetros de saída. (Para obter mais informações, consulte [Recuperando parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).) Para dar suporte a esse recurso, um driver deve definir SQL_GD_OUTPUT_PARAMS no valor de retorno quando SQL_GETDATA_EXTENSIONS é o *tipo de informação* em um **SQLGetInfo** chamar. Suporte para um tipo SQL com parâmetros de saída em fluxo deve ser implementado no driver. O Gerenciador de Driver não gerará um erro para um tipo SQL inválido. Os tipos de SQL que dão suporte a parâmetros de saída em fluxo é definido no driver.  
  
 Um driver deve retornar SQL_ERROR se o aplicativo usado **SQLGetData** para recuperar um parâmetro que não seja o mesmo que o parâmetro retornado por **SQLParamData**.  
  
##### <a name="asynchronous-execution-for-connection-operations-polling-method"></a>Execução assíncrona para operações de Conexão (método de sondagem)  
 Um driver pode habilitar o suporte assíncrono para várias operações de conexão.  
  
 A partir do Windows 7, o ODBC suporta o método de sondagem (para obter mais informações, consulte [execução assíncrona (método de sondagem)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md). Não há nenhum requisito para um driver ODBC versão 3.8 implementar operações assíncronas em identificadores de conexão. Mesmo se um driver não implementa operações assíncronas em identificadores de conexão, o driver ainda deve implementar o SQL_ASYNC_DBC_FUNCTIONS *tipo de informação* e retornar **SQL_ASYNC_DBC_NOT_CAPABLE**.  
  
 Quando as operações de conexão assíncrona estão habilitadas, o tempo de execução de uma operação de conexão é o tempo total de todas as chamadas repetidas. Se a última repetir a chamada ocorre depois que o tempo total excedeu o valor definido pelo atributo de conexão de SQL_ATTR_CONNECTION_TIMEOUT, e a operação não foi concluída, o driver retornará SQL_ERROR e registra um registro de diagnóstico com SQLState HYT01 e o mensagem de "tempo limite de Conexão expirado". Não há nenhum tempo limite se a operação foi concluída.  
  
##### <a name="sqlcancelhandle-function"></a>Função SQLCancelHandle  
 Dá suporte a ODBC 3.8 [função SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md), que é usado para cancelar as operações de conexão e instrução. Um driver que suporta **SQLCancelHandle** deve exportar a função. Um driver não deve cancelar a qualquer função de conexão síncrona ou assíncrona está em andamento se o aplicativo chamar **SQLCancel** ou **SQLCancelHandle** em um identificador de instrução. Da mesma forma, um driver não deve cancelar a qualquer função de instrução síncrona ou assíncrona está em andamento, se um aplicativo chamar **SQLCancelHandle** o identificador de conexão. Além disso, um driver não deve cancelar a operação de navegação (**SQLBrowseConnect** retorna SQL_NEED_DATA) se o aplicativo chama **SQLCancelHandle** o identificador de conexão. Nesses casos, um driver deve retornar HY010, "Erro de sequência de função".  
  
 Não é necessário dar suporte a ambos **SQLCancelHandle** e operações de conexão assíncrona ao mesmo tempo. Um driver pode dar suporte a operações assíncronas de conexão, mas não **SQLCancelHandle**, ou vice-versa.  
  
##### <a name="suspended-connections"></a>Conexões suspensas  
 O Gerenciador de Driver do ODBC 3.8 pode colocar uma conexão em estado suspenso. Um aplicativo chamará **SQLDisconnect** para liberar os recursos associados com a conexão. Nesse caso, um driver deve tentar liberar o máximo de recursos possível sem verificar o estado da conexão. Para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).  
  
##### <a name="driver-aware-connection-pooling"></a>Pool de conexões com reconhecimento de driver  
 ODBC no Windows 8 permite que os drivers personalizar o comportamento do pool de conexão. Para obter mais informações, consulte [Pooling de Conexão de reconhecimento de Driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md).  
  
##### <a name="asynchronous-execution-notification-method"></a>Execução assíncrona (método de notificação)  
 O ODBC 3.8 suporta o método de notificação para operações assíncronas, disponíveis a partir no Windows 8. Para obter mais informações, consulte [execução assíncrona (método de notificação)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md).  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolvendo um Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Drivers ODBC fornecidos pela Microsoft](../../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)   
 [Novidades no ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
