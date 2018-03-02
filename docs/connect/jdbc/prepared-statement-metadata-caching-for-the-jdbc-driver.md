---
title: "Preparar o cache para o Driver JDBC de metadados de instrução | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 13d4c0766552d9472038ffe7f2ff7fed6d73584d
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/02/2018
---
# <a name="prepared-statement-metadata-caching-for-the-jdbc-driver"></a>Metadados de instrução preparada cache para o Driver JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Este artigo fornece informações sobre as duas alterações que são implementadas para melhorar o desempenho do driver.

## <a name="batching-of-unprepare-for-prepared-statements"></a>Processamento em lotes de Unprepare para instruções preparadas
Uma vez que 6.1.6-preview de versão, uma melhoria no desempenho foi implementado através da redução do servidor processamentos ao SQL Server. Anteriormente, para cada consulta prepareStatement, uma chamada para unprepare também foi enviada. Agora, o driver de envio em lote é unprepare consultas até o limite "ServerPreparedStatementDiscardThreshold", que tem um valor padrão de 10.

> [!NOTE]  
>  Os usuários podem alterar o valor padrão com o seguinte método: setServerPreparedStatementDiscardThreshold (valor int)

Uma alteração mais de 6.1.6-preview é que antes disso, driver sempre chamaria sp_prepexec. Agora, para a primeira execução de uma instrução preparada, driver chama sp_executesql e para o resto executa sp_prepexec e atribui um identificador a ele. Mais detalhes podem ser encontrados [aqui](https://github.com/Microsoft/mssql-jdbc/wiki/PreparedStatement-metadata-caching).

> [!NOTE]  
>  Os usuários podem alterar o comportamento padrão para as versões anteriores de sempre chamar sp_prepexec por configuração enablePrepareOnFirstPreparedStatementCall para **true** usando o seguinte método: setEnablePrepareOnFirstPreparedStatementCall (valor booleano)

### <a name="list-of-the-new-apis-introduced-with-this-change-for-batching-of-unprepare-for-prepared-statements"></a>Lista de novas APIs introduzidas com essa alteração, para processamento em lotes de Unprepare para instruções preparadas

 **SQLServerConnection**
 
|Novo método|Description|  
|-----------|-----------------|  
|int getDiscardedServerPreparedStatementCount()|Retorna o número de pendente no momento preparada instrução unprepare ações.|
|void closeUnreferencedPreparedStatementHandles()|Força as solicitações de unprepare para qualquer instrução preparada com descartados pendentes a serem executados.|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|Retorna o comportamento de uma instância de conexão específica. Se false a primeira execução e chama sp_executesql não preparar uma instrução, depois que a segunda execução acontece chama sp_prepexec e instalação, na verdade, um identificador de instrução preparada. Execuções chamadas sp_execute a seguir. Isso alivia a necessidade de sp_unprepare na instrução preparada fechar se a instrução é executada apenas uma vez. O padrão para essa opção pode ser alterado pela chamada setDefaultEnablePrepareOnFirstPreparedStatementCall().|
|void setEnablePrepareOnFirstPreparedStatementCall(boolean value)|Especifica o comportamento de uma instância de conexão específica. Se o valor for false a primeira execução e chama sp_executesql não preparar uma instrução, depois que a segunda execução acontece chama sp_prepexec e instalação, na verdade, um identificador de instrução preparada. Execuções chamadas sp_execute a seguir. Isso alivia a necessidade de sp_unprepare na instrução preparada fechar se a instrução é executada apenas uma vez.|
|int getServerPreparedStatementDiscardThreshold()|Retorna o comportamento de uma instância de conexão específica. Essa configuração controla quantos pendentes preparado descarte de instrução ações (sp_unprepare) podem estar pendentes por conexão antes de uma chamada para limpar os identificadores pendentes no servidor é executada. Se a configuração for < = 1, unprepare ações são executadas imediatamente em Fechar instrução preparada. Se for definido como {@literal >} 1, estas chamadas são agrupadas para evitar a sobrecarga de chamada sp_unprepare com muita frequência. O padrão para essa opção pode ser alterado pela chamada getDefaultServerPreparedStatementDiscardThreshold().|
|void setServerPreparedStatementDiscardThreshold(int value)|Especifica o comportamento de uma instância de conexão específica. Essa configuração controla quantos pendentes preparado descarte de instrução ações (sp_unprepare) podem estar pendentes por conexão antes de uma chamada para limpar os identificadores pendentes no servidor é executada. Se a configuração for < = 1 unprepare ações são executados imediatamente em Fechar instrução preparada. Se ele for definido como 1 > estas chamadas são agrupadas para evitar a sobrecarga da chamada sp_unprepare com muita frequência.|

 **SQLServerDataSource**
 
|Novo método|Description|  
|-----------|-----------------|  
|void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall)|Se essa configuração for false a primeira execução de uma instrução preparada e chama sp_executesql não preparar uma instrução, depois que a segunda execução acontece chama sp_prepexec e instalação, na verdade, um identificador de instrução preparada. Execuções chamadas sp_execute a seguir. Isso alivia a necessidade de sp_unprepare na instrução preparada fechar se a instrução é executada apenas uma vez.|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|Se essa configuração retorna false, a primeira execução de uma instrução preparada chama sp_executesql e não prepara uma instrução, depois que a segunda execução acontece, ele chama sp_prepexec e instalação, na verdade, um identificador de instrução preparada. Execuções chamadas sp_execute a seguir. Isso alivia a necessidade de sp_unprepare na instrução preparada fechar se a instrução é executada apenas uma vez.|
|void setServerPreparedStatementDiscardThreshold(int serverPreparedStatementDiscardThreshold)|Essa configuração controla quantos pendentes preparado descarte de instrução ações (sp_unprepare) podem estar pendentes por conexão antes de uma chamada para limpar os identificadores pendentes no servidor é executada. Se a configuração for < = 1 unprepare ações são executados imediatamente em Fechar instrução preparada. Se for definido como {@literal >} 1 estas chamadas são agrupadas para evitar a sobrecarga da chamada sp_unprepare com muita frequência|
|int getServerPreparedStatementDiscardThreshold()|Essa configuração controla quantos pendentes preparado descarte de instrução ações (sp_unprepare) podem estar pendentes por conexão antes de uma chamada para limpar os identificadores pendentes no servidor é executada. Se a configuração for < = 1 unprepare ações são executados imediatamente em Fechar instrução preparada. Se for definido como {@literal >} 1 estas chamadas são agrupadas para evitar a sobrecarga da chamada sp_unprepare com muita frequência.|

## <a name="prepared-statement-metatada-caching"></a>Cache de metadados de instrução preparada
A partir da versão 6.3.0-preview, Microsoft JDBC driver para SQL Server dá suporte a cache de instrução preparada. Antes de v6.3.0-visualização, se um executa uma consulta que foi preparada e armazenada em cache, já chamando a mesma consulta novamente não resultará em Preparando-o. Agora, o driver procura a consulta no cache e localizar o identificador e executá-la com sp_execute.
Cache de metadados de instrução preparada é **desabilitado** por padrão. Para habilitá-lo, você precisa chamar o método a seguir no objeto de conexão:

`setStatementPoolingCacheSize(int value)   //value is the desired cache size (any value bigger than 0)`
`setDisableStatementPooling(boolean value) //false allows the caching to take place`

Por exemplo: `connection.setStatementPoolingCacheSize(10)`
`connection.setDisableStatementPooling(false)`

### <a name="list-of-the-new-apis-introduced-with-this-change-for-prepared-statement-metadata-caching"></a>Lista de novas APIs introduzidas com essa alteração, para a instrução preparada cache de metadados

 **SQLServerConnection**
 
|Novo método|Description|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean value)|Define o pooling de instrução como true ou false.|
|boolean getDisableStatementPooling()|Retorna VERDADEIRO se o pool de instrução está desabilitado.|
|void setStatementPoolingCacheSize(int value)|Especifica o tamanho do cache de instrução preparada para esta conexão. Um valor menor que 1 não significa que nenhum cache.|
|int getStatementPoolingCacheSize()|Retorna o tamanho do cache de instrução preparada para esta conexão. Um valor menor que 1 não significa que nenhum cache.|
|int getStatementHandleCacheEntryCount()|Retorna o número atual de identificadores de instrução preparada em pool.|
|boolean isPreparedStatementCachingEnabled()|Se o pool de instrução está habilitado ou não para essa conexão.|

 **SQLServerDataSource**
 
|Novo método|Description|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean disableStatementPooling)|Define a instrução pool como true ou false|
|boolean getDisableStatementPooling()|Retorna VERDADEIRO se o pool de instrução está desabilitado.|
|void setStatementPoolingCacheSize(int statementPoolingCacheSize)|Especifica o tamanho do cache de instrução preparada para esta conexão. Um valor menor que 1 não significa que nenhum cache.|
|int getStatementPoolingCacheSize()|Retorna o tamanho do cache de instrução preparada para esta conexão. Um valor menor que 1 não significa que nenhum cache.|

## <a name="see-also"></a>Consulte também  
 [Melhorando o desempenho e a confiabilidade com o JDBC Driver](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
