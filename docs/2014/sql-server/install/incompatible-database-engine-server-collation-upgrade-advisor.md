---
title: Agrupamento de servidor de mecanismo de banco de dados incompatível (Supervisor de atualização) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 80f499d6-2c90-49eb-a5b3-0bb5b7faaa3b
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: d66e01079a0ab86a1456e53dd310614d3c291267
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48173406"
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
  
  
