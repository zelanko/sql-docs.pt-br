---
title: Metadados de instrução em cache preparados para o JDBC Driver
description: Saiba como o JDBC Driver para SQL Server armazena em cache as instruções preparadas para melhorar o desempenho ao minimizar as chamadas para o banco de dados e como você pode controlar o comportamento dele.
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 67b35e04ede8608d222c8fc31d89bfd01b093ba7
ms.sourcegitcommit: 129f8574eba201eb6ade1f1620c6b80dfe63b331
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/30/2020
ms.locfileid: "87435393"
---
# <a name="prepared-statement-metadata-caching-for-the-jdbc-driver"></a>Metadados de instrução em cache preparados para o JDBC Driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Este artigo fornece informações sobre as duas alterações que foram implementadas para aprimorar o desempenho do driver.

## <a name="batching-of-unprepare-for-prepared-statements"></a>Envio em lote de instruções de cancelamento de preparação para instruções preparadas
Desde a versão 6.1.6-preview, um aprimoramento no desempenho foi implementado por meio da minimização de viagens de ida e volta do servidor para o SQL Server. Anteriormente, para cada consulta prepareStatement, uma chamada de cancelamento de preparação também foi enviada. Agora, o driver está enviando em lote consultas de cancelamento de preparação até o limite "ServerPreparedStatementDiscardThreshold", que tem um valor padrão de 10.

> [!NOTE]  
>  Os usuários podem alterar o valor padrão com o seguinte método: setServerPreparedStatementDiscardThreshold(int value)

Outra alteração que foi introduzida na versão 6.1.6-preview é que, antes disso, o driver sempre chamava sp_prepexec. Agora, para a primeira execução de uma instrução preparada, o driver chama sp_executesql e, para o restante, ele executa sp_prepexec e atribui um identificador a ele. Encontre mais detalhes [aqui](https://github.com/Microsoft/mssql-jdbc/wiki/PreparedStatement-metadata-caching).

> [!NOTE]  
>  Os usuários podem alterar o comportamento padrão para as versões anteriores chamando sempre sp_prepexec configurando enablePrepareOnFirstPreparedStatementCall como **true** usando o seguinte método: setEnablePrepareOnFirstPreparedStatementCall(boolean value)

### <a name="list-of-the-new-apis-introduced-with-this-change-for-batching-of-unprepare-for-prepared-statements"></a>Lista das novas APIs introduzidas com essa alteração, para o envio em lote de cancelamento de preparação para instruções preparadas

 **SQLServerConnection**
 
|Novo método|Descrição|  
|-----------|-----------------|  
|int getDiscardedServerPreparedStatementCount()|Retorna o número das ações atuais de cancelamento de preparação de instruções preparadas pendentes.|
|void closeUnreferencedPreparedStatementHandles()|Força o cancelamento da preparação de solicitações para as instruções preparadas descartadas pendentes a serem executadas.|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|Retorna o comportamento de uma instância de conexão específica. Se for false, a primeira execução chamará sp_executesql e não preparará uma instrução. Assim que a segunda execução ocorrer, ela chamará sp_prepexec e configurará efetivamente um identificador de instrução preparada. As execuções subsequentes chamarão sp_execute. Isso elimina a necessidade de sp_unprepare no fechamento da instrução preparada se a instrução é executada apenas uma vez. O padrão para essa opção pode ser alterado chamando setDefaultEnablePrepareOnFirstPreparedStatementCall().|
|void setEnablePrepareOnFirstPreparedStatementCall(boolean value)|Especifica o comportamento de uma instância de conexão específica. Se o valor for false, a primeira execução chamará sp_executesql e não preparará uma instrução. Assim que a segunda execução ocorrer, ela chamará sp_prepexec e configurará efetivamente um identificador de instrução preparada. As execuções subsequentes chamarão sp_execute. Isso elimina a necessidade de sp_unprepare no fechamento da instrução preparada se a instrução é executada apenas uma vez.|
|int getServerPreparedStatementDiscardThreshold()|Retorna o comportamento de uma instância de conexão específica. Essa configuração controla quantas ações de descarte de instruções preparadas pendentes (sp_unprepare) podem estar pendentes por conexão antes que uma chamada para limpar os identificadores pendentes no servidor seja executada. Se a configuração for < = 1, ações de cancelamento de preparação serão executadas imediatamente no fechamento da instrução preparada. Se o valor for definido como {@literal >} 1, essas chamadas serão agrupadas em lote para evitar a sobrecarga de chamar sp_unprepare com muita frequência. O padrão para essa opção pode ser alterado chamando getDefaultServerPreparedStatementDiscardThreshold().|
|void setServerPreparedStatementDiscardThreshold(int value)|Especifica o comportamento de uma instância de conexão específica. Essa configuração controla quantas ações de descarte de instruções preparadas pendentes (sp_unprepare) podem estar pendentes por conexão antes que uma chamada para limpar os identificadores pendentes no servidor seja executada. Se a configuração for < = 1, ações de cancelamento de preparação serão executadas imediatamente no fechamento da instrução preparada. Se o valor for definido como > 1, essas chamadas serão agrupadas em lote para evitar a sobrecarga de chamar sp_unprepare com muita frequência.|

 **SQLServerDataSource**
 
|Novo método|Descrição|  
|-----------|-----------------|  
|void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall)|Se essa configuração for false, a primeira execução de uma instrução preparada chamará sp_executesql e não preparará uma instrução. Assim que a segunda execução ocorrer, ela chamará sp_prepexec e configurará efetivamente um identificador de instrução preparada. As execuções subsequentes chamarão sp_execute. Isso elimina a necessidade de sp_unprepare no fechamento da instrução preparada se a instrução é executada apenas uma vez.|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|Se essa configuração retornar false, a primeira execução de uma instrução preparada chamará sp_executesql e não preparará uma instrução. Assim que a segunda execução ocorrer, ela chamará sp_prepexec e configurará efetivamente um identificador de instrução preparada. As execuções subsequentes chamarão sp_execute. Isso elimina a necessidade de sp_unprepare no fechamento da instrução preparada se a instrução é executada apenas uma vez.|
|void setServerPreparedStatementDiscardThreshold(int serverPreparedStatementDiscardThreshold)|Essa configuração controla quantas ações de descarte de instruções preparadas pendentes (sp_unprepare) podem estar pendentes por conexão antes que uma chamada para limpar os identificadores pendentes no servidor seja executada. Se a configuração for < = 1, ações de cancelamento de preparação serão executadas imediatamente no fechamento da instrução preparada. Se o valor for definido como {@literal >} 1, essas chamadas serão agrupadas em lote para evitar a sobrecarga de chamar sp_unprepare com muita frequência|
|int getServerPreparedStatementDiscardThreshold()|Essa configuração controla quantas ações de descarte de instruções preparadas pendentes (sp_unprepare) podem estar pendentes por conexão antes que uma chamada para limpar os identificadores pendentes no servidor seja executada. Se a configuração for < = 1, ações de cancelamento de preparação serão executadas imediatamente no fechamento da instrução preparada. Se o valor for definido como {@literal >} 1, essas chamadas serão agrupadas em lote para evitar a sobrecarga de chamar sp_unprepare com muita frequência.|

## <a name="prepared-statement-metadata-caching"></a>Armazenamento em cache de metadados de instruções preparadas
Com a versão 6.3.0-preview, o Microsoft JDBC Driver para SQL Server passa a ser compatível com o cache de instruções preparadas. Antes da v6.3.0-preview, se um usuário executasse uma consulta que já tivesse sido preparada e armazenada no cache, chamar a mesma consulta novamente não resultaria na preparação dela. Agora, o driver pesquisa a consulta no cache, localiza o identificador e executa-o com sp_execute.
O cache de metadados de **instrução** preparado está desabilitado por padrão. Para habilitá-lo, você precisa chamar o seguinte método no objeto de conexão:

`setStatementPoolingCacheSize(int value)   //value is the desired cache size (any value bigger than 0)`
`setDisableStatementPooling(boolean value) //false allows the caching to take place`

Por exemplo: `connection.setStatementPoolingCacheSize(10)`
`connection.setDisableStatementPooling(false)`

### <a name="list-of-the-new-apis-introduced-with-this-change-for-prepared-statement-metadata-caching"></a>Lista das novas APIs introduzidas com essa alteração, para cache de metadados de instruções preparadas

 **SQLServerConnection**
 
|Novo método|Descrição|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean value)|Define o pool de instruções como true ou false.|
|boolean getDisableStatementPooling()|Retorna true se o pool de instruções está desabilitado.|
|void setStatementPoolingCacheSize(int value)|Especifica o tamanho do cache de instruções preparadas para esta conexão. Um valor menor que 1 significa nenhum cache.|
|int getStatementPoolingCacheSize()|Retorna o tamanho do cache de instruções preparado para esta conexão. Um valor menor que 1 significa nenhum cache.|
|int getStatementHandleCacheEntryCount()|Retorna o número atual de identificadores de instruções preparadas agrupadas.|
|boolean isPreparedStatementCachingEnabled()|Se o pool de instruções está habilitado ou não para essa conexão.|

 **SQLServerDataSource**
 
|Novo método|Descrição|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean disableStatementPooling)|Define o pool de instruções como true ou false|
|boolean getDisableStatementPooling()|Retorna true se o pool de instruções está desabilitado.|
|void setStatementPoolingCacheSize(int statementPoolingCacheSize)|Especifica o tamanho do cache de instruções preparadas para esta conexão. Um valor menor que 1 significa nenhum cache.|
|int getStatementPoolingCacheSize()|Retorna o tamanho do cache de instruções preparado para esta conexão. Um valor menor que 1 significa nenhum cache.|

## <a name="see-also"></a>Confira também  
 [Melhorando o desempenho e a confiabilidade com o JDBC Driver](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
