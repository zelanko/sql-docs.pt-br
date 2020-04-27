---
title: rrRenderingError – erro do Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- rrRenderingError
ms.assetid: 0751efc3-b81b-44ee-8aac-8560f86ca322
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 390cd2efde37d5d04b7b7ef3a3799222e024b7e4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66099275"
---
# <a name="rrrenderingerror---reporting-services-error"></a>rrRenderingError - Erro do Reporting Services
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|rrRenderingError|  
|Origem do Evento|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings.resources.Strings|  
|Componente|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|Texto da mensagem|Ocorreu um erro na renderização do relatório. (rrRenderingError) %1|  
  
## <a name="explanation"></a>Explicação  
 Esta mensagem é retornada quando o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não puder renderizar ou exportar o relatório.  
  
 Uma mensagem que indica que o tamanho não é suportado, normalmente, é exibida quando o tamanho da página de RDL especificada não é válida. Especifique um tamanho válido de página de RDL e, em seguida, tente novamente.  
  
 Uma mensagem que indica que uma medida de tamanho de RDL não é suportada, normalmente, é exibida quando um tipo de unidade sem-suporte é especificado. Tipos de unidade válidos são cm, pol, mm, pc e pt. Especifique um tipo de unidade válido e tente novamente.  
  
 Uma mensagem que indica que um tamanho negativo não é suportado, normalmente, é exibida quando uma medida negativa para o tamanho da página, por exemplo, -5 cm, é especificada. Especifique um número positivo para o tamanho da página e, em seguida, tente novamente.  
  
 Uma mensagem que indica que um tamanho de RDL foi especificado fora de intervalo, normalmente, é exibida quando uma medida para o tamanho da página está fora do tamanho de margem de página válido. Especifique uma medida para o tamanho de página que está dentro dos tamanhos de margem de página válidos.  
  
 Uma mensagem que indica que uma cor especificada não é suportada, normalmente, é exibida quando uma cor especificada na RDL não é válida. Escolha uma cor suportada pelo RDL e, em seguida, tente novamente.  
  
 Uma mensagem que indica que a etiqueta de ação é opcional somente quando estiver usando uma única ação e que a adição de várias ações requer etiquetas para cada ação, normalmente, é exibida quando uma etiqueta de ação é especifica e ela não é válida. Especifique uma etiqueta de ação válida para cada ação.  
  
 Uma mensagem que indica que o argumento de estilo tem que ser de um tipo específico, normalmente, é exibida quando um valor de estilo incorreto para o tipo de dados é especificado. A especificação de RDL identifica os tipos válidos que você pode usar nos valores de estilo de diferentes elementos de RDL. Por exemplo, um valor de estilo incorreto para cor do plano de fundo é "2pt" e o valor incorreto para a altura é "verdade." Especifique um valor correto e, em seguida, tente novamente.  
  
 Uma mensagem que indica que o estilo de borda não é suportado, normalmente, é exibida quando o estilo de borda especificado não é válido. Especifique um estilo de borda suportado e, em seguida, tente novamente.  
  
 Uma mensagem que indica que o mimetype da imagem não é suportado, normalmente, é exibida quando o mimetype especificado para um item de relatório de imagem não é válido. Especifique um mimetype com suporte para o item de relatório e, em seguida, tente novamente.  
  
 Uma mensagem que indica que o número de linhas excede o máximo de linhas possível por folha, normalmente, é exibida quando o número de linhas em uma planilha do Excel é excedido. O Excel suporta até 65.000 linhas.  
  
 Uma mensagem que indica que o número de colunas excede o máximo de colunas possível por folha, normalmente, é exibida quando o número de colunas em uma planilha do Excel é excedido.  
  
## <a name="user-action"></a>Ação do usuário  
  
## <a name="internal-only"></a>Somente interno  
  
