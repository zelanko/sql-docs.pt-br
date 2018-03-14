---
title: "Tutorial: preparando o servidor para replicação | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: ce30a095-2975-4387-9377-94a461ac78ee
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3f7055cc15673a5dfd4564f26c4d314ccc0f5180
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2018
---
# <a name="tutorial-preparing-the-server-for-replication"></a>Tutorial: Preparando o servidor para replicação
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
É importante planejar a segurança antes de configurar a topologia de replicação. Este tutorial mostra a melhor forma de garantir a segurança de uma topologia de replicação e também como configurar a distribuição, que é a primeira etapa na replicação de dados. É preciso concluir este tutorial antes de qualquer outro.  
  
> [!NOTE]  
> Para replicar dados com segurança entre servidores, é necessário implementar todas as recomendações em [Práticas recomendadas em relação à segurança de replicação](../../relational-databases/replication/security/replication-security-best-practices.md).  
  
## <a name="what-you-will-learn"></a>O que você aprenderá  
Neste tutorial, você aprenderá como preparar um servidor para que a replicação possa ser executada de modo seguro com um mínimo de privilégios. A primeira lição mostra como criar as contas de serviço do Windows usadas para executar os agentes de replicação. A segunda lição mostra como configurar a pasta usada para gerar e armazenar instantâneos de publicação. A terceira lição mostra como configurar a distribuição e definir permissões.  
  
## <a name="requirements"></a>Requisitos  
Este tutorial é destinado a usuários que estão familiarizados com operações fundamentais de bancos de dados, mas que possuem pouca experiência com replicação.  
  
Para que você possa usar esse tutorial, os seguintes componentes devem estar instalados no sistema:  
  
-   [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] com o banco de dados do [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
**Tempo estimado para concluir este tutorial: 30 minutos.**  
  
## <a name="lessons-in-this-tutorial"></a>Lições neste tutorial  
  
-   [Lição 1: Criando contas do Windows para replicação](../../relational-databases/replication/lesson-1-creating-windows-accounts-for-replication.md)  
  
-   [Lição 2: Preparando a pasta do instantâneo](../../relational-databases/replication/lesson-2-preparing-the-snapshot-folder.md)  
  
-   [Lição 3: Configurando a distribuição](../../relational-databases/replication/lesson-3-configuring-distribution.md)  
  
[Inicie o tutorial](../../relational-databases/replication/lesson-1-creating-windows-accounts-for-replication.md)  
  
## <a name="see-also"></a>Consulte Também  
[Configurar a distribuição](../../relational-databases/replication/configure-distribution.md)  
[Segurança e proteção &#40;Replicação&#41;](../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  
  
