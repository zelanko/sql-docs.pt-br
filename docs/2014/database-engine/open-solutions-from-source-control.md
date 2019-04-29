---
title: Abrir soluções do controle do código-fonte | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- opening solutions
- solutions [SQL Server Management Studio], opening
ms.assetid: a96a1f0d-0183-4587-a3b0-4598309cbdd2
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9f8405c9fcb04559b6f25d2244bc36dde760a182
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62844760"
---
# <a name="open-solutions-from-source-control"></a>Abrir soluções no controle do código-fonte
  Você pode usar o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para abrir soluções diretamente do controle do código-fonte. Quando você faz isso, o ambiente do Studio cria uma cópia da última versão dos arquivos da solução no local que você especifica.  
  
 Se não existir uma cópia local da solução em seu disco local, abra o projeto a partir do controle do código-fonte antes de poder usar o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para fazer o check-out da solução ou recuperar os arquivos da solução.  
  
> [!NOTE]  
>  Se você já tiver uma cópia local da solução que você está abrindo a partir do controle do código-fonte, será solicitado a substituir a cópia local.  
  
### <a name="to-open-a-solution-from-source-control"></a>Para abrir uma solução no controle do código-fonte  
  
1.  Sobre o **arquivo** , aponte para **controle do código-fonte**e clique em **abrir do controle de origem**.  
  
2.  Se solicitado, faça logon no [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe.  
  
3.  No **criar projeto local do SourceSafe** diálogo caixa, selecione a pasta que contém a solução que você deseja abrir e, em seguida, clique em **Okey**.  
  
4.  Se já existir uma pasta de trabalho para a solução em sua unidade de disco local, o **criar um novo projeto na pasta** caixa muda para identificar o diretório local. Se não houver uma pasta de trabalho para a solução, você poderá digitar ou procurar o diretório local em que a solução deve ser aberta.  
  
5.  No **solução aberta** caixa de diálogo, selecione o arquivo de solução e clique em **Okey**.  
  
## <a name="see-also"></a>Consulte também  
 [Abrir projetos no controle do código-fonte](../../2014/database-engine/open-projects-from-source-control.md)  
  
  
