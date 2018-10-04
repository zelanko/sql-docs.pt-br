---
title: Publicar dados do Excel no MDS (suplemento MDS para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
ms.assetid: 89fce454-a816-4b33-a26a-d1b9741d269b
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 02bd2846f4425a4849ab16170c76a55af16c2b76
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48130846"
---
# <a name="publish-data-from-excel-to-mds-mds-add-in-for-excel"></a>Publicar dados do Excel no MDS (suplemento MDS para Excel)
  No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], publique dados no repositório do MDS quando terminar seu trabalho no Excel e desejar salvar as alterações para que outros usuários tenham acesso a elas.  
  
> [!NOTE]  
>  -   Quando você publicar alterações, os comentários das células gerenciadas pelo MDS serão excluídos.  
> -   Uma fórmula não tem suporte em uma célula gerenciada por MDS. Uma fórmula em uma célula gerenciada por MDS é tratada como um valor de texto.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional do **Gerenciador** .  
  
-   A planilha ativa deve conter dados gerenciados no MDS e você deve ter feito alterações ou adições aos dados gerenciados no MDS.  
  
-   Se você for adicionar membros, não precisará especificar um valor de **Código** se os códigos da entidade forem gerados automaticamente. Para obter mais informações, consulte [Criação automática de código &#40;Master Data Services&#41;](../automatic-code-creation-master-data-services.md).  
  
### <a name="to-publish-data-to-the-mds-repository"></a>Para publicar dados no repositório do MDS  
  
1.  No grupo **Publicar e Validar** , clique em **Publicar**.  
  
2.  Opcional. Se a caixa de diálogo **Publicar e Anotar** for exibida, opte por compartilhar a mesma anotação (comentário) para todas as atualizações, ou por anotar cada alteração individualmente.  
  
3.  Opcional. Selecione a caixa de seleção **Não mostrar esta caixa de diálogo novamente** . Você sempre pode mostrar a caixa de diálogo no futuro escolhendo **Configurações** e marcando a caixa de seleção **Mostrar a caixa de diálogo Publicar e Anotar ao publicar** .  
  
4.  Clique em **Publicar**.  
  
> [!NOTE]  
>  Se você for adicionar novos membros (linhas) à sua planilha e não conseguir publicá-los com êxito no repositório do MDS, talvez você não tenha a permissão **Atualizar** para todos os atributos da planilha. Na guia **Revisão** , no grupo **Alterações** , clique em **Desproteger Planilha** e tente publicar novamente.  
  
## <a name="next-steps"></a>Próximas etapas  
 [Aplicar regras de negócio &#40;suplemento do MDS para Excel&#41;](apply-business-rules-mds-add-in-for-excel.md)  
  
## <a name="see-also"></a>Consulte também  
 [Publicação de dados &#40;suplemento do MDS para Excel&#41;](overview-importing-data-from-excel-mds-add-in-for-excel.md)   
 [Validar dados &#40;Suplemento MDS para Excel&#41;](validating-data-mds-add-in-for-excel.md)  
  
  
