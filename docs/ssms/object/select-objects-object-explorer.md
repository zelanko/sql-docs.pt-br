---
title: Selecionar objetos (Pesquisador de Objetos) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-objects
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.common.selectobjects.f1
ms.assetid: 692477fe-dd7c-403d-acd2-bb108b6077f1
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cbff0ee5307e9f0d6d7e53a740c950c869dc93c5
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2018
ms.locfileid: "42775924"
---
# <a name="select-objects-object-explorer"></a>Selecionar objetos (Pesquisador de Objetos)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Use a caixa de diálogo **Selecionar Objetos** para adicionar um objeto a uma lista em outra caixa de diálogo. O título da caixa de diálogo e as opções disponíveis na caixa de diálogo dependem de como foram abertos. Aparecerão somente opções disponíveis; por exemplo, só estão disponíveis logons quando você está selecionando um proprietário para um objeto novo.  
  
## <a name="options"></a>Opções  
**Selecionar esses tipos de objeto**  
Exibe uma lista dos tipos aos quais pertencem os objetos a ser selecionados. Os tipos incluem entidades de segurança e protegíveis no nível do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do banco de dados. Essa caixa é preenchida com as seleções feitas na caixa de diálogo **Selecionar Tipos de Objeto** , acessada do botão **Tipo de Objetos** .  
  
**Digite os nomes de objeto a selecionar**  
Digite uma lista separada por ponto-e-vírgula com os nomes dos objetos a ser selecionados. Os objetos a serem selecionados devem ser de um tipo listado na caixa **Selecionar esses tipos de objeto** . Os objetos podem ser selecionados de uma lista acessada clicando no botão **Procurar** .  
  
**Tipos de objeto**  
Exibe uma lista de tipos de objeto. Selecione um ou mais marcando a caixa de seleção que corresponde ao tipo.  
  
**Verificar Nomes**  
Valida os nomes de objeto na caixa **Digitar os nomes de objeto a selecionar** . Se for listado um nome de objeto inválido, será mostrada a caixa de diálogo **Nome não Encontrado** . Com essa caixa de diálogo, o nome pode ser corrigido ou removido da lista de objetos a selecionar.  
  
**Procurar**  
Mostra a caixa de diálogo **Procurar por Objetos** . Ela contém uma lista de objetos dos tipos listados na caixa **Selecionar Esses Tipos de Objeto** . Selecione os objetos dessa lista marcando as caixas de seleção correspondentes.  
  
