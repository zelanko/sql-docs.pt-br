---
title: Microsoft Connectors para Oracle e Teradata da attunity (SSIS) | Microsoft Docs
ms.date: 05/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 926c0c51b5a55a2869b73666f5620fa56e139cca
ms.openlocfilehash: fd8b0177227167f6caa3417029bb2acb974fe181
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="microsoft-connectors-for-oracle-and-teradata-by-attunity-for-integration-services-ssis"></a>Microsoft Connectors para Oracle e Teradata da attunity para o Integration Services (SSIS)

Você pode baixar os conectores para o Integration Services attunity que otimizar o desempenho ao carregar dados de ou para Oracle ou Teradata em um pacote do SSIS.

## <a name="download-the-latest-attunity-connectors"></a>Baixe os conectores Attunity mais recentes

Obter a versão mais recente dos conectores aqui:  
[V 5.0 da Microsoft Connectors para Oracle e Teradata](https://www.microsoft.com/download/details.aspx?id=55179)

## <a name="issue---the-attunity-connectors-arent-visible-in-the-ssis-toolbox"></a>Problema - os conectores Attunity não são visíveis na caixa de ferramentas do SSIS

Para ver os conectores da Attunity na caixa de ferramentas do SSIS, sempre é necessário instalar a versão dos conectores que destinos a mesma versão do SQL Server como a versão do SQL Server Data Tools (SSDT) instalado em seu computador. (Você também pode ter versões anteriores dos conectores instalados). Esse requisito é independente da versão do SQL Server que você deseja direcionar em seus projetos do SSIS e pacotes.

Por exemplo, se você tiver instalado a versão mais recente do SSDT, você tem a versão 17 do SSDT com um número de compilação que começa com 14. Esta versão do SSDT adiciona suporte para SQL Server 2017. Para ver e usar a Attunity conectores no SSIS pacote desenvolvimento - mesmo se você deseja direcionar uma versão anterior do SQL Server, você também precisa instalar a versão mais recente dos conectores da Attunity, versão 5.0. Esta versão dos conectores também adiciona suporte para SQL Server 2017.

Verificar a versão instalada do SSDT no Visual Studio de **ajuda** | **sobre o Microsoft Visual Studio**, ou em **programas e recursos** no painel de controle. Em seguida, instale a versão correspondente dos conectores da Attunity da tabela a seguir.

|Versão do SSDT|Número de compilação do SSDT|Versão do SQL Server de destino|Versão necessária de conectores|
|---------|---------|---------|---------|
|17|Inicia com 14|SQL Server 2017|[V 5.0 da Microsoft Connectors para Oracle e Teradata](https://www.microsoft.com/download/details.aspx?id=55179)|
|16|Inicia com 13|SQL Server 2016|[V 4.0 do Microsoft Connectors para Oracle e Teradata](https://www.microsoft.com/download/details.aspx?id=52950)|
||||

## <a name="download-the-latest-sql-server-data-tools-ssdt"></a>Baixe o mais recente SQL Server Data Tools (SSDT)

Obter a versão mais recente do SSDT aqui:  
[Baixar o SQL Server Data Tools (SSDT)](..//ssdt/download-sql-server-data-tools-ssdt.md)
