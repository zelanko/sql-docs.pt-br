---
title: Agrupamento de servidor de mecanismo de banco de dados incompatível (Supervisor de atualização) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 80f499d6-2c90-49eb-a5b3-0bb5b7faaa3b
caps.latest.revision: 8
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: e182df78fc7faae8a50092fd51a8f2c0964fe2bc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37286642"
---
# <a name="incompatible-database-engine-server-collation-upgrade-advisor"></a>Agrupamento do servidor de mecanismo de banco de dados incompatível (Supervisor de Atualização)
  Supervisor de atualização detectado [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] está usando uma instância da [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que é configurado para usar um agrupamento do servidor incompatível.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo do SharePoint.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Description  
 Supervisor de atualização detectado [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] está usando uma instância da [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que é configurado para usar um agrupamento do servidor incompatível.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo do SharePoint utiliza a arquitetura de serviços compartilhados do SharePoint. O SharePoint não oferece suporte a [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] configurado para diferenciação de maiúsculas e minúsculas ou agrupamentos do servidor ou agrupamentos do servidor binários. Agrupamentos incompatíveis incluem agrupamentos que têm por padrão a diferenciação de maiúsculas e minúsculas ou binários e um agrupamento básico que, por padrão, é compatível mas foi configurado com qualquer um dos seguintes designadores de agrupamento:  
  
-   **Binary**  
  
-   **Diferencia maiusculas de minúsculas**  
  
-   **Ponto de código binário**  
  
 Como o agrupamento do servidor [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] atual é incompatível, a atualização está bloqueada.  
  
## <a name="corrective-action"></a>Ação corretiva  
 A propriedade de agrupamento do servidor [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] não pode ser alterada. Você não poderá concluir uma atualização do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Você precisará migrar sua instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para um novo servidor que está usando um agrupamento do servidor compatível. Para obter mais informações, consulte o seguinte:  
  
-   [Atualizar e migrar o Reporting Services](http://go.microsoft.com/fwlink/?LinkId=233227)  
  
-   [Selecionar um agrupamento do SQL Server](http://go.microsoft.com/fwlink/?LinkId=233226)  
  
  
