---
title: Monitor de dispositivo com o System Center Operations Manager (APS)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: de6cbf6e-f2e9-4877-94df-9c13b1182d56
caps.latest.revision: 14
ms.openlocfilehash: 02bdd22c66729ab471298e211b619e1cb1e4565c
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="monitor-the-appliance-by-using-system-center-operations-manager"></a>Monitorar o dispositivo usando o System Center Operations Manager
Descreve como usar o System Center Operations Manager para monitorar o SQL Server PDW e HDInsight.  
  
## <a name="before-you-begin"></a>Antes de começar  
  
### <a name="prerequisites"></a>Prerequisites  
  
1.  System Center Operations Manager 2007 R2, 2012 ou 2012 SP1 deve ser instalado e em execução.  
  
2.  SQL Server 2008 R2 Native Client ou SQL Server 2012 Native Client deve ser instalado.  
  
3.  Os pacotes de gerenciamento para monitorar o SQL Server PDW e HDInsight devem ser instalados, importados e configurados. Use o seguinte para obter instruções para executar essas tarefas.  
  
    -   [Instalar os pacotes de gerenciamento do SCOM &#40;Analytics Platform System&#41;](install-the-scom-management-packs.md)  
  
    -   [Importar o pacote de gerenciamento do SCOM para PDW &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-pdw.md) 
    
    -   [Configurar o SCOM para monitorar o Analytics Platform System &#40;Analytics Platform System&#41;](configure-scom-to-monitor-analytics-platform-system.md)
  
<!-- MISSING LINKS    -   [Import the SCOM Management Pack for HDInsight &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-hdinsight.md)  -->  
   
  
## <a name="to-monitor-sql-server-pdw-with-scom"></a>Para monitorar o SQL Server PDW com SCOM  
Depois de configurar os pacotes de gerenciamento do SCOM, clique em sobre o painel de monitoramento do SCOM e fazer drill down até **SQL Server Appliance** e **Microsoft SQL Server Parallel Data Warehouse**. Sob o Microsoft SQL Server Parallel Data Warehouse, há quatro opções: alertas, dispositivos, o diagrama de dispositivo e nós.  
  
### <a name="alerts"></a>Alertas  
Alertas são onde você pode encontrar os alertas atuais para gerenciar.  
  
![Alerts](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM.png "SCOM_SCOM")  
  
### <a name="appliances"></a>Dispositivos  
Os dispositivos são onde você encontrará os dispositivos de PDW do servidor do SQL que tenha atualmente descobertos e monitorados no seu ambiente. Se um dispositivo não aparecerão aqui e você criou a conexão ODBC para ele, em seguida, pode haver algum problema com sua conta PDWWatcher. Se eles aparecem como "Não monitorado" talvez haja algum problema com sua conta PDWMonitor. Tenha Paciência SCOM não fazer alterações em tempo real, mas verifica periodicamente se há novos dispositivos monitorar e periodicamente envia consultas com dispositivos para monitoramento.  
  
![Appliances](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM2.png "SCOM_SCOM2")  
  
### <a name="appliances-diagram"></a>Diagrama de aplicativos  
A página de diagrama de dispositivos é onde você pode obter uma aparência a integridade do seu dispositivo com uma exibição de árvore:  
  
![Diagrama de aplicativos](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM3.png "SCOM_SCOM3")  
  
### <a name="nodes"></a>Nós  
Por fim, o modo de exibição de nós permite ver a integridade do seu dispositivo por meio de cada nó:  
  
![Nodes](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM4.png "SCOM_SCOM4")  
  
## <a name="see-also"></a>Consulte também  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Alertas do Console de administração de Noções básicas sobre &#40;Analytics Platform System&#41;](understanding-admin-console-alerts.md)  
  
