---
title: 'Tarefa 11: Adicionar condicional dividir transformação para filtrar duplicatas | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3094bd57-5cf4-4860-bf51-fadd1b309f94
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 7f61fa706659a6f71b2c69f18bcf7b694993ed00
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36020381"
---
# <a name="task-11-adding-conditional-split-transform-to-filter-duplicates"></a>Tarefa 11: Adicionando a Transformação Divisão Condicional para filtrar duplicatas
  Nesta tarefa, você adiciona a Transformação Divisão Condicional ao fluxo de dados. Essa transformação ajuda o ajuda a filtrar duplicatas do conjunto de registros de entrada. A transformação Grupo Difuso agrupa os registros que considera correspondências e escolhe um dos registros como registro dinâmico. Todos os registros em um grupo têm o mesmo valor _key_out. O registro dinâmico no grupo tem o valor _key_in igual ao valor _key_out. Os outros registros no grupo têm valores diferentes para _key_in e _key_out. Assim, quando você filtrar usando a condição _key_in==_key_out, receberá apenas a linha dinâmica no grupo.  
  
1.  Arraste e solte **divisão condicional** de transformação de **comuns** seção o **caixa de ferramentas do SSIS** para o **de fluxo de dados** guia.  
  
2.  Clique com botão direito **transformação divisão condicional** no **de fluxo de dados** guia e, em seguida, clique em **Renomear**. Tipo **filtrar duplicatas** e pressione **ENTER**.  
  
3.  Conecte-se **agrupar fornecedores com IDs correspondentes** para **filtrar duplicatas**.  
  
4.  Clique duas vezes em **filtrar duplicatas** para iniciar o **o Editor de transformação de divisão condicional** caixa de diálogo.  
  
5.  Expanda **colunas** no painel superior esquerdo.  
  
6.  Arraste e solte **key_in** para o **condição** coluna.  
  
7.  Tipo = = (igual a) ao lado de **key_in** e arraste e solte **key_out**.  
  
8.  Clique em **caso 1** no **nome de saída** coluna, digite **registros exclusivos**e pressione **ENTER**.  
  
     ![Editor de transformação de divisão condicional](../../2014/tutorials/media/et-addingconditionalsplittransformtofilterduplicates.jpg "Editor de transformação de divisão condicional")  
  
9. Clique em **Okey** para fechar o **Editor de transformação de divisão condicional** caixa de diálogo.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 12: Adicionando a Transformação Coluna Derivada para adicionar as colunas necessárias pelo MDS](../../2014/tutorials/task-12-adding-derived-column-transform-to-add-columns-required-by-mds.md)  
  
  