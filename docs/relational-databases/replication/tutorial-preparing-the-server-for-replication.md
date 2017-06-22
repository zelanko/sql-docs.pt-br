---
title: "Tutorial: preparando o servidor para replicação | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: ce30a095-2975-4387-9377-94a461ac78ee
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8339e6f168eb678a066a6f8c13a300507ffb7cca
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="tutorial-preparing-the-server-for-replication"></a>Tutorial: Preparando o servidor para replicação
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
  
## <a name="see-also"></a>Consulte também  
[Configurar a distribuição](../../relational-databases/replication/configure-distribution.md)  
[Segurança e proteção &#40;Replicação&#41;](../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  
  

