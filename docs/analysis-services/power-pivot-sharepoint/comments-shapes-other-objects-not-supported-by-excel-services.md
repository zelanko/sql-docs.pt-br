---
title: "Comentários, formas, outros objetos que não tem suportados pelos serviços do Excel | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: ade92e15-dfbf-496b-9378-a00bd83ba750
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7be7712be44114606ec89f89683defeee8e3bd31
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="comments-shapes-other-objects-not-supported-by-excel-services"></a>Comentários, formas, outros objetos que não tem suportados pelos serviços do Excel
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Esse erro ocorre quando você adiciona segmentações de dados para um [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] pasta de trabalho de um [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] lista de campos.  
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Aplica-se a|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint|  
|Versão do Produto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|O Excel Web Access não pode renderizar o objeto Forma usado para controlar o posicionamento e a formatação de Segmentações de Dados acrescentadas a uma pasta de trabalho da Lista de Campos do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .|  
|Texto da mensagem|Os recursos a seguir não têm suporte dos Serviços do Excel e podem não ser exibidos ou ser exibidos apenas parcialmente:<br /><br /> Comentários, Formas ou outros objetos<br /><br /> Alguns recursos, como consultas de dados externas, exibem dados armazenados em cache que só podem ser atualizados no Microsoft Excel.|  
  
## <a name="explanation"></a>Explicação  
 O Excel Web Access mostra este erro quando você abre uma pasta de trabalho [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] em um navegador e clica no botão **Detalhes** , obtendo a mensagem **Recursos sem suporte Esta pasta de trabalho pode não ser exibida como o esperado**.  
  
 Este erro ocorre porque a pasta de trabalho [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] contém Segmentações de Dados cujo layout é controlado por um objeto Forma oculto no Excel. O objeto Forma controla a formatação e o posicionamento das Segmentações de Dados em posicionamentos horizontais e verticais.  
  
 Os Serviços do Excel não podem renderizar um objeto Forma, mas, como o objeto é oculto, o fato de ele não renderizar não é um problema.  
  
## <a name="user-action"></a>Ação do usuário  
 Este erro pode ser ignorado. Clique em **OK** para fechar a mensagem de erro e continuar a usar a pasta de trabalho e as Segmentações de Dados sem problema.  
  
  
