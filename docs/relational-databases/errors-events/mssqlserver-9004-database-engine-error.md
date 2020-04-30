---
title: MSSQLSERVER_9004 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9004 (Database Engine error)
ms.assetid: b528bb49-340c-4a81-9c8d-cefce6562f16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9593cfdc08161d3352c59332970aee668a89f4f0
ms.sourcegitcommit: 66407a7248118bb3e167fae76bacaa868b134734
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81727943"
---
# <a name="mssqlserver_9004"></a>MSSQLSERVER_9004
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|9004|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|LOG_CORRUPT|  
|Texto da mensagem|Erro ao processar o log do banco de dados '%.*ls'.  Se possível, restaure do backup. Se não houver um backup disponível, talvez seja necessário recriar o log.|  
  
## <a name="explanation"></a>Explicação  
Ocorreu um erro ao processar o log durante a reversão, a recuperação ou a replicação. Isso pode indicar um erro detectado pelo sistema operacional ou um erro de consistência interno detectado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] executa verificações lógicas na consistência do conteúdo do log de transações conforme faz a leitura e o processamento dele. Nem todos os aspectos do cabeçalho, blocos e registros do log são verificados. O número do Estado fornece mais informações sobre o tipo de falha:

 - **Estado 1** o cabeçalho do arquivo de log do VLF (arquivo de log virtual) foi danificado.  Caso um cabeçalho do arquivo de log danificado seja encontrado ao iniciar o banco de dados na inicialização do serviço, talvez você veja apenas o erro 9004 no LOG DE ERROS. O cabeçalho do arquivo de log é a primeira parte de cada VLF dentro de um log de transações. O cabeçalho do arquivo de log não é o mesmo que o cabeçalho de arquivo único ou os primeiros 8 KB do arquivo de log. Se o cabeçalho do arquivo do arquivo de log estiver danificado, você poderá receber a mensagem 5172, como quando ocorre corrupção do cabeçalho da página de um arquivo do banco de dados.
 - **Estado 2 e 3**  Um bloco de log era inválido ao executar a recuperação durante uma operação RESTORE.
 - **Estado 4 a 12**  São diversas verificações em blocos de log ao processar registros de log. Isso inclui a paridade, o setor e outras verificações lógicas sobre a consistência do log de transações

Na maioria dos casos, esse erro é visto apenas no LOG DE ERROS ou no Log de eventos de aplicativos do Windows com EventID = 9004 porque a operação que processa o log não é baseada em um comando de usuário direto (como a execução da recuperação quando o mecanismo do SQL Server é iniciado). Nessas situações, muitas vezes, o erro 9004 é visto junto com o erro 3414. Porém, algumas consultas, como ALTER DATABASE, podem exigir um processamento do log e, portanto, exibirão esses erros. Como o erro tem severidade = 21, a sessão de usuário está desconectada.

## <a name="cause"></a>Causa
O erro 9004 é um erro geral indicando que o conteúdo do log de transações está danificado. O motivo para o log se tornar inconsistente é semelhante a qualquer problema de corrupção de banco de dados detectado pelo mecanismo do SQL Server. Para encontrar a causa dos danos do log, você deve seguir técnicas semelhantes usadas para banco de dados corrompidos, incluindo uma análise de possíveis problemas de hardware, sistema de arquivos e E/S. Observe que DBCC CHECKDB não verifica o log de transações como parte de suas operações e não pode detectar erros de corrupção de log. O erro 9004 é gerado pelo próprio mecanismo do SQL Server.

## <a name="user-action"></a>Ação do usuário  
Uma das ações seguintes poderá corrigir esse erro:  
  
-   **Restaurar de um backup**:  faça a restauração a partir de um backup válido conhecido para se recuperar desse problema. É possível que, caso a parte de log de um banco de dados ou o backup de log tenha conteúdo danificado, você encontre o erro 9004 em RESTORE. Nessa situação, o log de transações no backup está danificado.
  
-   **Recompilar o log**:  se não for possível restaurar a partir de um backup, você poderá recompilar o log de transações para colocar o banco de dados online. Você deve reconhecer com atenção as ramificações da recompilação do log de transações. Isso inclui a *possível perda de consistência transacional em seu de banco de dados*. Para saber mais sobre como recompilar o log de transações, confira [Resolver erros no modo de emergência do banco de dados](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md#resolving-errors-in-database-emergency-mode).
  
-   **Examinar os logs em busca de problemas do sistema**: confira também o log de eventos do sistema e logs de erros para identificar problemas no sistema que podem ter causado o erro.  
  
