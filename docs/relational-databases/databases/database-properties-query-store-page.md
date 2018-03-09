---
title: "Propriedades do banco de dados (página Repositório de Consultas) | Microsoft Docs"
ms.custom: 
ms.date: 11/09/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.databaseproperties.querystore.f1
ms.assetid: da47d75e-291a-4305-acef-4b0aaf5215da
caps.latest.revision: "10"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 903eb21e82dc2b5e3a04f0b48b4f17365a0eac99
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="database-properties-query-store-page"></a>Propriedades do banco de dados (página Repositório de Consultas)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Acesse esta página do banco de dados principal e use-a para configurar e modificar as propriedades do repositório de consultas do banco de dados. Essas opções também podem ser configuradas usando as opções [ALTER DATABASE SET](../../t-sql/statements/alter-database-transact-sql-set-options.md). Para obter informações sobre repositório de consultas, veja [Monitoring Performance By Using the Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md).  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].|  
  
## <a name="options"></a>Opções  
 Modo de Operação  
 Os valores válidos são OFF, READ_ONLY e READ_WRITE. OFF desabilita o Repositório de Consultas. No modo READ_WRITE, o repositório de consultas coleta e persiste as informações das estatísticas de execução do plano de consulta e do tempo de execução. No modo READ_ONLY, as informações podem ser lidas do repositório de consultas, mas novas informações não são adicionadas. Se o espaço máximo alocado do repositório de consultas tiver se esgotado, o repositório de consultas alterará o modo de operação para READ_ONLY.  
  
 Modo de Operação (Real)  
 Descreve o modo de operação do repositório de consultas.  
  
 Modo de Operação (Solicitado)  
 Obtém e define o modo de operação desejado do repositório de consultas.  
  
 Intervalo de Limpeza de Dados (Minutos)  
 Determina a frequência na qual os dados gravados no repositório de consultas é persistida no disco. Para otimizar o desempenho, os dados coletados pelo repositório de consultas são gravados de maneira assíncrona no disco. A frequência em que essa transferência assíncrona ocorre é configurada.  
  
 Intervalo de Coleta de Estatísticas  
 Obtém e define o valor do intervalo da coleta de estatísticas.  
  
 Tamanho Máximo (MB)  
 Obtém e define o espaço total alocado para o repositório de consultas.  
  
 Modo de captura do Repositório de Consultas  
 -   Nenhum não captura novas consultas.  
  
-   Todos captura todas as consultas.  
  
-   Auto captura consultas com base no consumo de recursos.  
  
 Limite de Consulta Obsoleto (Dias)  
 Obtém e define o limite de consulta obsoleto. Configure o argumento STALE_QUERY_THRESHOLD_DAYS para especificar o número de dias que os dados devem ser mantidos no repositório de consultas.  
  
 Limpar Dados da Consulta  
 Remove o conteúdo do repositório de consultas.  
  
 Gráficos de pizza  
 O gráfico da esquerda mostra o consumo total do arquivo de banco de dados no disco e a parte do arquivo que é preenchida com os dados do repositório de consultas.  
  
 O gráfico à direita mostra a parte da cota do repositório de consultas usada no momento. Observe que a cota não é mostrada no gráfico à esquerda. A cota pode exceder o tamanho atual do banco de dados.  
  
## <a name="remarks"></a>Remarks  
 O recurso repositório de consultas fornece aos DBAs insights sobre escolha e desempenho do plano de consulta. Ele simplifica a solução de problemas, permitindo que você localize rapidamente diferenças de desempenho causadas por alterações nos planos de consulta. O recurso captura automaticamente um histórico de consultas, planos e estatísticas de tempo de execução e os mantém para sua análise. Ele separa os dados por janelas de tempo, permitindo que você veja os padrões de uso do banco de dados e entenda quando as alterações aos planos de consulta ocorreram no servidor. O repositório de consultas pode ser configurado usando essa página de propriedades do banco de dados do repositório de consultas, ou usando a opção [ALTER DATABASE SET](../../t-sql/statements/alter-database-transact-sql-set-options.md) . O repositório de consultas apresenta informações usando uma caixa de diálogo do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] . Para obter mais informações sobre o repositório de consultas, veja [Monitoring Performance By Using the Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do repositório de consultas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [Exibições de catálogo do repositório de consultas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)  
  
  
