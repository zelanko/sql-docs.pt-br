---
description: Atualizar um driver 3.5 para um driver 3.8
title: Atualizando um driver 3,5 para um driver 3,8 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ffba36ac-d22e-40b9-911a-973fa9e10bd3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ac140c92b4042df1b4754d3a56237a6aa4b3afaf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461328"
---
# <a name="upgrading-a-35-driver-to-a-38-driver"></a>Atualizar um driver 3.5 para um driver 3.8
Este tópico fornece diretrizes e considerações para atualizar um driver ODBC 3,5 para um driver ODBC 3,8.  
  
##### <a name="version-numbers"></a>Números de versão  
 As diretrizes a seguir estão relacionadas aos números de versão:  
  
-   Um driver deve dar suporte a SQL_OV_ODBC3_80 para SQL_ATTR_ODBC_VERSION, retornando SQL_ERROR para valores diferentes de SQL_OV_ODBC2, SQL_OV_ODBC3 e SQL_OV_ODBC3_80. As versões futuras do Gerenciador de driver assumirão que um driver dá suporte a um nível de conformidade ODBC se o driver retornar SQL_SUCCESS da [função SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md).  
  
-   Um driver da versão 3,8 deve retornar 3,80 de **SQLGetInfo** quando SQL_DRIVER_ODBC_VER for passado para *InfoType*. No entanto, os gerenciadores de driver mais antigos, que foram incluídos em versões mais antigas do Microsoft Windows, tratarão o driver como um driver de versão 3,5 e emitirão um aviso.  
  
     No Windows 7, a versão do Gerenciador de driver é 3,80. No Windows 8, a versão do Gerenciador de driver é 3,81 por meio do SQL_DM_VER SQLGetInfo (parâmetro*InfoType* ). SQL_ODBC_VER relata a versão como 3,80 no Windows 7 e no Windows 8.  
  
##### <a name="driver-specific-c-data-types"></a>Tipos de dados C específicos do driver  
 Um driver pode ter tipos de dados C personalizados quando ele funciona com um aplicativo ODBC da versão 3,8. (Para obter mais informações, consulte [C Data Types in ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).) No entanto, não há nenhum requisito para um driver 3,8 implementar qualquer tipo C específico de driver. Mas o driver ainda deve executar a verificação de intervalo de tipos de C; o Gerenciador de driver não fará isso para drivers de 3,8. Para facilitar o desenvolvimento de driver, o valor do tipo de dados C específico pode ser definido no seguinte formato:  
  
```  
SQL_DRIVER_C_TYPE_BASE+0, SQL_DRIVER_C_TYPE_BASE+1  
```  
  
##### <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>Tipos de dados específicos do driver, tipos de descritores, tipos de informações, tipos de diagnóstico e atributos  
 Ao desenvolver um novo driver, você deve usar o intervalo específico do driver para tipos de dados, tipos de descritores, tipos de informações, tipos de diagnóstico e atributos. Os intervalos específicos de driver e seus valores de tipo base são discutidos em [tipos de dados específicos de driver, tipos de descritores, tipos de informações, tipos de diagnóstico e atributos](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
##### <a name="connection-pooling"></a>Pool de conexões  
 Para um melhor gerenciamento do pool de conexões, o ODBC 3,8 apresenta o atributo de conexão SQL_ATTR_RESET_CONNECTION em **SQLSetConnectAttr**. SQL_RESET_CONNECTION_YES é o único valor válido para este atributo. SQL_ATTR_RESET_CONNECTION será definido logo antes que o Gerenciador de driver Coloque uma conexão no pool de conexões, permitindo que o driver redefina os outros atributos de conexão com seus valores padrão.  
  
 Para evitar a comunicação desnecessária com o servidor, um driver pode adiar a redefinição do atributo de conexão até a próxima comunicação com o servidor remoto, após a conexão ser reutilizada do pool.  
  
 Observe que SQL_ATTR_RESET_CONNECTION é usado somente na comunicação entre o Gerenciador de driver e um driver. Um aplicativo não pode definir esse atributo diretamente. Todos os drivers da versão 3,8 devem implementar esse atributo de conexão.  
  
##### <a name="streamed-output-parameters"></a>Parâmetros de saída em fluxo  
 A versão 3,8 do ODBC apresenta parâmetros de saída em fluxo, uma maneira mais escalonável de recuperar parâmetros de saída. (Para obter mais informações, consulte [recuperando parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).) Para dar suporte a esse recurso, um driver deve definir SQL_GD_OUTPUT_PARAMS no valor de retorno quando SQL_GETDATA_EXTENSIONS é o *InfoType* em uma chamada **SQLGetInfo** . O suporte para um tipo SQL com parâmetros de saída transmitidos deve ser implementado no driver. O Gerenciador de driver não gerará um erro para um tipo SQL inválido. Os tipos SQL que oferecem suporte a parâmetros de saída transmitidos são definidos no driver.  
  
 Um driver deve retornar SQL_ERROR se o aplicativo usou **SQLGetData** para recuperar um parâmetro que não seja o mesmo que o parâmetro retornado por **SQLParamData**.  
  
##### <a name="asynchronous-execution-for-connection-operations-polling-method"></a>Execução assíncrona para operações de conexão (método de sondagem)  
 Um driver pode habilitar o suporte assíncrono para várias operações de conexão.  
  
 A partir do Windows 7, o ODBC dá suporte ao método de sondagem (para obter mais informações, consulte [execução assíncrona (método de sondagem)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md). Não há nenhum requisito para um driver ODBC da versão 3,8 implementar operações assíncronas em identificadores de conexão. Mesmo que um driver não implemente operações assíncronas em identificadores de conexão, o driver ainda deve implementar o SQL_ASYNC_DBC_FUNCTIONS *InfoType* e retornar **SQL_ASYNC_DBC_NOT_CAPABLE**.  
  
 Quando operações de conexão assíncronas são habilitadas, o tempo de execução de uma operação de conexão é o tempo total de todas as chamadas repetidas. Se a última chamada repetida ocorrer depois que o tempo total tiver excedido o valor definido pelo atributo de conexão SQL_ATTR_CONNECTION_TIMEOUT e a operação não tiver sido concluída, o driver retornará SQL_ERROR e registrará um registro de diagnóstico com SQLState HYT01 e a mensagem "tempo limite de conexão expirado". Não haverá tempo limite se a operação tiver sido concluída.  
  
##### <a name="sqlcancelhandle-function"></a>Função SQLCancelHandle  
 O ODBC 3,8 dá suporte à [função SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md), que é usada para cancelar operações de conexão e de instrução. Um driver que dá suporte a **SQLCancelHandle** deve exportar a função. Um driver não deve cancelar nenhuma função de conexão síncrona ou assíncrona que está em andamento se o aplicativo chamar **SQLCancel** ou **SQLCancelHandle** em um identificador de instrução. Da mesma forma, um driver não deve cancelar nenhuma função de instrução síncrona ou assíncrona que esteja em andamento se um aplicativo chamar **SQLCancelHandle** no identificador de conexão. Além disso, um driver não deve cancelar a operação de navegação (**SQLBrowseConnect** retorna SQL_NEED_DATA) se o aplicativo chamar **SQLCancelHandle** no identificador de conexão. Nesses casos, um driver deve retornar HY010, "erro de sequência de função".  
  
 Não é necessário dar suporte a operações de conexão assíncronas e **SQLCancelHandle** ao mesmo tempo. Um driver pode dar suporte A operações de conexão assíncronas, mas não **SQLCancelHandle**, nem vice-versa.  
  
##### <a name="suspended-connections"></a>Conexões suspensas  
 O Gerenciador de driver ODBC 3,8 pode colocar uma conexão no estado suspenso. Um aplicativo chamará **SQLDisconnect** para liberar recursos associados à conexão. Nesse caso, um driver deve tentar liberar o máximo possível de recursos sem verificar o estado da conexão. Para obter mais informações sobre o estado suspenso, consulte a [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).  
  
##### <a name="driver-aware-connection-pooling"></a>Pool de conexões com reconhecimento de driver  
 O ODBC no Windows 8 permite que os drivers personalizem o comportamento do pool de conexões. Para obter mais informações, consulte [pooling de conexão com reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md).  
  
##### <a name="asynchronous-execution-notification-method"></a>Execução assíncrona (método de notificação)  
 O ODBC 3,8 dá suporte ao método de notificação para operações assíncronas, disponíveis a partir do Windows 8. Para obter mais informações, consulte [execução assíncrona (método de notificação)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolvendo um driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Drivers ODBC fornecidos pela Microsoft](../../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)   
 [Novidades no ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
