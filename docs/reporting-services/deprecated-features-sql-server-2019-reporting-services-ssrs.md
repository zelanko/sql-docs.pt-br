---
title: Recursos preteridos no SQL Server 2019 Reporting Services | Microsoft Docs
description: Este artigo descreve os recursos que serão preteridos na próxima versão do SQL Server Reporting Services.
ms.date: 11/21/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, backward compatibility
- deprecated features [Reporting Services]
- HTML OWC rendering extension [Reporting Services]
- Report Server Web service, endpoints
ms.assetid: 3876c01e-f81d-4cce-9104-5106a8c369e6
author: maggiesMSFT
ms.author: maggies
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: eaa7edebe99a7c444fe1bfa23971317517399ea2
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "74320270"
---
# <a name="deprecated-features-in-sql-server-2019-reporting-services"></a>Recursos preteridos no SQL Server 2019 Reporting Services

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2019-and-later](../includes/ssrs-appliesto-2019-and-later.md)] [!INCLUDE [ssrs-appliesto-pbirs](../includes/ssrs-appliesto-pbirs.md)]

Quando marcamos um recurso como preterido, isso significa que:

- O recurso está somente no modo de manutenção. Não faremos nenhuma nova alteração, incluindo alterações relacionadas à interoperabilidade com novos recursos.
- Buscamos não remover um recurso preterido de versões futuras para facilitar a atualização. No entanto, em situações raras, podemos optar por remover permanentemente o recurso de Reporting Services caso ele limite inovações futuras.
- Para novos desenvolvimentos, não é recomendável usar recursos preteridos.

**Recursos preteridos em uma versão futura do SQL Server**

O SQL Server Reporting Services dá suporte aos recursos a seguir na próxima versão do SQL Server, mas os substituirá em uma versão posterior. A versão específica do SQL Server não foi determinada.

| **Categoria** | **Recurso preterido** | **Substituição** |
| --- | --- | --- |
| Servidor de relatório | Galeria de Partes de Relatório | Nenhum |
| Servidor de relatório | Relatórios Móveis e Publicador de Relatórios Móveis | Os relatórios do Power BI no Servidor de Relatórios do Power BI oferecem capacidades móveis. |
| Servidor de relatório | Formatos de renderização XLS e DOC | Os formatos XLSX e DOCX estão disponíveis e têm suporte. |
| Servidor de relatório | Feed de Dados Atom | O suporte a feed oData está disponível para conjuntos de relatórios compartilhados no SSRS e Servidor de Relatórios do Power BI. |

## <a name="see-also"></a>Confira também

[Funcionalidade descontinuada no SSRS (SQL Server Reporting Services) 2019](discontinued-functionality-sql-server-reporting-services-2019.md)

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
