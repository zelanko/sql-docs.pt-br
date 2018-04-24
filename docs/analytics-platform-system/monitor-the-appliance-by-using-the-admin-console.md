---
title: Monitor com o Console de Admin - Analytics Platform System | Microsoft Docs
description: Para Analytics Platform System, o Console de administração é um aplicativo da web que revela as informações de estado, integridade e desempenho do dispositivo. Os usuários se conectar ao Console do administrador por meio de um navegador da internet.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5f7c6ef68a8f91121a63def8e2153a5c38873aa3
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/19/2018
---
# <a name="monitor-the-appliance-with-the-admin-console---analytics-platform-system"></a>Monitorar o dispositivo com o Console de administração - Analytics Platform System
O Console de administração é um aplicativo web SQL Server PDW que revela as informações de estado, integridade e desempenho do dispositivo. Os usuários se conectar ao Console do administrador por meio do Internet Explorer.  
  
## <a name="About"></a>Sobre o Console de administração  
![Appliance Console Home](./media/monitor-the-appliance-by-using-the-admin-console/SQL_Server_PDW_AdminConsol_ApplHome.png "SQL_Server_PDW_AdminConsol_ApplHome")  
  
**Dispositivo**  
Base  
Fornece um resumo rápido do estado do dispositivo.  
  
Integridade  
Exibe a topologia de aplicativo com indicadores que mostram a integridade de cada componente monitorado em cada nó. Permite que você exiba o status atual de nós individuais e as propriedades dos componentes do nó.  
  
Exibe os alertas de hardware e software.  
  
Monitor de desempenho  
Exibe gráficos de monitor de desempenho.  
  
**Parallel Data Warehouse**  
Base  
Fornece um resumo rápido do estado do PDW.  
  
Sessões  
Exibe sessões de usuário ativas do PDW. Isso pode ajudar para monitoramento de contenção de recursos.  
  
Consultas  
Exibe uma lista de consultas em execução e concluídos recentemente. Ele exibe erros relacionados, se houver. Também fornece a capacidade de exibir os detalhes das informações de execução de consulta execução plano e o nó.  
  
Carrega  
Exibe carregar planos, o estado atual do PDW carrega e erros relacionados, se houver.  
  
Backups/restaurações  
Exibe um log do PDW backup e restaurar operações.  
  
Integridade  
Exibe a topologia do PDW com indicadores que mostram a integridade de cada componente monitorado em cada nó. Permite que você exiba o status atual de nós individuais e as propriedades dos componentes do nó.  
  
Exibe os alertas de hardware e software.  
  
Recursos  
Exibe uma lista de bloqueios de recursos do PDW e seu status atual.  
  
Armazenamento  
Resume o uso do armazenamento PDW.  
  
Monitor de desempenho  
Exibe gráficos de monitor de desempenho do PDW.  
  
**HDInsight**  
Base  
Fornece um resumo rápido do estado do HDInsight.  
  
HDFS  
Resume a utilização de espaço de HDInsight e lista os principais consumidores de espaço de 10.  
  
Mapeamento/redução  
Resume o status dos trabalhos de MapReduce.  
  
Integridade  
Exibe a topologia de HDInsight com indicadores que mostram a integridade de cada componente monitorado em cada nó. Permite que você exiba o status atual de nós individuais e as propriedades dos componentes do nó.  
  
Exibe os alertas de hardware e software.  
  
Armazenamento  
Resume a utilização de armazenamento do HDInsight.  
  
Monitor de desempenho  
Exibe gráficos de monitor de desempenho.  
  
> [!NOTE]  
> O console de administração tem uma resolução de tela de 1024 x 768. O console de administração exibe melhor com uma resolução de tela de 1280 X 1024 ou superior.  
  
## <a name="Connect"></a>Conecte-se ao Console do administrador  
Para se conectar ao Console do administrador, requer:  
  
-   Ao menos o Internet Explorer versão 10.  
  
-   Permissões para acessar o Console de administração. <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   O endereço IP do cluster de nó de controle.  Obter isso do administrador do SQL Server PDW.  
  
Para se conectar ao Console do administrador, use o Internet Explorer e https para navegar até o endereço IP do cluster de nó de controle. Por exemplo, se o endereço IP do cluster de nó de controle é `10.192.63.102`, digite `https://10.192.63.102` na barra de endereços do navegador. A primeira tela solicitará sua **LOGIN** e **senha**. Forneça um logon de autenticação do SQL Server e senha, ou um logon de autenticação do Windows e senha do Windows. Se usar um logon de autenticação do Windows, o Console de administração usará a representação.  
  
## <a name="RelatedTasks"></a>Tarefas do Console do administrador  
O Console do administrador fornece a capacidade de monitorar o seguinte:  
  
|||  
|-|-|  
|**Tipo de informação**|**Como acessar no Console do administrador**|  
|Status geral do dispositivo|Clique em **dispositivo estado** no menu superior, ou **início**.|  
|Alertas|Clique em **alertas**. Para obter mais informações, consulte [Noções básicas sobre alertas do Console de administração &#40;Analytics Platform System&#41;](understanding-admin-console-alerts.md).|  
|Componentes do dispositivo e seu status|Clique em **dispositivo estado** no menu superior, ou **início**.|  
|Solicitações de monitor (incluindo consultas, cargas, backups e restaurações)|Clique em **sessões** para ver as sessões atualmente ativas ou recentes.<br /><br />Clique em **consultas** para ver as consultas atualmente ativas ou mais recentes. As informações exibidas para consultas incluem cargas, backups e restaurações.<br /><br />Clique em **bloqueios** para ver os bloqueios ativos.|  
|Monitorar as informações adicionais para cargas, backups e restaurações.|Clique em **cargas** ou **Backups/restaurações**.|  
|Informações de desempenho|Clique em **Monitor de desempenho**.|  
  
## <a name="see-also"></a>Consulte também  
[Monitoramento de dispositivo &#40;Analytics Platform System&#41;](appliance-monitoring.md)  
  
