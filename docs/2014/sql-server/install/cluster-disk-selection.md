---
title: Seleção de disco de cluster | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- cluster disk selection
ms.assetid: 0d6b863d-5972-4a20-9990-64ee8016fea6
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 156c17d7dae5c4de07033a96f2e936448d8d02ed
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66096500"
---
# <a name="cluster-disk-selection"></a>Seleção de Disco de Cluster
  Use a página **Seleção de Disco de Cluster** do Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a fim de selecionar o recurso de disco de cluster compartilhado do cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O disco de cluster é o local onde os dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são colocados.  
  
 Um disco de cluster compartilhado não é um requisito [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] para instalações de cluster. Um servidor de arquivos SMB é um armazenamento com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] suporte para instalações de cluster de failover e pode ser especificado usando a página **mecanismo de banco de dados-data diretórios** antes de concluir a instalação.  
  
> [!WARNING]  
>  Se você selecionou Analysis Services para ser instalado, especifique um disco de cluster compartilhado.  
>   
>  Se você pretende habilitar FILESTREAM nesta instância de cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , especifique um disco de cluster compartilhado.  
  
## <a name="options"></a>Opções  
 **Discos compartilhados**  
 Selecione um único disco na lista. O disco de cluster é o local onde os dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são colocados.  
  
 Apenas um disco pode ser especificado. Se você selecionar o grupo que contém o recurso de quorum de cluster, será exibido um aviso. É recomendável não efetuar a instalação no recurso de quorum de cluster.  
  
 **Discos compartilhados disponíveis**  
 Exibe uma lista de discos disponíveis, onde cada um deles é qualificado como um disco compartilhado, e uma descrição de cada recurso de disco.  
  
  
