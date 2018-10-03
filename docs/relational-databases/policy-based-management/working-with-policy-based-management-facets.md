---
title: Trabalhando com facetas do gerenciamento baseado em políticas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- viewing Policy-Based Management facets
- facets [Policy-Based Management], copying
- facets [Policy-Based Management], viewing
- copying Policy-Based Management facets
ms.assetid: 88d025c4-07c2-4e4d-8634-204249a8c82c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 18f47db0c69a228083714806a11d3c3dc85661be
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47706941"
---
# <a name="working-with-policy-based-management-facets"></a>Trabalhando com facetas do Gerenciamento Baseado em Políticas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Uma faceta do Gerenciamento Baseado em Política é um conjunto de propriedades lógicas que estão relacionadas a uma área de interesse de gerenciamento. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inclui várias facetas predefinidas. Por exemplo, a faceta de Configuração da Área da Superfície define, como propriedades, os recursos que são desativados por padrão.  
  
 Quando você gerencia muitas instâncias de ambientes semelhantes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , é possível configurar uma faceta em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], copiar o estado da faceta em um arquivo e, em seguida, importar esse arquivo para outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como uma política. Quando o estado é convertido em uma política, a política pode ser aplicada outras instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], objetos de instância, bancos de dados ou objetos de banco de dados.  
  
 Este tópico descreve como copiar o estado de uma faceta a um arquivo XML.  
  
##  <a name="BeforeYouBegin"></a> Permissões  
 Os procedimentos deste tópico exigem a associação à função PolicyAdministratorRole no banco de dados msdb.  
  
## <a name="viewing-and-copying-facet-states"></a>Exibindo e copiando estados da faceta  
 [Exibir as facetas de Gerenciamento Baseado em Políticas em um objeto do SQL Server](../../relational-databases/policy-based-management/view-the-policy-based-management-facets-on-a-sql-server-object.md)  
  
 [Copiar um estado de faceta do Gerenciamento Baseado em Políticas para um arquivo XML](../../relational-databases/policy-based-management/copy-a-policy-based-management-facet-state-to-an-xml-file.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Administrar servidores com Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
