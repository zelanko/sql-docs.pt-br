---
title: "Opções de backup | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- backing up databases [Analysis Services]
- databases [Analysis Services], backing up
ms.assetid: 02d33fc9-f3f4-4b85-8b90-449b68625cf7
caps.latest.revision: "26"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c8d6af5bf906e5889f0b974537651f46df6ecd68
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="backup-options"></a>Opções de backup
  Há várias maneiras de fazer backup dos bancos de dados do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e todos eles exigem que você tenha permissões de administrador do servidor e de banco de dados. É possível abrir a caixa de diálogo **Backup** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], selecionar a configuração de opções apropriada e executar o backup na própria caixa de diálogo. Ou, você pode criar um script que usa as configurações já especificadas no arquivo; depois o script pode ser salvo e executado sempre que necessário.  
  
## <a name="backup-and-synchronize"></a>Backup e sincronização  
 Se o banco de dados estiver em uma instância remota do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], você poderá usar o recurso de sincronização para fazer backup do banco de dados na instância local. As compilações de desenvolvimento de um banco de dados podem ser movidas para produção dessa maneira. Também é possível usar o backup convencional, baseado em arquivo, e fazer a restauração para mover a compilação de desenvolvimento para produção, mas a sincronização fornece uma funcionalidade adicional. Por exemplo, é possível ter configurações de segurança diferentes para os computadores de desenvolvimento e produção; a sincronização fornecerá a você a opção de manter essas configurações e sincronizar todos os objetos que não sejam funções. A sincronização também faz normalmente uma atualização incremental desses objetos que são diferentes para os computadores de origem e destino. Esse tipo de backup incremental não está disponível para usar o recurso de backup/restauração. Para obter mais informações, consulte [Sincronizar bancos de dados do Analysis Services](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md).  
  
> [!IMPORTANT]  
>  A conta de serviço do Analysis Services deve ter permissão para gravar no local de backup especificado de cada arquivo. Além disso, o usuário deve ter uma das seguintes funções: função de administrador na instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou membro de uma função de banco de dados com permissões de Controle total (Administrador) no banco de dados do qual será feito o backup.  
  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo Banco de Dados de Backup &#40;Analysis Services – Dados multidimensionais&#41;](http://msdn.microsoft.com/library/7811ce7d-6c37-4189-bfa6-ef36fb4932db)   
 [Backup e restauração de bancos de dados do Analysis Services](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)   
 [Elemento de backup &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)   
 [Fazendo backup, restaurando e sincronizando bancos de dados &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)  
  
  
