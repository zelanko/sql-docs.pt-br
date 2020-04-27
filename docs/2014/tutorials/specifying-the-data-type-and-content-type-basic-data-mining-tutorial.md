---
title: Especificando o tipo de dados e o tipo de conteúdo (tutorial de mineração de dados básico) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 72484d27-3ef1-4f16-813c-2f43231fc2da
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 583a6fda2dbb4698405a3d69f33955531b3c1c10
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62720051"
---
# <a name="specifying-the-data-type-and-content-type-basic-data-mining-tutorial"></a>Especificando o tipo de dados e o tipo de conteúdo (Tutorial de mineração de dados básico)
  Agora que você selecionou as colunas a serem usadas na criação da sua estrutura e no treinamento de seus modelos, faça as alterações necessárias nos dados padrão e nos tipos de conteúdo definidos pelo assistente.  
  
#### <a name="review-and-modify-content-type-and-data-type-for-each-column"></a>Revise e modifique o tipo de conteúdo e o tipo de dados de cada coluna.  
  
1.  Na página **especificar conteúdo e tipo de dados das colunas** , clique em **detectar** para executar um algoritmo que determina os tipos de conteúdo e dados padrão para cada coluna.  
  
2.  Examine as entradas nas colunas **tipo de conteúdo** e **tipo de dados** e altere-as, se necessário, para certificar-se de que as configurações sejam as mesmas listadas na tabela a seguir.  
  
     Em geral, o assistente detectará números e atribuirá um tipo de dados numérico apropriado, mas há muitos cenários em que talvez você queira manipular um número como texto. Por exemplo, o **GeographyKey** deve ser tratado como texto, porque seria inadequado executar operações matemáticas nesse identificador.  
  
    |Coluna|Tipo de conteúdo|Tipo de Dados|  
    |------------|------------------|---------------|  
    |**Endereço linha1**|**Discreto**|**Texto**|  
    |**Endereço Linha2**|**Discreto**|**Texto**|  
    |**Idade**|**Visa**|**long**|  
    |**Bike Buyer**|**Discreto**|**long**|  
    |**Distância do Trabalho**|**Discreto**|**Texto**|  
    |**CustomerKey**|**Chave**|**long**|  
    |**DateLastPurchase**|**Visa**|**Data**|  
    |**Endereço de email**|**Discreto**|**Texto**|  
    |**Educação em Inglês**|**Discreto**|**Texto**|  
    |**Ocupação em Inglês**|**Discreto**|**Texto**|  
    |**FirstName**|**Discreto**|**Texto**|  
    |**Sexo**|**Discreto**|**Texto**|  
    |**Geografia Principal**|**Discreto**|**Texto**|  
    |**Sinalizador do Proprietário da Casa**|**Discreto**|**Texto**|  
    |**Sobrenome**|**Discreto**|**Texto**|  
    |**Estado Civil**|**Discreto**|**Texto**|  
    |**Número de Carros**|**Discreto**|**long**|  
    |**Número de filhos em casa**|**Discreto**|**long**|  
    |**Região**|**Discreto**|**Texto**|  
    |**Total de Filhos**|**Discreto**|**long**|  
    |**Renda Anual**|**Visa**|**Double**|  
  
3.  Clique em **Avançar**.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Especificação de um conjunto de dados de teste para a estrutura &#40;tutorial de mineração de dados básico&#41;](../../2014/tutorials/specifying-a-testing-data-set-for-the-structure-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>Tarefa anterior da lição  
 [Criando uma estrutura de modelo de mineração de mala direta direcionada &#40;tutorial de mineração de dados básico&#41;](../../2014/tutorials/creating-a-targeted-mailing-mining-model-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Tipos de conteúdo &#40;mineração de dados&#41;](../../2014/analysis-services/data-mining/content-types-data-mining.md)   
 [Tipos de dados &#40;Mineração de dados&#41;](../../2014/analysis-services/data-mining/data-types-data-mining.md)  
  
  
