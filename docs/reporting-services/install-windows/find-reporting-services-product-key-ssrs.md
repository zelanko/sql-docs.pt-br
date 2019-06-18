---
title: Localizar a chave do produto (Product Key) para o SSRS (SQL Server Reporting Services) 2017 | Microsoft Docs
ms.date: 12/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 36460943b233f02e4d029b7865c7d7fa3844b488
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65502918"
---
# <a name="how-to-find-the-product-key-for-sql-server-2017-reporting-services"></a>Como localizar a chave do produto (Product Key) para o SQL Server 2017 Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2017-and-later](../../includes/ssrs-appliesto-2017-and-later.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

Saiba como localizar a chave do produto (Product Key) do SSRS (SQL Server Reporting Services) 2017 para que você possa instalar o servidor em um ambiente de produção.

Para localizar a chave do produto (Product Key), comece baixando e executando a instalação do SQL Server 2017.

1. Baixe o SQL Server 2017 em uma destas fontes:

    - Centro de Serviços de Licenciamento por Volume
    - Assinatura do MSDN
    - Loja (download na Microsoft Store)

1. Execute a instalação do SQL Server 2017 e copie a chave pré-populada:

    ![Copiar a chave do produto (Product Key) do SQL Server 2017](media/find-reporting-services-product-key-ssrs/ssrs-ss2017-copy-product-key.png)

1. [Execute a instalação do Reporting Services](install-reporting-services.md) e cole a chave:

     ![Colar a chave do produto (Product Key)](media/find-reporting-services-product-key-ssrs/ssrs-ssrs2017-paste-product-key.png)

Você só precisa executar esta etapa na primeira vez que instalar o SSRS 2017. As atualizações de serviço não deverão exigir a inserção da chave.

## <a name="related-information"></a>Informações relacionadas

- Para obter informações sobre como instalar o modo nativo do SQL Server Reporting Services, confira [Instalar o servidor de relatório no modo nativo do Reporting Services](install-reporting-services-native-mode-report-server.md). 

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

- Para obter informações sobre como instalar o SQL Server 2016 Reporting Services (e anteriores) no modo de integração do SharePoint, confira [Instalar o primeiro Servidor de Relatório no modo do SharePoint](install-the-first-report-server-in-sharepoint-mode.md).

::: moniker-end

## <a name="next-steps"></a>Próximas etapas

- [Instalar o SQL Server 2017 Reporting Services](install-reporting-services.md)
- Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
