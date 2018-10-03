---
title: 'Tarefa 11: Adicionar condicional dividir a transformação para filtrar duplicatas | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: 3094bd57-5cf4-4860-bf51-fadd1b309f94
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 01824587b583483a519a5f2a7d8731dd657aae48
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48161426"
---
# <a name="task-11-adding-conditional-split-transform-to-filter-duplicates"></a>Tarefa 11: Adicionando a Transformação Divisão Condicional para filtrar duplicatas
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
 [Tarefa 12: Adicionando a Transformação Coluna Derivada para adicionar as colunas necessárias pelo MDS](../../2014/tutorials/task-12-adding-derived-column-transform-to-add-columns-required-by-mds.md)  
  
  
