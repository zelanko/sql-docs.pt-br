---
title: Relatórios de clickthrough (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- clickthrough reports
- customizing clickthrough reports
- clickthrough reports, customizing
ms.assetid: cf2c396e-b0c6-41f9-8c45-ddc8406f7e85
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: d044b8f245d3c3ce2c092b7b5f2b094122f75f1e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48101196"
---
# <a name="clickthrough-reports-ssrs"></a>Relatórios de clickthrough (SSRS)
  Um relatório de clickthrough fornece informações detalhadas sobre os dados contidos no relatório principal. Um relatório de clickthrough é exibido quando o usuário clica nos dados interativos que aparecem no relatório principal. Esses relatórios são gerados automaticamente pelo servidor de relatórios. Você, como o designer de modelo, determina o que é exibido em relatórios de clickthrough, definindo o `DefaultDetailAttribute` e `DefaultAggregateAttribute` propriedades que você atribui a uma entidade no modelo de relatório.  
  
> [!NOTE]  
>  Relatórios de Clickthrough não estão disponíveis em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], consulte [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md). Caso você não tenha certeza sobre qual edição do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sua organização está usando, contate o administrador do banco de dados.  
  
## <a name="using-default-templates"></a>Usando modelos padrão  
 Por padrão, o servidor de relatórios gera dois tipos de modelos de clickthrough para cada entidade: um modelo de uma instância e um modelo de várias instâncias. O item no qual você clica determina qual modelo é usado. Se a pessoa que lê o relatório clicar em um atributo escalar, o modelo de uma instância será usado. Se a pessoa que lê o relatório clicar em um atributo de agregação, o modelo de várias instâncias será usado.  
  
#### <a name="single-instance-templates"></a>Modelos de uma instância  
 Um modelo de uma instância exibe todos os atributos da entidade de destino e todos os atributos de agregação padrão especificados para as entidades relacionadas que tenham uma relação um para muitos a partir da entidade de destino. Um modelo de uma instância parece semelhante à imagem a seguir.  
  
 ![Um relatório de clickthrough muitos-para-um.](../media/manytooneclickthrough.gif "Um relatório de clickthrough muitos-para-um.")  
  
#### <a name="multiple-instance-templates"></a>Modelos de várias instâncias  
 Um modelo de várias instâncias exibe somente os atributos de detalhes padrão da entidade de destino e todos os atributos de agregação padrão especificados para as entidades relacionadas que tenham uma relação um para muitos a partir da entidade de destino. Um modelo de várias instâncias parece semelhante à imagem a seguir.  
  
 ![Um relatório de clickthrough muitos-para-um.](../media/onetomanyclickthrough.gif "Um relatório de clickthrough muitos-para-um.")  
  
## <a name="customizing-clickthrough-reports"></a>personalizando relatórios de clickthrough  
 Em vez de usar os modelos padrão gerados pelo servidor de relatórios, você pode criar um relatório no Construtor de Relatórios e usá-lo como um relatório de clickthrough personalizado. Em seguida, você pode vincular seu relatório ao modelo como um relatório detalhado no Gerenciador de Relatórios.  
  
 Para transformar um Construtor de Relatórios em um relatório de clickthrough, é necessário selecionar a opção **Habilitar Drillthrough neste Relatório** na caixa de diálogo **Propriedades** do Construtor de Relatórios. Assim que essa opção for selecionada, um parâmetro de detalhamento será adicionado ao relatório e ele não poderá mais ser executado diretamente no Construtor de Relatórios. O parâmetro de detalhamento é automaticamente calculado pelo servidor de relatórios quando o leitor de relatório clicar em um item em um relatório do Construtor de Relatórios.  
  
> [!IMPORTANT]  
>  A entidade principal, ou básica, usada no relatório deve ser a mesma entidade à qual você vincula o relatório.  
  
## <a name="see-also"></a>Consulte também  
 [Vincular um relatório a um modelo como um relatório de clickthrough](../link-a-report-to-a-model-as-a-clickthrough-report.md)  
  
  
