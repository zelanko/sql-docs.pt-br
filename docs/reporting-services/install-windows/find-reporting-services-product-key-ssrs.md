---
title: Localizar a chave do produto (Product Key) para o SSRS (SQL Server Reporting Services) | Microsoft Docs
ms.date: 10/02/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 6033b15655cebd557ee93efabce32ea0981072f1
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952722"
---
# <a name="find-the-product-key-for-sql-server-reporting-services"></a>Localizar a chave do produto (Product Key) para o SQL Server Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2017-and-later](../../includes/ssrs-appliesto-2017-and-later.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

Saiba como localizar a chave do produto para SQL Server Reporting Services (SSRS) 2017 e 2019 para que você possa instalar o servidor em um ambiente de produção.

Para localizar a chave do produto (Product Key), comece baixando e executando a instalação do SQL Server.

1. [Baixe o SQL Server](../../database-engine/install-windows/install-sql-server.md).
1. Execute a instalação do SQL Server e copie a chave pré-populada:

    ![Copiar a chave do produto (Product Key) do SQL Server](media/find-reporting-services-product-key-ssrs/ssrs-ss2017-copy-product-key.png)

1. [Baixe Reporting Services](install-reporting-services.md), execute a instalação e cole a chave:

     ![Colar a chave do produto (Product Key)](media/find-reporting-services-product-key-ssrs/ssrs-ssrs2017-paste-product-key.png)

Você só precisa executar esta etapa na primeira vez que instalar o Reporting Services. As atualizações de serviço não deverão exigir a inserção da chave.

## <a name="next-steps"></a>Próximas etapas

- [Instalar o SQL Server Reporting Services](install-reporting-services.md)
- Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
