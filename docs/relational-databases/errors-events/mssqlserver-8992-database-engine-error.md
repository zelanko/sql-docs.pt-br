---
title: MSSQLSERVER_8992 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 8992 (Database Engine error)
ms.assetid: 68467e6a-09d8-478f-8bd9-3bb09453ada3
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d0b26c29f4043fe9b88baf1eafeef7b4fe7dedd6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver8992"></a>MSSQLSERVER_8992
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|8992|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC3_CHECK_CATALOG|  
|Texto da mensagem|Verifique a mensagem do catálogo ERROR nível LEVEL Estado STATE: MESSAGE.|  
  
## <a name="explanation"></a>Explicação  
DBCC CHECKCATALOG ou DBCC CHECKDB localizou uma inconsistência nas tabelas de metadados do sistema para o objeto especificado. Isto é, há uma inconsistência entre a ID do objeto registrado e o objeto especificado na mensagem de erro.  
  
Esse erro pode ocorrer quando uma ou mais tabelas do sistema foram atualizadas manualmente de uma maneira que cria uma inconsistência nos metadados do sistema. Por exemplo, um usuário pode ter excluído manualmente um objeto da tabela **sysobjects** sem remover as linhas associadas em outras tabelas como **sysindexes** e **syscolumns**.  
  
Esse erro pode ocorrer ao executar DBCC CHECKDB em um banco de dados que foi atualizado do SQL Server 2000 para o SQL Server 2005 ou posterior. No SQL Server 2000, o DBCC CHECKDB não incluía a funcionalidade DBCC CHECKCATALOG, portanto o erro não seria capturado antes da atualização a menos que DBCC CHECKCATALOG fosse executado especificamente no banco de dados no SQL Server 2000.  
  
Você pode consultar quaisquer um dos erros a seguir em conjunto com o erro 8992:  
  
Mensagem 3851 - Linha inválida (%ls) encontrada na tabela do sistema sys.%ls%ls.  
  
Mensagem 3852 - Linha (%ls) em sys.%ls%ls sem linha correspondente (%ls) em sys.%ls%ls.  
  
3853 - Atributo (%ls) da linha (%ls) em sys.%ls%ls sem linha correspondente (%ls) em sys.%ls%ls.  
  
3854 - Atributo (%ls) da linha (%ls) em sys.%ls%ls com linha correspondente (%ls) inválida em sys.%ls%ls.  
  
3855 - Atributo (%ls) existente sem uma linha (%ls) em sys.%ls%ls.  
  
3856 - O atributo (%ls) existe, mas não deveria, para a linha (%ls) em sys.%ls%ls.  
  
3857 - O atributo (%ls) é necessário, mas não existe para a linha (%ls) em sys.%ls%ls.  
  
3858 - O atributo (%ls) da linha (%ls) em sys.%ls%ls tem um valor inválido.  
  
## <a name="user-action"></a>Ação do usuário  
  
### <a name="drop-and-re-create-the-specified-object"></a>Descartar e recriar o objeto especificado  
Se possível, descarte e recrie o objeto especificado. Por exemplo, se o objeto for um procedimento armazenado ou um tipo definido pelo usuário, a recriação do objeto poderá resolver o problema.  
  
### <a name="restore-from-backup"></a>Restaurar a partir de backup  
Se o problema não estiver relacionado ao hardware e se houver um backup limpo conhecido, restaure o banco de dados do backup. Essa ação só será aplicável se o backup não contiver o erro de metadados.  
  
### <a name="export-the-data-to-a-new-database"></a>Exportar os dados para um novo banco de dados  
Se o backup também contiver a inconsistência de metadados, você precisará criar um novo banco de dados e exportar o conteúdo do banco de dados existente para o novo banco de dados.  
  
### <a name="dbcc-checkdb-cannot-repair-this-error"></a>DBCC CHECKDB não pode reparar este erro  
Esse erro não pode ser reparado.  Se você não conseguir restaurar o banco de dados com base em um backup, contate o CSS (Suporte e Atendimento ao Cliente) [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
### <a name="do-not-manually-update-system-tables"></a>Não atualizar manualmente tabelas do sistema  
Não faça atualizações manuais em tabelas do sistema. O SQL Server não oferece suporte a alterações manuais em bancos de dados do sistema. Se você atualizar uma tabela do sistema em um banco de dados do SQL Server, dois eventos (ID de evento 17659 e ID de evento 3859) serão registrados em log. Para obter mais informações, consulte o artigo KB 2688307, "ID de evento 17659 e ID de evento 3859 são registrados em log quando você atualiza tabelas do sistema em um banco de dados do SQL Server".  
  
## <a name="see-also"></a>Consulte Também  
[A ID de evento 17659 e a ID de evento 3859 são registradas em log quando você atualiza tabelas do sistema em um banco de dados do SQL Server](http://support.microsoft.com/kb/2688307/EN-US)  
  
