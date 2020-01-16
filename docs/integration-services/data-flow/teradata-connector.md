---
title: Microsoft Connector para Teradata | Microsoft Docs
ms.custom: ''
ms.date: 11/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ca25b7425ce74cea820e295a6a99bc3a3c1e2817
ms.sourcegitcommit: a02727aab143541794e9cfe923770d019f323116
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2020
ms.locfileid: "75755847"
---
# <a name="microsoft-connector-for-teradata-preview"></a>Microsoft Connector para Teradata (versão prévia)
[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

O Microsoft Connector para Teradata permite exportar dados de bancos de dados Teradata e carregar dados neles em um pacote SSIS.

Esse novo conector dá suporte a bancos de dados com tabelas habilitadas para 1 MB.

## <a name="version-support"></a>Suporte à versão

Há suporte para os seguintes produtos do Microsoft SQL Server no Microsoft Connector para Teradata:

- Microsoft SQL Server 2019
- SSDT (Microsoft SQL Server Data Tools)

O Microsoft Connector para Teradata usa a interface de linguagem de programação de aplicativo do Teradata Parallel Transporter para carregar dados no banco de dados Teradata e exportar dados dele. As seguintes versões são compatíveis:

- Teradata PT (Teradata Parallel Transporter) 16.10
- Teradata PT (Teradata Parallel Transporter) 16.20

Há suporte para as seguintes versões de fontes de dados do banco de dados Teradata:

- Banco de dados Teradata 16.20
- Banco de dados Teradata 16.10
- Banco de dados Teradata 15.10
- Banco de dados Teradata 15.00

Verifique a [documentação do Teradata](https://docs.teradata.com/) para obter detalhes do guia do programador da interface de programação de aplicativo do Teradata Parallel Transporter.

## <a name="installation"></a>Instalação

### <a name="prerequisite"></a>Pré-requisito

Em computadores de 32 bits, instale os seguintes drivers de [Ferramentas e utilitários do Teradata: pacote de instalação do Windows](https://downloads.teradata.com/download/tools/teradata-tools-and-utilities-windows-installation-package):

- Driver ODBC do Teradata (32 bits)
- API do Teradata PT (32 bits)

Em computadores de 64 bits, instale os seguintes drivers:

- Driver ODBC do Teradata (64 bits)
- API do Teradata PT (64 bits)

Para instalar o conector para o banco de dados Teradata, baixe e execute o instalador da [última versão do Microsoft Connector para Teradata](https://www.microsoft.com/download/details.aspx?id=100599). Em seguida, siga as instruções no assistente de instalação.

Depois de instalar o conector, reinicie o SQL Server Integration Services para verificar se a origem e o destino do Teradata estão funcionando corretamente.

Para executar o pacote SSIS com o direcionamento para o SQL Server 2017 e anterior, você precisará instalar o **Microsoft Connector para Teradata da Attunity** com a versão correspondente usando o link abaixo:

- [SQL Server 2017: Microsoft Connector versão 5.0 para Teradata da Attunity](https://www.microsoft.com/download/details.aspx?id=55179)
- [SQL Server 2016: Microsoft Connector versão 4.0 para Teradata da Attunity](https://www.microsoft.com/download/details.aspx?id=52950)
- [SQL Server 2014: Microsoft Connector versão 3.0 para Teradata da Attunity](https://www.microsoft.com/download/details.aspx?id=44582)
- [SQL Server 2012: Microsoft Connector versão 2.0 para Teradata da Attunity](https://www.microsoft.com/download/details.aspx?id=29283)

## <a name="uninstallation"></a>Desinstalação

Execute o assistente de desinstalação para remover o **Microsoft Connector para Teradata**.

## <a name="next-steps"></a>Próximas etapas

- Configurar o [gerenciador de conexões do Teradata](teradata-connection-manager.md)
- Configurar a [fonte do Teradata](teradata-source.md)
- Configurar o [destino do Teradata](teradata-destination.md)
- Em caso de dúvidas, acesse a [Tech Community](https://aka.ms/AA6iwdw).
