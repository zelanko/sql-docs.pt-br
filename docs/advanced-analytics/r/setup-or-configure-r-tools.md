---
title: Ferramentas de R incluídas com a instalação do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 10/31/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7c04ae30-d391-4369-9742-d2b275e14c0d
caps.latest.revision: ''
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 8178f4a1347ef58fd7ee143fbe843e3525ac4cf0
ms.sourcegitcommit: 270de8a0260fa3c0ecc37f91eec4a5aee9b9834a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2018
---
# <a name="r-tools-included-with-sql-server-setup"></a>Ferramentas de R incluídas com a instalação do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Quando você instala o R com o SQL Server, você obtém as mesmas ferramentas de R que são instaladas com qualquer **base** instalação do R, como RGui, Rterm e assim por diante. Portanto, tecnicamente, você tem todas as ferramentas que você precisa para desenvolver e testar o código de R.

Este tópico lista as ferramentas incluídas com a instalação.

> [!TIP]
> 
> Geralmente é mais fácil depurar e testar o código R usando um ambiente de desenvolvimento dedicado. Você encontrará mais fáceis de executar seu código R no SQL Server, se você testá-lo com antecedência em uma ferramenta externa, para que você possa ler mensagens de erro detalhadas e depurar a solução.
> 
> Consulte este artigo para obter uma lista de ferramentas gratuitas que você pode usar para desenvolver soluções de R e como configurá-los para trabalhar com o SQL Server: [configurar um cliente de ciência de dados](set-up-a-data-science-client.md)

**Aplica-se a:** SQL Server 2016 R Services (no banco de dados) e Microsoft R Server (autônomo); SQL Server 2017 Services (no banco de dados) de aprendizado de máquina e Server (autônomo) de aprendizado de máquina

## <a name="r-tools-included-with-installation"></a>Ferramentas de R incluídas com a instalação

As seguintes ferramentas de R padrão são incluídas em um *base instalação* do R e, portanto, são instalados por padrão.

+ **O RTerm**: um terminal de linha de comando para execução de scripts de R

+ **RGui.exe**: um editor interativo simples de R. Os argumentos de linha de comando são os mesmos para RGui.exe e RTerm.

+ **RScript**: uma ferramenta de linha de comando para executar scripts R no modo de lote.

Para localizar essas ferramentas, determine a biblioteca de R instalado quando você configurar o SQL Server ou a recurso de aprendizado de máquina autônomo. Por exemplo, em uma instalação padrão, as ferramentas de R estão localizadas nessas pastas:

+ SQL Server 2016 R Services: `~\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64`
+ Microsoft R Server autônomo: `~\Program Files\Microsoft R\R_SERVER\bin\x64`
+ SQL Server 2017 aprendizado de máquina serviços: `~\Program Files\Microsoft SQL Server\MSSQL14.<instancename>\R_SERVICES\bin\x64`
+ Server (autônomo) de aprendizado de máquina: `~\Program Files\Microsoft\ML Server\R_SERVER\bin\x64`

Se você precisar de ajuda com as ferramentas de R, basta abrir **RGui**, clique em **ajuda**e selecione uma das opções.

## <a name="introducing-microsoft-r-client"></a>Introdução ao cliente Microsoft R

O cliente do Microsoft R é um download gratuito que permite o acesso aos pacotes RevoScaleR para uso de desenvolvimento. Instalando o cliente do R, você pode criar soluções de R que podem ser executadas em todos os contextos de computação com suporte, incluindo a análise do SQL Server no banco de dados e computação distribuída de R no Hadoop, Spark ou Linux usando o servidor de aprendizado de máquina.

Se você já tiver instalado um ambiente de desenvolvimento R diferente, como RStudio, certifique-se reconfigurar o ambiente para usar as bibliotecas e executáveis fornecidos pelo cliente do Microsoft R. Ao fazer isso, você pode usar todos os recursos do pacote RevoScaleR, embora o desempenho será limitado.

Para obter mais informações, consulte [o que é cliente do Microsoft R?](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)
