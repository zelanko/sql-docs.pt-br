---
title: Trabalhando com facetas do gerenciamento baseado em políticas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- viewing Policy-Based Management facets
- facets [Policy-Based Management], copying
- facets [Policy-Based Management], viewing
- copying Policy-Based Management facets
ms.assetid: 88d025c4-07c2-4e4d-8634-204249a8c82c
caps.latest.revision: 29
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8b2b7217faed4a594c83a7eca6927a24733ac353
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37272592"
---
# <a name="working-with-policy-based-management-facets"></a>Trabalhando com facetas do Gerenciamento Baseado em Políticas
  Uma faceta do Gerenciamento Baseado em Política é um conjunto de propriedades lógicas que estão relacionadas a uma área de interesse de gerenciamento. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inclui várias facetas predefinidas. Por exemplo, a faceta de Configuração da Área da Superfície define, como propriedades, os recursos que são desativados por padrão.  
  
 Quando você gerencia muitas instâncias de ambientes semelhantes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , é possível configurar uma faceta em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], copiar o estado da faceta em um arquivo e, em seguida, importar esse arquivo para outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como uma política. Quando o estado é convertido em uma política, a política pode ser aplicada outras instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], objetos de instância, bancos de dados ou objetos de banco de dados.  
  
 Este tópico descreve como copiar o estado de uma faceta a um arquivo XML.  
  
##  <a name="BeforeYouBegin"></a> Permissões  
 Os procedimentos deste tópico exigem a associação à função PolicyAdministratorRole no banco de dados msdb.  
  
## <a name="viewing-and-copying-facet-states"></a>Exibindo e copiando estados da faceta  
 [Exibir as facetas de Gerenciamento Baseado em Políticas em um objeto do SQL Server](view-the-policy-based-management-facets-on-a-sql-server-object.md)  
  
 [Copiar um estado de faceta do Gerenciamento Baseado em Políticas para um arquivo XML](copy-a-policy-based-management-facet-state-to-an-xml-file.md)  
  
## <a name="see-also"></a>Consulte também  
 [Administrar servidores com Gerenciamento Baseado em Políticas](administer-servers-by-using-policy-based-management.md)  
  
  
