---
title: Monitorar com o SCOM - Analytics Platform System | Microsoft Docs
description: Use o System Center Operations Manager (SCOM) para monitorar o dispositivo do Analytics Platform System (APS).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 3c43734dbd7ef1a766f3f1258f97565ab82e175d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62639863"
---
# <a name="monitor-with-system-center-operations-manager---analytics-platform-system"></a>Monitorar com o System Center Operations Manager - Analytics Platform System
Use o System Center Operations Manager (SCOM) para monitorar o dispositivo do Analytics Platform System (APS).
  
## <a name="before-you-begin"></a>Antes de começar  
  
### <a name="prerequisites"></a>Prerequisites  
  
1.  System Center Operations Manager 2007 R2, 2012 ou 2012 SP1 deve ser instalado e em execução.  
  
2.  SQL Server 2008 R2 Native Client ou SQL Server 2012 Native Client deve ser instalado.  
  
3.  Os pacotes de gerenciamento para monitorar o SQL Server PDW devem ser instalados, importados e configurados. Use os seguintes artigos para obter instruções para executar essas tarefas.  
  
    -   [Instalar os pacotes de gerenciamento do SCOM &#40;Analytics Platform System&#41;](install-the-scom-management-packs.md)  
  
    -   [Importar o pacote de gerenciamento do SCOM para PDW &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-pdw.md) 
    
    -   [Configurar o SCOM para monitorar o Analytics Platform System &#40;Analytics Platform System&#41;](configure-scom-to-monitor-analytics-platform-system.md)
  
<!-- MISSING LINKS    -   [Import the SCOM Management Pack for HDInsight &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-hdinsight.md)  -->  
   
  
## <a name="to-monitor-sql-server-pdw-with-scom"></a>Para monitorar o SQL Server PDW com SCOM  
Depois de configurar os pacotes de gerenciamento do SCOM, clique o painel de monitoramento do SCOM e fazer drill down até **SQL Server Appliance** e, em seguida **Microsoft SQL Server Parallel Data Warehouse**. Sob o Microsoft SQL Server Parallel Data Warehouse, há quatro opções: Alertas, dispositivos, o diagrama de dispositivo e nós.  
  
### <a name="alerts"></a>Alertas  
Os alertas são onde você pode encontrar os alertas atuais para gerenciar.  
  
![Alerts](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM.png "SCOM_SCOM")  
  
### <a name="appliances"></a>Dispositivos  
Os dispositivos são onde você encontrará os dispositivos de PDW do servidor do SQL que tenha atualmente descobertos e monitorados em seu ambiente. Se um dispositivo não aparece aqui e você criou a conexão ODBC para ele, em seguida, pode haver algo errado com sua conta PDWWatcher. Se eles aparecem como "Não monitorado", pode haver algo errado com sua conta PDWMonitor. Seja paciente, pois o SCOM não faz alterações em tempo real, mas verifica periodicamente se há novos dispositivos monitorar e periodicamente envia consultas para os dispositivos para monitoramento.  
  
![Appliances](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM2.png "SCOM_SCOM2")  
  
### <a name="appliances-diagram"></a>Diagrama de aplicativos  
A página de diagrama de dispositivos é onde você pode obter a integridade do seu dispositivo com uma exibição de árvore de examinar:  
  
![Diagrama de aplicativos](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM3.png "SCOM_SCOM3")  
  
### <a name="nodes"></a>Nós  
Por fim, o modo de exibição de nós permite que você veja a integridade do seu dispositivo por meio de cada nó:  
  
![Nodes](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM4.png "SCOM_SCOM4")  
  
## <a name="see-also"></a>Consulte também  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Console de administração de Noções básicas sobre alertas &#40;Analytics Platform System&#41;](understanding-admin-console-alerts.md)  
  
