---
title: Implantar soluções de modelo usando XMLA | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5ce0f50d158d715ddbbc689c47a012a4e92ba7c4
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37994928"
---
# <a name="deploy-model-solutions-using-xmla"></a>Implantar soluções de modelo usando XMLA
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], a opção **CREATE To** do comando **Script de Banco de Dados como** cria um script XML de um banco de dados inteiro do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou de um de seus objetos constituintes. O script resultante pode ser executado em outro computador para recriar o esquema (metadados) do banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . O script gera o banco de dados inteiro e não há nenhum mecanismo para atualizar de maneira incremental objetos já implantados ao usar o script. Depois de executar o script e implantar o banco de dados, o banco de dados recém-criado deve ser processado antes de os usuários poderem navegar nele.  
  
 Para obter mais informações sobre o comando **Script de Banco de Dados como** , consulte [Documentar e gerar scripts de um banco de dados do Analysis Services](../../analysis-services/multidimensional-models/document-and-script-an-analysis-services-database.md).  
  
## <a name="modifying-object-properties-in-the-xml-script"></a>Modificando as propriedades do objeto no script XML  
 Ao usar o comando **Script de Banco de Dados como** , você não pode modificar propriedades específicas (como o nome do banco de dados, as cadeias de caracteres de conexão da fonte de dados e as configurações de segurança) dos objetos do banco de dados. Essas propriedades devem ser modificadas manualmente no script depois que o script tiver sido gerado ou devem ser modificadas no banco de dados implantado depois de executar o script.  
  
> [!IMPORTANT]  
>  O script XML não conterá a senha se isso for especificado na cadeia de caracteres de conexão para uma fonte de dados ou para propósitos de representação. Considerando que a senha é necessária para propósitos de processamento nesse cenário, você precisará adicioná-la manualmente ao script XML antes de ele ser executado ou adicioná-la depois que o script XML tiver sido executado.  
  
## <a name="see-also"></a>Consulte também  
 [Deploy Model Solutions Using the Deployment Wizard](../../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)   
 [Sincronizar bancos de dados do Analysis Services](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)  
  
  
