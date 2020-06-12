---
title: 'Estudo de caso: Criando um ecossistema empresarial com o Microsoft Dynamics ERP e SQL Server a replicação 2014 para escalabilidade e desempenho | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 2b0b5ab7-4e08-431a-bd59-360177c4565c
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: dabe1a9e4ec2f7e7ea7db07abd16e86d5367be73
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84524092"
---
# <a name="case-study-building-an-enterprise-ecosystem-with-microsoft-dynamics-erp-and-sql-server-2014-replication-for-scalability-and-performance"></a>Estudo de caso: Criação de um ecossistema corporativo com o Microsoft Dynamics ERP e replicação do SQL Server 2014 para desempenho e escalabilidade

  **Resumo:** Este documento aborda os seguintes cenários:  
Como usar a replicação transacional no SQL Server 2014 para distribuir as transações de clientes do Dynamics AX entre vários nós. Como os dados são mantidos em todos os nós em tempo real, a replicação transacional fornece redundância, o que aumenta a disponibilidade e inclui os dados disponíveis para uma análise de desempenho mais eficiente.  
Como compreender as especificações envolvidas e aproveitar a replicação transacional para criar ecossistemas corporativos altamente escalonáveis no Microsoft Dynamics ERP. Forneça alto desempenho e escalabilidade sem personalizar os recursos do AX prontos para uso.  
  
 Normalmente, a replicação transacional é usada em fluxos de trabalho de servidor para servidor que requerem alta taxa de transferência. Isso inclui cenários como melhora da escalabilidade e disponibilidade; data warehouse e relatórios; integração de dados de vários sites; integração de dados heterogêneos; e descarregamento de processamento em lotes. Este white paper descreve um cenário distinto e padrões associados em que a replicação transacional é utilizada no Microsoft Dynamics ERP. Ele também aborda os desafios e as práticas recomendadas ao considerar a replicação transacional para criar soluções corporativas específicas para ERP (Enterprise Resource Planning), bem como a análise de desempenho em diferentes estágios.  
  
 Este conteúdo é adequado para desenvolvedores, arquitetos e administradores de banco de dados. Supõe-se que os leitores deste white paper tenham conhecimento básico do SQL Server 2008, 2012 ou 2014, bem como experiência em administração do SQL Server.  
  
 **Gravador:** Prabhakaran Sethuraman (PRAB), Microsoft  
  
 **Revisores técnicos:** Prabhakaran Sethuraman (PRAB), Microsoft; Santosh Padhy, Microsoft; Pavel Majstrov, Microsoft; Karthik Sankaranarayanan, Microsoft; Jon ACONE, Microsoft; David Stahlkopf, Microsoft; Kent Oldenburger, Microsoft; Mandi Ohlinger, Microsoft; Jason Roth, Microsoft  
  
 **Publicado em:** Outubro de 2015  
  
 **Aplica-se a:** SQL Server 2008, SQL Server 2012 e SQL Server 2014  
  
 Para examinar o documento, baixe o  
        [Estudo de caso: Criando um ecossistema empresarial com o Microsoft Dynamics ERP e SQL Server a replicação 2014 para escalabilidade e desempenho](https://download.microsoft.com/download/D/2/0/D20E1C5F-72EA-4505-9F26-FEF9550EFD44/A%20Case%20Study%20Using%20Replication%20to%20Build%20an%20Enterprise%20Ecosystem%20in%20Microsoft%20Dynamics%20ERP%20for%20Scalability%20and%20Performance.docx) Documento do Word.  
  
  
