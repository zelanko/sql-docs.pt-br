---
title: Adicionar um tipo de conteúdo de Conexão de modelo semântico BI a uma biblioteca (PowerPivot para SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 145505ed-50bc-4528-912b-2a5cd2566011
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 15537b159f34df3e69c3b415a8a00845ff2fe79f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37284102"
---
# <a name="add-a-bi-semantic-model-connection-content-type-to-a-library-powerpivot-for-sharepoint"></a>Adicionar um tipo de conteúdo de conexão de modelo semântico de BI a uma biblioteca (PowerPivot para SharePoint)
  Uma conexão de modelo semântico de BI é criada no SharePoint e fornece redirecionamento para dados de modelo de semântica de business intelligence em uma pastas de trabalho PowerPivot ou banco de dados de modelo de tabela do Analysis Services em um servidor de rede. Antes de criar uma conexão de modelo semântico de BI no SharePoint, você deve estender uma biblioteca de documentos para permitir a criação de um arquivo .bism. Esta etapa só precisa ser executada uma vez para cada biblioteca, mas você precisará repeti-la para qualquer biblioteca da qual deseje criar arquivos .bism. De acordo com as práticas recomendadas, você deve criar uma biblioteca centralizada para armazenar arquivos .bism, permitindo o gerenciamento de permissões em um local.  
  
> [!NOTE]  
>  Se você já usa Bibliotecas de Conexão de Dados SharePoint, o tipo de conteúdo da Conexão de Modelo Semântico de BI é acrescentado automaticamente a esse modelo de biblioteca. Você poderá ignorar as etapas desta seção se usar uma biblioteca de conexão de dados que já o permite criar novos documentos de conexão de modelo semântico de BI.  
  
##  <a name="bkmk_addtype"></a> Adicionar o tipo de conteúdo a uma biblioteca de documentos  
 Você deve ter pelo menos a permissão Gerenciar Listas para adicionar e configurar um tipo de conteúdo. Esta permissão é compilada no nível de permissão Design e superior.  
  
 O site que contém a biblioteca de documentos deve ter ativação de recurso para PowerPivot para SharePoint. Para obter mais informações, consulte [ativar a integração do recurso do PowerPivot para coleções de sites na Administração Central](activate-power-pivot-integration-for-site-collections-in-ca.md).  
  
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
  
     ![Submenu novo documento em uma biblioteca do SharePoint](../media/ssas-bismconnection-new.gif "submenu novo documento na biblioteca do SharePoint")  
  
 Depois de habilitar o tipo de conteúdo de conexão de modelo semântico de BI para uma biblioteca, você poderá criar uma conexão que fornece redirecionamento para dados de modelo semântico comerciais que podem ser usados pelo Excel ou relatórios do [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] . Escolha os links a seguir para saber mais sobre esta próxima etapa:  
  
 [Criar uma conexão de modelo semântico de BI para uma pastas de trabalho PowerPivot](create-a-bi-semantic-model-connection-to-a-power-pivot-workbook.md)  
  
 [Criar uma conexão de modelo semântico de BI com um banco de dados de modelo de tabela](create-a-bi-semantic-model-connection-to-a-tabular-model-database.md)  
  
## <a name="see-also"></a>Consulte também  
 [Conexão de modelo semântico de BI do PowerPivot &#40;. bism&#41;](power-pivot-bi-semantic-model-connection-bism.md)   
 [Usar uma conexão de modelo semântico de BI no Excel ou Reporting Services](use-a-bi-semantic-model-connection-in-excel-or-reporting-services.md)  
  
  
