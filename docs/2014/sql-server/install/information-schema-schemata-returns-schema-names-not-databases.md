---
title: INFORMATION_SCHEMA. Nomes de esquema retorna ESQUEMAS em um banco de dados, não os bancos de dados em uma instância | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- INFORMATION_SCHEMA.SCHEMATA view
ms.assetid: 4337b643-910d-47d7-bea8-f4052066b9a2
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e624597090ab6a7efdb21ebbff6785b1471d7367
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121833"
---
# <a name="informationschemaschemata-returns-schema-names-in-a-database-not-databases-in-an-instance"></a>INFORMATION_SCHEMA.SCHEMATA retorna nomes de esquemas em um banco de dados, e não bancos de dados em uma instância
  O Supervisor de Atualização detectou instruções que referenciam a exibição INFORMATION_SCHEMA.SCHEMATA. Em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa exibição retornava todos os bancos de dados em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e em versões posteriores, a exibição retorna todos os esquemas em um banco de dados.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 Em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a exibição INFORMATION_SCHEMA.SCHEMATA retornava todos os bancos de dados em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Agora, a exibição retorna todos os esquemas em um banco de dados, o que obedece ao padrão do SQL.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Modifique seu aplicativo para referenciar o **sys. Databases** catálogo para retornar todos os bancos de dados em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
