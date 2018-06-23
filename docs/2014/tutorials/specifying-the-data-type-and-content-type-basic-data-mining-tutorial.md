---
title: Especificando o tipo de dados e o tipo de conteúdo (Tutorial de mineração de dados básico) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 72484d27-3ef1-4f16-813c-2f43231fc2da
caps.latest.revision: 25
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 8ea7d719e4341ded35a874c1bdc6c9c9ea0892f9
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/21/2018
ms.locfileid: "36313204"
---
# <a name="specifying-the-data-type-and-content-type-basic-data-mining-tutorial"></a>Especificando o tipo de dados e o tipo de conteúdo (Tutorial de mineração de dados básico)
  Agora que você selecionou as colunas a serem usadas na criação da sua estrutura e no treinamento de seus modelos, faça as alterações necessárias nos dados padrão e nos tipos de conteúdo definidos pelo assistente.  
  
#### <a name="review-and-modify-content-type-and-data-type-for-each-column"></a>Revise e modifique o tipo de conteúdo e o tipo de dados de cada coluna.  
  
1.  Sobre o **colunas especificar conteúdo e tipo de dados** , clique em **detectar** para executar um algoritmo que determina os dados padrão e os tipos de conteúdo para cada coluna.  
  
2.  Revise as entradas de **tipo de conteúdo** e **tipo de dados** colunas e alterá-los, se necessário, para certificar-se de que as configurações são iguais às listadas na tabela a seguir.  
  
     Em geral, o assistente detectará números e atribuirá um tipo de dados numérico apropriado, mas há muitos cenários em que talvez você queira manipular um número como texto. Por exemplo, o **GeographyKey** devem ser tratados como texto, pois ele seria inadequado executar operações matemáticas neste identificador.  
  
    |coluna|Tipo de Conteúdo|Tipo de Dados|  
    |------------|------------------|---------------|  
    |**Endereço linha 1**|**Discreto**|**Texto**|  
    |**Linha de endereço 2**|**Discreto**|**Texto**|  
    |**Idade**|**Contínua**|**Long**|  
    |**Comprador de bicicleta**|**Discreto**|**Long**|  
    |**Distância do Trabalho**|**Discreto**|**Texto**|  
    |**CustomerKey**|**Chave**|**Long**|  
    |**DateLastPurchase**|**Contínua**|**Date**|  
    |**Endereço de email**|**Discreto**|**Texto**|  
    |**Educação em inglês**|**Discreto**|**Texto**|  
    |**Ocupação em inglês**|**Discreto**|**Texto**|  
    |**FirstName**|**Discreto**|**Texto**|  
    |**Gênero**|**Discreto**|**Texto**|  
    |**Chave de Geografia**|**Discreto**|**Texto**|  
    |**Sinalizador do Proprietário da Casa**|**Discreto**|**Texto**|  
    |**Last Name**|**Discreto**|**Texto**|  
    |**Estado Civil**|**Discreto**|**Texto**|  
    |**Número de Carros**|**Discreto**|**Long**|  
    |**Número de Crianças na Casa**|**Discreto**|**Long**|  
    |**Região**|**Discreto**|**Texto**|  
    |**Total de Filhos**|**Discreto**|**Long**|  
    |**Renda Anual**|**Contínua**|**Double**|  
  
3.  Clique em **Avançar**.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Especificando um conjunto de dados de teste para a estrutura &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/specifying-a-testing-data-set-for-the-structure-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>Tarefa anterior da lição  
 [Criando uma estrutura de modelo de mineração de mala direta &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/creating-a-targeted-mailing-mining-model-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de conteúdo &#40;mineração de dados&#41;](../../2014/analysis-services/data-mining/content-types-data-mining.md)   
 [Tipos de dados &#40;mineração de dados&#41;](../../2014/analysis-services/data-mining/data-types-data-mining.md)  
  
  