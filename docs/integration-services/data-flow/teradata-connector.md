---
description: Conector da Microsoft para o Teradata
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
ms.openlocfilehash: a866d7d1083435acffeb157edf9fe4a0bb725d3e
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88425758"
---
# <a name="microsoft-connector-for-teradata"></a>Conector da Microsoft para o Teradata

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

O Microsoft Connector para Teradata permite exportar dados de bancos de dados Teradata e carregar dados neles em um pacote SSIS.

Esse novo conector dá suporte a bancos de dados com tabelas habilitadas para 1 MB.

## <a name="version-support"></a>Suporte à versão

Há suporte para os seguintes produtos do Microsoft SQL Server no Microsoft Connector para Teradata:

- Microsoft SQL Server 2019
- Microsoft SSDT (SQL Server Data Tools) 15.8.1 ou posterior para Visual Studio 2017
- Microsoft SSDT (SQL Server Data Tools) para Visual Studio 2019

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

Em computadores de 32 bits, instale os seguintes drivers de [Ferramentas e utilitários do Teradata: pacote de instalação do Windows](https://downloads.teradata.com/download/tools/teradata-tools-and-utilities-windows-installation-package):

- Driver ODBC do Teradata (32 bits)
- API do Teradata PT (32 bits)

Em computadores de 64 bits, instale os seguintes drivers:

- Driver ODBC do Teradata (64 bits)
- API do Teradata PT (64 bits)

Para instalar o conector para o banco de dados Teradata, baixe e execute o instalador da [última versão do Microsoft Connector para Teradata](https://www.microsoft.com/download/details.aspx?id=100599). Em seguida, siga as instruções no assistente de instalação.

Depois de instalar o conector, reinicie o SQL Server Integration Services para verificar se a origem e o destino do Teradata estão funcionando corretamente.

## <a name="design-and-execute-ssis-packages"></a>Projetar e executar pacotes SSIS

O Microsoft Connector para Teradata fornece uma experiência de usuário semelhante com o Conector Teradata da Attunity. O usuário pode criar novos pacotes com base na experiência anterior, usando o SSDT para VS 2017 ou VS 2019, com *direcionamento para SQL Server 2019*.

A origem e o destino do Teradata estão na categoria Comum.

![O Componente do Teradata](media/teradata-component.png)

O gerenciador de conexões do Teradata é exibido como "TERADATA".

![O tipo do gerenciador de conexões do Teradata](media/teradata-connection-manager-type.png)

Os pacotes SSIS existentes que foram projetados com o Conector Teradata da Attunity serão atualizados automaticamente para usar o Microsoft Connector para Teradata. Os ícones também serão alterados.

Para executar o pacote SSIS com *direcionamento para o SQL Server 2017 e anterior*, você precisará instalar o **Microsoft Connector para Teradata da Attunity** com a versão correspondente usando o link abaixo:

- [SQL Server 2017: Microsoft Connector versão 5.0 para Teradata da Attunity](https://www.microsoft.com/download/details.aspx?id=55179)
- [SQL Server 2016: Microsoft Connector versão 4.0 para Teradata da Attunity](https://www.microsoft.com/download/details.aspx?id=52950)
- [SQL Server 2014: Microsoft Connector versão 3.0 para Teradata da Attunity](https://www.microsoft.com/download/details.aspx?id=44582)
- [SQL Server 2012: Microsoft Connector versão 2.0 para Teradata da Attunity](https://www.microsoft.com/download/details.aspx?id=29283)

Para projetar o pacote SSIS com o *direcionamento de SSDT para o SQL Server 2017 e anterior*, você precisará ter o **Microsoft Connector para Teradata** e instalar o **Microsoft Connector para Teradata da Attunity** com a versão correspondente.

## <a name="limitations-and-known-issues"></a>Limitações e problemas conhecidos

- No Editor de Origem/Destino do Teradata, a propriedade do **banco de dados padrão** não tem efeito.  Como solução alternativa, digite nome do banco de dados na caixa suspensa para filtrar a tabela ou a exibição.

- No Editor de Origem/Destino do Teradata, a etapa de mapeamento não funcionará quando o tipo for \<database>.<table/view>. Como solução alternativa, digite \<database>.<table/view> e clique no botão suspenso.

- No Editor de Origem do Teradata, a exibição não poderá ser exibida quando o modo de Acesso a dados for "Nome da Tabela – Exportação de TPT". Como solução alternativa, use o Editor Avançado da Origem do Teradata.

- No Destino de Teradata, o atributo ‘PackMaximum’ não pode ser configurado para ‘True’.  Caso contrário, ocorrerá um erro.

## <a name="uninstallation"></a>Desinstalação

Execute o assistente de desinstalação para remover o **Microsoft Connector para Teradata**.

## <a name="next-steps"></a>Próximas etapas

- Configurar o [gerenciador de conexões do Teradata](teradata-connection-manager.md)
- Configurar a [origem do Teradata](teradata-source.md)
- Configurar o [destino do Teradata](teradata-destination.md)
- Em caso de dúvidas, acesse a [Tech Community](https://aka.ms/AA6iwdw).
