---
title: Criar e gerenciar KPIs (SSAS tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.kpi.f1
ms.assetid: c96026c2-4394-4c3c-986b-4c95a4421900
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fc0bd941392c208ad693be21a391d7b9e3f587a1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/25/2020
ms.locfileid: "66067508"
---
# <a name="create-and-manage-kpis-ssas-tabular"></a>Criar e Gerenciar KPIs (SSAS tabular)
  Este tópico descreve como criar, editar ou excluir um KPI (Indicador chave de desempenho) em um modelo tabular. Para criar um KPI, você seleciona uma medida que é avaliada como o valor base do KPI. Use a caixa de diálogo Indicador Chave de Desempenho para selecionar uma segunda medida ou um valor absoluto que seja avaliado para um valor de destino. Em seguida, você pode definir os limites de status que abrangem o desempenho entre as medidas Base e Destino.  
  
 Este tópico inclui as seguintes tarefas:  
  
-   [Para criar um KPI](#bkmk_create_KPI)  
  
-   [Para editar um KPI](#bkmk_edit_KPI)  
  
-   [Para excluir um KPI e a medida base](#bkmk_delete)  
  
-   [Para excluir um KPI, mas manter a medida de base](#bkmk_delete_KPI)  
  
## <a name="tasks"></a>Tarefas  
  
> [!IMPORTANT]  
>  Antes de criar um KPI, primeiro você deve criar uma Medida base que será avaliada como valor. Em seguida, você estenderá a medida Base para um KPI. A criação de medidas é descrita em outro tópico, [Criar e gerenciar medidas &#40;SSAS de Tabela&#41;](measures-ssas-tabular.md). Um KPI também exige um valor de destino. Este valor pode ser de outra medida pré-definida ou um valor absoluto. Depois de estender uma Medida base para um KPI, você pode selecionar o valor de destino e pode definir limites de status na caixa de diálogo do Indicador chave de desempenho.  
  
###  <a name="to-create-a-kpi"></a><a name="bkmk_create_KPI"></a> Para criar um KPI  
  
1.  Na grade de medida, clique com o botão direito do mouse na medida que servirá como a medida Base (valor) e clique em **Criar KPI**.  
  
2.  Na caixa de diálogo **Indicador Chave de Desempenho** , em **Definir valor de destino**, selecione uma das seguintes opções:  
  
     Selecione **Medida**e, em seguida, selecione uma medida de destino na caixa de listagem.  
  
     Selecione **Valor absoluto**e digite um valor numérico.  
  
3.  Em **Definir limites de status**, clique e deslize os valores de limite baixo e alto.  
  
4.  Em **Selecionar estilo do ícone**, clique em um tipo de imagem.  
  
5.  Clique em **Descrições**e digite as descrições para KPI, Valor, Status e Destino.  
  
> [!TIP]  
>  Você pode usar o recurso Analisar no Excel para testar seu KPI. Para obter mais informações, consulte [Analisar no Excel &#40;SSAS de Tabela&#41;](analyze-in-excel-ssas-tabular.md).  
  
###  <a name="to-edit-a-kpi"></a><a name="bkmk_edit_KPI"></a> Para editar um KPI  
  
-   Na Grade de Medida, clique com o botão direito do mouse na medida que serve como a medida base (valor) do KPI e clique em **Editar Configurações do KPI**.  
  
###  <a name="to-delete-a-kpi-and-the-base-measure"></a><a name="bkmk_delete"></a> Para excluir um KPI e a medida de base  
  
-   Na grade de medida, clique com o botão direito do mouse na medida que serve como a medida base (valor) do KPI e clique em **Excluir**.  
  
###  <a name="to-delete-a-kpi-but-keep-the-base-measure"></a><a name="bkmk_delete_KPI"></a>Para excluir um KPI, mas manter a medida base  
  
-   Na grade de medida, clique com o botão direito do mouse na medida que serve como a medida base (valor) do KPI e clique em **Excluir KPI**.  
  
## <a name="alt-shortcuts"></a>Atalhos ALT  
  
|Seção da Interface do Usuário|Comando de teclas|  
|----------------|-----------------|  
|Medida base do KPI|ALT+B|  
|Status do KPI|ALT+S|  
|Medida|ALT+M|  
|Valor absoluto|ALT+A|  
|Definir limites de status|ALT+U|  
|Selecionar estilo do ícone|ALT+I|  
|Tendência|ALT+T|  
|Descrições|ALT+D|  
|Tendência|ALT+T|  
  
## <a name="see-also"></a>Consulte Também  
 [KPIs &#40;SSAS de tabela&#41;](kpis-ssas-tabular.md)   
 [Medidas &#40;&#41;de tabela do SSAS](measures-ssas-tabular.md)   
 [Criar e gerenciar medidas &#40;SSAS de Tabela&#41;](create-and-manage-measures-ssas-tabular.md)  
  
  
