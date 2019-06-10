---
title: Histórico de espelhamento de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.dbmmonitor.databasemirroringhistory.f1
ms.assetid: 1d6e4b10-4a23-47d7-9918-c417992f09d3
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: a20b27bd5a3c8b22171bf61ef6ebfda2725c5fc0
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66774691"
---
# <a name="database-mirroring-history"></a>Histórico do espelhamento de banco de dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use essa caixa de diálogo para exibir o histórico de status de espelhamento de um banco de dados espelho em uma instância de servidor especificada.  
  
 **Para usar o SQL Server Management Studio para monitorar o espelhamento de banco de dados**  
  
-   [Iniciar o Monitor de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
## <a name="options"></a>Opções  
 **Instância de servidor**  
 Nome da instância de servidor a partir da qual o histórico está sendo informado.  
  
 **Backup de banco de dados**  
 Nome do banco de dados cujo histórico está sendo informado.  
  
 **Filtrar lista por**  
 Lista valores de filtro. A escolha de um novo valor atualiza a grade automaticamente.  
  
 Os possíveis valores de filtro são:  
  
-   Últimas duas horas  
  
-   Últimas quatro horas  
  
-   Últimas oito horas  
  
-   Último dia  
  
-   Últimos dois dias  
  
-   Últimos 100 registros  
  
-   Últimos 500 registros  
  
-   Últimos 1000 registros  
  
-   Todos os registros  
  
 **Atualizar**  
 Clique para atualizar a lista de histórico.  
  
> [!NOTE]  
>  Esta caixa de diálogo não atualiza a lista de histórico automaticamente. Para atualizar a lista, clique em **Atualizar** ou escolha outra opção de filtro. Somente membros da função de servidor fixa **sysadmin** podem atualizar o histórico de espelhamento.  
  
 **Histórico**  
 Exibe a lista de histórico. Clique em um cabeçalho de coluna para classificar a grade por essa coluna. A lista contém as seguintes colunas:  
  
|Nome da coluna|Descrição|  
|-----------------|-----------------|  
|**Hora registrada**|Carimbo de data/hora da linha do histórico.|  
|**Função**|Função de espelhamento atual da instância de servidor deste banco de dados, Principal ou Espelho.|  
|**Estado de Espelhamento**|Estado do banco de dados:<br /><br /> Desconectado<br /><br /> Failover pendente<br /><br /> Suspenso<br /><br /> Sincronizado<br /><br /> Sincronizando<br /><br /> Unknown (desconhecido)|  
|**Conexão de Testemunha**|Estado da conexão de testemunha na sessão de espelhamento de banco de dados, Conectado ou Desconectado. Se não houver nenhum servidor testemunha, o valor será NULL.|  
|**Log Não Enviado**|Tamanho, em quilobytes (KB), do log não enviado na fila de envio da instância de servidor principal.|  
|**Tempo para Envio**|Tempo aproximado exigido pela instância de servidor principal para enviar o log atualmente na fila de envio para a instância de servidor espelho (a *taxa de envio*). Como a taxa de transações de entrada pode variar significativamente, a hora para enviar o log é uma estimativa. A taxa de envio, porém, pode ser útil para estimar aproximadamente a hora exigida para um failover manual.|  
|**Send Rate**|Taxa em que as transações estão sendo enviadas à instância de servidor espelho, em KB por segundo.|  
|**Nova Taxa de Transação**|Taxa em que as transações de entrada estão sendo inseridas no log do servidor principal, em KB por segundo. Para determinar se o espelhamento está atrasado, acompanhando ou atualizado, compare esse valor ao valor do **Tempo para Envio** .|  
|**Transação Não Enviada Mais Antiga**|Idade da transação não enviada mais antiga na fila de envio. A idade dessa transação indica quantos minutos de transações ainda não foram enviados à instância de servidor espelho. Esse valor ajuda a medir o potencial de perda de dados em termos de tempo.|  
|**Log Não Restaurado**|A quantidade de log em espera na fila de restauração, em quilobytes (KB).|  
|**Tempo para Recuperar**|Número aproximado de minutos exigido para que o log atualmente na fila de restauração seja aplicado ao banco de dados espelho.|  
|**Taxa de Recuperação**|Taxa em que as transações estão sendo recuperadas no banco de dados espelho, em KB por segundo.|  
|**Sobrecarga Espelhada Confirmada**|Atraso médio por transação em milissegundos (somente em modos síncronos). Esse atraso consiste na quantidade de sobrecarga incidente enquanto a instância do servidor principal aguarda que a instância do servidor espelho grave o registro do log da transação na fila de restauração.|  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar o Monitor de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [Monitorando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [Iniciar o Assistente para Configurar Segurança de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
  
