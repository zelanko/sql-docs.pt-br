---
title: Implantar modelos de tabela do Analysis Services do SQL Server Data Tools | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 09d859cf8b5c372b9588266b9210837012396ea6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68162865"
---
# <a name="deploy-from-sql-server-data-tools"></a>Implantar das Ferramentas de Dados do SQL Server
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Use as tarefas neste tópico para implantar uma solução modelo tabular usando o comando implantar no SSDT.  
  
##  <a name="bkmk_deploy"></a> Configurar as propriedades Opções de Implantação e Servidor de Implantação  
 Antes de implantar sua solução modelo tabular, primeiro especifique as propriedades Deployment Options e Deployment Server. Para obter mais informações sobre configurações e propriedades de implantação, consulte [implantação de solução de modelo Tabular](../../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md).  
  
#### <a name="to-configure-options-and-properties"></a>Para configurar as propriedades e opções  
  
1.  No SSDT, no **Gerenciador de soluções**, clique com botão direito no nome do projeto e, em seguida, clique em **propriedades**.  
  
2.  No  **\<nome do projeto > propriedades** caixa de diálogo, no **opções de implantação**, especifique as configurações de propriedade se elas forem diferentes das configurações padrão.  
  
    > [!NOTE]  
    >  Para modelos em modo armazenado em cache, o **Modo de Consulta** é sempre **Na Memória**.  
  
    > [!NOTE]  
    >  Você não pode especificar **Configurações de Representação** para modelos no modo DirectQuery.  
  
3.  Em **Servidor de Implantação**, especifique as configurações de propriedade **Servidor** (nome), **Edição**, **Banco de Dados** (nome) e **Nome do Cubo** se estiverem diferentes das configurações padrão e clique em **OK**.  
  
> [!NOTE]  
>  Você também pode especificar a configuração de propriedade Servidor de Implantação Padrão para que qualquer projeto que você crie seja automaticamente implantado no servidor especificado. Para obter mais informações, consulte [configurar propriedades de implantação e modelagem de dados padrão](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md).  
  
##  <a name="bkmk_deploy_proc"></a> Implantar um modelo tabular  
  
#### <a name="to-deploy-a-tabular-model"></a>Para implantar um modelo de tabela
  
-   No SSDT, sobre o **compilar** menu, clique em **Deploy \<nome do projeto >** .  
  
     A caixa de diálogo **Implantação** aparecerá e indicará o status da implantação de metadados e o processamento (a menos que a propriedade Opção de Processamento esteja configurada como Não Processar) de cada tabela incluída no modelo. Depois que o processo de implantação for concluído, use o SSMS para se conectar à instância do Analysis Services e verificar que o novo objeto de banco de dados de modelo foi criado ou usar um cliente de relatório de aplicativo para se conectar ao modelo implantado.  
  
##  <a name="bkmk_deploy_status"></a> Status de Implantação  
 A caixa de diálogo **Implantar** o habilita a monitorar o progresso de uma operação de Implantação. Uma operação de implantação também pode ser interrompida.  
  
 **Status**  
 Indica se a operação de implantação foi bem-sucedida ou não.  
  
 **Detalhes**  
 Lista os itens de metadados que foram implantados, o status de cada item de metadados, e fornece uma mensagem de quaisquer problemas.  
  
 **Parar a implantação**  
 Clique para interromper a operação de implantação. Essa opção será útil se a operação de implantação estiver demorando muito ou se houver muitos erros.  
  
## <a name="see-also"></a>Confira também  
 [Implantação de solução de modelo de tabela](../../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md)   
 [Configurar propriedades de implantação e modelagem de dados padrão](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)  
  
  
