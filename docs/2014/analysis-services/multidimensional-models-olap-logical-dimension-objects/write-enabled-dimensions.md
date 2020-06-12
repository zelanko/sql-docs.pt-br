---
title: Dimensões habilitadas para gravação | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- write-enabled dimensions [Analysis Services]
- dimensions [Analysis Services], write-enabled
- dimension writeback [Analysis Services]
- write-enabled cubes [Analysis Services]
- writeback [Analysis Services], dimensions
ms.assetid: 0bac050d-cd3b-427b-884a-65a91be89500
author: minewiskan
ms.author: owend
ms.openlocfilehash: f8f0f1c959d44b4d3e133e5676e9aca9365a628d
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545085"
---
# <a name="write-enabled-dimensions"></a>Dimensões habilitadas para gravação
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  
  
 Os dados em uma dimensão são, geralmente, somente leitura. No entanto, em determinados cenários, talvez você queira habilitar uma dimensão para gravação. No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , a habilitação de gravação de uma dimensão permite que os usuários empresariais modifiquem o conteúdo da dimensão e vejam o efeito imediato das alterações nas hierarquias da dimensão. Todas as dimensões com base em uma única tabela podem ser habilitadas para gravação. Em uma dimensão habilitada para gravação, os usuários empresariais e administrados podem alterar, mover, adicionar e excluir membros de atributo dentro da dimensão. Essas atualizações são referidas coletivamente como *write-back da dimensão*.  
  
 O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oferece suporte a write-back da dimensão em todos os atributos de dimensão e todos os membros de uma dimensão podem ser modificados. Para um cubo ou partição habilitada para gravação, as atualizações são armazenadas em uma tabela de write-back separada das tabelas de origem do cubo. No entanto, para uma dimensão habilitada para gravação, as atualizações são gravadas diretamente em uma tabela de dimensão. Além disso, se uma dimensão habilitada para gravação for incluída em um cubo com várias partições onde algumas ou todas as suas fontes de dados possuírem cópias da tabela da dimensão, apenas a tabela de dimensão original será atualizada durante o processo write-back.  
  
 Dimensões e cubos habilitados para gravação têm recursos diferentes, mas complementares. Uma dimensão habilitada para gravação permite que os usuários atualizem membros, enquanto que um cubo habilitado para gravação permite que eles atualizem valores de célula. Embora esses dois recursos sejam complementares, não é necessário usar ambos os recursos combinados. Uma dimensão não precisa ser incluída em um cubo para que o write-back da dimensão possa ocorrer. Uma dimensão habilitada para gravação também pode ser incluída em um cubo que não é habilitado para gravação. Você usa procedimentos diferentes a habilitar dimensões e cubos para gravação e para manter sua segurança.  
  
 As seguintes restrições são aplicáveis para o write-back da dimensão:  
  
-   Ao criar um novo membro, você deve incluir todo atributo em uma dimensão. Você não pode inserir um membro sem especificar um valor para o atributo de chave da dimensão. Portanto, a criação de membros está sujeita às restrições (como valores de chave não nulos) definidas na tabela de dimensões.  
  
-   Há suporte para write-back da dimensão apenas para esquemas em estrela. Em outras palavras, uma dimensão deve estar baseada em uma única tabela de dimensões diretamente relacionada a uma tabela de fatos. Após habilitar uma dimensão para gravação, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] valida esse requisito na implantação para um banco de dados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] existente ou na criação de um projeto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Todo membro existente de um write-back da dimensão pode ser modificado ou excluído. Quando um membro é excluído, a exclusão propaga-se em cascata para todos os membros filhos. Por exemplo, em uma dimensão Cliente que contém os atributos RegiãoPaís, Província, Cidade e Cliente, a exclusão de um país/região excluiria todas as províncias, cidades e clientes pertencentes à região/país excluída. Se um país/região tiver somente uma província, excluir essa província também excluirá o país/região.  
  
 Os membros de um write-back da dimensão podem ser movidos apenas no mesmo nível. Por exemplo, uma cidade pode ser movida para um nível de Cidade em um país/região ou província diferente, mas uma cidade não pode ser movida para um nível de Província ou PaísRegião. Em uma hierarquia pai-filho, todos os membros são membros folha e, portanto, um membro pode ser movido para qualquer nível diferente do nível `(All)`.  
  
 Se um membro de uma hierarquia pai-filho for excluído, os filhos do membro serão movidos para o pai do membro. Permissões de atualização na tabela relacional são necessárias no membro excluído, mas nenhuma permissão é necessária nos membros movidos. Quando um aplicativo move um membro em uma hierarquia pai-filho, o aplicativo pode especificar na operação UPDATE se os descendentes do membro serão movidos com o membro ou serão movidos para o pai do membro. Para excluir recursivamente um membro em uma hierarquia pai-filho, um usuário deve possuir permissões de atualização na tabela relacional para o membro e todos os seus descendentes.  
  
> [!NOTE]  
>  Atualizações para o atributo pai em uma hierarquia pai-filho não devem incluir atualizações de quaisquer outras propriedades ou atributos.  
  
 Todas as alterações de uma dimensão acarretam a modificação da estrutura da dimensão. Cada alteração de uma dimensão é considerada uma única transação, exigindo processamento incremental para atualizar a estrutura da dimensão. Dimensões habilitadas para gravação têm os mesmos requisitos de processamento que quaisquer outras dimensões.  
  
> [!NOTE]  
>  Não há suporte para o write-back das dimensões vinculadas.  
  
## <a name="security"></a>Segurança  
 Os únicos usuários empresariais que podem atualizar um write-back da dimensão habilitada para gravação são aqueles nas funções de banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , para os quais foram concedidas as permissões de leitura/gravação na dimensão. Para cada função, você pode controlar quais membros podem ou não serem atualizados. Para que usuários empresariais atualizem dimensões habilitadas para gravação, o aplicativo cliente deve oferecer suporte a esse recurso. Para esses usuários, uma dimensão habilitada para gravação deve estar incluída em um cubo processado desde a última alteração da dimensão. Para saber mais, veja [Autorizar o acesso a objetos e operações &#40;Analysis Services 41](../multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md).  
  
 Usuários e grupos incluídos em uma função de Administrador podem atualizar os membros de atributo de uma dimensão habilitada para gravação, mesmo se a dimensão não estiver incluída em um cubo.  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades da dimensão do banco de dados](database-dimension-properties.md)   
 [Partições habilitadas para gravação](../multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions.md)   
 [Dimensões &#40;Analysis Services – Dados Multidimensionais&#41;](dimensions-analysis-services-multidimensional-data.md)  
  
  
