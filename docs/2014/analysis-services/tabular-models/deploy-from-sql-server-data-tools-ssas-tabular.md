---
title: Implantar do SQL Server Data Tools (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.deploystatus.f1
ms.assetid: 67dde3fe-ba43-41f3-b56c-c656029ee93f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6429fb7f30c748c7ac0a8ab69bc16c3d63b4d3ae
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66067296"
---
# <a name="deploy-from-sql-server-data-tools-ssas-tabular"></a>Implantar das Ferramentas de Dados do SQL Server (SSAS tabular)
  Use as tarefas neste tópico para implantar uma solução de modelo de tabela, usando o comando Implantar do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Seções neste tópico:  
  
-   [Configurar as propriedades Opções de Implantação e Servidor de Implantação](#bkmk_deploy)  
  
-   [Implantar uma solução de modelo tabular](#bkmk_deploy_proc)  
  
-   [Status de Implantação](#bkmk_deploy_status)  
  
##  <a name="bkmk_deploy"></a> Configurar as propriedades Opções de Implantação e Servidor de Implantação  
 Antes de implantar sua solução modelo tabular, primeiro especifique as propriedades Deployment Options e Deployment Server. Para obter mais informações sobre configurações e propriedades de implantação, consulte [Tabular Model Solution Deployment &#40;SSAS Tabular&#41;](tabular-model-solution-deployment-ssas-tabular.md).  
  
#### <a name="to-configure-deployment-options-and-deployment-server-properties"></a>Para configurar as propriedades Opções de Implantação e Servidor de Implantação  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], no **Gerenciador de Soluções**, clique com o botão direito do mouse no nome do projeto e, em seguida, clique em **Propriedades**.  
  
2.  No  **\<nome do projeto > propriedades** caixa de diálogo, no **opções de implantação**, especifique as configurações de propriedade se elas forem diferentes das configurações padrão.  
  
    > [!NOTE]  
    >  Para modelos em modo armazenado em cache, o **Modo de Consulta** é sempre **Na Memória**.  
  
    > [!NOTE]  
    >  Você não pode especificar **Configurações de Representação** para modelos no modo DirectQuery.  
  
3.  Em **Servidor de Implantação**, especifique as configurações de propriedade **Servidor** (nome), **Edição**, **Banco de Dados** (nome) e **Nome do Cubo** se estiverem diferentes das configurações padrão e clique em **OK**.  
  
> [!NOTE]  
>  Você também pode especificar a configuração de propriedade Servidor de Implantação Padrão para que qualquer projeto que você crie seja automaticamente implantado no servidor especificado. Para obter mais informações, consulte [Configurar propriedades padrão de implantação e modelagem de dados &#40;SSAS de Tabela&#41;](properties-ssas-tabular.md).  
  
##  <a name="bkmk_deploy_proc"></a> Implantar uma solução de modelo tabular  
  
#### <a name="to-deploy-a-tabular-model-solution"></a>Para implantar uma solução de modelo tabular  
  
-   No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]diante a **Build** menu, clique em **implantar \<nome do projeto >** .  
  
     A caixa de diálogo **Implantação** aparecerá e indicará o status da implantação de metadados e o processamento (a menos que a propriedade Opção de Processamento esteja configurada como Não Processar) de cada tabela incluída no modelo. Depois que o processo de implantação for concluído, use o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para conectar à instância do Analysis Services e verificar se o novo objeto de banco de dados modelo foi criado ou use um aplicativo de relatório cliente para conectar-se ao modelo implantado.  
  
##  <a name="bkmk_deploy_status"></a> Status de Implantação  
 A caixa de diálogo **Implantar** o habilita a monitorar o progresso de uma operação de Implantação. Uma operação de implantação também pode ser interrompida.  
  
 **Status**  
 Indica se a operação de implantação foi bem-sucedida ou não.  
  
 **Detalhes**  
 Lista os itens de metadados que foram implantados, o status de cada item de metadados, e fornece uma mensagem de quaisquer problemas.  
  
 **Parar a implantação**  
 Clique para interromper a operação de implantação. Essa opção será útil se a operação de implantação estiver demorando muito ou se houver muitos erros.  
  
## <a name="see-also"></a>Consulte também  
 [Implantação de uma solução de modelo de tabela &#40;SSAS de Tabela&#41;](tabular-model-solution-deployment-ssas-tabular.md)   
 [Configurar propriedades padrão de implantação e modelagem de dados &#40;SSAS de Tabela&#41;](properties-ssas-tabular.md)  
  
  
