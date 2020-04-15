---
title: Atualizando um driver 3.5 para um driver 3.8 | Microsoft Docs
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
ms.openlocfilehash: dcd01d050e806b733d75c54058945d367a33d6a7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294427"
---
# <a name="upgrading-a-35-driver-to-a-38-driver"></a>Atualizar um driver 3.5 para um driver 3.8
Este tópico fornece diretrizes e considerações para atualizar um driver ODBC 3.5 para um driver ODBC 3.8.  
  
##### <a name="version-numbers"></a>Números de versão  
 As seguintes diretrizes referem-se aos números das versões:  
  
-   O motorista deve apoiar SQL_OV_ODBC3_80 para SQL_ATTR_ODBC_VERSION, retornando SQL_ERROR por valores diferentes SQL_OV_ODBC2, SQL_OV_ODBC3 e SQL_OV_ODBC3_80. As versões futuras do Driver Manager assumirão que um driver suporta um nível de conformidade ODBC se o driver retornar SQL_SUCCESS da [função SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md).  
  
-   Um driver versão 3.8 deve retornar 03.80 do **SQLGetInfo** quando SQL_DRIVER_ODBC_VER for passado para *infoType*. No entanto, os driver managers mais antigos, que foram incluídos em versões mais antigas do Microsoft Windows, tratarão o driver como um driver versão 3.5 e emitirão um aviso.  
  
     No Windows 7, a versão driver manager é 03.80. No Windows 8, a versão driver manager é 03.81 através do sqlgetinfo SQL_DM_VER ( parâmetro*InfoType).* SQL_ODBC_VER relata a versão como 03.80 tanto no Windows 7 quanto no Windows 8.  
  
##### <a name="driver-specific-c-data-types"></a>Tipos de dados C específicos para o driver  
 Um driver pode ter tipos de dados C personalizados quando trabalha com um aplicativo ODBC versão 3.8. (Para obter mais informações, consulte [C Data Types in ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).) No entanto, não há necessidade de um driver 3.8 implementar qualquer tipo C específico do driver. Mas o motorista ainda deve realizar a verificação de faixa dos tipos C; o Driver Manager não fará isso para 3,8 motoristas. Para facilitar o desenvolvimento do driver, o valor do tipo de dados C específico do driver pode ser definido no seguinte formato:  
  
```  
SQL_DRIVER_C_TYPE_BASE+0, SQL_DRIVER_C_TYPE_BASE+1  
```  
  
##### <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>Tipos de dados específicos do driver, tipos de descritores, tipos de informações, tipos de diagnóstico e atributos  
 Ao desenvolver um novo driver, você deve usar a faixa específica do driver para tipos de dados, tipos de descritores, tipos de informações, tipos de diagnóstico e atributos. As faixas específicas do driver e seus valores de tipo base são discutidos em [tipos de dados específicos do driver, tipos de descritores, tipos de informações, tipos de diagnóstico e atributos](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
##### <a name="connection-pooling"></a>Pool de conexões  
 Para um melhor gerenciamento do pool de conexões, o ODBC 3.8 introduz o atributo de conexão SQL_ATTR_RESET_CONNECTION no **SQLSetConnectAttr**. SQL_RESET_CONNECTION_YES é o único valor válido para este atributo. SQL_ATTR_RESET_CONNECTION serão definidos pouco antes de o Driver Manager colocar uma conexão no pool de conexões, permitindo que o motorista redefinisse os outros atributos de conexão aos seus valores padrão.  
  
 Para evitar uma comunicação desnecessária com o servidor, o driver pode adiar o atributo de conexão redefinido até a próxima comunicação com o servidor remoto, depois que a conexão for reutilizada do pool.  
  
 Observe que SQL_ATTR_RESET_CONNECTION só é usado na comunicação entre o Driver Manager e um motorista. Um aplicativo não pode definir esse atributo diretamente. Todos os drivers da versão 3.8 devem implementar este atributo de conexão.  
  
##### <a name="streamed-output-parameters"></a>Parâmetros de saída em fluxo  
 A versão 3.8 do ODBC introduz parâmetros de saída em fluxo, uma maneira mais escalável de recuperar parâmetros de saída. (Para obter mais informações, consulte [Recuperando parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).) Para suportar esse recurso, um driver deve definir SQL_GD_OUTPUT_PARAMS no valor de retorno quando SQL_GETDATA_EXTENSIONS é o *InfoType* em uma chamada **SQLGetInfo.** O suporte para um tipo SQL com parâmetros de saída streamed deve ser implementado no driver. O Gerenciador de driver não gerará um erro para um tipo SQL inválido. Os tipos SQL que suportam parâmetros de saída em fluxo são definidos no driver.  
  
 Um driver deve retornar SQL_ERROR se o aplicativo usou **SQLGetData** para recuperar um parâmetro que não seja o mesmo que o parâmetro retornado pelo **SQLParamData**.  
  
##### <a name="asynchronous-execution-for-connection-operations-polling-method"></a>Execução assíncrona para operações de conexão (método de votação)  
 Um driver pode habilitar suporte assíncrono para várias operações de conexão.  
  
 A partir do Windows 7, o ODBC suporta o método de votação (para obter mais informações, consulte [Execução Assíncrona (Método de Votação)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md). Não há necessidade de um driver ODBC versão 3.8 implementar operações assíncronas nas alças de conexão. Mesmo que um driver não implemente operações assíncronas nas alças de conexão, o motorista ainda deve implementar o *infoType* SQL_ASYNC_DBC_FUNCTIONS e retornar **SQL_ASYNC_DBC_NOT_CAPABLE**.  
  
 Quando as operações de conexão assíncronas são habilitadas, o tempo de execução de uma operação de conexão é o tempo total de todas as chamadas repetidas. Se a última chamada repetida ocorrer após o tempo total ter excedido o valor definido pelo atributo de conexão SQL_ATTR_CONNECTION_TIMEOUT e a operação não tiver terminado, o driver retorna SQL_ERROR e registra um registro de diagnóstico com o SQLState HYT01 e a mensagem "Tempo de conexão expirado". Não há tempo nem um para o final da operação.  
  
##### <a name="sqlcancelhandle-function"></a>Função SQLCancelHandle  
 O ODBC 3.8 suporta [a função SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md), que é usada para cancelar operações de conexão e declaração. Um driver que suporta **SQLCancelHandle** deve exportar a função. Um driver não deve cancelar nenhuma função de conexão síncrona ou assíncrona que esteja em andamento se o aplicativo chamar **SQLCancel** ou **SQLCancelHandle** em uma alça de declaração. Da mesma forma, um driver não deve cancelar qualquer função de declaração síncrona ou assíncrona que esteja em andamento se um aplicativo chamar **SQLCancelHandle** na alça de conexão. Além disso, um driver não deve cancelar a operação de navegação **(O SQLBrowseConnect** retorna SQL_NEED_DATA) se o aplicativo chamar **SQLCancelHandle** na alça de conexão. Nestes casos, um driver deve retornar HY010, "erro de seqüência de função".  
  
 Não é necessário suportar tanto as operações **de conexão SQLCancelHandle** quanto assíncronas ao mesmo tempo. Um driver pode suportar operações de conexão assíncronas, mas não **SQLCancelHandle,** ou vice-versa.  
  
##### <a name="suspended-connections"></a>Conexões suspensas  
 O Gerenciador de Driver ODBC 3.8 pode colocar uma conexão em estado suspenso. Um aplicativo chamará **o SQLDisconnect** para liberar recursos associados à conexão. Neste caso, um motorista deve tentar liberar o máximo de recursos possível sem verificar o estado da conexão. Para obter mais informações sobre o estado suspenso, consulte [SQLEndTran Function](../../../odbc/reference/syntax/sqlendtran-function.md).  
  
##### <a name="driver-aware-connection-pooling"></a>Pool de conexões com reconhecimento de driver  
 O ODBC no Windows 8 permite que os drivers personalizem o comportamento do pool de conexões. Para obter mais informações, consulte [Pooling de conexão com reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md).  
  
##### <a name="asynchronous-execution-notification-method"></a>Execução assíncrona (método de notificação)  
 O ODBC 3.8 suporta o método de notificação para operações assíncronas, disponível a partir do Windows 8. Para obter mais informações, consulte [Execução Assíncrona (Método de Notificação)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolvendo um Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Drivers ODBC fornecidos pela Microsoft](../../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)   
 [Novidades no ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
