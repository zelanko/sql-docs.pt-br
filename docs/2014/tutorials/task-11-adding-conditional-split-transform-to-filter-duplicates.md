---
title: 'Tarefa 11: Adicionar condicional dividir a transformação para filtrar duplicatas | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 3094bd57-5cf4-4860-bf51-fadd1b309f94
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 71b050e49440764d355d4658607600c135741f50
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65476747"
---
# <a name="task-11-adding-conditional-split-transform-to-filter-duplicates"></a>Tarefa 11: Adicionar a Transformação Divisão Condicional para filtrar duplicatas
  Nesta tarefa, você adiciona a Transformação Divisão Condicional ao fluxo de dados. Essa transformação ajuda o ajuda a filtrar duplicatas do conjunto de registros de entrada. A transformação Grupo Difuso agrupa os registros que considera correspondências e escolhe um dos registros como registro dinâmico. Todos os registros em um grupo têm o mesmo valor _key_out. O registro dinâmico no grupo tem o valor _key_in igual ao valor _key_out. Os outros registros no grupo têm valores diferentes para _key_in e _key_out. Assim, quando você filtrar usando a condição _key_in==_key_out, receberá apenas a linha dinâmica no grupo.  
  
1.  Arrastar e soltar **divisão condicional** transformar de **comuns** seção os **caixa de ferramentas do SSIS** para o **de fluxo de dados** guia.  
  
2.  Clique com botão direito **transformação divisão condicional** na **fluxo de dados** guia e, em seguida, clique em **Renomear**. Tipo de **filtrar duplicatas** e pressione **ENTER**.  
  
3.  Conectar-se **agrupar fornecedores com IDs correspondentes** à **filtrar duplicatas**.  
  
4.  Clique duas vezes em **filtrar duplicatas** para iniciar o **Editor de transformação de divisão condicional** caixa de diálogo.  
  
5.  Expandir **colunas** no painel superior esquerdo.  
  
6.  Arrastar e soltar **key_in** para o **condição** coluna.  
  
7.  Tipo = = (igual a) ao lado **key_in** e arraste e solte **key_out**.  
  
8.  Clique em **caso 1** na **nome de saída** coluna, digite **registros exclusivos**e pressione **ENTER**.  
  
     ![Editor de transformação de divisão condicional](../../2014/tutorials/media/et-addingconditionalsplittransformtofilterduplicates.jpg "Editor de transformação de divisão condicional")  
  
9. Clique em **Okey** para fechar o **Editor de transformação de divisão condicional** caixa de diálogo.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 12: Adicionar transformação coluna derivada para adicionar colunas exigidas pelo MDS](../../2014/tutorials/task-12-adding-derived-column-transform-to-add-columns-required-by-mds.md)  
  
  
