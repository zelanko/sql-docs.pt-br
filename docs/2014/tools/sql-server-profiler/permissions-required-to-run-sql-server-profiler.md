---
title: Permissões necessárias para executar o SQL Server Profiler | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Profiler [SQL Server Profiler], permissions
- traces [SQL Server], replaying
- replaying traces
- SQL Server Profiler, permissions
- security [SQL Server], SQL Server Profiler
ms.assetid: 5c580a87-88ae-4314-8fe1-54ade83f227f
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 981305998f4526f10accfd7a4787a6854c6c910d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008798"
---
# <a name="permissions-required-to-run-sql-server-profiler"></a>Permissões necessárias para executar o SQL Server Profiler
  Por padrão, executar o [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] requer as mesmas permissões de usuário que os procedimentos armazenados Transact-SQL utilizados para criar rastreamentos. Para executar o [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)], os usuários devem dispor da permissão ALTER TRACE. Para obter mais informações, veja [Permissões GRANT do servidor &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-server-permissions-transact-sql).  
  
> [!IMPORTANT]  
>  Os usuários que tiverem a permissão SHOWPLAN, ALTER TRACE ou VIEW SERVER STATE poderão exibir consultas capturadas na saída do Plano de Execução. Essas consultas podem conter informações confidenciais, como senhas. Portanto, é recomendável que você somente conceda essas permissões a usuários autorizados a exibir informações confidenciais, como membros da função de banco de dados fixa db_owner, ou membros da função de servidor fixa sysadmin. Além disso, também é recomendável somente salvar arquivos do Plano de Execução ou arquivos de rastreamento que contenham eventos relacionados ao Plano de Execução em um local que use o sistema de arquivos NTFS e restringir o acesso a usuários autorizados a exibir informações confidenciais.  
  
## <a name="permissions-used-to-replay-traces"></a>Permissões usadas para repetir rastreamentos  
 Repetir rastreamentos também requer que o usuário responsável disponha da permissão ALTER TRACE.  
  
 No entanto, durante a repetição, o [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] usará o comando EXECUTE AS se um evento Audit Login for encontrado no rastreamento que está sendo repetido. O [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] usa o comando EXECUTE AS para representar o usuário associado ao evento de logon.  
  
 Se o [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] encontrar um evento de logon em um rastreamento que está sendo repetido, serão realizadas as seguintes verificações de permissão:  
  
1.  O Usuário1, que tem a permissão ALTER TRACE, inicia a repetição de um rastreamento.  
  
2.  Um evento de logon para o Usuário2 é encontrado no rastreamento que está sendo repetido.  
  
3.  O [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] usa o comando EXECUTE AS para representar o Usuário2.  
  
4.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenta autenticar User2 e, dependendo dos resultados, uma destas situações ocorrerá:  
  
    1.  Se o Usuário2 não puder ser autenticado, o [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] retornará um erro e continuará repetindo o rastreamento como Usuário1.  
  
    2.  Se o Usuário2 for autenticado com êxito, a repetição do rastreamento continua como Usuário2.  
  
5.  As permissões do Usuário2 são verificadas no banco de dados de destino e, dependendo dos resultados, uma destas situações ocorrerá:  
  
    1.  Se o Usuário2 tiver permissões no banco de dados de destino, a representação tem êxito e o rastreamento é repetido como Usuário2.  
  
    2.  Se o Usuário2 não tiver permissões no banco de dados de destino, o servidor buscará um usuário Convidado naquele banco de dados.  
  
6.  A existência de um usuário Convidado é verificada no banco de dados de destino e, dependendo dos resultados, uma destas situações ocorrerá:  
  
    1.  Se existir uma conta Convidado, o rastreamento é repetido como a conta Convidado.  
  
    2.  Se não existir conta Convidado no banco de dados de destino, é retornado um erro e o rastreamento é repetido como Usuário1.  
  
 O diagrama a seguir mostra esse processo de verificação de permissões durante a repetição de rastreamentos:  
  
 ![Permissões de rastreamento do SQL Server Profiler replay](../../database-engine/media/replaytracedecisiontree.gif "permissões de rastreamento de reprodução do SQL Server Profiler")  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do SQL Server Profiler &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql)   
 [Repetir rastreamentos](replay-traces.md)   
 [Criar um rastreamento &#40;SQL Server Profiler&#41;](create-a-trace-sql-server-profiler.md)   
 [Repetir uma tabela de rastreamento &#40;SQL Server Profiler&#41;](replay-a-trace-table-sql-server-profiler.md)   
 [Reproduzir um arquivo de rastreamento &#40;SQL Server Profiler&#41;](replay-a-trace-file-sql-server-profiler.md)  
  
  
