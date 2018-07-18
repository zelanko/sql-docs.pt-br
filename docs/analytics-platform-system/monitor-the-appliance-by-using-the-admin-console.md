---
title: Monitorar com o Console de Admin - Analytics Platform System | Microsoft Docs
description: Para o Analytics Platform System, o Console de administração é um aplicativo web que revela as informações de estado, integridade e desempenho do dispositivo. Os usuários se conectar ao Console do administrador por meio de um navegador da internet.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d094f809052222238806e679e38c6578422fd9aa
ms.sourcegitcommit: 731c5aed039607a8df34c63e780d23a8fac937e1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/07/2018
ms.locfileid: "37909846"
---
# <a name="monitor-the-appliance-with-the-admin-console---analytics-platform-system"></a>Monitorar o dispositivo com o Console de administração - Analytics Platform System
O Console de administração é um aplicativo web do SQL Server PDW que traz à tona as informações de estado, integridade e desempenho do dispositivo. Os usuários se conectar ao Console do administrador por meio do Internet Explorer.  
  
## <a name="About"></a>Sobre o Console de administração  
![Appliance Console Home](./media/monitor-the-appliance-by-using-the-admin-console/SQL_Server_PDW_AdminConsol_ApplHome.png "SQL_Server_PDW_AdminConsol_ApplHome")  
  
**Dispositivo**  
Base  
Fornece um resumo rápido do estado do dispositivo.  
  
Integridade  
Exibe a topologia de dispositivo com indicadores mostrando a integridade de cada componente monitorado dentro de cada nó. Permite que você exiba o status atual de nós individuais e as propriedades dos componentes do nó.  
  
Exibe os alertas de hardware e software.  
  
Monitor de desempenho  
Exibe gráficos do monitor de desempenho.  
  
**Parallel Data Warehouse**  
Base  
Fornece um resumo rápido do estado do PDW.  
  
Sessões  
Exibe as sessões de usuário do Active Directory PDW. Isso pode ajudar para monitoramento de contenção de recursos.  
  
Consultas  
Exibe uma lista de consultas em execução e concluídos recentemente. Ele exibe erros relacionados, se houver. Também fornece a capacidade de exibir os detalhes das informações de execução de consulta execução plano e o nó.  
  
Cargas  
Exibe carregar planos, o estado atual do PDW cargas e erros relacionados, se houver.  
  
Backups/restaurações  
Exibe um log do PDW backup e restaurar operações.  
  
Integridade  
Exibe a topologia do PDW com indicadores mostrando a integridade de cada componente monitorado dentro de cada nó. Permite que você exiba o status atual de nós individuais e as propriedades dos componentes do nó.  
  
Exibe os alertas de hardware e software.  
  
Recursos  
Exibe uma lista de bloqueios de recursos do PDW e seu status atual.  
  
Armazenamento  
Resume a utilização de armazenamento do PDW.  
  
Monitor de desempenho  
Exibe gráficos de monitor de desempenho do PDW.  
 
> [!NOTE]  
> O console de administração tem uma resolução de tela 1024 x 768. O console de administração exibe melhor com uma resolução de tela de 1280 X 1024 ou superior.  
  
## <a name="Connect"></a>Conectar-se ao Console do administrador  
Para se conectar ao Console do administrador, requer:  
  
-   Pelo menos o Internet Explorer versão 10.  
  
-   Permissões para acessar o Console de administração. <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   O endereço IP do cluster de nó de controle.  Para obter isso do administrador do SQL Server PDW.  
  
Para se conectar ao Console do administrador, use o Internet Explorer e https para navegar até o endereço IP do cluster de nó de controle. Por exemplo, se o endereço IP do cluster de nó de controle é `10.192.63.102`, insira `https://10.192.63.102` na barra de endereços do navegador. A primeira tela solicitará sua **LOGIN** e **senha**. Forneça um logon de autenticação do SQL Server e senha, ou um logon de autenticação do Windows e senha do Windows. Se usar um logon de autenticação do Windows, o Console de administração usará a representação.  
  
## <a name="RelatedTasks"></a>Tarefas do Console do administrador  
O Console de administração fornece a capacidade de monitorar o seguinte:  
  
|||  
|-|-|  
|**Tipo de informação**|**Como acessar no Console do administrador**|  
|Status geral do dispositivo|Clique em **estado de dispositivo** no menu superior, ou **Home**.|  
|Alertas|Clique em **alertas**. Para obter mais informações, consulte [Noções básicas sobre alertas do Console de administração &#40;Analytics Platform System&#41;](understanding-admin-console-alerts.md).|  
|Componentes do dispositivo e seu status|Clique em **estado de dispositivo** no menu superior, ou **Home**.|  
|Solicitações de monitor (incluindo consultas, carrega, backups e restaurações)|Clique em **sessões** para ver as sessões atualmente ativas ou mais recentes.<br /><br />Clique em **consultas** para ver as consultas atualmente ativos ou mais recentes. As informações exibidas para consultas incluem cargas, backups e restaurações.<br /><br />Clique em **bloqueios** para ver os bloqueios ativos.|  
|Monitorar as informações adicionais de cargas, backups e restaurações.|Clique em **cargas** ou **Backups/restaurações**.|  
|Informações de desempenho|Clique em **Monitor de desempenho**.|  
  
## <a name="see-also"></a>Consulte também  
[Monitoramento de dispositivo &#40;Analytics Platform System&#41;](appliance-monitoring.md)  
  
