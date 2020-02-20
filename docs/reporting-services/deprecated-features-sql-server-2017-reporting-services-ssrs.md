---
title: Recursos preteridos no SQL Server 2017 Reporting Services | Microsoft Docs
description: Este artigo descreve os recursos que serão preteridos na próxima versão do SQL Server Reporting Services.
ms.date: 11/20/2019
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
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: d8fe51ce9d86688669e84ad866ad9f5e6da075e8
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "74320310"
---
# <a name="deprecated-features-in-sql-server-2017-reporting-services"></a>Recursos preteridos no SQL Server 2017 Reporting Services

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2017](../includes/ssrs-appliesto-2017.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../includes/ssrs-appliesto-not-pbirs.md)]

Quando marcamos um recurso como preterido, isso significa que:

- O recurso está somente no modo de manutenção. Não faremos nenhuma nova alteração, incluindo alterações relacionadas à interoperabilidade com novos recursos.
- Buscamos não remover um recurso preterido de versões futuras para facilitar a atualização. No entanto, em situações raras, podemos optar por remover permanentemente o recurso de Reporting Services caso ele limite inovações futuras.
- Para novos desenvolvimentos, não é recomendável usar recursos preteridos.

## <a name="features-deprecated-in-the-next-version-of-sql-server"></a>Recursos preteridos na próxima versão do SQL Server

Os recursos do SQL Server 2017 Reporting Services a seguir serão preteridos na próxima versão do SQL Server. Não use esses recursos em novo um trabalho de desenvolvimento e, assim que possível, modifique os aplicativos que os utilizam atualmente.

> [!NOTE]
> Essa lista é idêntica à lista do SQL Server 2016 Reporting Services (13.x). Não há nenhum novo recurso preterido ou descontinuado anunciado para o SQL Server 2017 Reporting Services (14.x).


| **Categoria** | **Recurso preterido** | **Substituição** |
| --- | --- | --- |
| Servidor de relatório | Renderizador do HTML 4.0. | Renderizador do HTML 5 |

## <a name="see-also"></a>Confira também

[Funcionalidade descontinuada no SSRS (SQL Server Reporting Services)](discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
