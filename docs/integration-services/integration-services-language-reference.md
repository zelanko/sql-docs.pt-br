---
title: Referência de Linguagem do Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: c67b72f1-0a1e-42f0-878a-84e85efc915b
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: da169ff3be06b9617ddf5fc7929254bee91037ce
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/14/2018
ms.locfileid: "51642303"
---
# <a name="integration-services-language-reference"></a>Referência de Linguagem do Integration Services
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Esta seção descreve a API [!INCLUDE[tsql](../includes/tsql-md.md)] para administração de projetos do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] implantados em uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 O [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] armazena objetos, configurações e dados operacionais em um banco de dados chamado de catálogo do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. O nome padrão do catálogo [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] é SSISDB. Os objetos armazenados no catálogo incluem projetos, pacotes, parâmetros, ambientes e histórico operacional.  
  
 O catálogo do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] armazena seus dados em tabelas internas que não são visíveis aos usuários. Porém, ele expõe as informações necessárias por meio de um conjunto de exibições públicas que você pode consultar. Também fornece um conjunto de procedimentos armazenados que você pode usar para executar tarefas comuns no catálogo.  
  
 Normalmente, você gerencia objetos do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no catálogo por meio da abertura do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. No entanto, você também pode usar as exibições de banco de dados e chamar os procedimentos armazenados diretamente, ou escrever código personalizado que chame a API gerenciada. O [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] e a API gerenciada consultam as exibições e chamam os procedimentos armazenados descritos nesta seção para executar muitas de suas tarefas.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Exibições &#40;catálogo do Integration Services&#41;](../integration-services/system-views/views-integration-services-catalog.md)  
 Consulte as exibições para inspecionar objetos, configurações e dados operacionais do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
 [Procedimentos armazenados &#40;catálogo do Integration Services&#41;](../integration-services/system-stored-procedures/stored-procedures-integration-services-catalog.md)  
 Chame os procedimentos armazenados para adicionar, remover ou modificar objetos e configurações do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
 [Funções &#40;catálogo do Integration Services&#41;](https://msdn.microsoft.com/library/9f2aec85-3d4c-415f-b1f8-8328a60b1c7f)  
 Chame as funções para administrar projetos do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
  
