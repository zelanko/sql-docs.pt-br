---
title: "Tutorial: Preparando o servidor para replica&#231;&#227;o | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
helpviewer_keywords: 
  - "replicação [SQL Server], tutoriais"
ms.assetid: ce30a095-2975-4387-9377-94a461ac78ee
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# Tutorial: Preparando o servidor para replica&#231;&#227;o
É importante planejar a segurança antes de configurar a topologia de replicação. Este tutorial mostra a melhor forma de garantir a segurança de uma topologia de replicação e também como configurar a distribuição, que é a primeira etapa na replicação de dados. É preciso concluir este tutorial antes de qualquer outro.  
  
> [!NOTE]  
> Para replicar dados com segurança entre servidores, é necessário implementar todas as recomendações em [Práticas recomendadas em relação à segurança de replicação](../../relational-databases/replication/security/replication-security-best-practices.md).  
  
## O que você aprenderá  
Neste tutorial, você aprenderá como preparar um servidor para que a replicação possa ser executada de modo seguro com um mínimo de privilégios. A primeira lição mostra como criar as contas de serviço do Windows usadas para executar os agentes de replicação. A segunda lição mostra como configurar a pasta usada para gerar e armazenar instantâneos de publicação. A terceira lição mostra como configurar a distribuição e definir permissões.  
  
## Requisitos  
Este tutorial é destinado a usuários que estão familiarizados com operações fundamentais de bancos de dados, mas que possuem pouca experiência com replicação.  
  
Para que você possa usar esse tutorial, os seguintes componentes devem estar instalados no sistema:  
  
-   [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] com o banco de dados do [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
**Tempo estimado para concluir este tutorial: 30 minutos.**  
  
## Lições neste tutorial  
  
-   [Lição 1: Criando contas do Windows para replicação](../../relational-databases/replication/lesson-1-creating-windows-accounts-for-replication.md)  
  
-   [Lição 2: Preparando a pasta do instantâneo](../../relational-databases/replication/lesson-2-preparing-the-snapshot-folder.md)  
  
-   [Lição 3: Configurando a distribuição](../../relational-databases/replication/lesson-3-configuring-distribution.md)  
  
[Inicie o tutorial](../../relational-databases/replication/lesson-1-creating-windows-accounts-for-replication.md)  
  
## Consulte também  
[Configurar a distribuição](../../relational-databases/replication/configure-distribution.md)  
[Segurança e proteção &#40;Replicação&#41;](../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  
  
