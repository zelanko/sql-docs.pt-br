---
title: Restaurar a caixa de diálogo de banco de dados (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.Restore.f1
ms.assetid: a3990d47-55e2-424e-8eac-87edc937e806
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 42649fd9fe8284e89aebd37c2d9b668a3ac34a2f
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66070259"
---
# <a name="restore-database-dialog-box-analysis-services---multidimensional-data"></a>Caixa de diálogo Restaurar Banco de Dados (Analysis Services - Dados multidimensionais)
  Use a caixa de diálogo **Restaurar Banco de Dados** no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para restaurar um banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] de um arquivo de backup utilizando o formato [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Backup File (.abf).  
  
> [!IMPORTANT]  
>  Para cada arquivo de backup, o usuário que executar o comando de restauração deve ter permissão para ler no local de backup especificado para cada arquivo. Para restaurar um banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que não esteja instalado no servidor, o usuário também deve ser membro da função de servidor dessa instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Para substituir um banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , o usuário deve ter uma das seguintes funções: membro da função de servidor da instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ou membro de uma função de banco de dados com permissões de Controle Total (Administrador) no banco de dados a ser restaurado.  
  
> [!NOTE]  
>  Após restaurar um banco de dados existente, o usuário que o restaurou poderá perder o acesso ao banco de dados restaurado. Essa perda de acesso pode ocorrer se, no momento da execução do backup, o usuário não for membro da função de servidor, nem membro da função de banco de dados com permissões de Controle total (Administrador).  
  
 **Para exibir a caixa de diálogo restaurar banco de dados**  
  
-   No [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], clique com o botão direito do mouse na pasta **Bancos de Dados** de uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ou em um banco de dados em **Pesquisador de Objetos**e então clique em **Restaurar**.  
  
 A caixa de diálogo **Restaurar Banco de Dados** contém as páginas a seguir.  
  
## <a name="pages"></a>Pages (Páginas)  
 **Geral**  
 Use esta página para selecionar o banco de dados a restaurar, o arquivo de backup do qual restaurar o banco de dados e também as opções gerais e senha a utilizar ao restaurar o banco de dados. Para obter mais informações sobre essa página, consulte [Geral &#40;caixa de diálogo Restaurar Banco de Dados&#41; &#40;Analysis Services – Dados Multidimensionais&#41;](general-restore-database-dialog-box-analysis-services-multidimensional-data.md).  
  
 **Partições**  
 Use esta página para restaurar partições locais a locais especificados e restaurar partições remotas de arquivos de backup remotos. Para obter mais informações sobre essa página, consulte [Partições &#40;caixa de diálogo Restaurar Banco de Dados&#41; &#40;Analysis Services – Dados Multidimensionais&#41;](partitions-restore-database-dialog-box-analysis-services-multidimensional-data.md).  
  
## <a name="see-also"></a>Consulte também  
 [Designers e caixas de diálogo do Analysis Services &#40;dados multidimensionais&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Backup e restauração de bancos de dados do Analysis Services](multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
