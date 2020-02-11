---
title: Verificar se há atualizações ou desativar atualizações (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 9c69792d-d7c4-453b-ae2f-6d2d071d8606
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 27942be9c32d4537f729adbd69df1c64a9c9ff6f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109869"
---
# <a name="check-for-updates-or-turn-updates-off-report-builder-and-ssrs"></a>Verificar ou desativar atualizações (Construtor de Relatórios e SSRS)
  Sempre que você abre um relatório, o Construtor de Relatórios verifica se as instâncias publicadas das partes de relatório no relatório foram atualizadas no servidor de relatório ou no site do SharePoint integrado com o servidor de relatório. Também procura alterações nos itens dependentes das partes de relatório, como o conjunto de dados e os parâmetros. Se as partes de relatório ou suas dependências foram atualizados no site ou servidor, uma barra de informações no relatório exibe o número de partes atualizadas. Você pode optar por exibir e aceitar ou rejeitar as atualizações ou descartar a barra de informações.  
  
 Você também pode desabilitar a barra de informações e não ser informado se as instâncias publicadas das partes de relatório foram alteradas. Essa é uma configuração de usuário; ela será desabilitada para todos os relatórios que você abrir. Mesmo que você tenha desabilitado a barra de informações, ainda poderá procurar atualizações.  
  
### <a name="to-turn-on-and-off-report-part-updates"></a>Para ligar e desligar as atualizações de parte de relatório  
  
1.  Clique no botão Construtor de Relatórios e clique em **Opções**.  
  
2.  Na caixa de diálogo **Opções** , na guia **recursos** , marque ou desmarque a caixa de seleção **Mostrar atualizações em partes de relatório em meus relatórios** .  
  
> [!NOTE]  
>  Esta é uma configuração de usuário. Ela será desabilitada para todos os relatórios que você abrir.  
  
### <a name="to-check-for-updates"></a>Para verificar atualizações  
  
-   Clique com o botão direito do mouse na superfície de design fora do relatório ou no corpo do relatório e clique em **verificar se há atualizações**.  
  
## <a name="see-also"></a>Consulte Também  
 [Partes de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-parts-report-builder-and-ssrs.md)   
 [Publicar e republicar partes de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-design/publish-and-republish-report-parts-report-builder-and-ssrs.md)   
 [Procurar partes de relatório e definir uma pasta padrão &#40;Construtor de Relatórios e SSRS&#41;](report-design/browse-for-report-parts-and-set-a-default-folder-report-builder-and-ssrs.md)   
 [Solucionar problemas de partes de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../2014/reporting-services/troubleshoot-report-parts-report-builder-and-ssrs.md)   
 [Partes de relatório e conjuntos de dados no Construtor de Relatórios](report-data/report-parts-and-datasets-in-report-builder.md)  
  
  
