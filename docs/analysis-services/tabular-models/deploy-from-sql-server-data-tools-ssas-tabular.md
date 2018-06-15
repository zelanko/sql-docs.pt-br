---
title: Implantação do SQL Server Data Tools | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 009c286c105f8088897343f3694c7b3106ca493a
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34042330"
---
# <a name="deploy-from-sql-server-data-tools"></a>Implantar das Ferramentas de Dados do SQL Server
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Use as tarefas neste tópico para implantar uma solução de modelo de tabela usando o comando implantar no SSDT.  
  
##  <a name="bkmk_deploy"></a> Configurar as propriedades Opções de Implantação e Servidor de Implantação  
 Antes de implantar sua solução modelo tabular, primeiro especifique as propriedades Deployment Options e Deployment Server. Para obter mais informações sobre configurações e propriedades de implantação, consulte [implantação de solução de modelo de tabela](../../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md).  
  
#### <a name="to-configure-options-and-properties"></a>Configurar propriedades e opções  
  
1.  No SSDT, em **Solution Explorer**, clique no nome do projeto e, em seguida, clique em **propriedades**.  
  
2.  No  **\<nome do projeto > propriedades** caixa de diálogo, na **opções de implantação**, especifique as configurações de propriedade se diferentes das configurações padrão.  
  
    > [!NOTE]  
    >  Para modelos em modo armazenado em cache, o **Modo de Consulta** é sempre **Na Memória**.  
  
    > [!NOTE]  
    >  Você não pode especificar **Configurações de Representação** para modelos no modo DirectQuery.  
  
3.  Em **Servidor de Implantação**, especifique as configurações de propriedade **Servidor** (nome), **Edição**, **Banco de Dados** (nome) e **Nome do Cubo** se estiverem diferentes das configurações padrão e clique em **OK**.  
  
> [!NOTE]  
>  Você também pode especificar a configuração de propriedade Servidor de Implantação Padrão para que qualquer projeto que você crie seja automaticamente implantado no servidor especificado. Para obter mais informações, consulte [configurar propriedades de implantação e modelagem de dados padrão](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md).  
  
##  <a name="bkmk_deploy_proc"></a> Implantar um modelo de tabela  
  
#### <a name="to-deploy-a-tabular-model"></a>Para implantar um modelo de tabela
  
-   No SSDT, sobre o **criar** menu, clique em **implantar \<nome do projeto >**.  
  
     A caixa de diálogo **Implantação** aparecerá e indicará o status da implantação de metadados e o processamento (a menos que a propriedade Opção de Processamento esteja configurada como Não Processar) de cada tabela incluída no modelo. Após a conclusão do processo de implantação, use o SSMS para conectar-se à instância do Analysis Services e verificar se que o novo objeto de banco de dados de modelo foi criado ou usar um cliente de aplicativo para se conectar ao modelo implantado de relatório.  
  
##  <a name="bkmk_deploy_status"></a> Status de Implantação  
 A caixa de diálogo **Implantar** o habilita a monitorar o progresso de uma operação de Implantação. Uma operação de implantação também pode ser interrompida.  
  
 **Status**  
 Indica se a operação de implantação foi bem-sucedida ou não.  
  
 **Detalhes**  
 Lista os itens de metadados que foram implantados, o status de cada item de metadados, e fornece uma mensagem de quaisquer problemas.  
  
 **Parar a implantação**  
 Clique para interromper a operação de implantação. Essa opção será útil se a operação de implantação estiver demorando muito ou se houver muitos erros.  
  
## <a name="see-also"></a>Consulte também  
 [Implantação de solução de modelo de tabela](../../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md)   
 [Configurar propriedades de implantação e modelagem de dados padrão](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)  
  
  
