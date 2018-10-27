---
title: As opções de backup | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 62f5bf26f80ea1018a5a3330efa0f055021ff0f5
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50145431"
---
# <a name="backup-options"></a>Opções de backup
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Há várias maneiras de fazer backup dos bancos de dados do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e todos eles exigem que você tenha permissões de administrador do servidor e de banco de dados. É possível abrir a caixa de diálogo **Backup** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], selecionar a configuração de opções apropriada e executar o backup na própria caixa de diálogo. Ou, você pode criar um script que usa as configurações já especificadas no arquivo; depois o script pode ser salvo e executado sempre que necessário.  
  
## <a name="backup-and-synchronize"></a>Backup e sincronização  
 Se o banco de dados estiver em uma instância remota do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], você poderá usar o recurso de sincronização para fazer backup do banco de dados na instância local. As compilações de desenvolvimento de um banco de dados podem ser movidas para produção dessa maneira. Também é possível usar o backup convencional, baseado em arquivo, e fazer a restauração para mover a compilação de desenvolvimento para produção, mas a sincronização fornece uma funcionalidade adicional. Por exemplo, é possível ter configurações de segurança diferentes para os computadores de desenvolvimento e produção; a sincronização fornecerá a você a opção de manter essas configurações e sincronizar todos os objetos que não sejam funções. A sincronização também faz normalmente uma atualização incremental desses objetos que são diferentes para os computadores de origem e destino. Esse tipo de backup incremental não está disponível para usar o recurso de backup/restauração. Para obter mais informações, consulte [Sincronizar bancos de dados do Analysis Services](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md).  
  
> [!IMPORTANT]  
>  A conta de serviço do Analysis Services deve ter permissão para gravar no local de backup especificado de cada arquivo. Além disso, o usuário deve ter uma das seguintes funções: função de administrador na instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou membro de uma função de banco de dados com permissões de Controle total (Administrador) no banco de dados do qual será feito o backup.  
  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo Banco de Dados de Backup &#40;Analysis Services – Dados multidimensionais&#41;](http://msdn.microsoft.com/library/7811ce7d-6c37-4189-bfa6-ef36fb4932db)   
 [Backup e restauração de bancos de dados do Analysis Services](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)   
 [Elemento Backup &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla)   
 [Fazendo backup, restaurando e sincronizando bancos de dados &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)  
  
  
