---
title: MSSQLSERVER_8992 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8992 (Database Engine error)
ms.assetid: 68467e6a-09d8-478f-8bd9-3bb09453ada3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9d5da60bc3e2716fb808c47f949b3b918b4e9d85
ms.sourcegitcommit: cebf41506a28abfa159a5dd871b220630c4c4504
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77479672"
---
# <a name="mssqlserver_8992"></a>MSSQLSERVER_8992
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|8992|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC3_CHECK_CATALOG|  
|Texto da mensagem|Verifique a mensagem do catálogo ERROR Nível LEVEL Estado STATE: MESSAGE.|  

> [!NOTE]
> A mensagem de erro 8992 referencia outra mensagem específica (que varia de 3851 a 3858) sobre a inconsistência real.

## <a name="explanation"></a>Explicação  
DBCC CHECKCATALOG ou DBCC CHECKDB localizou uma inconsistência nas tabelas de metadados do sistema para o objeto especificado. Isto é, há uma inconsistência entre a ID do objeto registrado e o objeto especificado na mensagem de erro.  
  
Esse erro pode ocorrer quando uma ou mais tabelas do sistema foram atualizadas manualmente de uma maneira que cria uma inconsistência nos metadados do sistema. Por exemplo, um usuário pode ter excluído manualmente um objeto da tabela **sysobjects** sem remover as linhas associadas em outras tabelas como **sysindexes** e **syscolumns**.  
  
Esse erro pode ocorrer ao executar DBCC CHECKDB em um banco de dados que foi atualizado do SQL Server 2000 para o SQL Server 2005 ou posterior. No SQL Server 2000, o DBCC CHECKDB não incluía a funcionalidade DBCC CHECKCATALOG, portanto o erro não seria capturado antes da atualização a menos que DBCC CHECKCATALOG fosse executado especificamente no banco de dados no SQL Server 2000.  
  
Você pode consultar quaisquer um dos erros a seguir em conjunto com o erro 8992:  
|||
|-|-| 
|ID da Msg|Texto da Msg|
|3851|Uma linha inválida (%ls) foi encontrada na tabela do sistema sys.%ls%ls.|
|3852|Linha (%ls) em sys.%ls%ls sem linha correspondente (%ls) em sys.%ls%ls.|
|3853|Atributo (%ls) da linha (%ls) em sys.%ls%ls sem linha correspondente (%ls) em sys.%ls%ls.|
|3854|Atributo (%ls) da linha (%ls) em sys.%ls%ls com linha correspondente (%ls) inválida em sys.%ls%ls.|
|3855|Atributo (%ls) existente sem uma linha (%ls) em sys.%ls%ls.|
|3856|O atributo (%ls) existe, mas não deveria, para a linha (%ls) em sys.%ls%ls.|
|3857|O atributo (%ls) é necessário, mas não existe para a linha (%ls) em sys.%ls%ls.|
|3858|O atributo (%ls) da linha (%ls) em sys.%ls%ls tem um valor inválido.|

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

Não faça atualizações manuais em tabelas do sistema. O SQL Server não oferece suporte a alterações manuais em bancos de dados do sistema. Se você atualizar uma tabela do sistema em um banco de dados do SQL Server, os seguintes eventos serão registrados em log:

#### <a name="when-a-system-table-is-manually-updated"></a>Quando uma tabela do sistema é atualizada manualmente

Msg 17659: Aviso: a ID da tabela do sistema <id> foi atualizada diretamente na ID do banco de dados <id> e a coerência de cache talvez não tenha sido mantida. O SQL Server deve ser reiniciado.

#### <a name="starting-a-database-with-a-system-table-that-was-manually-updated"></a>Iniciando um banco de dados com uma tabela do sistema que foi atualizada manualmente

Msg 3859: Aviso: o catálogo do sistema foi atualizado diretamente na ID do banco de dados <id>, mais recentemente em date_time

#### <a name="when-you-execute-the-dbcc_checkdb-command-after-a-system-table-is-manually-updated"></a>quando você executa o comando DBCC_CHECKDB depois que uma tabela do sistema é atualizada manualmente

Msg 3859: Aviso: o catálogo do sistema foi atualizado diretamente na ID do banco de dados <id>, mais recentemente em date_time.  

## <a name="see-also"></a>Consulte Também

[Tabelas base do sistema](../system-tables/system-base-tables.md)
  
