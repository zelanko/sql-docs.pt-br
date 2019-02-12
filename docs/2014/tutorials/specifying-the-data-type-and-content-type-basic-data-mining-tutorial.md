---
title: Especificando o tipo de dados e o tipo de conteúdo (Tutorial de mineração de dados básico) | Microsoft Docs
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
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56040197"
---
# <a name="specifying-the-data-type-and-content-type-basic-data-mining-tutorial"></a>Especificando o tipo de dados e o tipo de conteúdo (Tutorial de mineração de dados básico)
  Agora que você selecionou as colunas a serem usadas na criação da sua estrutura e no treinamento de seus modelos, faça as alterações necessárias nos dados padrão e nos tipos de conteúdo definidos pelo assistente.  
  
#### <a name="review-and-modify-content-type-and-data-type-for-each-column"></a>Revise e modifique o tipo de conteúdo e o tipo de dados de cada coluna.  
  
1.  Sobre o **colunas especificar conteúdo e tipo de dados** , clique em **detectar** para executar um algoritmo que determina os dados padrão e tipos de conteúdo para cada coluna.  
  
2.  Revise as entradas a **tipo de conteúdo** e **tipo de dados** colunas e alterá-las se necessário, para certificar-se de que as configurações são os mesmos que os listados na tabela a seguir.  
  
     Em geral, o assistente detectará números e atribuirá um tipo de dados numérico apropriado, mas há muitos cenários em que talvez você queira manipular um número como texto. Por exemplo, o **GeographyKey** deve ser tratado como texto, pois ele seria inadequado executar operações matemáticas neste identificador.  
  
    |coluna|Tipo de Conteúdo|Tipo de Dados|  
    |------------|------------------|---------------|  
    |**Linha de endereço1**|**Discreto**|**Texto**|  
    |**Linha de endereço2**|**Discreto**|**Texto**|  
    |**Idade**|**contínua**|**Long**|  
    |**Bike Buyer**|**Discreto**|**Long**|  
    |**Distância do Trabalho**|**Discreto**|**Texto**|  
    |**CustomerKey**|**Chave**|**Long**|  
    |**DateLastPurchase**|**contínua**|**Data**|  
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
    |**Renda Anual**|**contínua**|**Double**|  
  
3.  Clique em **Avançar**.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Especificando um conjunto de dados de teste para a estrutura &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/specifying-a-testing-data-set-for-the-structure-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>Tarefa anterior da lição  
 [Criando uma estrutura de modelo de mineração de mala direta &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/creating-a-targeted-mailing-mining-model-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de conteúdo &#40;Data Mining&#41;](../../2014/analysis-services/data-mining/content-types-data-mining.md)   
 [Tipos de dados &#40;Mineração de dados&#41;](../../2014/analysis-services/data-mining/data-types-data-mining.md)  
  
  
