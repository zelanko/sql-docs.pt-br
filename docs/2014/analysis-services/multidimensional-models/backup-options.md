---
title: As opções de backup | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- backing up databases [Analysis Services]
- databases [Analysis Services], backing up
ms.assetid: 02d33fc9-f3f4-4b85-8b90-449b68625cf7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5047647ef5f440987b4b20db99ad42dacf4fc4d0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62726975"
---
# <a name="backup-options"></a>Opções de backup
  Há várias maneiras de fazer backup dos bancos de dados do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e todos eles exigem que você tenha permissões de administrador do servidor e de banco de dados. É possível abrir a caixa de diálogo **Backup** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], selecionar a configuração de opções apropriada e executar o backup na própria caixa de diálogo. Ou, você pode criar um script que usa as configurações já especificadas no arquivo; depois o script pode ser salvo e executado sempre que necessário.  
  
## <a name="backup-and-synchronize"></a>Backup e sincronização  
 Se o banco de dados estiver em uma instância remota do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], você poderá usar o recurso de sincronização para fazer backup do banco de dados na instância local. As compilações de desenvolvimento de um banco de dados podem ser movidas para produção dessa maneira. Também é possível usar o backup convencional, baseado em arquivo, e fazer a restauração para mover a compilação de desenvolvimento para produção, mas a sincronização fornece uma funcionalidade adicional. Por exemplo, é possível ter configurações de segurança diferentes para os computadores de desenvolvimento e produção; a sincronização fornecerá a você a opção de manter essas configurações e sincronizar todos os objetos que não sejam funções. A sincronização também faz normalmente uma atualização incremental desses objetos que são diferentes para os computadores de origem e destino. Esse tipo de backup incremental não está disponível para usar o recurso de backup/restauração. Para obter mais informações, consulte [Sincronizar bancos de dados do Analysis Services](synchronize-analysis-services-databases.md).  
  
> [!IMPORTANT]  
>  A conta de serviço do Analysis Services deve ter permissão para gravar no local de backup especificado de cada arquivo. Além disso, o usuário deve ter uma das seguintes funções: função de administrador na instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou membro de uma função de banco de dados com permissões de Controle total (Administrador) no banco de dados do qual será feito o backup.  
  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo Banco de Dados de Backup &#40;Analysis Services – Dados multidimensionais&#41;](../backup-database-dialog-box-analysis-services-multidimensional-data.md)   
 [Backup e restauração de bancos de dados do Analysis Services](backup-and-restore-of-analysis-services-databases.md)   
 [Elemento Backup &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla)   
 [Fazendo backup, restaurando e sincronizando bancos de dados &#40;XMLA&#41;](../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)  
  
  
