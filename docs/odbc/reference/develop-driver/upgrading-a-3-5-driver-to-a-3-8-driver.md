---
title: Atualizar um Driver 3.5 para um Driver 3.8 | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ffba36ac-d22e-40b9-911a-973fa9e10bd3
caps.latest.revision: "27"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6772088bfbb33590f7986ee65550f64d5845cc69
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="upgrading-a-35-driver-to-a-38-driver"></a>Atualizar um Driver 3.5 para um Driver 3.8
Este tópico fornece diretrizes e considerações de atualização de um driver de ODBC 3.5 para um driver de ODBC 3.8.  
  
##### <a name="version-numbers"></a>Números de versão  
 As diretrizes a seguir se relacionam com números de versão:  
  
-   Um driver deve oferecer suporte a SQL_OV_ODBC3_80 para SQL_ATTR_ODBC_VERSION, retornando valores diferentes de SQL_OV_ODBC2, SQL_OV_ODBC3 e SQL_OV_ODBC3_80 SQL_ERROR. Versões futuras do Gerenciador de Driver pressupõem que um driver dá suporte a um nível de compatibilidade do ODBC, se o driver retornará SQL_SUCCESS de [função SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md).  
  
-   Um versão 3.8 do driver deve retornar 03.80 de **SQLGetInfo** quando SQL_DRIVER_ODBC_VER é passado para *informação*. No entanto, gerenciadores de Driver mais antigos, que foram incluídos em versões anteriores do Microsoft Windows, tratará o driver como um driver de versão 3.5 e emitirá um aviso.  
  
     No Windows 7, a versão do Gerenciador de Driver é 03.80. No Windows 8, a versão do Gerenciador de Driver é 03.81 por meio de SQL_DM_VER SQLGetInfo (*informação* parâmetro). SQL_ODBC_VER informa a versão como 03.80 no Windows 7 e Windows 8.  
  
##### <a name="driver-specific-c-data-types"></a>Tipos de dados C específicos do driver  
 Um driver pode a tipos de dados C personalizada quando ele funciona com um aplicativo de ODBC versão 3.8. (Para obter mais informações, consulte [tipos de dados C em ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).) No entanto, não há nenhum requisito para um driver 3.8 implementar qualquer tipo de C específicos do driver. Mas o driver ainda deve executar a verificação de intervalo de tipos C; o Gerenciador de Driver não fará isso para 3.8 drivers. Para facilitar o desenvolvimento de driver, o valor do tipo de dados de C específico, driver pode ser definido no seguinte formato:  
  
```  
SQL_DRIVER_C_TYPE_BASE+0, SQL_DRIVER_C_TYPE_BASE+1  
```  
  
##### <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>Tipos de dados específica do driver, tipos de descritor, tipos de informação, tipos de diagnóstico e atributos  
 Ao desenvolver um novo driver, você deve usar o intervalo de específicos de driver para tipos de dados, tipos de descritor, tipos de informação, tipos de diagnóstico e atributos. Intervalos específicos de driver e seus valores de tipo de base são discutidos em [tipos de dados específicos do Driver, tipos de descritor, tipos de informações, tipos de diagnóstico e atributos](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
##### <a name="connection-pooling"></a>Pool de conexões  
 Para um melhor gerenciamento de pool de conexão, o ODBC 3.8 apresenta o atributo de conexão SQL_ATTR_RESET_CONNECTION na **SQLSetConnectAttr**. SQL_RESET_CONNECTION_YES é o único valor válido para este atributo. SQL_ATTR_RESET_CONNECTION será definida antes que o Gerenciador de Driver coloca uma conexão no pool de conexão, permitindo que o driver redefinir os outros atributos de conexão para seus valores padrão.  
  
 Para evitar a comunicação desnecessária com o servidor, um driver pode adiar o atributo de conexão redefinir até a próxima comunicação com o servidor remoto, depois que a conexão for reutilizada a partir do pool.  
  
 Observe que SQL_ATTR_RESET_CONNECTION só é usado na comunicação entre o Gerenciador de Driver e um driver. Um aplicativo não é possível definir esse atributo diretamente. Todos os drivers de versão 3.8 devem implementar esse atributo de conexão.  
  
##### <a name="streamed-output-parameters"></a>Parâmetros de saída em fluxo  
 O ODBC versão 3.8 apresenta parâmetros de saída em fluxo, uma maneira mais escalonável para recuperar os parâmetros de saída. (Para obter mais informações, consulte [recuperar parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).) Para dar suporte a esse recurso, um driver deve definir SQL_GD_OUTPUT_PARAMS no valor de retorno quando está SQL_GETDATA_EXTENSIONS o *informação* em uma **SQLGetInfo** chamar. Suporte para um tipo de SQL com parâmetros de saída em fluxo deve ser implementado no driver. O Gerenciador de Driver não irá gerar um erro para um tipo SQL inválido. Os tipos de SQL que oferecem suporte a parâmetros de saída em fluxo é definido no driver.  
  
 Um driver deve retornar SQL_ERROR se o aplicativo usado **SQLGetData** para recuperar um parâmetro que não seja o mesmo que o parâmetro retornado por **SQLParamData**.  
  
##### <a name="asynchronous-execution-for-connection-operations-polling-method"></a>Execução assíncrona para operações de Conexão (método de pesquisa)  
 Um driver pode habilitar o suporte assíncrono para várias operações de conexão.  
  
 Começando no Windows 7, o ODBC suporta o método de sondagem (para obter mais informações, consulte [execução assíncrona (método de sondagem)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md). Não há nenhum requisito para um driver ODBC versão 3.8 implementar operações assíncronas em identificadores de conexão. Mesmo se um driver não implementa operações assíncronas em identificadores de conexão, o driver ainda deve implementar a SQL_ASYNC_DBC_FUNCTIONS *informação* e retornar **SQL_ASYNC_DBC_NOT_CAPABLE**.  
  
 Quando as operações de conexão assíncrona estão habilitadas, o tempo de execução de uma operação de conexão é o tempo total de todas as chamadas repetidas. Se a última repetir a chamada ocorre depois que o tempo total excedeu o valor definido pelo atributo de conexão SQL_ATTR_CONNECTION_TIMEOUT, e a operação não foi concluída, o driver retornará SQL_ERROR e registra um registro de diagnóstico com SQLState HYT01 e o mensagem de "tempo limite de Conexão expirou". Não há nenhum tempo limite se a operação concluída.  
  
##### <a name="sqlcancelhandle-function"></a>Função SQLCancelHandle  
 Oferece suporte a ODBC 3.8 [SQLCancelHandle função](../../../odbc/reference/syntax/sqlcancelhandle-function.md), que é usado para cancelar operações de conexão e instrução. Um driver que suporta **SQLCancelHandle** deve exportar a função. Um driver não deverá cancelar qualquer função de conexão síncrona ou assíncrona está em andamento, se o aplicativo chama **SQLCancel** ou **SQLCancelHandle** em um identificador de instrução. Da mesma forma, um driver não deverá cancelar qualquer função de instrução síncrona ou assíncrona está em andamento, se um aplicativo chamar **SQLCancelHandle** no identificador da conexão. Além disso, um driver não deve cancelar a operação de busca (**SQLBrowseConnect** retorna SQL_NEED_DATA) se o aplicativo chama **SQLCancelHandle** no identificador da conexão. Nesses casos, um driver deve retornar HY010, "Erro de sequência de função".  
  
 Não é necessário dar suporte a ambos **SQLCancelHandle** e operações assíncronas de conexão ao mesmo tempo. Um driver pode dar suporte a operações assíncronas de conexão, mas não **SQLCancelHandle**, ou vice-versa.  
  
##### <a name="suspended-connections"></a>Conexões suspensos  
 O Gerenciador de Driver do ODBC 3.8 pode colocar uma conexão em estado suspenso. Um aplicativo chamará **SQLDisconnect** para liberar os recursos associados com a conexão. Nesse caso, um driver deve tentar liberar quantos recursos possível sem verificar o estado da conexão. Para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).  
  
##### <a name="driver-aware-connection-pooling"></a>Pool de conexões com reconhecimento de driver  
 O ODBC no Windows 8 permite que os drivers personalizar o comportamento do pool de conexão. Para obter mais informações, consulte [Pooling de Conexão com reconhecimento de Driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md).  
  
##### <a name="asynchronous-execution-notification-method"></a>Execução assíncrona (método de notificação)  
 ODBC 3.8 suporta o método de notificação para operações assíncronas, disponíveis começando no Windows 8. Para obter mais informações, consulte [execução assíncrona (método de notificação)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolvendo um Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Drivers ODBC fornecidos pela Microsoft](../../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)   
 [Novidades no ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
