---
title: 'Tutorial: preparando o servidor para replicação | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: ce30a095-2975-4387-9377-94a461ac78ee
caps.latest.revision: 14
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: c9dc9fe91d66158dcba280eb568053f2f0d0c9c5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120989"
---
# <a name="tutorial-preparing-the-server-for-replication"></a>Tutorial: Preparando o servidor para replicação
  É importante planejar a segurança antes de configurar a topologia de replicação. Este tutorial mostra a melhor forma de garantir a segurança de uma topologia de replicação e também como configurar a distribuição, que é a primeira etapa na replicação de dados. É preciso concluir este tutorial antes de qualquer outro.  
  
> [!NOTE]  
>  Para replicar dados com segurança entre servidores, é necessário implementar todas as recomendações em [Práticas recomendadas em relação à segurança de replicação](security/replication-security-best-practices.md).  
  
## <a name="what-you-will-learn"></a>O que você aprenderá  
 Neste tutorial, você aprenderá como preparar um servidor para que a replicação possa ser executada de modo seguro com um mínimo de privilégios. A primeira lição mostra como criar as contas de serviço do Windows usadas para executar os agentes de replicação. A segunda lição mostra como configurar a pasta usada para gerar e armazenar instantâneos de publicação. A terceira lição mostra como configurar a distribuição e definir permissões.  
  
## <a name="requirements"></a>Requisitos  
 Este tutorial é destinado a usuários que estão familiarizados com operações fundamentais de bancos de dados, mas que possuem pouca experiência com replicação.  
  
 Para que você possa usar esse tutorial, os seguintes componentes devem estar instalados no sistema:  
  
-   [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] com o banco de dados do [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Para reforçar a segurança, os bancos de dados de exemplo não são instalados por padrão.  
  
 **Tempo estimado para concluir este tutorial: 30 minutos.**  
  
## <a name="lessons-in-this-tutorial"></a>Lições neste tutorial  
  
-   [Lição 1: Criando contas do Windows para replicação](lesson-1-creating-windows-accounts-for-replication.md)  
  
-   [Lição 2: Preparando a pasta do instantâneo](lesson-2-preparing-the-snapshot-folder.md)  
  
-   [Lição 3: Configurando a distribuição](lesson-3-configuring-distribution.md)  
  
 [Inicie o tutorial](lesson-1-creating-windows-accounts-for-replication.md)  
  
## <a name="see-also"></a>Consulte também  
 [Configurar Distribuição](configure-distribution.md)   
 [Segurança e proteção &#40;Replicação&#41;](security/security-and-protection-replication.md)  
  
  