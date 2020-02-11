---
title: INFORMATION_SCHEMA. SCHEMATA retorna os nomes de esquema em um banco de dados, não em uma instância | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- INFORMATION_SCHEMA.SCHEMATA view
ms.assetid: 4337b643-910d-47d7-bea8-f4052066b9a2
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0e3683ee043785ec6adc349ac52301280c7bc2b8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66094725"
---
# <a name="information_schemaschemata-returns-schema-names-in-a-database-not-databases-in-an-instance"></a>INFORMATION_SCHEMA.SCHEMATA retorna nomes de esquemas em um banco de dados, e não bancos de dados em uma instância
  O Supervisor de Atualização detectou instruções que referenciam a exibição INFORMATION_SCHEMA.SCHEMATA. Em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa exibição retornava todos os bancos de dados em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e em versões posteriores, a exibição retorna todos os esquemas em um banco de dados.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>DESCRIÇÃO  
 Em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a exibição INFORMATION_SCHEMA.SCHEMATA retornava todos os bancos de dados em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Agora, a exibição retorna todos os esquemas em um banco de dados, o que obedece ao padrão do SQL.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Modifique seu aplicativo para fazer referência à exibição de catálogo **Sys. databases** para retornar todos os bancos de dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]uma instância do.  
  
## <a name="see-also"></a>Consulte Também  
 [Problemas de atualização do Mecanismo de Banco de Dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
