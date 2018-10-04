---
title: Opções de restauração | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- databases [Analysis Services], restoring
- restoring databases [Analysis Services]
ms.assetid: 75c73802-f321-4671-afc7-54505d62c013
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 348e3254cb31cfef72e40b35ac74cbe9cf578834
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48060352"
---
# <a name="restore-options"></a>Opções de restauração
  Há muitos modos de restaurar bancos de dados do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e todos eles requerem que você tenha permissões de administrador de computador servidor e de banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Para restaurar um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , você pode abrir a caixa de diálogo **Restaurar Banco de Dados** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], selecionar a configuração de opções apropriadas e depois executar a restauração na caixa de diálogo. Ou, você pode criar um script que usa as configurações já especificadas no arquivo; o script pode ser salvo e executado sempre que necessário. Desse modo, a restauração é concluída usando o XMLA, como descrito na próxima seção.  
  
## <a name="restoring-databases-using-xmla"></a>Restaurando bancos de dados usando o XMLA  
 O comando XMLA Restore é um modo de automatizar o processo de restauração executando uma restauração com base em um arquivo .abf. O comando Restore tem várias propriedades que podem ser definidas para especificar definições de segurança, onde partições remotas deveriam ser armazenadas e a realocação de objetos relacionais OLAP (ROLAP). Para obter mais informações, consulte [Restore Element &#40;XMLA&#41;](../xmla/xml-elements-commands/restore-element-xmla.md).  
  
> [!IMPORTANT]  
>  Para cada arquivo de backup, o usuário que executar o comando de restauração deve ter permissão para ler no local de backup especificado para cada arquivo. Para restaurar um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que não esteja instalado no servidor, o usuário também deve ser membro da função de servidor dessa instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Para substituir um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , o usuário deve ter uma das seguintes funções: membro da função de servidor da instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou membro de uma função de banco de dados com permissões de Controle Total (Administrador) no banco de dados a ser restaurado.  
  
> [!NOTE]  
>  Após restaurar um banco de dados existente, o usuário que o restaurou poderá perder o acesso ao banco de dados restaurado. Essa perda de acesso pode ocorrer se, no momento da execução do backup, o usuário não for membro da função de servidor, nem membro da função de banco de dados com permissões de Controle total (Administrador).  
  
## <a name="see-also"></a>Consulte também  
 [Restaurar a caixa de diálogo banco de dados &#40;Analysis Services - dados multidimensionais&#41;](../restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [Backup e restauração de bancos de dados do Analysis Services](backup-and-restore-of-analysis-services-databases.md)   
 [Restaurar o elemento &#40;XMLA&#41;](../xmla/xml-elements-commands/restore-element-xmla.md)   
 [Fazendo backup, restaurando e sincronizando bancos de dados &#40;XMLA&#41;](../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)  
  
  
