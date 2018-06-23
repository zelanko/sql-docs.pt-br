---
title: Propriedades do banco de dados (página Repositório de Consultas) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.databaseproperties.querystore.f1
ms.assetid: da47d75e-291a-4305-acef-4b0aaf5215da
caps.latest.revision: 8
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 4ab58b6fedbf00bfc6f7bf981ca51ca7e7c4087e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008661"
---
# <a name="database-properties-query-store-page"></a>Propriedades do banco de dados (página Repositório de Consultas)
  Acesse esta página do banco de dados principal e use-a para configurar e modificar as propriedades do repositório de consultas do banco de dados. Essas opções também podem ser configuradas usando as opções [ALTER DATABASE SET](/sql/t-sql/statements/alter-database-transact-sql-set-options). Para obter informações sobre repositório de consultas, veja [Monitoring Performance By Using the Query Store](../performance/monitoring-performance-by-using-the-query-store.md).  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].|  
  
## <a name="options"></a>Opções  
 Habilitar  
 Habilita e desabilita o repositório de consultas.  
  
 Modo de Operação  
 Os valores válidos são READ_ONLY e READ_WRITE. No modo READ_WRITE, o repositório de consultas coleta e persiste as informações das estatísticas de execução do plano de consulta e do tempo de execução. No modo READ_ONLY, as informações podem ser lidas do repositório de consultas, mas novas informações não são adicionadas. Se o espaço máximo alocado do repositório de consultas tiver se esgotado, o repositório de consultas alterará o modo de operação para READ_ONLY.  
  
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
  
 Limite de Consulta Obsoleto (Dias)  
 Obtém e define o limite de consulta obsoleto. Configure o argumento STALE_QUERY_THRESHOLD_DAYS para especificar o número de dias que os dados devem ser mantidos no repositório de consultas.  
  
 Limpar Dados da Consulta  
 Remove o conteúdo do repositório de consultas.  
  
 Gráficos de pizza  
 O gráfico da esquerda mostra o consumo total do arquivo de banco de dados no disco e a parte do arquivo que é preenchida com os dados do repositório de consultas.  
  
 O gráfico à direita mostra a parte da cota do repositório de consultas usada no momento. Observe que a cota não é mostrada no gráfico à esquerda. A cota pode exceder o tamanho atual do banco de dados.  
  
## <a name="remarks"></a>Remarks  
 O recurso repositório de consultas fornece aos DBAs insights sobre escolha e desempenho do plano de consulta. Ele simplifica a solução de problemas, permitindo que você localize rapidamente diferenças de desempenho causadas por alterações nos planos de consulta. O recurso captura automaticamente um histórico de consultas, planos e estatísticas de tempo de execução e os mantém para sua análise. Ele separa os dados por janelas de tempo, permitindo que você veja os padrões de uso do banco de dados e entenda quando as alterações aos planos de consulta ocorreram no servidor. O repositório de consultas pode ser configurado usando essa página de propriedades do banco de dados do repositório de consultas, ou usando a opção [ALTER DATABASE SET](/sql/t-sql/statements/alter-database-transact-sql-set-options) . O repositório de consultas apresenta informações usando uma caixa de diálogo do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] . Para obter mais informações sobre o repositório de consultas, veja [Monitoring Performance By Using the Query Store](../performance/monitoring-performance-by-using-the-query-store.md).  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do Repositório de Consultas &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql)   
 [Exibições de catálogo do repositório de consultas &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/query-store-catalog-views-transact-sql)  
  
  
