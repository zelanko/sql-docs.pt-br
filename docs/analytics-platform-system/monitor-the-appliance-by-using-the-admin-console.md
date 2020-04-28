---
title: Monitorar com o console de administração
description: Para o Analytics Platform System, o console de administração é um aplicativo Web que mostra as informações de estado, integridade e desempenho do dispositivo. Os usuários se conectam ao console de administração por meio de um navegador da Internet.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 977e38016fbb58356d22ccfc5f783539e5f852d5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74400939"
---
# <a name="monitor-the-appliance-with-the-admin-console---analytics-platform-system"></a>Monitorar o dispositivo com o console do administrador-Analytics Platform System
O console de administração é um aplicativo Web SQL Server PDW que mostra as informações de estado, integridade e desempenho do dispositivo. Os usuários se conectam ao console de administração por meio do Internet Explorer.  
  
## <a name="about-the-admin-console"></a><a name="About"></a>Sobre o console de administração  
![Início do console de dispositivo](./media/monitor-the-appliance-by-using-the-admin-console/SQL_Server_PDW_AdminConsol_ApplHome.png "SQL_Server_PDW_AdminConsol_ApplHome")  
  
**Baseado**  
Home  
Fornece um resumo rápido do estado do dispositivo.  
  
Integridade  
Exibe a topologia do dispositivo com indicadores que mostram a integridade de cada componente monitorado em cada nó. Permite exibir o status atual de nós individuais e propriedades dos componentes do nó.  
  
Exibe alertas de hardware e software.  
  
Monitor de desempenho  
Exibe grafos do monitor de desempenho.  
  
**Parallel Data Warehouse**  
Home  
Fornece um resumo rápido do estado do PDW.  
  
Sessões  
Exibe sessões de usuário do PDW ativo. Isso pode ajudar a monitorar a contenção de recursos.  
  
Consultas  
Exibe uma lista de consultas em execução e consultas concluídas recentemente. Ele exibirá erros relacionados, se houver. Também fornece a capacidade de exibir detalhes do plano de execução de consulta e das informações de execução do nó.  
  
Cargas  
Exibe os planos de carga, o estado atual das cargas do PDW e os erros relacionados, se houver.  
  
Backups/restaurações  
Exibe um log de operações de backup e restauração do PDW.  
  
Integridade  
Exibe a topologia do PDW com indicadores que mostram a integridade de cada componente monitorado em cada nó. Permite exibir o status atual de nós individuais e propriedades dos componentes do nó.  
  
Exibe alertas de hardware e software.  
  
Recursos  
Exibe uma lista de bloqueios de recursos do PDW e seu status atual.  
  
Armazenamento  
Resume a utilização do armazenamento do PDW.  
  
Monitor de desempenho  
Exibe grafos do monitor de desempenho do PDW.  
 
> [!NOTE]  
> O console de administração tem uma resolução de tela de 1024x768. O console de administração do exibe melhor com uma resolução de tela de 1280 X 1024 ou superior.  
  
## <a name="connect-to-the-admin-console"></a><a name="Connect"></a>Conectar-se ao console de administração  
Para se conectar ao console de administração, o requer:  
  
-   Pelo menos o Internet Explorer versão 10.  
  
-   Permissões para acessar o console de administração. <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   O endereço IP do cluster do nó de controle.  Obtenha isso do seu administrador de SQL Server PDW.  
  
Para se conectar ao console de administração, use o Internet Explorer e o HTTPS para navegar até o endereço IP do cluster do nó de controle. Por exemplo, se o endereço IP do cluster do nó de controle `10.192.63.102`for, `https://10.192.63.102` insira na barra de endereços do navegador. A primeira tela solicitará seu **logon** e **senha**. Forneça um logon de autenticação SQL Server e uma senha, ou um logon de autenticação do Windows e uma senha do Windows. Se você estiver usando um logon de autenticação do Windows, o console de administração usará a representação.  
  
## <a name="admin-console-tasks"></a><a name="RelatedTasks"></a>Tarefas do console de administração  
O console de administração do fornece a capacidade de monitorar o seguinte:  
  
|||  
|-|-|  
|**Tipo de informação**|**Como acessar no console de administração**|  
|Status geral do dispositivo|Clique em **estado do dispositivo** no menu superior ou em **página inicial**.|  
|Alertas|Clique em **Alertas**. Para obter mais informações, consulte [Understanding admin console alerts &#40;Analytics Platform System&#41;](understanding-admin-console-alerts.md).|  
|Componentes do dispositivo e seu status|Clique em **estado do dispositivo** no menu superior ou em **página inicial**.|  
|Monitorar solicitações (incluindo consultas, carregamentos, backups e restaurações)|Clique em **sessões** para ver as sessões atualmente ativas ou recentes.<br /><br />Clique em **consultas** para ver as consultas atualmente ativas ou recentes. As informações exibidas para consultas incluem cargas, backups e restaurações.<br /><br />Clique em **bloqueios** para ver os bloqueios ativos.|  
|Monitore informações adicionais para cargas, backups e restaurações.|Clique em **cargas** ou **backups/restaurações**.|  
|Informações de desempenho|Clique em **Monitor de desempenho**.|  
  
## <a name="see-also"></a>Consulte Também  
[Monitoramento de dispositivo &#40;o sistema de plataforma de análise&#41;](appliance-monitoring.md)  
  
