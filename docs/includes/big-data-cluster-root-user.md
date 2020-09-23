---
author: MikeRayMSFT
ms.prod: sql
ms.technology: big-data-cluster
ms.topic: include
ms.date: 06/22/2020
ms.author: mikeray
ms.openlocfilehash: b72f8044638adbf75049392fae32447a8a749a6d
ms.sourcegitcommit: d973b520f387b568edf1d637ae37d117e1d4ce32
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85215036"
---
A partir do SQL Server 2019 CU5, quando você implanta um novo cluster com a autenticação básica, todos os pontos de extremidade, incluindo o gateway, usam `AZDATA_USERNAME` e `AZDATA_PASSWORD`. Os pontos de extremidade em clusters que são atualizados para CU5 continuam usando `root` como o nome de usuário para se conectar ao ponto de extremidade do gateway. Essa alteração não se aplica às implantações que usam a autenticação do Active Directory. Confira [Credenciais para acessar serviços por meio do ponto de extremidade do gateway](../big-data-cluster/release-notes-big-data-cluster.md#credentials-for-accessing-services-through-gateway-endpoint) nas notas sobre a versão.