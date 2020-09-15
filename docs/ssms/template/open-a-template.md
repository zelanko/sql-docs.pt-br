---
description: Abrir um modelo
title: Abrir um modelo
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- templates [Transact-SQL], opening
- opening templates
ms.assetid: 605b0f4c-5ba1-4249-ad1c-6341df77cd7a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 730963488d34750ead61fe2662eb8201f91b30e1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88417852"
---
# <a name="open-a-template"></a>Abrir um modelo
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Você pode abrir um modelo a partir do Explorador de Modelos.  
  
## <a name="to-open-a-template-from-template-explorer"></a>Para abrir um modelo a partir do Explorador de Modelos  
Você pode abrir modelos a partir do Explorador de Modelos.  
  
1.  Para abrir o Gerenciador de Modelos, no menu **Exibir** , clique em **Gerenciador de Modelos**.  
  
2.  Na lista de categorias de modelo, expanda a categoria que contém o modelo que você deseja abrir.  
  
3.  Há três modos de abrir o modelo:  
  
    1.  Clique duas vezes no modelo para abri-lo em uma janela de editor de código.  
  
    2.  Clique com o botão direito do mouse no modelo e selecione **Abrir** para abri-lo em uma janela do editor de código.  
  
    3.  Arraste o modelo para uma janela do editor de código para adicionar o código do modelo ao conteúdo da janela do editor.  
  
Após abrir o modelo, use a caixa de diálogo **Substituir Parâmetros do Modelo** para substituir os parâmetros do modelo pelos seus próprios valores.  
  
Se a abertura de um modelo iniciar uma nova janela do editor, a janela será aberta com as credenciais da conexão ativa atual. Por exemplo, se você estiver concentrado em uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)] no Pesquisador de Objetos quando você abrir o modelo CREATE DATABASE, uma nova janela do editor será aberta usando uma conexão com essa instância. Se não houver nenhuma conexão ativa, o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] apresentará uma caixa de diálogo de logon.  
  
## <a name="see-also"></a>Consulte Também  
[Explorador de Modelos](../../ssms/template/template-explorer.md)  
[Substituir Parâmetros do Modelo](../../ssms/template/replace-template-parameters.md)  
  
