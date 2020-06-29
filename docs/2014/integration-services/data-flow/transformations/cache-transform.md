---
title: Transformação Cache | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.cachetrans.f1
helpviewer_keywords:
- Cache transform
ms.assetid: a5683fc8-9c32-4634-819e-e9815627e4f1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 43008af4396ccf0e4eaf89082194de97e839ff04
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85431053"
---
# <a name="cache-transform"></a>transformação Cache
  A Transformação Cache gera um conjunto de dados de referência para uma Transformação Pesquisa, gravando dados de uma fonte de dados conectada no fluxo de dados para um gerenciador de conexões de Cache. A transformação Pesquisa executa pesquisas, unindo dados em colunas de entrada de uma fonte de dados conectados com colunas no banco de dados de referência.  
  
 Você pode usar o gerenciador de conexões de Cache quando deseja configurar a Transformação Pesquisa para executar no modo de cache cheio. Nesse modo, o conjunto de dados de referência é carregado no cache antes da execução da Transformação Pesquisa.  
  
 Para obter instruções sobre como configurar a Transformação Pesquisa em modo de cache cheio com o gerenciador de conexões de Cache e a Transformação Cache, consulte [Implementar uma Transformação Pesquisa em modo cache cheio usando o Gerenciador de Conexões do Cache](../../connection-manager/lookup-transformation-full-cache-mode-ole-db-connection-manager.md).  
  
 Para obter mais informações sobre o cache do conjunto de dados de referência, consulte [Lookup Transformation](lookup-transformation.md).  
  
> [!NOTE]  
>  A Transformação Cache grava apenas linhas exclusivas no gerenciador de conexões do Cache.  
  
 Em um único pacote, somente uma transformação Cache pode gravar dados no mesmo gerenciador de conexões de cache. Se o pacote contiver várias transformações Cache, a primeira transformação, que é chamada quando o pacote é executado, gravará os dados no gerenciador de conexões. As operações de gravação das transformações Cache subsequentes falham.  
  
 Para obter mais informações, consulte [Cache Connection Manager](../../connection-manager/cache-connection-manager.md) e [Cache Connection Manager Editor](../../cache-connection-manager-editor.md).  
  
## <a name="configuration-of-the-cache-transform"></a>Configuração da transformação Cache  
 Você pode configurar o gerenciador de conexões de cache para salvar os dados em um arquivo de cache (.caw).  
  
 Você pode configurar a transformação Cache das seguintes formas:  
  
-   Especificando o gerenciador de conexões de cache.  
  
-   Mapeando as colunas de entrada na transformação Cache para as colunas de destino do gerenciador de conexões de cache.  
  
    > [!NOTE]  
    >  Cada coluna de entrada deve ser mapeada para uma coluna de destino e os tipos de dados de coluna devem corresponder. Caso contrário, o Designer [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] exibirá uma mensagem de erro.  
  
     Você pode usar o **Editor do Gerenciador de Conexões de Cache** para modificar tipos de dados de coluna, nomes e outras propriedades de coluna.  
  
 Você pode definir propriedades por meio do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] Designer. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** , consulte [Transformation Custom Properties](transformation-custom-properties.md).  
  
 Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades de um componente de fluxo de dados](../set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Transformações de Integration Services](integration-services-transformations.md)   
 [Fluxo de Dados](../data-flow.md)  
  
  
