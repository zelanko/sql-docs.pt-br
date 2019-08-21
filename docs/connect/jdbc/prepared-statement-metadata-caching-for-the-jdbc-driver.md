---
title: Metadados de instrução em cache preparados para o JDBC Driver | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 97224f53bb716abe3b79dd00df12d0eed4a63cec
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027839"
---
# <a name="prepared-statement-metadata-caching-for-the-jdbc-driver"></a>Metadados de instrução em cache preparados para o JDBC Driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Este artigo fornece informações sobre as duas alterações que são implementadas para aprimorar o desempenho do driver.

## <a name="batching-of-unprepare-for-prepared-statements"></a>Envio em lote de instruções preparadas
Desde a versão 6.1.6-Preview, uma melhoria no desempenho foi implementada por meio da minimização de viagens de ida e volta do servidor para SQL Server. Anteriormente, para cada consulta prepareStatement, uma chamada para Unprepare também foi enviada. Agora, o driver está em lotes despreparar consultas até o limite "ServerPreparedStatementDiscardThreshold", que tem um valor padrão de 10.

> [!NOTE]  
>  Os usuários podem alterar o valor padrão com o seguinte método: setServerPreparedStatementDiscardThreshold (valor int)

Uma outra alteração introduzida em 6.1.6-Preview é que, antes disso, o driver sempre chamaria sp_prepexec. Agora, para a primeira execução de uma instrução preparada, o driver chama sp_executesql e, para o REST, ele executa o sp_prepexec e atribui um identificador a ele. Mais detalhes podem ser encontrados [aqui](https://github.com/Microsoft/mssql-jdbc/wiki/PreparedStatement-metadata-caching).

> [!NOTE]  
>  Os usuários podem alterar o comportamento padrão para as versões anteriores do sempre chamando sp_prepexec definindo enablePrepareOnFirstPreparedStatementCall como **true** usando o seguinte método: setEnablePrepareOnFirstPreparedStatementCall (valor booliano )

### <a name="list-of-the-new-apis-introduced-with-this-change-for-batching-of-unprepare-for-prepared-statements"></a>Lista das novas APIs introduzidas com essa alteração, para o envio em lote de instruções preparadas de despreparar

 **SQLServerConnection**
 
|Novo método|Descrição|  
|-----------|-----------------|  
|int getDiscardedServerPreparedStatementCount()|Retorna o número de ações de despreparação da instrução preparada pendente no momento.|
|void closeUnreferencedPreparedStatementHandles()|Força as solicitações de despreparação para qualquer instrução preparada pendente descartada a ser executada.|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|Retorna o comportamento de uma instância de conexão específica. Se false, a primeira execução chamará sp_executesql e não preparará uma instrução, depois que a segunda execução for chamada de sp_prepexec e, na verdade, configurará um identificador de instrução preparado. As execuções a seguir chamam sp_execute. Isso alivia a necessidade de sp_unprepare na instrução preparada fechar se a instrução for executada apenas uma vez. O padrão para essa opção pode ser alterado chamando setDefaultEnablePrepareOnFirstPreparedStatementCall ().|
|void setEnablePrepareOnFirstPreparedStatementCall (valor booliano)|Especifica o comportamento de uma instância de conexão específica. Se value for false, a primeira execução chamará sp_executesql e não preparará uma instrução, depois que a segunda execução ocorrer, ela chamará sp_prepexec e, na verdade, configurará um identificador de instrução preparado. As execuções a seguir chamam sp_execute. Isso alivia a necessidade de sp_unprepare na instrução preparada fechar se a instrução for executada apenas uma vez.|
|int getServerPreparedStatementDiscardThreshold()|Retorna o comportamento de uma instância de conexão específica. Essa configuração controla quantas ações de descarte de instrução preparadas pendentes (sp_unprepare) podem estar pendentes por conexão antes que uma chamada para limpar os identificadores pendentes no servidor seja executada. Se a configuração for < = 1, as ações despreparar serão executadas imediatamente no fechamento da instrução preparada. Se estiver definido como {@literal >} 1, essas chamadas serão agrupadas em lote para evitar a sobrecarga de chamar sp_unprepare com muita frequência. O padrão para essa opção pode ser alterado chamando getDefaultServerPreparedStatementDiscardThreshold ().|
|void setServerPreparedStatementDiscardThreshold (valor int)|Especifica o comportamento de uma instância de conexão específica. Essa configuração controla quantas ações de descarte de instrução preparadas pendentes (sp_unprepare) podem estar pendentes por conexão antes que uma chamada para limpar os identificadores pendentes no servidor seja executada. Se a configuração for < = 1 as ações despreparar serão executadas imediatamente no fechamento da instrução preparada. Se estiver definido como > 1, essas chamadas serão agrupadas em lote para evitar a sobrecarga de chamar sp_unprepare com muita frequência.|

 **SQLServerDataSource**
 
|Novo método|Descrição|  
|-----------|-----------------|  
|void setEnablePrepareOnFirstPreparedStatementCall (enablePrepareOnFirstPreparedStatementCall booliano)|Se essa configuração for falsa, a primeira execução de uma instrução preparada chamará sp_executesql e não preparará uma instrução, depois que a segunda execução ocorrer, ela chamará sp_prepexec e, na verdade, configurará um identificador de instrução preparado. As execuções a seguir chamam sp_execute. Isso alivia a necessidade de sp_unprepare na instrução preparada fechar se a instrução for executada apenas uma vez.|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|Se essa configuração retornar false, a primeira execução de uma instrução preparada chamará sp_executesql e não preparará uma instrução, depois que a segunda execução ocorrer, ela chamará sp_prepexec e, na verdade, configurará um identificador de instrução preparado. As execuções a seguir chamam sp_execute. Isso alivia a necessidade de sp_unprepare na instrução preparada fechar se a instrução for executada apenas uma vez.|
|void setServerPreparedStatementDiscardThreshold (int serverPreparedStatementDiscardThreshold)|Essa configuração controla quantas ações de descarte de instrução preparadas pendentes (sp_unprepare) podem estar pendentes por conexão antes que uma chamada para limpar os identificadores pendentes no servidor seja executada. Se a configuração for < = 1 as ações despreparar serão executadas imediatamente no fechamento da instrução preparada. Se estiver definido como {@literal >} 1, essas chamadas serão agrupadas em lote para evitar a sobrecarga de chamar sp_unprepare com muita frequência|
|int getServerPreparedStatementDiscardThreshold()|Essa configuração controla quantas ações de descarte de instrução preparadas pendentes (sp_unprepare) podem estar pendentes por conexão antes que uma chamada para limpar os identificadores pendentes no servidor seja executada. Se a configuração for < = 1 as ações despreparar serão executadas imediatamente no fechamento da instrução preparada. Se estiver definido como {@literal >} 1, essas chamadas serão agrupadas em lote para evitar a sobrecarga de chamar sp_unprepare com muita frequência.|

## <a name="prepared-statement-metatada-caching"></a>Cache metadados de instrução preparada
A partir da versão 6.3.0-Preview, o Microsoft JDBC Driver for SQL Server dá suporte ao cache de instruções preparado. Antes do v 6.3.0-Preview, se um executar uma consulta que já foi preparada e armazenada no cache, chamar a mesma consulta novamente não resultará na preparação dela. Agora, o driver pesquisa a consulta no cache e encontra o identificador e executa-o com sp_execute.
O cache de metadados de **instrução** preparado está desabilitado por padrão. Para habilitá-lo, você precisa chamar o seguinte método no objeto de conexão:

`setStatementPoolingCacheSize(int value)   //value is the desired cache size (any value bigger than 0)`
`setDisableStatementPooling(boolean value) //false allows the caching to take place`

Por exemplo: `connection.setStatementPoolingCacheSize(10)`
`connection.setDisableStatementPooling(false)`

### <a name="list-of-the-new-apis-introduced-with-this-change-for-prepared-statement-metadata-caching"></a>Lista das novas APIs introduzidas com essa alteração, para cache de metadados de instrução preparada

 **SQLServerConnection**
 
|Novo método|Descrição|  
|-----------|-----------------|  
|void setDisableStatementPooling (valor booliano)|Define o pool de instruções como true ou false.|
|boolean getDisableStatementPooling()|Retornará true se o pool de instruções estiver desabilitado.|
|void setStatementPoolingCacheSize (valor int)|Especifica o tamanho do cache de instruções preparado para esta conexão. Um valor menor que 1 significa nenhum cache.|
|int getStatementPoolingCacheSize()|Retorna o tamanho do cache de instruções preparado para esta conexão. Um valor menor que 1 significa nenhum cache.|
|int getStatementHandleCacheEntryCount()|Retorna o número atual de identificadores de instrução preparados em pool.|
|isPreparedStatementCachingEnabled booliano ()|Se o pooling de instruções está habilitado ou não para essa conexão.|

 **SQLServerDataSource**
 
|Novo método|Descrição|  
|-----------|-----------------|  
|void setDisableStatementPooling (disableStatementPooling booliano)|Define o pool de instruções como true ou false|
|boolean getDisableStatementPooling()|Retornará true se o pool de instruções estiver desabilitado.|
|void setStatementPoolingCacheSize (int statementPoolingCacheSize)|Especifica o tamanho do cache de instruções preparado para esta conexão. Um valor menor que 1 significa nenhum cache.|
|int getStatementPoolingCacheSize()|Retorna o tamanho do cache de instruções preparado para esta conexão. Um valor menor que 1 significa nenhum cache.|

## <a name="see-also"></a>Confira também  
 [Melhorando o desempenho e a confiabilidade com o JDBC Driver](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
