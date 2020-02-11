---
title: Configurar fuso horário
description: A página fuso horário permite que você defina o fuso horário de todos os nós em seu dispositivo de sistema de plataforma de análise (APS).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 1da16790d011a628bc2536de051eb1181f06b8cf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401391"
---
# <a name="appliance-time-zone-configuration---analytics-platform-system"></a>Configuração de fuso horário do dispositivo – Analytics Platform System
A página **fuso horário** permite que você defina o fuso horário de todos os nós em seu dispositivo de sistema de plataforma de análise (APS).  
  
## <a name="to-set-the-time-zone"></a>Para definir o fuso horário  
  
1.  Inicie o Configuration Manager. Para obter mais informações, consulte [iniciar o Configuration Manager &#40;&#41;do sistema de plataforma de análise ](launch-the-configuration-manager.md).  
  
2.  Pare os serviços do dispositivo usando a página **status dos serviços** na Configuration Manager. Consulte [status dos serviços do PDW &#40;Analytics Platform System&#41;](pdw-services-status.md) para obter instruções.  
  
3.  No painel esquerdo da Configuration Manager, clique em **fuso horário**. Selecione o fuso horário desejado no menu suspenso **fuso horário** . Dependendo do seu local, você também pode optar por selecionar a caixa ao lado de **ajustar automaticamente o relógio para o horário de verão**.  
  
4.  Clique em **aplicar** para salvar as alterações.  
  
5.  Reinicie os serviços do dispositivo usando a página **status dos serviços** na Configuration Manager. Se você também estiver planejando alterar os privilégios, poderá fazer isso antes de reiniciar o dispositivo.  
  
![Hora do dispositivo DWConfig](./media/appliance-time-zone-configuration/SQL_Server_PDW_DWConfig_ApplTopTime.png "SQL_Server_PDW_DWConfig_ApplTopTime")  
  
## <a name="see-also"></a>Consulte Também  
[Inicie o Configuration Manager &#40;o sistema de plataforma de análise&#41;](launch-the-configuration-manager.md)  
  
