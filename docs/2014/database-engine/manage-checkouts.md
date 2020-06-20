---
title: Gerenciar Check-outs | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- source controls [SQL Server Management Studio], checkouts
- checkouts [SQL Server Management Studio]
- checking out files
ms.assetid: ddd4adba-d432-4005-9cb2-bb9ee3163d8e
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: cdfa25cdc27e707d4be705e66b215130c9d70ce1
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84930867"
---
# <a name="manage-checkouts"></a>Gerenciar check-outs
  Depois que um arquivo é adicionado ao controle do código-fonte, faça check-out do arquivo antes de você fazer modificações nele. Ao fazer o check-out de um arquivo com controle do código-fonte, o provedor de controle do código-fonte cria uma cópia da versão mais recente em seu disco local e remove o atributo somente leitura do arquivo. Em algumas circunstâncias, você pode precisar editar um arquivo sem fazer check-out do mesmo. Para obter mais informações sobre como editar um arquivo sem fazer check-out do arquivo, consulte [Editar arquivos com check-in](../../2014/database-engine/edit-checked-in-files.md).  
  
 Você pode usar o [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para fazer check-out de arquivos manualmente ou automaticamente. Você faz check-out dos arquivos manualmente abrindo a solução que contém os arquivos no [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] ambiente e, em seguida, clicando no comando **check-out** . Você também pode fazer check-out dos arquivos automaticamente se configurar o ambiente do [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] para essa finalidade.  
  
 Dependendo das opções definidas pelo administrador do provedor de controle de código-fonte, você também pode fazer check-out dos arquivos em modo exclusivo ou compartilhado. Quando você fizer o check-out de um arquivo exclusivamente, somente você poderá modificá-lo, nenhum outro usuário poderá fazer o check-out do arquivo até você terminar. Quando você fizer o check-out em um arquivo no modo compartilhado, qualquer número de usuários poderá fazer check-out do mesmo arquivo. Cada vez que um usuário faz check-in de um arquivo, o provedor de controle do código-fonte tenta mesclar o arquivo com a versão mais recente disponível no servidor. Caso haja conflito entre a versão de check-in e a mais recente, o provedor de controle do código-fonte solicitará que o usuário resolva os conflitos.  
  
 A tabela a seguir descreve os tópicos dessa seção.  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Fazer check-out de arquivos](../../2014/database-engine/check-out-files.md)|Fornece instruções sobre como fazer check-out de um arquivo para que você possa modificá-lo.|  
|[Desfazer check-outs](../../2014/database-engine/undo-checkouts.md)|Explica como cancelar um check-out existente.|  
|[Fazer check-out automático de arquivos na edição](../../2014/database-engine/automatically-check-out-files-upon-edit.md)|Explica como configurar o controle do código-fonte para fazer check-out de um arquivo quando você começa a editá-lo.|  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciar Check-ins](../../2014/database-engine/manage-checkins.md)   
 [Editar arquivos com check-in](../../2014/database-engine/edit-checked-in-files.md)  
  
  
