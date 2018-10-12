---
title: Metadados de instrução em cache preparados para o JDBC Driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3c412a4364e18a70cf10d9896138c5056318ae20
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47767330"
---
# <a name="prepared-statement-metadata-caching-for-the-jdbc-driver"></a>Metadados de instrução em cache preparados para o JDBC Driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Este artigo fornece informações sobre as duas alterações que são implementadas para aprimorar o desempenho do driver.

## <a name="batching-of-unprepare-for-prepared-statements"></a>Processamento em lotes de Unprepare para instruções preparadas
Uma vez que a versão 6.1.6-preview, uma melhoria no desempenho foi implementado através da redução do servidor idas e vindas ao SQL Server. Anteriormente, cada consulta prepareStatement, uma chamada para unprepare também foi enviada. Agora, o driver de envio em lote é unprepare consultas até o limite "ServerPreparedStatementDiscardThreshold", que tem um valor padrão de 10.

> [!NOTE]  
>  Os usuários podem alterar o valor padrão com o seguinte método: setServerPreparedStatementDiscardThreshold (valor int)

Mais uma alteração introduzida do 6.1.6-preview é que antes disso, driver sempre chamaria sp_prepexec. Agora, para a primeira execução de uma instrução preparada, driver chama sp_executesql e para o restante executa sp_prepexec e atribui um identificador a ele. Mais detalhes podem ser encontrados [aqui](https://github.com/Microsoft/mssql-jdbc/wiki/PreparedStatement-metadata-caching).

> [!NOTE]  
>  Os usuários podem alterar o comportamento padrão para as versões anteriores de sempre chamar sp_prepexec por configuração enablePrepareOnFirstPreparedStatementCall para **verdadeira** usando o seguinte método: setEnablePrepareOnFirstPreparedStatementCall (valor booleano)

### <a name="list-of-the-new-apis-introduced-with-this-change-for-batching-of-unprepare-for-prepared-statements"></a>Lista das novas APIs introduzidas com essa alteração, para processamento em lotes de Unprepare para instruções preparadas

 **SQLServerConnection**
 
|Novo método|Descrição|  
|-----------|-----------------|  
|int getDiscardedServerPreparedStatementCount()|Retorna o número de pendente no momento preparada instrução unprepare ações.|
|void closeUnreferencedPreparedStatementHandles()|Força as solicitações de unprepare para qualquer instrução preparada descartadas de pendentes a serem executadas.|
|getEnablePrepareOnFirstPreparedStatementCall() booliano|Retorna o comportamento de uma instância de conexão específica. Se false a primeira execução e chama sp_executesql não prepara uma instrução, depois que a segunda execução acontece, ele chama o sp_prepexec e configurar, na verdade, um identificador de instrução preparada. Os seguintes execuções chamadas sp_execute. Isso alivia a necessidade de sp_unprepare na instrução preparada fechar se a instrução é executada apenas uma vez. O padrão para essa opção pode ser alterado pela chamada setDefaultEnablePrepareOnFirstPreparedStatementCall().|
|void setEnablePrepareOnFirstPreparedStatementCall(boolean value)|Especifica o comportamento para uma instância de conexão específica. Se o valor for false a primeira execução e chama sp_executesql não prepara uma instrução, depois que a segunda execução acontece, ele chama o sp_prepexec e configurar, na verdade, um identificador de instrução preparada. Os seguintes execuções chamadas sp_execute. Isso alivia a necessidade de sp_unprepare na instrução preparada fechar se a instrução é executada apenas uma vez.|
|int getServerPreparedStatementDiscardThreshold()|Retorna o comportamento de uma instância de conexão específica. Essa configuração controla quantos pendentes preparado descarte instrução ações (sp_unprepare) podem estar pendentes por conexão antes de uma chamada para limpar os identificadores pendentes no servidor é executada. Se a configuração for < = 1, unprepare ações são executadas imediatamente na instrução preparada fechar. Se ele for definido como {@literal >} 1, essas chamadas são agrupados em lotes, para evitar a sobrecarga de chamada sp_unprepare com muita frequência. O padrão para essa opção pode ser alterado pela chamada getDefaultServerPreparedStatementDiscardThreshold().|
|void setServerPreparedStatementDiscardThreshold(int value)|Especifica o comportamento para uma instância de conexão específica. Essa configuração controla quantos pendentes preparado descarte instrução ações (sp_unprepare) podem estar pendentes por conexão antes de uma chamada para limpar os identificadores pendentes no servidor é executada. Se a configuração for < = 1 unprepare ações são executadas imediatamente no fechamento instrução preparada. Se estiver definido como 1 > essas chamadas são agrupados em lotes, para evitar a sobrecarga da chamada sp_unprepare com muita frequência.|

 **SQLServerDataSource**
 
|Novo método|Descrição|  
|-----------|-----------------|  
|void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall)|Se essa configuração for false a primeira execução de uma instrução preparada e chama sp_executesql não prepara uma instrução, depois que a segunda execução acontece, ele chama o sp_prepexec e configurar, na verdade, um identificador de instrução preparada. Os seguintes execuções chamadas sp_execute. Isso alivia a necessidade de sp_unprepare na instrução preparada fechar se a instrução é executada apenas uma vez.|
|getEnablePrepareOnFirstPreparedStatementCall() booliano|Se essa configuração retorna false, a primeira execução de uma instrução preparada chama sp_executesql e não prepara uma instrução, depois que a segunda execução acontece, ele chama o sp_prepexec e configurar, na verdade, um identificador de instrução preparada. Os seguintes execuções chamadas sp_execute. Isso alivia a necessidade de sp_unprepare na instrução preparada fechar se a instrução é executada apenas uma vez.|
|void setServerPreparedStatementDiscardThreshold(int serverPreparedStatementDiscardThreshold)|Essa configuração controla quantos pendentes preparado descarte instrução ações (sp_unprepare) podem estar pendentes por conexão antes de uma chamada para limpar os identificadores pendentes no servidor é executada. Se a configuração for < = 1 unprepare ações são executadas imediatamente no fechamento instrução preparada. Se ele for definido como {@literal >} 1 essas chamadas são agrupados em lotes, para evitar a sobrecarga da chamada sp_unprepare com muita frequência|
|int getServerPreparedStatementDiscardThreshold()|Essa configuração controla quantos pendentes preparado descarte instrução ações (sp_unprepare) podem estar pendentes por conexão antes de uma chamada para limpar os identificadores pendentes no servidor é executada. Se a configuração for < = 1 unprepare ações são executadas imediatamente no fechamento instrução preparada. Se ele for definido como {@literal >} 1 essas chamadas são agrupados em lotes, para evitar a sobrecarga da chamada sp_unprepare com muita frequência.|

## <a name="prepared-statement-metatada-caching"></a>Cache de metadados de instrução preparada
A partir da versão 6.3.0-preview, o Microsoft JDBC driver para SQL Server dá suporte ao cache de instrução preparada. Antes de v6.3.0-preview, se um executa uma consulta que foi preparada e armazenada no cache, já chamando a mesma consulta novamente não resultará em Preparando-o. Agora, o driver procura a consulta no cache e localizar o identificador e executá-lo com sp_execute.
O cache de metadados de instrução preparada é **desabilitada** por padrão. Para habilitá-lo, você precisa chamar o método a seguir no objeto de conexão:

`setStatementPoolingCacheSize(int value)   //value is the desired cache size (any value bigger than 0)`
`setDisableStatementPooling(boolean value) //false allows the caching to take place`

Por exemplo: `connection.setStatementPoolingCacheSize(10)`
`connection.setDisableStatementPooling(false)`

### <a name="list-of-the-new-apis-introduced-with-this-change-for-prepared-statement-metadata-caching"></a>Lista das novas APIs introduzidas com essa alteração, instrução preparada para o cache de metadados

 **SQLServerConnection**
 
|Novo método|Descrição|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean value)|Define o pooling de instrução como verdadeira ou falsa.|
|getDisableStatementPooling() booliano|Retorna VERDADEIRO se o pool de instrução é desabilitado.|
|void setStatementPoolingCacheSize(int value)|Especifica o tamanho do cache de instrução preparada para essa conexão. Um valor menor que 1 significa sem cache.|
|int getStatementPoolingCacheSize()|Retorna o tamanho do cache de instrução preparada para essa conexão. Um valor menor que 1 significa sem cache.|
|int getStatementHandleCacheEntryCount()|Retorna o número atual de identificadores de instrução preparada em pool.|
|isPreparedStatementCachingEnabled() booliano|Se o pooling de instrução está habilitado ou não para essa conexão.|

 **SQLServerDataSource**
 
|Novo método|Descrição|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean disableStatementPooling)|Define a instrução de pooling como true ou false|
|getDisableStatementPooling() booliano|Retorna VERDADEIRO se o pool de instrução é desabilitado.|
|void setStatementPoolingCacheSize(int statementPoolingCacheSize)|Especifica o tamanho do cache de instrução preparada para essa conexão. Um valor menor que 1 significa sem cache.|
|int getStatementPoolingCacheSize()|Retorna o tamanho do cache de instrução preparada para essa conexão. Um valor menor que 1 significa sem cache.|

## <a name="see-also"></a>Consulte Também  
 [Melhorando o desempenho e a confiabilidade com o JDBC Driver](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
