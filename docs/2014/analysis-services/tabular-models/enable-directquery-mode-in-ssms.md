---
title: Configurar o acesso na memória ou DirectQuery para um banco de dados modelo de tabela | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a5d439a9-5be1-4145-90e8-90777d80e98b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 55a1a296e6a7b2a2155dea590be9321b22e73451
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66067191"
---
# <a name="configure-in-memory-or-directquery-access-for-a-tabular-model-database"></a>Configure o Acesso Na Memória ou DirectQuery para um banco de dados modelo de tabela
  Este tópico descreve como alterar as propriedades de conexão de um modelo de tabela que já foi implantado, para habilitar o uso do modelo no modo Consulta Direta.  
  
 Para obter mais informações sobre essas propriedades e a configuração para os cenários mais comuns, consulte [cenários de implantação do DirectQuery &#40;SSAS tabular&#41;](../directquery-deployment-scenarios-ssas-tabular.md).  
  
## <a name="requirements"></a>Requisitos  
 Habilitar o uso do modo Consulta Direta em um modelo de tabela é um processo de várias etapas. Você deve:  
  
1.  Verificar se o modelo não tem recursos que podem causar erros de validação no modo Consulta Direta.  
  
2.  Alterar o modo de armazenamento no modelo para dar suporte a Consulta Direta.  
  
3.  Implantar o modelo em um modo que dá suporte a consultas em um modo Consulta Direta híbrido ou puro.  
  
4.  Editar a cadeia de conexão no banco de dados implantado para dar suporte ao modo Consulta Direta.  
  
 Este tópico supõe que você tenha criado e validado seu modelo, e somente precise habilitar o acesso Consulta Direta de um cliente como o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)].  
  
## <a name="procedure"></a>Procedimento  
  
#### <a name="change-the-connection-string-properties-of-the-model"></a>Alterar as propriedades de cadeia de conexão de um modelo  
  
1.  No SQL Server Management Studio, abra a instância para a qual você implantou o modelo.  
  
2.  No Pesquisador de objetos, clique com o botão direito do mouse no nome do banco de dados modelo e selecione **Propriedades**.  
  
3.  Localize a propriedade **DirectQueryMode**. Para habilitar o uso da fonte de dados relacional, esta propriedade deve ser definida como um destes valores:  
  
    -   **DirectQuery**  
  
    -   **InMemoryWithDirectQuery**  
  
    -   **DirectQueryWithInMemory**  
  
  
