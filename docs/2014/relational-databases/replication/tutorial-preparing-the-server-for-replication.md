---
title: 'Tutorial: preparando o servidor para replicação | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: ce30a095-2975-4387-9377-94a461ac78ee
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c9b8ed6778a087c2200012c6df1409b187b39329
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63199075"
---
# <a name="tutorial-preparing-the-server-for-replication"></a>Tutorial: Preparando o servidor para replicação
  É importante planejar a segurança antes de configurar a topologia de replicação. Este tutorial mostra a melhor forma de garantir a segurança de uma topologia de replicação e também como configurar a distribuição, que é a primeira etapa na replicação de dados. É preciso concluir este tutorial antes de qualquer outro.  
  
> [!NOTE]  
>  Para replicar dados com segurança entre servidores, você deve implementar todas as recomendações nas [práticas recomendadas de segurança de replicação](security/replication-security-best-practices.md).  
  
## <a name="what-you-will-learn"></a>O que você aprenderá  
 Neste tutorial, você aprenderá como preparar um servidor para que a replicação possa ser executada de modo seguro com um mínimo de privilégios. A primeira lição mostra como criar as contas de serviço do Windows usadas para executar os agentes de replicação. A segunda lição mostra como configurar a pasta usada para gerar e armazenar instantâneos de publicação. A terceira lição mostra como configurar a distribuição e definir permissões.  
  
## <a name="requirements"></a>Requisitos  
 Este tutorial é destinado a usuários que estão familiarizados com operações fundamentais de bancos de dados, mas que possuem pouca experiência com replicação.  
  
 Para que você possa usar esse tutorial, os seguintes componentes devem estar instalados no sistema:  
  
-   
  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] com o banco de dados do [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Para reforçar a segurança, os bancos de dados de exemplo não são instalados por padrão.  
  
 **Tempo estimado para concluir este tutorial: 30 minutos.**  
  
## <a name="lessons-in-this-tutorial"></a>Lições neste tutorial  
  
-   [Lição 1: Criando contas do Windows para replicação](lesson-1-creating-windows-accounts-for-replication.md)  
  
-   [Lição 2: preparando a pasta de instantâneos](lesson-2-preparing-the-snapshot-folder.md)  
  
-   [Lição 3: Configurando a distribuição](lesson-3-configuring-distribution.md)  
  
 [Inicie o tutorial](lesson-1-creating-windows-accounts-for-replication.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar Distribuição](configure-distribution.md)   
 [Segurança de Replicação do SQL Server](security/view-and-modify-replication-security-settings.md)  
  
  
