---
title: Práticas recomendadas para filtros de linha com base em hora | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- best practices
ms.assetid: 773c5c62-fd44-44ab-9c6b-4257dbf8ffdb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 70fb66a1b61dbbdec0fd8443ac150b32c3770818
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48145516"
---
# <a name="best-practices-for-time-based-row-filters"></a>Práticas recomendadas para filtros de linha baseados em tempo
  Usuários de aplicativos requerem frequentemente um subconjunto de dados baseados no tempo de uma tabela. Por exemplo, um vendedor pode requisitar dados de pedidos da semana passada ou um organizador de eventos pode requisitar dados para os eventos da semana seguinte. Em muitos casos, os aplicativos usam consultas que contêm a função `GETDATE()` para realizar isso. Considere a seguinte instrução de filtro de linha:  
  
```  
WHERE SalesPersonID = CONVERT(INT,HOST_NAME()) AND OrderDate >= (GETDATE()-6)  
```  
  
 Com um filtro desse tipo, é normalmente presumido que duas coisas sempre ocorram quando o Merge Agent é executado: as linhas que satisfazem esse filtro são replicadas aos Assinantes; e linhas que não mais satisfazem esse filtro, são limpas nos Assinantes. (Para obter mais informações sobre a filtragem com `HOST_NAME()`, consulte [Parameterized Row Filters](parameterized-filters-parameterized-row-filters.md).) Entretanto, a replicação de mesclagem apenas replica e limpa os dados que foram alterados desde a última sincronização, independentemente de como você defina o filtro de linha para aqueles dados.  
  
 Para a replicação de mesclagem processar uma linha, os dados na linha devem satisfazer o filtro de linha e devem ter sido alterados desde a última sincronização. No caso da tabela **SalesOrderHeader** , é inserido **OrderDate** quando uma linha é inserida. As linhas são replicadas ao Assinante como esperado porque a inserção é uma alteração de dados. Entretanto, se houver linhas no Assinante que não mais satisfazem o filtro (são para pedidos anteriores a sete dias), elas não serão removidas do Assinante a menos que tenham sido atualizadas por algum outro motivo.  
  
 O caso do organizador de eventos destaca mais o assunto com este tipo de filtragem. Considere o seguinte filtro para uma tabela **Eventos** :  
  
```  
WHERE EventCoordID = CONVERT(INT,HOST_NAME()) AND EventDate <= (GETDATE()+6)  
```  
  
 Para uma tabela que contém eventos, inserções poderiam ser feitas bem antes da data de evento. Se uma inserção para um evento na próxima semana foi feita um mês atrás e a linha não foi atualizada por algum outro motivo, a linha não será replicada ao Assinante mesmo se satisfizer o filtro de linha.  
  
 Além disso, dependendo de como a publicação é configurada, a replicação de mesclagem avalia filtros em momentos diferentes:  
  
-   Se uma publicação usar partições pré-computadas (o padrão), os filtros serão avaliados quando uma linha for inserida ou atualizada.  
  
-   Se a publicação não usar partições pré-computadas, os filtros serão avaliados quando o Merge Agent for executado.  
  
 Para obter mais informações sobre partições pré-computadas, consulte [Otimizar o desempenho de filtro com parâmetros com partições pré-computadas](parameterized-filters-optimize-for-precomputed-partitions.md). A hora em que o filtro é avaliado afeta quais dados satisfazem o filtro. Por exemplo, se uma publicação usa partições pré-computadas, e você sincronizar os dados a cada dois dias, o subconjunto de dados para o vendedor poderia incluir linhas dois dias antes do esperado.  
  
## <a name="recommendations-for-using-time-based-row-filters"></a>Recomendações para usar filtros de linha baseados em tempo  
 O método seguinte fornece uma abordagem robusta e direta para filtragem baseada em tempo:  
  
-   Adicionar uma coluna à tabela do tipo de dados `bit`. Esta coluna é usada para indicar se uma linha deveria ser replicada.  
  
-   Use um filtro de linha que faz referência à nova coluna em lugar de uma coluna baseada no tempo.  
  
-   Crie um trabalho do SQL Server Agent (ou um trabalho agendada por algum outro mecanismo) que atualiza a coluna antes do agendamento para a execução do Merge Agent.  
  
 Essa abordagem trata das falhas usando `GETDATE()` ou outro método baseado em tempo e evita o problema em determinar quando os filtros são avaliados por partições. Considere o seguinte exemplo para uma tabela **Eventos** :  
  
|**EventID**|**EventName**|**EventCoordID**|**EventDate**|**Replicar**|  
|-----------------|-------------------|----------------------|-------------------|-------------------|  
|1|Recepção|112|2006-10-04|1|  
|2|Jantar|112|2006-10-10|0|  
|3|Festa|112|2006-10-11|0|  
|4|Casamento|112|2006-10-12|0|  
  
 O filtro de linha para esta tabela teria essa aparência:  
  
```  
WHERE EventCoordID = CONVERT(INT,HOST_NAME()) AND Replicate = 1  
```  
  
 O trabalho do SQL Server Agent poderia executar instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)] semelhante para o próximo antes de cada execução do Merge Agent:  
  
```  
UPDATE Events SET Replicate = 0 WHERE Replicate = 1  
GO  
UPDATE Events SET Replicate = 1 WHERE EventDate <= GETDATE()+6  
GO  
```  
  
 A primeira linha redefine a coluna **Replicar** para **0**, e a segunda linha define a coluna para **1** para eventos que ocorram nos próximos sete dias. Se esta instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] for executada em 10/07/2006, a tabela será atualizada para:  
  
|**EventID**|**EventName**|**EventCoordID**|**EventDate**|**Replicar**|  
|-----------------|-------------------|----------------------|-------------------|-------------------|  
|1|Recepção|112|2006-10-04|0|  
|2|Jantar|112|2006-10-10|1|  
|3|Festa|112|2006-10-11|1|  
|4|Casamento|112|2006-10-12|1|  
  
 Os eventos para a próxima semana estão sinalizados agora como estando prontos para serem replicados. A próxima vez que o Merge Agent for executado para a assinatura que o coordenador de eventos 112 usa, as linhas 2,3 e 4 serão baixadas para o Assinante e a linha 1 será removida do Assinante.  
  
## <a name="see-also"></a>Consulte também  
 [GETDATE &#40;Transact-SQL&#41;](/sql/t-sql/functions/getdate-transact-sql)   
 [Implementar trabalhos](../../../ssms/agent/implement-jobs.md)   
 [Parameterized Row Filters](parameterized-filters-parameterized-row-filters.md)  
  
  
