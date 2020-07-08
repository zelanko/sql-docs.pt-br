---
title: Definir filtros | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.replconflictviewer.definefilters.f1
helpviewer_keywords:
- Define Filters dialog box
ms.assetid: 1fa71d22-ce5a-4aae-ba05-4d755842aeac
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7ef180ac401b540d1abe50688b98e691c819f55f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85654060"
---
# <a name="define-filters"></a>Definir Filtros
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  A caixa de diálogo **Definir Filtros** permite que você defina filtros que são aplicados em conflitos de dados para consultar um subconjunto dos conflitos na grade. Para definir um filtro, escolha um operador na caixa de listagem suspensa **Operador** e então insira em um valor. Por exemplo, para mostrar somente conflitos onde o perdedor do conflito é o servidor **ReplTest1**, selecione **Igual a** na caixa de lista suspensa **Operador** e insira **ReplTest1** na primeira coluna **Valor** .  
  
## <a name="options"></a>Opções  
 **Operador**  
 Selecione um operador para o filtro, como **Menor que ou Igual a**.
  
 **Valor**  
 Insira um valor para o filtro. A maioria dos operadores só exige um valor na primeira coluna **Valor** , mas os operadores **Entre** e **Não Entre** requerem um valor em ambas as coluna **Valor** .  
  
 **Limpar**  
 Clique nesse botão para limpar todos os filtros anteriormente definidos.  
  
## <a name="see-also"></a>Consulte Também  
 [Visualizador de Conflitos de Replicação da Microsoft &#40;replicação de mesclagem&#41;](../../relational-databases/replication/microsoft-replication-conflict-viewer-merge-replication.md)   
 [Visualizador de Conflitos de Replicação da Microsoft &#40;replicação transacional&#41;](../../relational-databases/replication/microsoft-replication-conflict-viewer-transactional-replication.md)  
  
  
