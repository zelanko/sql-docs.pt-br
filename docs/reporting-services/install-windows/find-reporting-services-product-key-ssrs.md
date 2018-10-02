---
title: Localizar a chave do produto (Product Key) para o SSRS (SQL Server Reporting Services) 2017 | Microsoft Docs
ms.date: 12/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 63fda18a7dce1b6cf27cc21f6decab18948e1209
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47709107"
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

- Para obter informações sobre como instalar o modo nativo do SQL Server 2016 Reporting Services, consulte [Instalar o servidor de relatório no modo nativo do Reporting Services](install-reporting-services-native-mode-report-server.md). 
- Para obter informações sobre como instalar o SQL Server 2016 Reporting Services no modo de integração do SharePoint, consulte [Instalar o primeiro Servidor de Relatório no modo do SharePoint](install-the-first-report-server-in-sharepoint-mode.md).

## <a name="next-steps"></a>Próximas etapas

- [Instalar o SQL Server 2017 Reporting Services](install-reporting-services.md)
- Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
