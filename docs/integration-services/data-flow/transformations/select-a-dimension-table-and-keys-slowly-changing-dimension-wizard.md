---
title: Selecionar uma Tabela e Chaves de Dimensão (Assistente para Dimensões de Alteração Lenta) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.loaddimwizard.selecttableandkeys.f1
ms.assetid: 01e0495f-de35-4607-ba19-0539e801e8fd
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 403ce296913bfcfbf55aedb75e989dd5d296c6c2
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65725890"
---
# <a name="select-a-dimension-table-and-keys-slowly-changing-dimension-wizard"></a>Selecionar uma Tabela e Chaves de Dimensão (Assistente para Dimensões de Alteração Lenta)

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Use a página **Selecionar uma Tabela e Chaves de Dimensão** para selecionar uma tabela de dimensões a ser carregada. Mapeie colunas do fluxo de dados para as colunas que serão carregadas.  
  
 Para obter mais informações sobre este assistente, consulte [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md).  
  
## <a name="options"></a>Opções  
 **Connection manager**  
 Selecione um gerenciador de conexões OLE DB existente na lista ou clique em **Novo** para criar um novo gerenciador de conexões OLE DB.  
  
> [!NOTE]  
>  O Assistente para Dimensão de Alteração Lenta dá suporte apenas a gerenciadores de conexões OLE DB e a conexões ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 **Nova**  
 Use a caixa de diálogo **Configurar Gerenciador de Conexões OLE DB** para selecionar um gerenciador de conexões existente ou clique em **Nova** para criar uma nova conexão OLE DB.  
  
 **Tabela ou Exibição**  
 Selecione uma tabela ou exibição da lista.  
  
 **Colunas de Entrada**  
 Selecione na lista as colunas de entrada para as quais você pode especificar mapeamento.  
  
 **Colunas de Dimensão**  
 Exiba todas as colunas de dimensão disponíveis.  
  
 **Tipo de Chave**  
 Selecione uma das colunas de dimensão para servir de chave de negócio. É necessário possuir uma chave de negócio.  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar saídas por meio do Assistente para Dimensões de Alteração Lenta](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
