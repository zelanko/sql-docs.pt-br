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
ms.openlocfilehash: c7a9df15948ddea5fe76efa1cce688f704cbe5c9
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065366"
---
# <a name="incompatible-database-engine-server-collation-upgrade-advisor"></a>Ordenação do servidor de mecanismo de banco de dados incompatível (Supervisor de Atualização)
  O supervisor de atualização detectado [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] está usando uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que está configurada para usar um agrupamento de servidor incompatível.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Modo do SharePoint.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrição  
 O supervisor de atualização detectado [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] está usando uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que está configurada para usar um agrupamento de servidor incompatível.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]O modo do SharePoint utiliza a arquitetura de serviços compartilhados do SharePoint. O SharePoint não oferece suporte a [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] configurado para diferenciação de maiúsculas e minúsculas ou ordenações do servidor ou ordenações do servidor binários. Ordenações incompatíveis incluem ordenações que têm por padrão a diferenciação de maiúsculas e minúsculas ou binários e uma ordenação básica que, por padrão, é compatível mas foi configurada com qualquer um dos seguintes designadores de ordenação:  
  
-   **Binary**  
  
-   **Diferenciar maiúsculas de minúsculas**  
  
-   **Ponto de código binário**  
  
 Como a ordenação do servidor [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] atual é incompatível, a atualização está bloqueada.  
  
## <a name="corrective-action"></a>Ação corretiva  
 A propriedade de ordenação do servidor [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] não pode ser alterada. Você não poderá concluir uma atualização do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Você precisará migrar sua instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para um novo servidor que está usando uma ordenação do servidor compatível. Para saber mais, consulte o seguinte:  
  
-   [Atualizar e migrar o Reporting Services](https://go.microsoft.com/fwlink/?LinkId=233227)  
  
-   [Selecionando uma ordenação do SQL Server](https://go.microsoft.com/fwlink/?LinkId=233226)  
  
  
