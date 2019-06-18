---
title: SQL Server, objeto Estatística de SQL| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:SQL Statistics
- SQL Statistics object
ms.assetid: da7dbb4b-f632-45a0-b1ab-c35cc2695c86
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: 1a1218e5d27abd72acef7967e0a71284384fed89
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62629144"
---
# <a name="sql-server-sql-statistics-object"></a>SQL Server, objeto SQL Statistics
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O objeto **SQLServer:SQL Statistics** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece contadores para monitorar a compilação e o tipo de solicitações enviadas a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A monitoração do número de compilações e recompilações de consultas e do número de lotes recebidos por uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece uma indicação da velocidade com que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está processando as consultas do usuário e o grau de eficácia com que o otimizador de consulta está processando as consultas.  
  
 Compilação é uma parte significativa do tempo de retorno de uma consulta. Para economizar no custo da compilação, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] salva o plano de consulta compilado em um cache de consulta. O objetivo do cache é reduzir a compilação por meio do armazenamento das consultas compiladas para reutilização posterior encerrando, assim, a solicitação para recompilar consultas quando forem executadas mais tarde. Porém, cada consulta exclusiva deve ser compilada pelo menos uma vez. Recompilações de consultas podem ser causadas pelos seguintes fatores:  
  
-   Alterações do esquema, inclusive alterações no esquema de base, como adição de colunas ou índices a uma tabela, ou alterações no esquema de estatística, como inserção ou exclusão de um número significativo de linhas de uma tabela.  
  
-   Alterações de ambiente (instrução SET). Alterações em configurações de sessão como ANSI_PADDING ou ANSI_NULLS podem fazer com que uma consulta seja recompilada.  
  
 Para obter mais informações sobre parametrização simples e forçada, consulte [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
 Esses são os contadores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **SQL Statistics**.  
  
|Contadores do SQL Server SQL Statistics|Descrição|  
|----------------------------------------|-----------------|  
|**Tentativas de Param. Autom./s**|Número de tentativas de parametrização automática por segundo. O total deve ser a soma das parametrizações automáticas que falharam, seguras e inseguras. A parametrização automática ocorre quando uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenta parametrizar uma solicitação do [!INCLUDE[tsql](../../includes/tsql-md.md)] substituindo alguns literais por parâmetros de modo a permitir a reutilização do plano de execução resultante armazenado em cache em várias solicitações que parecem semelhantes. Observe que as parametrizações automáticas também são conhecidas como parametrizações simples em versões mais novas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esse contador não inclui parametrizações forçadas.|  
|**Solicitações em Lote/s**|Número de lotes de comando [!INCLUDE[tsql](../../includes/tsql-md.md)] recebidos por segundo. Essa estatística é afetada por todas as restrições (tais como E/S, número de usuários, tamanho do cache, complexidade das solicitações etc.). Altas solicitações em lote significam uma boa taxa de transferência.|  
|**Param Autom. com Falha/s**|Número de tentativas de parametrização automática com falhas por segundo. Esse número deve ser pequeno. Observe que as parametrizações automáticas também são conhecidas como parametrizações simples em versões posteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Parametrizações Forçadas/s**|Número de parametrizações forçadas com êxito por segundo.|  
|**Execuções de Planos Guiados/s**|Número de execuções de plano por segundo no qual o plano de consulta foi gerado usando guia de plano.|  
|**Execuções de Planos Extraviados/s**|Número de execuções de plano por segundo no qual uma guia de plano não pôde ser honrada durante geração de plano. A guia de plano foi desconsiderada e a compilação normal foi usada para gerar o plano executado.|  
|**Param. Autom. Seguras/s**|Número de tentativas de parametrizações automáticas seguras por segundo. Segura refere-se a uma determinação de que um plano de execução armazenado em cache pode ser compartilhado entre diferentes instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] que parecem ser semelhantes. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] faz diversas tentativas de parametrização automática, algumas que demonstram ser seguras e outras que apresentam falhas. Observe que as parametrizações automáticas também são conhecidas como parametrizações simples em versões posteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Isso não inclui parametrizações forçadas.|  
|**Taxa de Atenção do SQL**|Número de atenções por segundo. Uma atenção é uma solicitação feita pelo cliente para encerrar a solicitação que está sendo executada no momento.|  
|**Compilações de SQL/s**|Número de compilações de SQL por segundo. Indica o número de vezes que o caminho do código de compilação é digitado. Inclui compilações causadas por recompilações do nível de instrução em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Depois que a atividade de usuário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver estável, esse valor alcança um estado fixo.|  
|**Recompilações de SQL/s**|Número de recompilações de instruções por segundo. Conta o número de vezes que as recompilações de instrução são acionadas. Geralmente é preferível que as recompilações sejam baixas.|  
|**Param. Autom. sem segurança/s**|Número de tentativas de parametrização automática não segura por segundo. Por exemplo, a consulta tem algumas características que impedem o plano armazenado em cache de ser compartilhado. Esses são designados como inseguros. Isso não conta o número de parametrizações forçadas.|  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server, objeto Cache de planos](../../relational-databases/performance-monitor/sql-server-plan-cache-object.md)   
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
