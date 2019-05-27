---
title: Destino de arquivo de evento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- event file target
- file target [SQL Server extended events]
- targets [SQL Server extended events], file target
ms.assetid: 4f0ee6ec-a0a8-4c38-aa61-8293ab6ac7fd
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 53cf3aa4b23484bb22f4237fbf61874990381067
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66064858"
---
# <a name="event-file-target"></a>Event File Target
  O destino de arquivo de evento é um destino que grava buffers completos em disco.  
  
 A tabela a seguir descreve as opções disponíveis para configurar o destino de arquivo de evento.  
  
|Opção|Valores permitidos|Descrição|  
|------------|--------------------|-----------------|  
|filename|Qualquer cadeia de caracteres até 260 caracteres. Esse valor é necessário.|O local e nome do arquivo.<br /><br /> É possível usar qualquer extensão de nome de arquivo.|  
|max_file_size|Qualquer inteiro de 64 bits. Esse valor é opcional.|O tamanho máximo de arquivo em megabytes (MB). Se max_file_size não for especificado, o arquivo aumentará até que o disco fique cheio. O tamanho de arquivo padrão é 1 GB.<br /><br /> max_file_size deve ser maior que o tamanho atual dos buffers de sessão. Se não for, o destino de arquivo não inicializará, reportando que max_file_size é inválido. Para exibir o tamanho atual dos buffers, examine a coluna buffer_size na exibição de gerenciamento dinâmico [sys.dm_xe_sessions](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-sessions-transact-sql) .<br /><br /> Se o tamanho do arquivo padrão for menor do que o tamanho do buffer de sessão, é recomendável definir max_file_size com o valor especificado na coluna max_memory na exibição do catálogo [sys.server_event_sessions](/sql/relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql) .<br /><br /> Quando max_file_size é definido com um tamanho maior que o tamanho dos buffers de sessão, ele pode ser arredondado para baixo, para o múltiplo mais próximo do tamanho do buffer de sessão. Isso pode criar um arquivo de destino menor do que o valor especificado de max_file_size. Por exemplo, se o tamanho do buffer é 100 MB e max_file_size está definido como 150 MB, o tamanho de arquivo resultante é arredondado para baixo para 100 MB, porque um segundo buffer não caberia nos 50 MB restantes de espaço.<br /><br /> Se o tamanho do arquivo padrão for menor do que o tamanho do buffer de sessão, é recomendável definir max_file_size com o valor da coluna max_memory na exibição do catálogo [sys.server_event_sessions](/sql/relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql) .|  
|max_rollover_files|Qualquer inteiro de 32 bits. Esse valor é opcional.|O número máximo de arquivos a serem retidos no sistema de arquivos. O valor padrão é 5.|  
|incremento|Qualquer inteiro de 32 bits. Esse valor é opcional.|O crescimento incremental, em megabytes (MB), para o arquivo. Se não for especificado, o valor padrão do incremento será duas vezes o tamanho do buffer de sessão.|  
  
 Na primeira vez que um destino de arquivo de evento é criado, o nome de arquivo especificado é acrescentado com _0\_ e um valor inteiro longo. O valor inteiro é calculado como o número de milissegundos entre 1º de janeiro de 1601 e a data e hora, o arquivo é criado. Os arquivos de substituição subsequentes também usam esse formato. Examinando o valor do inteiro longo, você pode determinar o arquivo mais atual. O seguinte exemplo ilustra como arquivos são nomeados em um cenário no qual você especifica a opção de nome de arquivo como C:\OutputFiles\MyOutput.xel:  
  
-   primeiro arquivo criado - C:\OutputFiles\MyOutput_0_128500310259380000.xel  
  
-   primeiro arquivo de substituição - C:\OutputFiles\MyOutput_0_128505831770890000.xel  
  
-   segundo arquivo de substituição - C:\OutputFiles\MyOutput_0_132410772966237000.xel  
  
## <a name="adding-the-target-to-a-session"></a>Adicionando o destino a uma sessão  
 Para adicionar o destino do arquivo de evento a uma sessão Eventos Estendidos, inclua as seguintes instruções ao criar ou alterar uma sessão de evento, substituindo *file_name* pelo nome e o caminho do arquivo desejados:  
  
```  
ADD TARGET package0.event_file(  
   SET filename='file_name.xel')  
```  
  
## <a name="reviewing-the-target-output"></a>Revisando a saída de destino  
 Para examinar a saída de destino do arquivo, você deve usar a função sys.fn_xe_file_target_read_file. Nós recomendamos que você converta os dados como XML. Você pode usar a seguinte sintaxe, substituindo *file_name* pelo nome e o caminho do arquivo especificado quando você adicionou o destino:  
  
```  
SELECT *, CAST(event_data AS XML) AS 'event_data_XML'  
FROM sys.fn_xe_file_target_read_file('file_name*.xel', NULL, NULL, NULL)  
```  
  
## <a name="see-also"></a>Consulte também  
 [Destinos de eventos estendidos do SQL Server](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [sys.fn_xe_file_target_read_file &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql)   
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)  
  
  
