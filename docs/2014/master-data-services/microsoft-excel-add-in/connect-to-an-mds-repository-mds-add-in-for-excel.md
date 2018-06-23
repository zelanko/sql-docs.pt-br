---
title: Conectar-se a um repositório do MDS (Suplemento MDS para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8f427312-4c09-4c8b-b9f9-8b235557a74b
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 5c2fd145d78c4c24d9f43a5919d53af3c3aab3c6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122635"
---
# <a name="connect-to-an-mds-repository-mds-add-in-for-excel"></a>Conectar-se a um repositório do MDS (suplemento MDS para Excel)
  No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], você deve se conectar a um repositório do MDS antes de poder carregar ou publicar dados.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional do **Gerenciador** .  
  
### <a name="to-connect-to-an-mds-repository"></a>Para conectar-se a um repositório do MDS  
  
1.  No MDS [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], na guia **Dados Mestre** , no grupo **Conectar e Carregar** , clique na seta sob o botão **Conectar** e clique em **Gerenciar Conexões**.  
  
2.  Na caixa de diálogo **Gerenciar Conexões** , na seção **Nova uma conexão** , clique em **Criar uma nova conexão**.  
  
3.  Clique em **Nova**.  
  
4.  Na caixa de diálogo **Adicionar Nova Conexão** , no campo **Descrição** , digite uma descrição para a conexão. Essa conexão será exibida quando você clicar na seta sob o botão **Conectar** da barra de ferramentas.  
  
5.  Na caixa **Endereço do servidor MDS**, digite a URL do aplicativo Web do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)], por exemplo, http://contoso/mds.  
  
    > [!NOTE]  
    >  Verifique se você usa o nome de computador; não use "localhost".  
  
6.  Clique em **OK**. O nome será exibido na seção **Conexões Existentes** .  
  
7.  Opcionalmente, clique em **Testar** para testar a conexão. Uma caixa de diálogo de confirmação ou de erro será exibida. Clique em **OK** para fechá-la.  
  
8.  Clique em **Conectar**. O painel **Master Data Services** será exibido.  
  
## <a name="next-steps"></a>Próximas etapas  
  
-   [Carregar dados do MDS no Excel](export-data-to-excel-from-master-data-services.md)  
  
-   [Filtrar dados antes de carregar &#40;suplemento do MDS para Excel&#41;](filter-data-before-exporting-mds-add-in-for-excel.md)  
  
## <a name="see-also"></a>Consulte também  
 [Conexões &#40;Suplemento MDS para Excel&#41;](connections-mds-add-in-for-excel.md)  
  
  