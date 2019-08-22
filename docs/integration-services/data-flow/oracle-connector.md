---
title: Microsoft Connector para Oracle | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a0ad547d26c86c43b0009cdf20acae33ed7e8ab7
ms.sourcegitcommit: 57e20b7d02853ec9af46b648106578aed133fb45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2019
ms.locfileid: "69553234"
---
# <a name="microsoft-connector-for-oracle"></a>Microsoft Connector para Oracle

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

O Microsoft Connector para Oracle permite explorar dados e carregar dados da origem do Oracle em um pacote SSIS.

## <a name="version-support"></a>Suporte à versão

Os seguintes produtos do Microsoft SQL Server são suportados pelo Microsoft Connector para Oracle:

- A partir do SQL Server 2019
- SQL Server Data Tools (SSDT)

As seguintes versões do Oracle Database de fontes de dados têm suporte:

- Oracle 10.x
- Oracle 11.x
- Oracle 12c
- Oracle 18c (sem o suporte à Autenticação do Windows)

O Oracle Database tem suporte em todos os sistemas operacionais e plataformas.
> [!NOTE]
>
> O cliente Oracle não é necessário para o Microsoft Connector para o Oracle Database no SQL Server 2019.

## <a name="installation"></a>Instalação

Se você precisar executar o pacote no SQL Server, obtenha o Microsoft Connector para o programa de instalação do Oracle Database [aqui](https://www.microsoft.com/en-us/download/details.aspx?id=58228). Em seguida, siga as instruções no assistente de instalação.

Depois de instalar o Connector, reinicie o Serviço de Integração do SQL Server para verificar se a origem e o destino Oracle estão funcionando corretamente.

Se você precisar criar um pacote com o Connector, não é preciso baixar o Connector. Ele já está incluso no SQL Server Data Tools (SSDT) desde a versão 15.9.0.

## <a name="uninstallation"></a>Desinstalação

Você pode executar o assistente de desinstalação para remover o Microsoft Connector para Oracle Database do SQL Server.

## <a name="design-ssis-package-with-previous-version"></a>Criar o pacote do SSIS com a versão anterior

Desde a versão 15.9.0, o SSDT já inclui o Microsoft Connector para o Oracle Database, portanto, não é necessário instalar nada ao criar pacotes do SSIS para SQL Server 2019.

Para criar um pacote do SSIS para o SQL Server 2017 e versões anteriores, é preciso instalar o Connector para Oracle da Attunity com a versão correspondente.

**Links para download:**

- [SQL Server 2017: Microsoft Connector versão 5.0 para Oracle da Attunity](https://www.microsoft.com/en-us/download/details.aspx?id=55179)
- [SQL Server 2016: Microsoft Connector versão 4.0 para Oracle da Attunity](https://www.microsoft.com/en-us/download/details.aspx?id=52950)
- [SQL Server 2014: Microsoft Connector versão 3.0 para Oracle da Attunity](https://www.microsoft.com/en-us/download/details.aspx?id=44582)
- [SQL Server 2012: Microsoft Connector versão 2.0 para Oracle da Attunity](https://www.microsoft.com/en-us/download/details.aspx?id=29283)

## <a name="next-steps"></a>Próximas etapas

- Configurar o [Gerenciador de Conexões do Oracle](oracle-connection-manager.md).
- Configurar a [Origem do Oracle](oracle-source.md).
- Configurar o [Destino Oracle](oracle-destination.md).
- Caso tenha dúvidas, visite a [TechCommunity](https://aka.ms/AA5u35j).
