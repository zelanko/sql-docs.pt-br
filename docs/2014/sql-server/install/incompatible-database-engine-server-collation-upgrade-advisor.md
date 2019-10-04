---
title: Agrupamento de servidor Mecanismo de Banco de Dados incompatível (Supervisor de atualização) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 80f499d6-2c90-49eb-a5b3-0bb5b7faaa3b
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: fbd4c1e55bb49c6ae8f75d3d12cc243df963018a
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952229"
---
# <a name="incompatible-database-engine-server-collation-upgrade-advisor"></a>Ordenação do servidor de mecanismo de banco de dados incompatível (Supervisor de Atualização)
  O supervisor de atualização detectou [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] está usando uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que está configurado para usar um agrupamento de servidor incompatível.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] modo do SharePoint.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrição  
 O supervisor de atualização detectou [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] está usando uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que está configurado para usar um agrupamento de servidor incompatível.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o modo do SharePoint utiliza a arquitetura dos serviços compartilhados do SharePoint. O SharePoint não oferece suporte a [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] configurado para diferenciação de maiúsculas e minúsculas ou ordenações do servidor ou ordenações do servidor binários. Ordenações incompatíveis incluem ordenações que têm por padrão a diferenciação de maiúsculas e minúsculas ou binários e uma ordenação básica que, por padrão, é compatível mas foi configurada com qualquer um dos seguintes designadores de ordenação:  
  
-   **Binary**  
  
-   **Diferenciar maiúsculas de minúsculas**  
  
-   **Ponto binário**  
  
 Como a ordenação do servidor [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] atual é incompatível, a atualização está bloqueada.  
  
## <a name="corrective-action"></a>Ação corretiva  
 A propriedade de ordenação do servidor [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] não pode ser alterada. Você não poderá concluir uma atualização do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Você precisará migrar sua instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para um novo servidor que está usando uma ordenação do servidor compatível. Para obter mais informações, consulte o seguinte:  
  
-   [Atualizar e migrar o Reporting Services](https://go.microsoft.com/fwlink/?LinkId=233227)  
  
-   [Selecionando um agrupamento de SQL Server](https://go.microsoft.com/fwlink/?LinkId=233226)  
  
  
