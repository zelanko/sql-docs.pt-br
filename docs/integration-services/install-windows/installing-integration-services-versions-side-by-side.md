---
title: "Instalando o Integration Services lado a lado de versões | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interoperability and coexistence [Integration Services]
- Integration Services, interoperability and coexistence
ms.assetid: edfbcd56-012f-462e-a542-95491394fda9
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 114e51f111e4b3dfece42c9510a35bb9be5d5652
ms.contentlocale: pt-br
ms.lasthandoff: 09/27/2017

---
# <a name="installing-integration-services-versions-side-by-side"></a>Instalando as Versões do Integration Services Lado a Lado
  Você pode instalar   
      [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]Integration Services (SSIS)-lado a lado com versões anteriores do SSIS. Este tópico descreve algumas limitações das instalações lado a lado.  
  
## <a name="designing-and-maintaining-packages"></a>Criação e manutenção de pacotes  
 Para criar e manter pacotes destinados ao SQL Server 2016, SQL Server 2014 ou SQL Server 2012, use o SQL Server Data Tools (SSDT) para Visual Studio 2015. Para obter o SSDT, consulte [Baixar o SQL Server Data Tools mais recente](../../ssdt/download-sql-server-data-tools-ssdt.md).  
  
 Na página de propriedades de um projeto do Integration Services, na guia **Geral** de **Propriedades de Configuração**, selecione a propriedade **TargetServerVersion** e escolha o SQL Server 2016, SQL Server 2014 ou SQL Server 2012.  
  
|Versão de destino do SQL Server|Ambiente de desenvolvimento para os pacotes do SSIS|  
|----------------------------------|-----------------------------------------------|  
|2016|SQL Server Data Tools para Visual Studio 2015|  
|2014|SQL Server Data Tools para Visual Studio 2015<br /><br /> ou<br /><br /> SQL Server Data Tools - Business Intelligence para Visual Studio 2013|  
|2012|SQL Server Data Tools para Visual Studio 2015<br /><br /> ou<br /><br /> SQL Server Data Tools – Business Intelligence para Visual Studio 2012|  
|2008|Business Intelligence Development Studio do SQL Server 2008|  
  
 Quando você adiciona um pacote existente a um projeto existente, o pacote é convertido para o formato de destino do projeto.  
  
## <a name="running-packages"></a>Pacotes em execução  
 Você pode usar a versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do utilitário **dtexec** ou do Agente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para executar pacotes do Integration Services criados por versões anteriores das ferramentas de desenvolvimento. Quando essas ferramentas do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] carregam um pacote criado em uma versão anterior das ferramentas de desenvolvimento, a ferramenta converte temporariamente o pacote na memória para o formato de pacote que o [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] usa. Se o pacote tiver problemas que impedem uma conversão bem-sucedida, a ferramenta do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] não poderá executar o pacote até que esses problemas sejam resolvidos. Para obter mais informações, veja [Atualizar pacotes do Integration Services](../../integration-services/install-windows/upgrade-integration-services-packages.md).  
  
  

