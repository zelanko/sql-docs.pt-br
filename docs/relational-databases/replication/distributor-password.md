---
description: Senha do Distribuidor
title: Senha do distribuidor | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.configuredistributionwizard.distributorpassword.f1
ms.assetid: 52787c5e-c9ef-440e-a000-0787111b7dbb
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 8740af3ff189bf929c1a97caaf5d3cc31e283714
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88498733"
---
# <a name="distributor-password"></a>Senha do Distribuidor
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  Se na página **Publicadores** deste assistente você tiver habilitado um ou mais Publicadores para usar esse servidor como Distribuidor remoto, terá de especificar uma senha para a conexão que a replicação faz entre o Publicador e o Distribuidor remoto, usando o logon **distributor_admin** . A mesma senha deve ser inserida, para cada Publicador que usa esse Distribuidor remoto, na página **Senha Administrativa** do Assistente para Nova Publicação ou no Assistente para Configurar Distribuição. Para mais informações sobre segurança de distribuidores, consulte [Proteger o distribuidor](../../relational-databases/replication/security/secure-the-distributor.md).  
  
## <a name="options"></a>Opções  
 **Senha**  
 Insira uma senha forte para a conexão entre o Publicador e o Distribuidor remoto.  
  
 **Confirmar Senha**  
 Reinsira a senha para confirmar que ela foi inserida corretamente.  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar Distribuição](../../relational-databases/replication/configure-distribution.md)   
 [Configurar a publicação e a distribuição](../../relational-databases/replication/configure-publishing-and-distribution.md)  
  
  
