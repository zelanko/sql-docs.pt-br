---
title: Comparar fontes de dados compartilhadas e inseridas – Construtor de Relatórios e Reporting Services | Microsoft Docs
ms.date: 11/18/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 33e257659922e3e0dcf06f559838db0c58f0b18e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "77081795"
---
# <a name="compare-shared-and-embedded-data-sources---report-builder--reporting-services-ssrs"></a>Comparar fontes de dados compartilhadas e inseridas – Construtor de Relatórios e SSRS (Reporting Services)

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]
 
É possível se conectar a dados com uma fonte de dados compartilhada ou inserida. Uma *fonte de dados compartilhada* é definida independentemente de qualquer relatório. É possível usá-la em vários relatórios em um servidor de relatório ou um site do SharePoint. Uma *fonte de dados inserida* é definida em um relatório. Só é possível usá nesse relatório. 

 As fontes de dados compartilhadas são úteis quando você usa fontes de dados frequentemente. É recomendável criar e usar fontes de dados compartilhadas o máximo possível. Elas facilitam o acesso e o gerenciamento dos relatórios, além de ajudar a proteger os relatórios e as fontes de dados acessados. Se precisar de uma fonte de dados compartilhada, peça ao administrador do sistema para criar uma para você.  
  
 Uma fonte de dados inserida, também conhecida como uma *fonte de dados específica do relatório*, é uma conexão de dados salva na definição de relatório. As informações de conexão de fonte de dados inserida só podem ser usadas pelo relatório no qual a fonte de dados está inserida. Para definir e gerenciar fontes de dados inseridas, use a caixa de diálogo **Propriedades da Fonte de Dados** .  
  
 A diferença entre as fontes de dados inseridas e compartilhadas está em como elas são criadas, armazenadas e gerenciadas.  
  
-   No Designer de Relatórios, crie fontes de dados inseridas e compartilhadas como parte de um projeto do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] . Você pode controlar se elas devem ser usadas localmente para visualização ou implantadas como parte do projeto para um servidor de relatório ou site do SharePoint. Você pode usar extensões de dados personalizadas que foram instaladas em seu computador e no servidor de relatório ou site do SharePoint onde você implanta seus relatórios.  
  
     Os administradores do sistema podem instalar e configurar extensões de processamento de dados adicionais e provedores de dados do .NET Framework. Para obter mais informações, consulte [Extensões de processamento de dados e provedores de dados do .NET Framework &#40;SSRS&#41;](../../reporting-services/report-data/data-processing-extensions-and-net-framework-data-providers-ssrs.md).  
  
     Os desenvolvedores podem usar a API <xref:Microsoft.ReportingServices.DataProcessing> para criar extensões de processamento de dados para dar suporte a tipos de fonte de dados adicionais.  
  
-   No [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)], navegue para um servidor de relatório ou site do SharePoint e selecione fontes de dados compartilhadas ou crie fontes de dados inseridas no relatório. Não é possível criar uma fonte de dados compartilhada no [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]. Não é possível usar extensões de dados personalizadas no [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)].  

## <a name="summary-of-differences"></a>Resumo das diferenças
  
 A tabela seguinte resume as diferenças entre fontes de dados inseridas e compartilhadas.  
  
|Descrição|Inserida<br /><br /> fonte de dados|Compartilhado<br /><br /> fonte de dados|  
|-----------------|------------------------------|----------------------------|  
|A conexão de dados é inserida na definição do relatório.|![Disponível](../../reporting-services/report-data/media/greencheck.gif "Disponível")||  
|O ponteiro para a conexão de dados no servidor de relatório é inserido na definição do relatório.||![Disponível](../../reporting-services/report-data/media/greencheck.gif "Disponível")|  
|Gerenciada no servidor de relatório|![Disponível](../../reporting-services/report-data/media/greencheck.gif "Disponível")|![Disponível](../../reporting-services/report-data/media/greencheck.gif "Disponível")|  
|Obrigatória para conjuntos de dados compartilhados||![Disponível](../../reporting-services/report-data/media/greencheck.gif "Disponível")|  
|Obrigatória para componentes||![Disponível](../../reporting-services/report-data/media/greencheck.gif "Disponível")|  

## <a name="next-steps"></a>Próximas etapas

[Criar e gerenciar fontes de dados compartilhadas](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)   
[Criar e modificar fontes de dados inseridas](../../reporting-services/report-data/create-and-modify-embedded-data-sources.md)   
[Definir propriedades de implantação](../../reporting-services/tools/set-deployment-properties-reporting-services.md)   
[Especificar informações de credenciais e de conexão para fontes de dados de relatório](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)  

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
