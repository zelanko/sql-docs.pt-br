---
title: Trabalhando com facetas do gerenciamento baseado em políticas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- viewing Policy-Based Management facets
- facets [Policy-Based Management], copying
- facets [Policy-Based Management], viewing
- copying Policy-Based Management facets
ms.assetid: 88d025c4-07c2-4e4d-8634-204249a8c82c
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: f8853222158fd4a5397e60bdffe4171cd8d66694
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85774080"
---
# <a name="working-with-policy-based-management-facets"></a>Trabalhando com facetas do Gerenciamento Baseado em Políticas
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Uma faceta do Gerenciamento Baseado em Política é um conjunto de propriedades lógicas que estão relacionadas a uma área de interesse de gerenciamento. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inclui várias facetas predefinidas. Por exemplo, a faceta de Configuração da Área da Superfície define, como propriedades, os recursos que são desativados por padrão.  
  
 Quando você gerencia muitas instâncias de ambientes semelhantes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , é possível configurar uma faceta em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], copiar o estado da faceta em um arquivo e, em seguida, importar esse arquivo para outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como uma política. Quando o estado é convertido em uma política, a política pode ser aplicada outras instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], objetos de instância, bancos de dados ou objetos de banco de dados.  
  
 Este tópico descreve como copiar o estado de uma faceta a um arquivo XML.  
  
##  <a name="permissions"></a><a name="BeforeYouBegin"></a> Permissões  
 Os procedimentos deste tópico exigem a associação à função PolicyAdministratorRole no banco de dados msdb.  
  
## <a name="viewing-and-copying-facet-states"></a>Exibindo e copiando estados da faceta  
 [Exibir as facetas do gerenciamento baseado em políticas em um objeto do SQL Server](../../relational-databases/policy-based-management/view-the-policy-based-management-facets-on-a-sql-server-object.md)  
  
 [Copiar um estado de faceta do gerenciamento baseado em políticas para um arquivo XML](../../relational-databases/policy-based-management/copy-a-policy-based-management-facet-state-to-an-xml-file.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Administrar servidores com Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
