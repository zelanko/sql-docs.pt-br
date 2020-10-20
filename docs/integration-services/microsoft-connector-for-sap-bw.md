---
description: Microsoft Connector for SAP BW
title: Microsoft Connector para SAP BW | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5281f080-53d5-4679-aa26-f4cd4ac7a2df
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 05fefa983f3b58f8ca8be95772d3fbc49f3e9afb
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194041"
---
# <a name="microsoft-connector-for-sap-bw"></a>Microsoft Connector for SAP BW

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  O [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW consiste em um conjunto de três componentes que permitem extrair dados do sistema SAP Netweaver BW versão 7 ou carregar dados nele.  
  
 O [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW para SQL Server 2016 é um componente do SQL Server 2016 Feature Pack. Para instalar o Connector for SAP BW e sua documentação, baixe e execute o instalador na [página Web do SQL Server 2016 Feature Pack](https://go.microsoft.com/fwlink/?LinkId=746297).  

> [!IMPORTANT]
> Microsoft não prevê o fornecimento de uma versão atualizada do Connector para SAP BW. A Microsoft não é proprietária do código-fonte para os componentes do SAP BW, que foram desenvolvidos por terceiros, e, portanto, não pode atualizá-los. Considere a possibilidade de adquirir os componentes de conectividade SAP mais recentes de um parceiro de ISV da Microsoft, como a [Theobald Software](https://theobald-software.com/en/xtract-is-productinfo.html). Os parceiros de ISV da Microsoft adaptaram seus componentes de conectividade SAP para SSIS para instalação no Azure.
 
> [!IMPORTANT]  
>  A documentação do Microsoft Connector for SAP BW supõe familiaridade com o ambiente do SAP Netweaver BW. Para obter mais informações sobre o SAP Netweaver BW ou para obter informações sobre como configurar objetos e processos do SAP Netweaver BW, consulte sua documentação do SAP.  
  
> [!IMPORTANT]  
>  A extração de dados do SAP Netweaver BW exige licenciamento SAP adicional. Verifique esses requisitos com a SAP.  
  
## <a name="components"></a>Componentes  
 O [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW tem os seguintes componentes:  
  
-   **Origem do SAP BW** – a origem do SAP BW é um componente de origem de fluxo de dados que permite extrair dados de um sistema SAP Netweaver BW versão 7.  
  
-   **Destino do SAP BW** – o destino do SAP BW é um componente de destino de fluxo de dados que permite carregar dados em um sistema SAP Netweaver BW versão 7.  
  
-   **Gerenciador de conexões do SAP BW** – o gerenciador de conexões do SAP BW conecta uma origem do SAP BW ou um destino do SAP BW a um sistema SAP Netweaver BW versão 7.  
  
 Para obter um passo a passo que demonstre como configurar e usar o gerenciador de conexões do SAP BW, a origem e o destino, consulte o white paper [Usando o SQL Server Integration Services com SAP BI 7.0](/previous-versions/sql/sql-server-2008/dd299430(v=sql.100)). Este white paper também mostra como configurar os objetos necessários no SAP BW.  
  
## <a name="documentation"></a>Documentação  
 Este arquivo da Ajuda para o [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW contém os seguintes tópicos e seções:  
  
 [Instalação do Microsoft Connector para SAP BW](../integration-services/installing-the-microsoft-connector-for-sap-bw.md)  
 Descreve os requisitos de instalação para o [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW.  
  
 [Componentes do Microsoft Connector 1.1 para SAP BW](../integration-services/microsoft-connector-for-sap-bw-components.md)  
 Descreve cada componente do [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW.  
  
 [Ajuda F1 do Microsoft Connector para SAP BW](../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
 Descreve a interface do usuário de cada componente do [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW.  
  
