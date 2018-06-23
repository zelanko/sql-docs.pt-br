---
title: Exibir a lista de pacotes no servidor do Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 67a992d1-7524-4f4b-b3d8-ebd9e5ea82a8
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 2c027225d0419359c36401151a16216befb4e4df
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007745"
---
# <a name="view-the-list-of-packages-on-the-integration-services-server"></a>Exibir a lista de pacotes no servidor do Integration Services
  Você pode exibir a lista de pacotes armazenados no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em uma de duas diferentes maneiras.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] acesso  
 Para exibir a lista de pacotes armazenados no servidor, consulte a exibição [catalog.packages &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-views/catalog-packages-ssisdb-database).  
  
 No [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]  
 Para exibir pacotes armazenados no servidor usando o Pesquisador de Objetos no [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], siga o procedimento abaixo.  
  
### <a name="to-view-packages-using-includessmanstudiofullincludesssmanstudiofull-mdmd"></a>Para exibir pacotes usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]  
  
1.  No [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], conecte-se ao servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Ou seja, conecte-se à instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda o banco de dados do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
2.  Em Pesquisador de Objetos, expanda a árvore para exibir o nó **Catálogos do Integration Services** .  
  
3.  Expanda o nó **Catálogos do Integration Services** para exibir o nó **SSISDB** .  
  
4.  Expanda o nó **SSISDB** para abrir a lista de uma ou mais pastas. Cada pasta contém um ou mais projetos na pasta **Projetos** e cada projeto contém um mais pacotes na pasta **Pacotes** .  
  
  
