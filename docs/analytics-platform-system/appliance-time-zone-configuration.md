---
title: Configurar o fuso horário - Analytics Platform System | Microsoft Docs
description: A página de fuso horário permite que você defina o fuso horário para todos os nós em seu dispositivo do Analytics Platform System (APS).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 6a17ef4e77f9703a285f1e232077582e4441f293
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63275982"
---
# <a name="appliance-time-zone-configuration---analytics-platform-system"></a>Configuração de fuso horário do dispositivo - Analytics Platform System
O **fuso horário** página permite que você defina o fuso horário para todos os nós em seu dispositivo do Analytics Platform System (APS).  
  
## <a name="to-set-the-time-zone"></a>Para definir o fuso horário  
  
1.  Inicie o Gerenciador de configuração. Para obter mais informações, consulte [iniciar o Configuration Manager &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md).  
  
2.  Parar os serviços de dispositivo usando o **Status de serviços** página no Configuration Manager. Ver [Status de serviços do PDW &#40;Analytics Platform System&#41; ](pdw-services-status.md) para obter instruções.  
  
3.  No painel esquerdo do Gerenciador de configuração, clique em **fuso horário**. Selecione o fuso horário desejado do **fuso horário** menu suspenso. Dependendo do seu local, você também pode optar por selecionar a caixa ao lado **ajustar automaticamente o relógio para horário de verão**.  
  
4.  Clique em **aplicar** para salvar suas alterações.  
  
5.  Reinicie os serviços de dispositivo usando o **Status de serviços** página no Configuration Manager. Se também estiver planejando alterar os privilégios, você pode fazer isso antes de reiniciar o dispositivo.  
  
![DWConfig Appliance Time](./media/appliance-time-zone-configuration/SQL_Server_PDW_DWConfig_ApplTopTime.png "SQL_Server_PDW_DWConfig_ApplTopTime")  
  
## <a name="see-also"></a>Consulte também  
[Inicie o Gerenciador de configuração &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)  
  
