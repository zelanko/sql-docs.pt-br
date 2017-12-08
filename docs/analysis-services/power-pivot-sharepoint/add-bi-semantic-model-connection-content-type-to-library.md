---
title: "Adicionar tipo de Conexão de modelo semântico de BI conteúdo à biblioteca | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: power-pivot-sharepoint
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 145505ed-50bc-4528-912b-2a5cd2566011
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 228022da2c96886d099c1f5dbdf1a52bd9815aed
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="add-bi-semantic-model-connection-content-type-to-library"></a>Adicionar tipo de Conexão de modelo semântico de BI conteúdo à biblioteca
  Uma conexão de modelo semântico de BI é criada no SharePoint e fornece redirecionamento para dados de modelo de semântica de business intelligence em uma pasta de trabalho [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ou banco de dados de modelo de tabela do Analysis Services em um servidor de rede. Antes de criar uma conexão de modelo semântico de BI no SharePoint, você deve estender uma biblioteca de documentos para permitir a criação de um arquivo .bism. Esta etapa só precisa ser executada uma vez para cada biblioteca, mas você precisará repeti-la para qualquer biblioteca da qual deseje criar arquivos .bism. De acordo com as práticas recomendadas, você deve criar uma biblioteca centralizada para armazenar arquivos .bism, permitindo o gerenciamento de permissões em um local.  
  
> [!NOTE]  
>  Se você já usa Bibliotecas de Conexão de Dados SharePoint, o tipo de conteúdo da Conexão de Modelo Semântico de BI é acrescentado automaticamente a esse modelo de biblioteca. Você poderá ignorar as etapas desta seção se usar uma biblioteca de conexão de dados que já o permite criar novos documentos de conexão de modelo semântico de BI.  
  
##  <a name="bkmk_addtype"></a> Adicionar o tipo de conteúdo a uma biblioteca de documentos  
 Você deve ter pelo menos a permissão Gerenciar Listas para adicionar e configurar um tipo de conteúdo. Esta permissão é compilada no nível de permissão Design e superior.  
  
 O site que contém a biblioteca de documentos deve ter ativação de recurso para [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint. Para obter mais informações, consulte [Ativar a Integração de Recursos do Power Pivot para as Coleções de Sites na Administração Central](../../analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca.md).  
  
1.  Abra a biblioteca de documentos para a qual você deseja habilitar o tipo de conteúdo da Conexão de Modelo Semântico de BI.  
  
2.  Na faixa de opções do SharePoint, em Ferramentas de Biblioteca, clique em **Biblioteca**.  
  
3.  Clique em **Configurações da Biblioteca**.  
  
4.  Em Configurações Gerais, clique em **Configurações avançadas**.  
  
5.  Em Tipos de Conteúdo, na seção "Permitir o gerenciamento de tipos de conteúdo?", clique em **Sim**.  
  
6.  Clique em **OK**.  
  
7.  Na seção Tipos de Conteúdo, clique em **Adicionar a partir de tipos de conteúdo de site existentes**. Se você não vir essa página, volte para o site, clique em **Biblioteca** em Ferramentas de Biblioteca e clique em **Definições da Biblioteca**.  
  
8.  Em Tipos de Conteúdo, clique em **Adicionar a partir de tipos de conteúdo de site existentes**.  
  
9. Em Selecionar tipos de conteúdo de site de:, selecione **Business Intelligence**.  
  
10. Em Tipos Disponíveis de Conteúdo do Site, clique em **Arquivo de Conexão de Modelo Semântico de BI**e em **Adicionar** para mover o tipo de conteúdo selecionado para a lista Tipos de conteúdo a serem adicionados.  
  
11. Clique em **OK**.  
  
12. Para verificar se você adicionou o tipo de conteúdo, volte para a biblioteca e clique em **Novo Documento** na área de Documentos da faixa de opções de biblioteca. Você deverá ver o **Arquivo de Conexão do Modelo Semântico de BI** na lista Novos Documentos.  
  
     ![Submenu novo documento em uma biblioteca do SharePoint](../../analysis-services/power-pivot-sharepoint/media/ssas-bismconnection-new.gif "submenu novo documento em uma biblioteca do SharePoint")  
  
 Depois de habilitar o tipo de conteúdo de conexão de modelo semântico de BI para uma biblioteca, você poderá criar uma conexão que fornece redirecionamento para dados de modelo semântico comerciais que podem ser usados pelo Excel ou relatórios do [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] . Escolha os links a seguir para saber mais sobre esta próxima etapa:  
  
 [Criar uma conexão de modelo semântico de BI para uma pasta de trabalho do Power Pivot](../../analysis-services/power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-power-pivot-workbook.md)  
  
 [Criar uma conexão de modelo semântico de BI com um banco de dados de modelo de tabela](../../analysis-services/power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-tabular-model-database.md)  
  
## <a name="see-also"></a>Consulte também  
 [Conexão de modelo semântico de BI &#40;.bism&#41; do Power Pivot](../../analysis-services/power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md)   
 [Usar uma conexão de modelo semântico de BI no Excel ou Reporting Services](../../analysis-services/power-pivot-sharepoint/use-a-bi-semantic-model-connection-in-excel-or-reporting-services.md)  
  
  
