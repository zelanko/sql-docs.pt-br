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
ms.openlocfilehash: d2639f783f862e27041985ac27ff16740b47cbb5
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53356759"
---
# <a name="incompatible-database-engine-server-collation-upgrade-advisor"></a>Ordenação do servidor de mecanismo de banco de dados incompatível (Supervisor de Atualização)
  Supervisor de atualização detectado [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] está usando uma instância da [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que é configurado para usar um agrupamento do servidor incompatível.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo do SharePoint.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrição  
 Supervisor de atualização detectado [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] está usando uma instância da [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que é configurado para usar um agrupamento do servidor incompatível.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo do SharePoint utiliza a arquitetura de serviços compartilhados do SharePoint. O SharePoint não oferece suporte a [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] configurado para diferenciação de maiúsculas e minúsculas ou ordenações do servidor ou ordenações do servidor binários. Ordenações incompatíveis incluem ordenações que têm por padrão a diferenciação de maiúsculas e minúsculas ou binários e uma ordenação básica que, por padrão, é compatível mas foi configurada com qualquer um dos seguintes designadores de ordenação:  
  
-   **Binary**  
  
-   **Diferencia maiusculas de minúsculas**  
  
-   **Ponto de código binário**  
  
 Como a ordenação do servidor [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] atual é incompatível, a atualização está bloqueada.  
  
## <a name="corrective-action"></a>Ação corretiva  
 A propriedade de ordenação do servidor [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] não pode ser alterada. Você não poderá concluir uma atualização do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Você precisará migrar sua instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para um novo servidor que está usando uma ordenação do servidor compatível. Para obter mais informações, consulte o seguinte:  
  
-   [Atualizar e migrar o Reporting Services](https://go.microsoft.com/fwlink/?LinkId=233227)  
  
-   [Selecionar um agrupamento do SQL Server](https://go.microsoft.com/fwlink/?LinkId=233226)  
  
  
