---
title: Implantar soluções modelo usando XMLA | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- XML scripts [Analysis Services]
- scripts [Analysis Services], deployment
- deploying [Analysis Services], XML scripts
- Analysis Services deployments, XML scripts
ms.assetid: a8cb1837-fcac-4730-bea4-a72cf94d9f7c
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 872f4297aa6d98c35b85bb81588c27d1060066fd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019943"
---
# <a name="deploy-model-solutions-using-xmla"></a>Implantar soluções de modelo usando XMLA
  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], a opção **CREATE To** do comando **Script de Banco de Dados como** cria um script XML de um banco de dados inteiro do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou de um de seus objetos constituintes. O script resultante pode ser executado em outro computador para recriar o esquema (metadados) do banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . O script gera o banco de dados inteiro e não há nenhum mecanismo para atualizar de maneira incremental objetos já implantados ao usar o script. Depois de executar o script e implantar o banco de dados, o banco de dados recém-criado deve ser processado antes de os usuários poderem navegar nele.  
  
 Para obter mais informações sobre o comando **Script de Banco de Dados como** , consulte [Documentar e gerar scripts de um banco de dados do Analysis Services](document-and-script-an-analysis-services-database.md).  
  
## <a name="modifying-object-properties-in-the-xml-script"></a>Modificando as propriedades do objeto no script XML  
 Ao usar o comando **Script de Banco de Dados como** , você não pode modificar propriedades específicas (como o nome do banco de dados, as cadeias de caracteres de conexão da fonte de dados e as configurações de segurança) dos objetos do banco de dados. Essas propriedades devem ser modificadas manualmente no script depois que o script tiver sido gerado ou devem ser modificadas no banco de dados implantado depois de executar o script.  
  
> [!IMPORTANT]  
>  O script XML não conterá a senha se isso for especificado na cadeia de caracteres de conexão para uma fonte de dados ou para propósitos de representação. Considerando que a senha é necessária para propósitos de processamento nesse cenário, você precisará adicioná-la manualmente ao script XML antes de ele ser executado ou adicioná-la depois que o script XML tiver sido executado.  
  
## <a name="see-also"></a>Consulte também  
 [Implantar soluções modelo usando o Assistente de implantação](deploy-model-solutions-using-the-deployment-wizard.md)   
 [Sincronizar bancos de dados do Analysis Services](synchronize-analysis-services-databases.md)  
  
  