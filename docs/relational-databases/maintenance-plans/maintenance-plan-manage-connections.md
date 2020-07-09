---
title: Plano de manutenção (Gerenciar conexões) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.maint.connections.f1
ms.assetid: 95ad9375-6584-423e-b9de-0e86782f8017
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 495ec4a69d960cfec8534b37490b10fe66c5934d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85754544"
---
# <a name="maintenance-plan-manage-connections"></a>Plano de manutenção (Gerenciar Conexões)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Use a caixa de diálogo **Gerenciar Conexões** para especificar as propriedades das conexões usadas por planos de manutenção. Quando você cria um plano de manutenção, é criada uma conexão local para o servidor em que você criou o plano. Use essa conexão para criar tarefas que executam trabalho nessa conexão local. Quando necessário, use a caixa de diálogo **Gerenciar Conexões** para adicioná-las. Quando conexões adicionais são configuradas, elas aparecem na caixa de conexões para cada tarefa.  
  
## <a name="options"></a>Opções  
 **Servidor**  
 Instância de servidor.  
  
 **Autenticação**  
 Indica se a conexão é feita com autenticação do Windows ou com autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  

> [!IMPORTANT]  
> O pacote é armazenado no banco de dados **msdb** com seu **ProtectionLevel** definida como **ServerStorage**, portanto, quando a *Autenticação do SQL Server* é usada, a senha não será criptografada no **msdb**. Você pode usar a *Autenticação do SQL Server* desde que **msdb** esteja protegido, porém é recomendado usar a *Autenticação do Windows*

## <a name="see-also"></a>Consulte Também  
 [Planos de manutenção](../../relational-databases/maintenance-plans/maintenance-plans.md)  
  
  
