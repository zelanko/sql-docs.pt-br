---
title: Associar um parâmetro de consulta a um parâmetro de relatório (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- queries [Reporting Services], parameters
- parameters [Reporting Services], queries
ms.assetid: 6d297e1a-ff71-472a-addc-349e863092b5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 290da32b7ca9c1ab61f84371152c7b72f8168a10
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62697526"
---
# <a name="associate-a-query-parameter-with-a-report-parameter-report-builder-and-ssrs"></a>Associar um parâmetro de consulta a um parâmetro de relatório (Construtor de Relatórios e SSRS)
  Quando você define uma consulta de conjunto de dados que contém uma variável de consulta, o comando de consulta é analisado. Para cada variável de consulta, são criados um parâmetro de conjunto de dados e um parâmetro de relatório correspondentes. O parâmetro de conjunto de dados aponta para o parâmetro de relatório. Dessa forma, o usuário pode inserir um valor que é passado diretamente para a consulta. Toda vez que você edita o comando de consulta, ocorre o mesmo processo.  
  
 Se você renomear o parâmetro de relatório associado a um parâmetro de consulta, deverá vincular manualmente os parâmetros de consulta ao parâmetro de relatório renomeado usando o procedimento descrito neste tópico.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-associate-a-query-parameter-with-a-report-parameter"></a>Para associar um parâmetro de consulta a um parâmetro de relatório  
  
1.  No painel de dados do relatório, clique com o botão direito do mouse no conjunto de dados, clique em **Propriedades do Conjunto de Dados** e, depois, em **Parâmetros**.  
  
    > [!NOTE]  
    >  Se o painel Dados do Relatório não estiver visível, clique em **Dados do Relatório** no menu **Exibir**.  
  
2.  Na coluna **Nome do Parâmetro**, localize o nome do parâmetro de consulta. Os nomes de parâmetro são preenchidos automaticamente com base na consulta. Sempre que você altera a consulta, ela é verificada em busca de novos parâmetros de consulta. Os parâmetros de consulta criados manualmente não são alterados quando a consulta é alterada.  
  
    -   Em **Nome do Parâmetro**, localize o nome do parâmetro de consulta conforme exibido na consulta. Você também pode adicionar manualmente um novo parâmetro de consulta e inserir um nome.  
  
    -   Em **Valor do Parâmetro**, digite ou selecione uma expressão avaliada como o valor passado para o parâmetro de consulta. Normalmente é o nome do parâmetro de relatório.  
  
        > [!NOTE]  
        >  Os valores de um parâmetro de consulta não se limitam a parâmetros de relatório. Para o valor do parâmetro, você pode usar qualquer expressão avaliada como um valor.  
  
3.  Repita a etapa 2 para especificar mais parâmetros de consulta.  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [O conceito de parâmetros de relatório &#40;relatórios e SSRS&#41;](../report-design/report-parameters-concepts-report-builder-and-ssrs.md)  
  
  
